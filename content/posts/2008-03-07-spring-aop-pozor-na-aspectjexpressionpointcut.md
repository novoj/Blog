---
status: publish
published: true
title: Spring AOP - Pozor na AspectJExpressionPointcut!
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Tento týden jsem řešil problém s nedostatkem paměti při spouštění testů
  jednoho projektu. Pro běh testů nestačilo výchozích 64MB paměti Javy na heapu, což
  mi připadlo v porovnání s velikostí projektu podezřelé. Začal jsem profilovat a
  jelikož mne výsledky poněkud překvapily, chci se s Vámi o ně v tomto článku podělit.\r\n\r\nHned
  na úvod řeknu, že jádrem problému byla třída <a href=\"http://www.jdocs.com/spring/2.0.6/org/springframework/aop/aspectj/AspectJExpressionPointcut.html\"
  target=\"_new\">AspectJExpressionPointcut</a>. Tato třída je ve Spring dokumentaci
  zmiňována hned několikrát, velmi jednoduše se používá a ze všech dostupných materiálů
  jsem dospěl k názoru, že se jedná o doporučovaný a běžně používaný standard.\r\n\r\n"
wordpress_id: 55
wordpress_url: http://blog.novoj.net/2008/03/07/spring-aop-pozor-na-aspectjexpressionpointcut/
date: '2008-03-07 20:28:23 +0100'
date_gmt: '2008-03-07 19:28:23 +0100'
categories:
- Programování
- Spring Framework
tags: []
comments: []
---
<p>Tento týden jsem řešil problém s nedostatkem paměti při spouštění testů jednoho projektu. Pro běh testů nestačilo výchozích 64MB paměti Javy na heapu, což mi připadlo v porovnání s velikostí projektu podezřelé. Začal jsem profilovat a jelikož mne výsledky poněkud překvapily, chci se s Vámi o ně v tomto článku podělit.</p>
<p>Hned na úvod řeknu, že jádrem problému byla třída <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/aop/aspectj/AspectJExpressionPointcut.html" target="_new">AspectJExpressionPointcut</a>. Tato třída je ve Spring dokumentaci zmiňována hned několikrát, velmi jednoduše se používá a ze všech dostupných materiálů jsem dospěl k názoru, že se jedná o doporučovaný a běžně používaný standard.</p>
<p><a id="more"></a><a id="more-55"></a></p>
<h3>Identifikace problému</h3>
<p>V mém případě jsem pomocí AOP ošetřil kolem deseti tříd (jednou kvůli implementaci security a podruhé kvůli transakcím), načež mi za integračním serveru začaly padat testy na OutOfMemoryError (Java heap space). Rozjel jsem si testy lokálně a došel jsem ke stejnému výsledku. Po spuštění testů s nastavením:</p>
<p>[source lang="java"]<br />
-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/heapdump.bin<br />
[/source]</p>
<p>jsem z Javy dostal HeapDump v okamžiku kdy paměť došla a začal jsem dump analyzovat pomocí NetBeans Profileru. Okamžitě na mne vyskočilo, že třída <a href="http://java.sun.com/j2se/1.5.0/docs/api/java/lang/reflect/Method.html" target="_new">java.lang.reflect.Method</a> zabírá v paměti 15,2% místa o celkové velikosti téměř 10MB se 125tis. instancemi. Po krátkém zkoumání jsem zjistil, že většinu instancí drží právě <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/aop/aspectj/AspectJExpressionPointcut.html" target="_new">AspectJExpressionPointcut</a> ve své shadowMapCache. Tuto cache používá pro ukládání indexu, kde klíčem je právě Method a hodnotou je <a href="http://www.eclipse.org/aspectj/doc/next/weaver-api/org/aspectj/weaver/tools/ShadowMatch.html" target="_new">org.aspectj.weaver.tools.ShadowMatch</a>, který udržuje informaci o tom, zda tato metoda odpovídá / neodpovídá deklaraci pointcutu. Celý index nepoužívá weak nebo soft reference a drží si objekty natvrdo.</p>
<h3>Vysvětlení</h3>
<p>Jistým uklidněním může být, že Spring testy se chovají k aplikačním kontextům poněkud odlišně, než je tomu v provozním systému. V testech se drží cache všech aplikačních kontextů z testů, které mají odlišnou "konfiguraci" (myšleno odlišné návratové hodnoty z getConfigLocations metody). Tím pádem je v paměti současně drženo větší množství kontextů (v mém případě jich bylo 24), které mají v sobě každý uvedené AspectJExpressionPoincuty, které defakto většinou drží stejnou shadowMapCache.</p>
<p>I tak se mi ale zdá, že je implementace AspectJExpressionPointcut poněkud nešetrná k paměti. Je důležité si uvědomit, že pro každou třídu je drženo v shadowMapCache tolik položek, kolik je metod dané třídy v celé hierarchii dědičnosti. Takže u mých "jednoduchých" DAO s deseti metodami, které dědí z org.springframework.orm.ibatis.support.SqlMapClientDaoSupport, jsem napočítal okolo 35 metod celkově. Při pronásobení se začínáme dostávat už na zajímavá čísla. Jen pro zajímavost jeden objekt typu java.lang.reflection.Method v paměti (podle profileru) drží 77B paměti. ShadowMatchImpl, který je jako hodnota v indexu, drží dalších 40 (celkově u mě dalších 4,5MB). Když jsem tedy sečetl cekovou náročnost AspectJExpressionPointcut pro mé testy zjistil jsem že se jednalo o 22,1% (6.9% + 15,2%) celkové obsazené paměti jen na tento jeden index!</p>
<p>Přestože se jedná o specifický případ v kombinaci s chováním Spring testů, jsem přesvědčen o tom, že masivnější používání AspectJExpressionPointcut v projektu může pozlobit i na produkci (zvlášť pokud byste v některých momentech měli více aplikačních kontextů najednou - jako je tomu v našem případě).</p>
<h3>Řešení</h3>
<p>Jakmile se podařilo objevit jádro problému, bylo řešení už jednoduché. Přepsal jsem deklarace AOP z použití AspectJExpression na implementaci standardních Spring AOP interfaců:</p>
<h4>Dříve:</h4>
<p>[source lang="xml"]<br />
<aop:pointcut id="myPointcut" expression="execution(* com.pckg.*.*(..))"/><br />
<aop:advisor advice-ref="someAdvice" pointcut-ref="myPointcut"/><br />
[/source]</p>
<h4>Nyní:</h4>
<p>[source lang="xml"]<br />
<bean id="myPointcut" class="org.springframework.aop.support.JdkRegexpMethodPointcut"></p>
<property name="classFilter">
			<bean class="org.springframework.aop.support.RootClassFilter"><br />
				<constructor-arg value="com.pckg.SomeClassOrInterface"/><br />
			</bean>
		</property>
<property name="pattern" value=".*"/>
	</bean><br />
<aop:advisor advice-ref="someAdvice" pointcut-ref="myPointcut"/><br />
[/source]</p>
<p>Problém samozřejmě zmizel.</p>
