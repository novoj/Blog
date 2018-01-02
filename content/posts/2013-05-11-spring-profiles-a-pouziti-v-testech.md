---
status: publish
published: true
title: Spring profiles a použití v testech
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft  wp-image-2564\" title=\"Spring 3.1\" src=\"http://blog.novoj.net/binary/2013/05/Logo_Spring_258x151.png\"
  alt=\"\" width=\"181\" height=\"106\" />Po 3 letech dělám větší refaktoring na našem
  direct mailingovém modulu a jako první jsem se rozhodl povýšit verze knihoven a
  zrefaktorovat JUnit testy, které jsou tam ještě psané ve stylu JDK 1.4.\r\n\r\nV
  souvislosti s tím jsem samozřejmě přepracoval formu testů z dědičné hierarchie na
  anotace, které byly představeny poprvé ve <a href=\"http://static.springsource.org/spring/docs/3.2.x/spring-framework-reference/html/testing.html\"
  target=\"_blank\">Spring 3.X</a> (pokud se nepletu). A tu jsem zjistil, že mám drobný
  problém - v původní verzi mého kódu jsem využíval dynamické kompozice Springového
  kontextu k tomu, abych stejné integrační testy pustil proti různým implementacím
  úložišť dat (paměť, MySQL databáze, Oracle databáze ...). V aktuální verzi Springu
  se ale v anotaci <a href=\"http://static.springsource.org/spring/docs/3.2.x/javadoc-api/org/springframework/test/context/ContextConfiguration.html\"
  target=\"_blank\">@ContextConfiguration</a> uvádí statický výčet konfiguračních
  XML a to situaci komplikuje.\r\n\r\nŘešení této situace je samozřejmě možné i v
  aktuálním Springu a řešení je nyní dispozici víc. V tomto článku bych chtěl pro
  vás i pro své kolegy popsat to, co se líbí mě ...\r\n\r\n<strong>Varování! </strong>V
  tomto článku nenajdete nic novějšího, než je v dokumentaci Springu - tento článek
  má jediný význam - upozornit na zajímavé novinky ve Spring 3.1+ pro vývojáře, kteří
  (stejně jako já) začínali na starém Springu a některých novinek si v záplavě zpráv
  nestihli všimnout.\r\n\r\n"
wordpress_id: 2561
wordpress_url: http://blog.novoj.net/?p=2561
date: '2013-05-11 10:03:00 +0200'
date_gmt: '2013-05-11 09:03:00 +0200'
categories:
- Programování
- Java
- Testování
- Spring Framework
tags: []
comments: []
---
<p><img class="alignleft  wp-image-2564" title="Spring 3.1" src="http://blog.novoj.net/binary/2013/05/Logo_Spring_258x151.png" alt="" width="181" height="106" />Po 3 letech dělám větší refaktoring na našem direct mailingovém modulu a jako první jsem se rozhodl povýšit verze knihoven a zrefaktorovat JUnit testy, které jsou tam ještě psané ve stylu JDK 1.4.</p>
<p>V souvislosti s tím jsem samozřejmě přepracoval formu testů z dědičné hierarchie na anotace, které byly představeny poprvé ve <a href="http://static.springsource.org/spring/docs/3.2.x/spring-framework-reference/html/testing.html" target="_blank">Spring 3.X</a> (pokud se nepletu). A tu jsem zjistil, že mám drobný problém - v původní verzi mého kódu jsem využíval dynamické kompozice Springového kontextu k tomu, abych stejné integrační testy pustil proti různým implementacím úložišť dat (paměť, MySQL databáze, Oracle databáze ...). V aktuální verzi Springu se ale v anotaci <a href="http://static.springsource.org/spring/docs/3.2.x/javadoc-api/org/springframework/test/context/ContextConfiguration.html" target="_blank">@ContextConfiguration</a> uvádí statický výčet konfiguračních XML a to situaci komplikuje.</p>
<p>Řešení této situace je samozřejmě možné i v aktuálním Springu a řešení je nyní dispozici víc. V tomto článku bych chtěl pro vás i pro své kolegy popsat to, co se líbí mě ...</p>
<p><strong>Varování! </strong>V tomto článku nenajdete nic novějšího, než je v dokumentaci Springu - tento článek má jediný význam - upozornit na zajímavé novinky ve Spring 3.1+ pro vývojáře, kteří (stejně jako já) začínali na starém Springu a některých novinek si v záplavě zpráv nestihli všimnout.</p>
<p><a id="more"></a><a id="more-2561"></a></p>
<p>K řešení výše uvedeného problému bych mohl sice využít možnost dědičné kompozice aplikačních kontextů, ale musel bych  kopírovat umístění konfiguračních souborů pro jednotlivá úložiště, což je poměrně nepraktické (zvlášť, když je těchto testovacích tříd hodně). Koukněte se sami:</p>
<p><strong>Base test:</strong></p>
<p>[source lang="java"]@ContextConfiguration(<br />
  locations = {<br />
    &quot;classpath:/META-INF/lib_mail/spring/test-context.xml&quot;<br />
  }<br />
)<br />
public abstract class AbstractMessageStorageTestCase {<br />
    @Autowired private MessageStorage messageStorage;</p>
<p>    @Test<br />
    public void shouldPersistSimpleMessageBatch() {<br />
       ....<br />
    }</p>
<p>    @Test(expected = RecipientNotDefinedException.class)<br />
    public void shouldFailToPersistMessageBatchWithoutRecipients() {<br />
       ....<br />
    }<br />
}[/source]</p>
<p><strong>Konkrétní test A:</strong></p>
<p>[source lang="java"]@ContextConfiguration(<br />
  locations = {<br />
    &quot;classpath:/META-INF/lib_mail/spring/mysql-datasource.xml&quot;,<br />
    &quot;classpath:META-INF/lib_mail/spring/mail-database-dao-config.xml&quot;<br />
  }<br />
)<br />
public class MysqlMessageStorageTest extends AbstractMessageStorageTestCase {</p>
<p>}[/source]</p>
<p><strong>Konkrétní test B:</strong></p>
<p>[source lang="java"]@ContextConfiguration(<br />
  locations = {<br />
    &quot;classpath:/META-INF/lib_mail/spring/memory-dao-config.xml&quot;<br />
  }<br />
)public class MemoryMessageStorageTest extends AbstractMessageStorageTestCase {</p>
<p>}[/source]</p>
<p>Nehledě na to, že jsem si už nějakou dědičnost v testech zavedl a ta mi celou věc ještě více komplikuje.</p>
<p>Elegantnějším řešením je využít poměrně zajímavou novinku - tzv. <strong>profily.</strong> Ty můžete využít nejen pro testy ale i v produkčním kódu (což je věc, kterou určitě začnu praktikovat). V mém případě jsem si hlavním konfiguračním souboru pro testy udělal následující rozdělení:</p>
<p><strong>Test-config.xml</strong></p>
<p>[source lang="xml"]&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;<br />
&lt;beans xmlns=&quot;http://www.springframework.org/schema/beans&quot;<br />
	   xmlns:xsi=&quot;http://www.w3.org/2001/XMLSchema-instance&quot;<br />
	   xsi:schemaLocation=&quot;http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.2.xsd&quot;&gt;</p>
<p>    &lt;!-- sdílené konfigurace pro všechny testy --&gt;<br />
    &lt;import resource=&quot;classpath:/META-INF/lib_mail/spring/mail-config.xml&quot;/&gt;<br />
    &lt;import resource=&quot;classpath:/META-INF/lib_mail/spring/mail-test-basis.xml&quot;/&gt;</p>
<p>    &lt;!-- specifické nastavení pro profil database --&gt;<br />
    &lt;beans profile=&quot;database&quot;&gt;</p>
<p>        &lt;!-- tento konfigurační soubor je sdílený pro všechny DB implementace --&gt;<br />
        &lt;import resource=&quot;classpath:META-INF/lib_mail/spring/mail-database-dao-config.xml&quot;/&gt;</p>
<p>        &lt;beans profile=&quot;mysql&quot;&gt;<br />
            &lt;!-- pro mysql ale nahazujeme jiný JDBC datasource --&gt;<br />
            &lt;import resource=&quot;datasource-mysql.xml&quot;/&gt;<br />
        &lt;/beans&gt;</p>
<p>        &lt;beans profile=&quot;oracle&quot;&gt;<br />
            &lt;!-- pro oracle ale nahazujeme jiný JDBC datasource --&gt;<br />
            &lt;import resource=&quot;datasource-oracle.xml&quot;/&gt;<br />
        &lt;/beans&gt;</p>
<p>    &lt;/beans&gt;</p>
<p>    &lt;!-- specifické nastavení pro profil memory --&gt;<br />
    &lt;beans profile=&quot;memory&quot;&gt;</p>
<p>        &lt;import resource=&quot;classpath:META-INF/lib_mail/spring/mail-memory-dao-config.xml&quot;/&gt;</p>
<p>    &lt;/beans&gt;</p>
<p>&lt;/beans&gt;[/source]</p>
<p>Třída Base test zůstává potom úplně stejná. V jednotlivých testovacích třídách, které mají integračně testovat odlišné implementace úložišť nyní pouze aktivuji profily, které odpovídají konkrétním implementacím:</p>
<p><strong>Konkrétní test A:</strong></p>
<p>[source lang="java"]@ActiveProfiles({&quot;database&quot;, &quot;mysql&quot;})<br />
public class MysqlMessageStorageTest extends AbstractMessageStorageTestCase {</p>
<p>}[/source]</p>
<p><strong>Konkrétní test B:</strong></p>
<p>[source lang="java"]@ActiveProfiles({&quot;memory&quot;})<br />
public class MemoryMessageStorageTest extends AbstractMessageStorageTestCase {</p>
<p>}[/source]</p>
<p>Výsledkem je přehledný kód, kde máte všechno pohromadě a přehledně na jednom místě, takže pochopení logiky a použití je přímočaré.</p>
