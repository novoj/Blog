---
status: publish
published: true
title: PermGenSpace problem? No problem!
author:
  display_name: Michal Franc
  login: frc
  email: franc@fg.cz
  url: http://www.michalfranc.com
author_login: frc
author_email: franc@fg.cz
author_url: http://www.michalfranc.com
excerpt: "Tento článek vyšel na našem <a href=\"http://www.fg.cz\" target=\"_new\">firemním</a>
  intranetu. Jelikož je jeho obsah velmi přínosný ve své jednoduchosti a agregace
  poznatků z řady roztříštěných zdrojů po internetu, požádal jsem autora Michala France
  o svolení k jeho zveřejnění. Jak to dopadlo, můžete vytušit už sami. Výsledkem je
  že se s Vámi mohu podělit o zkušenosti s (vy)řešením problémů OutOfMemory v oblasti
  PermGenSpace při redeploy našich aplikací v aplikačních kontejnerech. Před aplikací
  těchto znalostí jsme vcelku pravidelně po dvou \"redeployích\" restartovali celý
  server, protože docházela PermGenSpace. V současném stavu aplikační server žije
  i po několika desítkách redeployů.\r\n<h3>A nyní slíbený článek</h3>\r\n<em>Každého
  programátora to jednou čeká. Jeho aplikace začne padat na OutOfMemoryError. Dá se
  krčit rameny se slovy \"já vážně nevím čím to je\", nebo s tím něco udělat.</em>\r\n\r\n"
wordpress_id: 63
wordpress_url: http://blog.novoj.net/2008/04/11/permgenspace-problem-no-problem/
date: '2008-04-11 11:27:47 +0200'
date_gmt: '2008-04-11 10:27:47 +0200'
categories:
- Java
tags: []
comments:
- id: 1939
  author: Ladislav Thon
  author_email: ladicek@gmail.com
  author_url: ''
  date: '2008-04-11 14:18:16 +0200'
  date_gmt: '2008-04-11 13:18:16 +0200'
  content: Žil jsem v dojmu, že naopak právě umístění knihoven do aplikačního serveru
    způsobuje problémy (objekt třídy nahrané classloaderem aplikačního serveru nebo
    bootstrap classloaderem má referenci na objekt třídy nahrané classloaderem aplikace)
    a že by se knihovny měly umisťovat přímo k aplikaci. Jak to ksakru je? :-)
- id: 1940
  author: Michal Franc
  author_email: franc@fg.cz
  author_url: http://www.fg.cz
  date: '2008-04-11 14:56:44 +0200'
  date_gmt: '2008-04-11 13:56:44 +0200'
  content: "To všechno platí až na malé vyjímky ;o)\r\n\r\nChápu to tak, že problematická
    je přítomnost commons-logging v aplikačním serveru. Nebudu zastírat že v tom plavu
    a víc sem experimentoval.\r\n\r\nNicméně v odkazovaných článcích lze nějaké info
    nalézt:\r\n\r\nhttp://blogs.sun.com/fkieviet/entry/classloader_leaks_the_dreaded_java\r\nNot
    a problem if the Apache Commons code is loaded in your application's classloader.
    However, you do have a problem if this code is also present in the classpath of
    the application server because those classes take precedence. As a result now
    you have references to classes in your application from the application server's
    classloader... a classloader leak!\r\n\r\nhttp://wiki.apache.org/jakarta-commons/Logging/UndeployMemoryLeak\r\nExcept
    for the brain-dead design of JDBC where jdbc drivers loaded via a custom classloader
    apparently get stored in a map within java.sql.DriverManager thereby causing cyclic
    references to that classloader."
- id: 1944
  author: Pavel Jetenský
  author_email: mail@jetensky.net
  author_url: http://jetensky.net/blog
  date: '2008-04-15 12:17:37 +0200'
  date_gmt: '2008-04-15 11:17:37 +0200'
  content: Tak tenhle článek obsahuje spoustu hodnotného a vydestilovaného úsilí.
    Určitě ho nečtu naposled, díky moc pánové...
- id: 2623
  author: Jakub Příkazský
  author_email: jakub.prikazsky@gmail.com
  author_url: ''
  date: '2008-08-01 09:59:05 +0200'
  date_gmt: '2008-08-01 08:59:05 +0200'
  content: "Děkuji za velmi pěkný článek, \r\n\r\nse stejným problémem jsem se potýkal
    cca před 1,5 rokem ale vy jste byl mnohem preciznější :-). Na problém s JDBC drivery
    a Springem jsem přišel také, ale externí knhovny jsem příliš nezkoumal. Zajímalo
    by mě, do jaké míry se Vám podařilo problém odstranit (nebo zmizel úplně?). Pokud
    si vzpomínám, tak jsem tehdy došel do celkem rozumného stavu, kdy mi Tomcat lehnul
    až po několika desítkách restartů.\r\n\r\nMám drobnou poznámku, odkaz na RSS kanály
    úplně dole ve stránce není správný a měl by být nejspíš takový http://blog.novoj.net/feed/"
- id: 2644
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2008-08-03 18:35:30 +0200'
  date_gmt: '2008-08-03 17:35:30 +0200'
  content: "Jakube díky za info, ty linky vytváří FeedBurner plugin a přestože vypadají
    \"zvláštně\", jsou funkční (přesměrovávají na RSS generované FeedBurnerem). Navíc
    \ např podle článku: http://www.brindys.com/winrss/feedformat.html se zdá, že
    odkaz je i správně.\r\n\r\nSoučasný status quo je ten, že problém se nám 100%
    odstranit nepodařilo. Po úvodním nadšení jsme zjistili, že problém se podařilo
    odstranit na testované instalaci, nicméně na jiných přetrvával. Od té doby dopisuji
    k článku další problémy, na které jsme narazili a které postupně odstraňujeme."
- id: 2772
  author: Jirka Hradil
  author_email: jirka@hradil.cz
  author_url: http://www.hradil.cz
  date: '2008-08-19 22:51:58 +0200'
  date_gmt: '2008-08-19 21:51:58 +0200'
  content: "Děkuji za tento článek. Doplňuji další odkazy, kde je problematika také
    velmi hezky popsána:\r\n\r\nhttp://blogs.sun.com/fkieviet/entry/classloader_leaks_the_dreaded_java\r\nhttp://blogs.sun.com/fkieviet/entry/how_to_fix_the_dreaded"
- id: 75523
  author: free list building software
  author_email: galen_montoya@fast-mail.org
  author_url: http://dobroda.hu/vendegkonyv/index_uj.php
  date: '2012-06-21 13:53:00 +0200'
  date_gmt: '2012-06-21 12:53:00 +0200'
  content: "I absolutely love your site.. Very nice colors &amp; theme.\r\nDid you
    make this web site yourself? Please \r\nreply back as I'm attempting to create
    my very own website and would like to know where you got this from or exactly
    what the theme is called. Thank you!"
- id: 151897
  author: Ondřej Medek
  author_email: xmedeko@gmail.com
  author_url: http://xmedeko.blogspot.cz
  date: '2013-05-22 08:07:05 +0200'
  date_gmt: '2013-05-22 07:07:05 +0200'
  content: "SAP MAT je teď Eclipse MAT. Také si přihodím trochu do redeploy memory
    leaks mlýna:\r\n\r\nhttp://xmedeko.blogspot.cz/2010/02/java-web-container-hunting-redeploy.html"
- id: 151898
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-05-22 08:30:12 +0200'
  date_gmt: '2013-05-22 07:30:12 +0200'
  content: Díky za tipy na články!
---
<p>Tento článek vyšel na našem <a href="http://www.fg.cz" target="_new">firemním</a> intranetu. Jelikož je jeho obsah velmi přínosný ve své jednoduchosti a agregace poznatků z řady roztříštěných zdrojů po internetu, požádal jsem autora Michala France o svolení k jeho zveřejnění. Jak to dopadlo, můžete vytušit už sami. Výsledkem je že se s Vámi mohu podělit o zkušenosti s (vy)řešením problémů OutOfMemory v oblasti PermGenSpace při redeploy našich aplikací v aplikačních kontejnerech. Před aplikací těchto znalostí jsme vcelku pravidelně po dvou "redeployích" restartovali celý server, protože docházela PermGenSpace. V současném stavu aplikační server žije i po několika desítkách redeployů.</p>
<h3>A nyní slíbený článek</h3>
<p><em>Každého programátora to jednou čeká. Jeho aplikace začne padat na OutOfMemoryError. Dá se krčit rameny se slovy "já vážně nevím čím to je", nebo s tím něco udělat.</em></p>
<p><a id="more"></a><a id="more-63"></a></p>
<h3>Tak mu dej víc paměti</h3>
<p>V ideálním případě je chyba způsobena pouze poddimenzovaným nastavením limitů paměti. Pak stačí nastavit JVM následovně (hodnoty doplnit dle uvážení).</p>
<p>Pro java.lang.OutOfMemoryError: Java heap space</p>
<p>[source lang="xml"]-Xmx256m[/source]</p>
<p>Pro java.lang.OutOfMemoryError: PermGen space</p>
<p>[source lang="xml"]-XX:MaxPermSize=128m[/source]</p>
<p>Další volby v <a href="http://java.sun.com/javase/technologies/hotspot/vmoptions.jsp">dokumentaci Java HotSpot VM</a><span class="absUrlLink"></span>.</p>
<h3>Tak tohle nepomohlo, prubni jmap</h3>
<p>Většinou ale zvýšení přiřazené paměti problém jen oddálí. Pak přijdou na řadu diagnostické nástroje. Tím nejjednodušším je jmap.</p>
<p>Pomocí jmap je možné získat užitečné informace o využití paměti a umožňuje získat HEAP dump.</p>
<p>Více informací o jmap s příklady naleznete v sumarizaci na <a href="http://prefetch.net/blog/index.php/2007/10/27/summarizing-java-heap-utilization-with-jmap/">Blog O'Matty</a><span class="absUrlLink"> </span></p>
<p>S jmap jsem narazil na problém pod Windows Vista. Nepodařilo se mi ho donutit komunikovat s java procesem, který běžel jako service. Pořád tvrdošíjně tvrdil, že „Not enough storage is available to process this command”. Jediné řešení které znám je spustit proces přímo z příkazové řádky.</p>
<h3>Můžu zjistit něco i bez jmap?</h3>
<p>Na JDK 1.5 lze použít následující JSP (je možné ho nakopírovat přímo do deploynuté aplikace)</p>
<p>[source language="html"]<br />
&lt;%@ page import=&quot;java.lang.management.*&quot; %&gt;<br />
&lt;%@ page import=&quot;java.util.*&quot; %&gt;<br />
&lt;h1&gt;Memory&lt;/h1&gt;<br />
&lt;table border=&quot;1&quot;&gt;<br />
&lt;tr&gt;&lt;th width=&quot;100&quot;&gt;&lt;b&gt;Name&lt;/b&gt;&lt;/th&gt;&lt;th width=&quot;150&quot;&gt;Type&lt;/th&gt;&lt;th colspan=&quot;6&quot;&gt;Usage&lt;/th&gt;&lt;/tr&gt;<br />
&lt;tr&gt;<br />
        &lt;td colspan=&quot;2&quot;&gt;&lt;b&gt;Heap Memory summary&lt;/b&gt;&lt;/td&gt;<br />
        &lt;td&gt;&lt;b&gt;Usage&lt;/b&gt;&lt;/td&gt;&lt;td&gt;&lt;%= String.valueOf( ManagementFactory.getMemoryMXBean().getHeapMemoryUsage() ).replace(&quot;)&quot;,&quot;)&lt;/td&gt;&lt;td&gt;&quot;)%&gt;&lt;/td&gt;<br />
&lt;/tr&gt;<br />
&lt;tr&gt;<br />
        &lt;td colspan=&quot;2&quot;&gt;&lt;b&gt;Non-Heap Memory summary&lt;/b&gt;&lt;/td&gt;<br />
        &lt;td&gt;&lt;b&gt;Usage&lt;/b&gt;&lt;/td&gt;&lt;td&gt;&lt;%= String.valueOf( ManagementFactory.getMemoryMXBean().getNonHeapMemoryUsage() ).replace(&quot;)&quot;,&quot;)&lt;/td&gt;&lt;td&gt;&quot;)%&gt;&lt;/td&gt;<br />
&lt;/tr&gt;<br />
&lt;tr&gt;&lt;th colspan=&quot;8&quot;&gt;&lt;/th&gt;&lt;/tr&gt;<br />
&lt;%<br />
Iterator iter = ManagementFactory.getMemoryPoolMXBeans().iterator();<br />
while (iter.hasNext()) {<br />
        MemoryPoolMXBean item = (MemoryPoolMXBean) iter.next(); %&gt;<br />
&lt;tr&gt;<br />
        &lt;td rowspan=&quot;2&quot;&gt;&lt;b&gt;&lt;%= item.getName() %&gt;&lt;/b&gt;&lt;/td&gt;<br />
        &lt;td rowspan=&quot;2&quot;&gt;&lt;%= item.getType() %&gt;&lt;/td&gt;<br />
        &lt;td&gt;&lt;b&gt;Usage&lt;/b&gt;&lt;/td&gt;&lt;td&gt;&lt;%= String.valueOf( item.getUsage() ).replace(&quot;)&quot;,&quot;)&lt;/td&gt;&lt;td&gt;&quot;) %&gt;&lt;/td&gt;<br />
&lt;/tr&gt;<br />
&lt;tr&gt;&lt;td&gt;&lt;b&gt;Peak&lt;/b&gt;&lt;/td&gt;&lt;td&gt;&lt;%= String.valueOf( item.getPeakUsage() ).replace(&quot;)&quot;,&quot;)&lt;/td&gt;&lt;td&gt;&quot;) %&gt;&lt;/td&gt;&lt;/tr&gt;<br />
&lt;%}%&gt;<br />
&lt;/table&gt;<br />
[/source]</p>
<p>Výpis informací může vypadat nějak takhle:</p>
<p style="text-align: center"><a href="http://blog.novoj.net/2008/04/11/permgenspace-problem-no-problem/jmx-memory-information/" rel="attachment wp-att-64" title="JMX memory information"><img src="http://blog.novoj.net/binary//2008/04/jmx-info.thumbnail.gif" alt="JMX memory information" /></a></p>
<h3> Co je to ten perm gen?</h3>
<p>Telegraficky - popis jednotlivých oblastí paměťi JVM (formulace dávají přednost srozumitelnosti před přesnou charakteristikou):</p>
<ul>
<li>Eden Space - oblast kde jsou instance objektů umístěny po jejich vytvoření (young generation)</li>
<li>Survivor Space, Tenured Gen, From/To space - instance objektů s delší platností</li>
<li>Perm Gen - interní data JVM, zde se ukládají načtené třídy (class)</li>
<li>Code Cache - oblast obsahující bytecode přeložený do nativní podoby</li>
</ul>
<p style="text-align: center"><img src="http://blog.novoj.net/binary//2008/04/jvm-gen.gif" alt="Mapa paměti JVM" /></p>
<p>Více se dá dočíst v <a href="http://java.sun.com/docs/hotspot/gc5.0/gc_tuning_5.html">Tuning Garbage Collection with the 5.0 Java Virtual Machine</a><span class="absUrlLink"> </span></p>
<h3>Paměti to žere dost, ale kde?</h3>
<p>Přehled o objektech v paměti lze získat pomocí profilerů. Našinec asi vynechá klasickou komerční řadu produktů (<a href="http://www.yourkit.com/overview/index.jsp">YourKit</a><span class="absUrlLink"></span>, <a href="http://www.quest.com/jprobe/">JProbe</a><span class="absUrlLink"></span>, <a href="http://www.ej-technologies.com/products/jprofiler/overview.html">JProfiler</a><span class="absUrlLink"></span>) a bude hledat něco zdarma (<a href="http://www.netbeans.org/features/java/profiler.html">NetBeans Profiler</a><span class="absUrlLink"></span>). Problémy se ale nejčastěji objevují na produkčních prostředích. A zde je použití profilerů mnohem složitější. Většinou zbývá jediná možnost, získat dump paměti a ten následně analyzovat.</p>
<h4>Použití jmap</h4>
<p>Příklady použití jmap pod Linuxem</p>
<p>[source lang="xml"]<br />
jmap -heap:format=b 18302<br />
Attaching to process ID 18302, please wait...<br />
Debugger attached successfully.<br />
Server compiler detected.<br />
JVM version is 1.5.0_11-b03<br />
heap written to heap.bin<br />
[/source]</p>
<p>A pod windows (JDK 1.6)</p>
<p>[source lang="xml"]<br />
jmap -dump:format=b,file=heap.bin 18302<br />
[/source]</p>
<p>Hodnota 18302 je číslo procesu (PID).</p>
<h4>Dump přímo z JVM</h4>
<p>Následující užitečná nastavení:</p>
<p>JVM provede heap dump pokud dojde k OutOfMemoryError</p>
<p>[source lang="xml"]-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/dump.hprof[/source]</p>
<p>JVM provede heap dump pokud obdrží Ctrl Break</p>
<p>[source lang="xml"]-XX:+HeapDumpOnCtrlBreak[/source]</p>
<p>Generování dumpu může trvat poměrně dlouho (jednotky minut), proto pozor v jaké době dump děláte. JVM v průběhu generování samozřejmně nepracuje.</p>
<h3>Mrkneš se na ten dump? Já se v tom nevyznám.</h3>
<p>Zbývá už „jen zanalyzovat” jaké objekty jsou v paměti. Lze využít některý z profilerů, ale jsou zde i další nástroje.</p>
<h4>jhat - <a href="http://java.sun.com/javase/6/docs/technotes/tools/share/jhat.html">Java Heap Analysis Tool</a><span class="absUrlLink"> </span></h4>
<p>Příklad použití (s nastavením 512MB pro jhat).</p>
<p>[source lang="xml"]<br />
&amp;gt; jhat -J-mx512m dump.hprof<br />
Reading from dump.hprof...<br />
Dump file created Thu Apr 10 18:27:40 CEST 2008<br />
Snapshot read, resolving...<br />
Resolving 639872 objects...<br />
Chasing references, expect 127 dots<br />
...............................................................................................................................<br />
Eliminating duplicate references<br />
...............................................................................................................................<br />
Snapshot resolved.<br />
Started HTTP server on port 7000<br />
Server is ready.<br />
[/source]</p>
<p>JHAT nastartuje webovou aplikaci. Nasměrujte prohlížeč na <a href="http://localhost:7000/">http://localhost:7000/</a><span class="absUrlLink"></span></p>
<p style="text-align: center"><img src="http://blog.novoj.net/binary//2008/04/jhat1.gif" alt="JHat console" /></p>
<p style="text-align: center"><img src="http://blog.novoj.net/binary//2008/04/jhat2.gif" alt="JHat console" /></p>
<h4>Sap Memory Analyzer</h4>
<p>Tento nástroj je skutečně to nejlepší co se mi podařilo pro analýzu heap dumpu najít.</p>
<p><a href="http://blog.novoj.net/binary//2008/04/sap_memory_analyzer_03.png" title="SAP Memory Analyzer"></a></p>
<p style="text-align: center"><a href="http://blog.novoj.net/binary//2008/04/sap_memory_analyzer_03.png" title="SAP Memory Analyzer"><img src="http://blog.novoj.net/binary//2008/04/sap_memory_analyzer_03.thumbnail.png" alt="SAP Memory Analyzer" /></a></p>
<p>Program je <a href="https://www.sdn.sap.com/irj/sdn/wiki?path=/display/Java/Java+Memory+Analysis">volně ke stažení zde</a><span class="absUrlLink"></span>.</p>
<h3>To neřeš, perm gen dochází jen po redeploy</h3>
<p>Častý problém - na aplikačním serveru dochází Perm Gen po několika restartech aplikačního kontextu.</p>
<p>Na serveru nedochází k uvolnění classloaderů a v perm gen zůstávají třídy staré verze aplikace (<a href="http://blogs.sun.com/fkieviet/entry/classloader_leaks_the_dreaded_java">více popisuje Frank Kieviet</a><span class="absUrlLink"></span>).</p>
<p>Ano i já jsem objevil již objevené.</p>
<h4>Problém první - commons logging</h4>
<p>Problémy s commons-logging jsou <a href="http://wiki.apache.org/jakarta-commons/Logging/UndeployMemoryLeak">dobře popsané</a><span class="absUrlLink"></span>, celkem i srozumitelné, ale přece jen. Vzhledem k tomu, že existuje jednoduchý způsob jak se commons-logging úplně zbavit, proč to neudělat.</p>
<p><a href="http://www.slf4j.org/docs.html">SLF4J</a><span class="absUrlLink"></span> umí nahradit commons logging beze změny v aplikaci, pouze nahrazením knihoven. S Maven je řešení úžasně jednoduché. Jediný problém je, jak zajistit aby se do výsledného buildu nedostal commons-logging z tranzitivních dependencí. Řešení je nastavit scope na provided.</p>
<p>Příslušná část pom.xml pak vypadá následovně:</p>
<p>[source lang="xml"]<br />
&lt;dependency&gt;<br />
    &lt;groupId&gt;commons-logging&lt;/groupId&gt;<br />
    &lt;artifactId&gt;commons-logging&lt;/artifactId&gt;<br />
    &lt;version&gt;1.1&lt;/version&gt;<br />
    &lt;scope&gt;provided&lt;/scope&gt;<br />
    &lt;!-- provided knihovny se nedostanou do vysledného WARu/EARu --&gt;<br />
&lt;/dependency&gt;<br />
&lt;dependency&gt;<br />
    &lt;groupId&gt;org.slf4j&lt;/groupId&gt;<br />
    &lt;artifactId&gt;slf4j-api&lt;/artifactId&gt;<br />
    &lt;version&gt;1.5.0&lt;/version&gt;<br />
&lt;/dependency&gt;<br />
&lt;dependency&gt;<br />
    &lt;groupId&gt;org.slf4j&lt;/groupId&gt;<br />
    &lt;artifactId&gt;jcl104-over-slf4j&lt;/artifactId&gt;<br />
    &lt;version&gt;1.5.0&lt;/version&gt;<br />
&lt;/dependency&gt;<br />
&lt;dependency&gt;<br />
    &lt;groupId&gt;org.slf4j&lt;/groupId&gt;<br />
    &lt;artifactId&gt;slf4j-log4j12&lt;/artifactId&gt;<br />
    &lt;version&gt;1.5.0&lt;/version&gt;<br />
&lt;/dependency&gt;<br />
&lt;dependency&gt;<br />
    &lt;groupId&gt;log4j&lt;/groupId&gt;<br />
    &lt;artifactId&gt;log4j&lt;/artifactId&gt;<br />
    &lt;version&gt;1.2.14&lt;/version&gt;<br />
    &lt;!-- SLF4J vyžaduje min. verzi 1.2.12 --&gt;<br />
&lt;/dependency&gt;<br />
[/source]</p>
<h4>Problém druhý - JDBC drivery</h4>
<p>DriverManager v JDBC způsobuje další leak. Pokud nelze přesunout JDBC drivery do knihoven aplikačního serveru, je zde možnost použít context listener pro uvolnění registrovaných driverů:</p>
<p>[source lang="java"]<br />
public class CleanupListener implements ServletContextListener {<br />
    public void contextInitialized(ServletContextEvent event) { }<br />
    public void contextDestroyed(ServletContextEvent event) {<br />
        try {<br />
            Introspector.flushCaches();<br />
            for ( Enumeration e = DriverManager.getDrivers(); e.hasMoreElements(); ) {<br />
                 Driver driver = (Driver) e.nextElement();<br />
                if (driver.getClass().getClassLoader() == getClass().getClassLoader()) {<br />
                     DriverManager.deregisterDriver(driver);<br />
                }<br />
            }<br />
        } catch (Throwable e) {<br />
            System.err.println(&quot;Failled to cleanup ClassLoader for webapp&quot;);<br />
            e.printStackTrace();<br />
        }<br />
    }<br />
}<br />
[/source]</p>
<p>Uvedené řešení, stejně jako problémy s dalšími knihovnami naleznete v článku <a href="http://opensource.atlassian.com/confluence/spring/pages/viewpage.action?pageId=2669">Memory leak - classloader won't let go</a><span class="absUrlLink"></span>.</p>
<p>Asi se zeptáte proč vše neřešit vhodným umístěním knihoven přímo do aplikačního serveru. Zní to jednoduše, nicméně úmyslně jsem řešil problém tak, aby aplikace nebyla závislá na konfiguraci prostředí.</p>
<h3>Dovětek</h3>
<p>Na závěr ještě doporučuji <a href="http://java.sun.com/j2se/1.5/pdf/jdk50_ts_guide.pdf">JavaTM 2 Platform - Troubleshooting and Diagnostic Guide</a><span class="absUrlLink"> a </span><a href="http://www.szegedi.org/articles/memleak.html" target="_blank">A day in the life of a memory leak hunter</a>.</p>
<p>Většina nástrojů je závislá na JDK 1.5, dump lze získat i z posledních verzí JDK 1.4.2. Pokud někdo víte jak vymámit dump z JDK 1.4.2_04 podělte se prosím.</p>
<p>Pro ne-Sunovské implementace JVM může být vše jinak ;-)</p>
<h3>Update k 9.5.2008 - další způsoby jak leakovat classloader</h3>
<p>Následným zkoumáním našich web aplikací jsme přišli na další způsoby, jak spolehlivě přijít o možnost GC classloaderu:</p>
<ul>
<li>
      <strong>Leakování Java Timeru</strong><br> </p>
<p>      při použití Timerů ze standardního balíku Javy se často používá strategie, že při naběhnutí aplikace se nastartují vlákna, která v pravidelných intervalech provádějí určité servisní činnosti. Častou chybou ale je, že při ukončení aplikace, se nastartované Timery neuzavřou. Tím pádem zůstanou instance vašich objektů živé i po stopnutí web aplikace a zamezí zGC classloaderu celé web aplikace.</p>
</li>
<li>
      <strong>Leakování referencí v ThreadLocal</strong><br></p>
<p>      další poměrně často využívaná technika ve web aplikacích je používání ThreadLocal objektů, držících reference na objekty po celou dobu zpracování requestu. Pokud se tyto proměnné na konci zpracování nevyčistí, může v nich zůstat reference na objekt z web aplikace, což opět zabrání zGC jejího classloaderu. Tuto chybu obsahuje například i knihovna iBatis - <a href="https://issues.apache.org/jira/browse/IBATIS-376" target="_new">chyba je již nahlášená z roku 2006</a>, takže kdo ví, jestli se jejího vyřešení dočkáme.
   </li>
</ul>
<h3>Update k 19.6.2008 - způsobů jak leakovat je na tisíc ;-) </h3>
<ul>
<li>
      <strong>Leakování class v Introspectoru</strong><br> </p>
<p>      Pokud používáte (nebo některá z knihoven) JavaBeany a přistupuje te k nim reflexním způsobem (tzn. používáte např. Commons BeanUtils, Spring, nebo další frameworky, které pracují s JavaBeanami) je třeba starat se o vyčištění <a href="http://java.sun.com/j2se/1.5.0/docs/api/java/beans/Introspector.html" target="_new">Introspector</a> cache - což je cache, která udržuje meta informace o třídách, jejich property a dalších věcech, které jsou potřeba. Cache je životně důležitá z hlediska performance. Bohužel Introspector sídlí v classloaderu Javy a tudíž mimo kontext classloader webové aplikace. Classy uložené v cache tedy zabrání GC classloaderu web aplikace. Pokud používáte spring můžete využít <a href="http://static.springframework.org/spring/docs/2.0.x/api/org/springframework/web/util/IntrospectorCleanupListener.html" target="_new">IntrospectorCleanupListener</a>, který je ale potřeba zaregistrovat do web.xml.</p>
<p>      Zajímavé počtení najdeme v dokumentaci k tomuto listeneru:</p>
<p>      <i>Application classes hardly ever need to use the JavaBeans Introspector directly, so are normally not the cause of Introspector resource leaks. Rather, many libraries and frameworks do not clean up the Introspector: e.g. Struts and Quartz.</i></p>
<p>      Cache lze vyčistit také jednoduše vlasním kódem zavoláním: Introspector.flushCaches();</p>
</li>
</ul>
