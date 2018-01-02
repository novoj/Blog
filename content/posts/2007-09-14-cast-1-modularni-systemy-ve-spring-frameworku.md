---
status: publish
published: true
title: 'Část #1: Modulární systémy ve Spring Frameworku'
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "V tomto díle si povíme něco o aplikačních kontextech, jejich vlastnostech
  a možnosti jejich řetězení do stromové struktury. Tato část je základem principem
  celého modulární skladby, jejíž detaily vám budu v následujících dílech popisovat.
  Jak jsem již uváděl v předmluvě, nejedná se o nic světoborného, jen o základní principy
  Springu.\r\n\r\n"
wordpress_id: 30
wordpress_url: http://blog.novoj.net/2007/09/14/cast-1-modularni-systemy-ve-spring-frameworku/
date: '2007-09-14 05:04:20 +0200'
date_gmt: '2007-09-14 04:04:20 +0200'
categories:
- Spring Framework
tags: []
comments: []
---
<p>V tomto díle si povíme něco o aplikačních kontextech, jejich vlastnostech a možnosti jejich řetězení do stromové struktury. Tato část je základem principem celého modulární skladby, jejíž detaily vám budu v následujících dílech popisovat. Jak jsem již uváděl v předmluvě, nejedná se o nic světoborného, jen o základní principy Springu.</p>
<p><a id="more"></a><a id="more-30"></a></p>
<h3>Aplikační kontexty</h3>
<p>Celý Spring je postaven na aplikačních kontextech. Aplikační kontext se dá nejlépe přiblížit ke class loaderům v Javě, má i řadu podobných vlastností. Aplikační kontexty mohou tvořit strom, kontexty v nižších úrovních se odkazují na kontexty nadřazené. Z nižších kontextů jsou viditelné beany v kontextech nadřazených, z nižších kontextů jsou ApplicationEventy posílány ke zpracování i do nadřazených kontextů. Pouze post processorové faktory (<a href="http://www.springframework.org/docs/api/org/springframework/beans/factory/config/BeanPostProcessor.html" target="_new">BeanPostProcessor</a> a <a href="http://www.springframework.org/docs/api/org/springframework/beans/factory/config/BeanFactoryPostProcessor.html" target="_new">BeanFactoryPostProcessor</a>) jsou pro každý kontext definovány zvlášť.</p>
<p><a href="http://www.springframework.org/docs/api/org/springframework/context/ApplicationContext.html" target="_new">Aplikační kontext</a> je něco víc jak <a href="http://www.springframework.org/docs/api/org/springframework/beans/factory/BeanFactory.html" target="_new">BeanFactory</a> - krom jiného se stará o:</p>
<ul>
<li>inicializaci Multicasteru (ten se stará o distribuci událostí), buď defaultním objektem SimpleApplicationEventMulticaster nebo vámi definovaným objektem, který je nalezen v konfiguraci pod názvem "applicationEventMulticaster"</li>
<li>automatické nalezení bean ApplicationListenerů v konfiguraci a jejich zaregistrování do Multicasteru </li>
<li>zaregistruje JVM shutdown hook, na který se můžete navěsit v případě, že chcete uvolnit nějaké zdroje, pokud je zvenčí vyvoláno ukončení JVM</li>
<li>postprocessing vašich bean - konkrétně splnění kontraktů rozhraní ApplicationContextAware, ApplicationContextAwareProcessor, ResourceLoaderAware, ApplicationEventPublisherAware, MessageSourceAware</li>
<li>poskytuje podporu pro AOP</li>
</ul>
<p><a href="http://www.springframework.org/docs/reference/beans.html" target="_new">Dokumentace Springu</a> mluví rozdílech aplikačního kontextu a bean factory takto:</p>
<p style="font-style: italic; margin-left: 20px; margin-right: 20px;">"Users are sometimes unsure whether a BeanFactory or an ApplicationContext is best suited for use in a particular situation. A BeanFactory  pretty much just instantiates and configures beans. An ApplicationContext also does that, and it provides the supporting infrastructure to enable lots of enterprise-specific features such as transactions and AOP."</p>
<p>V celé řadě případů si vystačíte pouze s jedním hlavním aplikačním kontextem. Někdy však můžete zcela nevědomky používat dva - například Springový plugin do Strutsů funguje tak, že pro každý Strutsový modul vytváří vlastní aplikační kontext s definicí action bean a navěšuje jej na hlavní WebApplicationContext uložený v ServletContextu (viz. metoda: createWebApplicationContext třídy <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/web/struts/ContextLoaderPlugIn.html" target="_new">ContextLoaderPlugIn</a>).</p>
<p>Také WebApplicationContext nemusí být tím hlavním. Pokud do web.xml do init parametru přidáte parametr s názvem "parentContextKey" a jako hodnotu doplníte klíč pod kterým se v BeanFactoryLocator nalézá jiný aplikační kontext, bude tento aplikační kontext dosazen jako parent kontext toho webového (viz. třída <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/web/context/ContextLoader.html" target="_new">ContextLoader</a>, metoda loadParentContext). Dosadit parent kontext pro web aplikační kontext můžete také velmi jednoduše přepsáním této třídy a předefinováním metody loadParentContext.</p>
<h3>Kouzlo řetězení Spring aplikačních kontextů</h3>
<p>Řetězení aplikačních kontextů můžeme použít k oddělení kontextů jednotlivých částí aplikace s možností vysdílet jejich společné části. Představte si, že vyvíjíte dvě aplikační knihovny, které spolu co se týče business logiky nijak nesouvisí - například nějaká reportovací knihovna a knihovna pro správu uživatelů. Obě dvě knihovny se vyvíjejí nezávisle a obě jsou postavené na Springu. Pak máte nějakou web aplikaci, ve které chcete oba "moduly" využít. Vzhledem k tomu, že oba moduly byly vyvíjeny nezávisle, může se jednoduše stát, že budou mít některé beany stejné názvy a při startu by vám Spring vyhořel (a je ještě řada dalších věcí, které by mohly způsobit problémy).</p>
<p>Ideální by bylo umožnit oběma modulům žít dále ve svých oddělených aplikačních kontextech. Co však s beanami, které bychom chtěli mít společné? Stačí nám k tomu definovat rootovský aplikační kontext, který bude obsahovat definici společných bean a oběma modulům nastavit tento "root" kontext jako jejich parent kontext. </p>
<p><b>Pozn.:</b> společnými beanami jsou myšleny např. MailSender, DataSource, TransactionManager a podobné beany, které potřebuje ke svému chodu každý modul (nebo alespoň větší část modulů) a které chceme zároveň konfigurovat a mít pouze jednou v celé aplikaci. </p>
<p>Z jednotlivých modulů se vyjmou deklarace sdílených bean a přesunou se do extra konfiguračního souboru, který využijeme pouze pro testy. V reálné aplikaci tyto beany vždy dostaneme "svrchu" od root aplikačního kontextu. Pokud bychom narazili na problém rozdílného pojmenování sdílených bean v root kontextu oproti názvům, které očekává modul, můžeme jednoduše <a href="http://www.springframework.org/docs/reference/beans.html#beans-beanname-alias" target="_new">aliasem</a> vytvořit beanu s potřebným názvem pro konkrétní modul.</p>
<p>Tuto kompozici používá například <a href="http://osflash.org/red5" target="_new">open source Flash server Red5</a> a nyní i <a href="http://www.fg.cz/cz/nabizime_uspech/edee.shtml" target="_new">CMS FG Forrest</a> ;-) .</p>
<h3>Jak inicializovat root context</h3>
<p>Root context je typicky singletonem - ukládáme jej do statické proměnné a existuje pouze jednou v celé aplikaci. Je to obdobná strategie, kterou používá <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/context/access/ContextSingletonBeanFactoryLocator.html?render=tab" target="_new">ContextSingletonBeanFactoryLocator</a>, který bychom mohli k této operaci využít. Pro vlastní inicializaci je asi nejvhodnější statický konstruktor. Pro inspiraci uvádím příklad kódu:</p>
<p>[source lang="java"]<br />
public class RootContextLocator {<br />
     private static ApplicationContext rootContext;</p>
<p>     static {<br />
          //ve statickém konstruktoru inicializujeme konfiguraci<br />
          rootContext = new ClasspathXmlApplicationContext("classpath:META-INF/rootApplicationContext.xml");<br />
     }</p>
<p>     public static ApplicationContext getRootApplicationContext() {<br />
          return rootContext;<br />
     }</p>
<p>}<br />
[/source]</p>
<p>Kdekoliv v aplikaci je pak možné díky statické metodě získat přístup k root kontextu. Existence jediné instance tohoto kontextu je zajištěna právě statickým konstruktorem třídy RootContextLocator.</p>
<p>Root kontext bude obvykle poměrně hubený - bude obsahovat jen pár společných bean. S postupem času si ukážeme, že hlavním cílem root kontextu je, stát se jakousi postavou ve středu dění (z anglického "man in the middle" ;-) ), která se stará především o koordinaci podřízených kontextů a sloužící k jejich vzájemnému propojení.</p>
<div style="margin: 10px; padding: 5px; border: 1px solid white; background-color: #333333; font-size: 90%">
<strong>Použití v J2EE</strong></p>
<p>Tímto způsobem můžeme také vytvořit root kontext, který bude jedinečný (společný) pro různé web aplikace i EJB v rámci jednoho EARu. V případě, že bude RootContextLocator třída nahrávaná EAR root classloaderem (<a href="http://www.objectsource.com/j2eechapters/Ch21-ClassLoaders_and_J2EE.htm" target="_new">více o classloaderech v J2EE</a>) a můžeme tedy sdílet základní beany i mezi různými web aplikacemi a EJB.</p>
<p>V souvislosti s J2EE připomínám, že aplikační servery mohou používat více JVM pro stejný EAR. V takovém případě bude root kontext fyzicky vícekrát (to je ostatně společný problém všech singletonů v J2EE prostředí) a proto je třeba tento fakt brát v úvahu. Což tedy znamená, že stavové informace je vhodné ukládat do bean, o jejich replikaci se nám aplikační server postará (např. beany uložené v session) nebo si takové údaje ukládat např. do databáze a držet se spíše stateless bean (myšleno Spring bean).</p>
<p>Další věcí, kterou je dobré si uvědomit, že v J2EE v podstatě nesmíte skoro nic. O propagaci datasourců a dalších věcí do web aplikací a EJB se stará sám kontejner a asi by nebylo nejvhodnější se mu plést do práce paralelním pašováním datasourcu z root spring kontextu (osobně si myslím, že ten by se ani k datasourcu v JNDI při inicializaci ještě ani nemohl dostat).</p>
<p>Upozorňuji, že v J2EE nejsem kovaný, takže pokud byste se hodlali pouštět do něčeho podobného, ověřte si chování na nějakém prototypu.</p>
<p>Každopádně podobnou architekturu už si vyzkoušeli ve zmíněném Red5 serveru - viz. <a href="http://osflash.org/pipermail/red5devs_osflash.org/2006-April/000636.html" target="_new">mail jednoho z vývojářů</a>.
</div>
<h3>Co bude v další části seriálu?!</h3>
<p>V další části seriálu bude rozebrána problematika refreshe stromu aplikačních kontextů. Toto je skvělá vlastnost Springu, která je často nedoceněná a málo používaná. Díky ní je možné jednoduše zahodit všechny současné instance bean definované v aplikačním kontextu a provést kompletní reinicalizaci kontextu s aktuální konfigurací (tak můžeme elegantně změnit chování aplikace bez nutnosti restartu serveru). S refreshem aplikačního kontextu se dá vyřešit poměrně dost věcí i v produkčním prostředí - navíc netrpí problémem PermGenSpace jako při reloadu kontextu celé aplikace na serveru. V situaci, kdy máme ale celý strom aplikačních kontextů se nám situace poměrně komplikuje - refresh se totiž stromem sám od sebe nezpropaguje.</p>
<p><a href="http://blog.novoj.net/2007/09/20/cast-2-modularni-systemy-ve-spring-frameworku/">Díl #2: Refresh stromu aplikačních kontextů</a></p>
