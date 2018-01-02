---
status: publish
published: true
title: Nepíšete javadoc komentáře? Díky Java 8 vězte, že dobře děláte!
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<div style=\"border: 1px solid white; background-color: #333333; font-size:
  90%; margin-top: 20px; margin-right: 80px;\">\r\n\r\n<a title=\"Tomáš Zilvar\" href=\"https://cz.linkedin.com/pub/tomáš-zilvar/a/744/3a2\"><img
  style=\"margin-left: 10px; margin-right: 10px; margin-top: 10px;\" src=\"http://blog.novoj.net/binary/2015/10/TZI_square.jpg\"
  alt=\"Tomáš Zilvar\" width=\"50\" height=\"50\" align=\"left\" /></a>\r\n\r\n<strong>O
  autorovi: </strong><a href=\"Tomáš Zilvar\">LinkedIn</a>\r\n<p style=\"margin: 10px;\">Tomáš
  za dobu svého působení v oboru soudí, že programátor jest živoucím důkazem platnosti
  Paretova pravidla 80/20 - 20 % času programuje a 80 % času bádá, proč to nefunguje.
  Empiricky mezitím ověřil, že je to nezávislé na tom, zda programuje v korporaci
  nebo malé firmě, i na použité technologii.</p>\r\n\r\n</div>\r\nJavu 8 na rozdíl
  od Javadoc komentářů (to jsou ty mezi /** a */;) nepoužívá úplně každý javista,
  ale jak se říká, jednou tam musíme všichni. Kvůli rozhodnutí Oracle přidat do Java
  8 javadocu hodně striktní kontrolu obsahu javadoc komentářů, a to rovnou ve výchozím
  nastavení, může ale jejich kombinace přivodit i zásadní bolehlav způsobený nemožností
  releasovat starší projekty kvůli na první pohled absurdním chybám. Jak z toho ven,
  aniž bychom museli přepisovat několik let starou dokumentaci?\r\n\r\n"
wordpress_id: 3072
wordpress_url: http://blog.novoj.net/?p=3072
date: '2015-11-05 14:32:26 +0100'
date_gmt: '2015-11-05 13:32:26 +0100'
categories:
- Programování
- Java
tags: []
comments: []
---
<div style="border: 1px solid white; background-color: #333333; font-size: 90%; margin-top: 20px; margin-right: 80px;">
<p><a title="Tomáš Zilvar" href="https://cz.linkedin.com/pub/tomáš-zilvar/a/744/3a2"><img style="margin-left: 10px; margin-right: 10px; margin-top: 10px;" src="http://blog.novoj.net/binary/2015/10/TZI_square.jpg" alt="Tomáš Zilvar" width="50" height="50" align="left" /></a></p>
<p><strong>O autorovi: </strong><a href="Tomáš Zilvar">LinkedIn</a></p>
<p style="margin: 10px;">Tomáš za dobu svého působení v oboru soudí, že programátor jest živoucím důkazem platnosti Paretova pravidla 80/20 - 20 % času programuje a 80 % času bádá, proč to nefunguje. Empiricky mezitím ověřil, že je to nezávislé na tom, zda programuje v korporaci nebo malé firmě, i na použité technologii.</p>
</div>
<p>Javu 8 na rozdíl od Javadoc komentářů (to jsou ty mezi /** a */;) nepoužívá úplně každý javista, ale jak se říká, jednou tam musíme všichni. Kvůli rozhodnutí Oracle přidat do Java 8 javadocu hodně striktní kontrolu obsahu javadoc komentářů, a to rovnou ve výchozím nastavení, může ale jejich kombinace přivodit i zásadní bolehlav způsobený nemožností releasovat starší projekty kvůli na první pohled absurdním chybám. Jak z toho ven, aniž bychom museli přepisovat několik let starou dokumentaci?</p>
<p><a id="more"></a><a id="more-3072"></a></p>
<h2>Pokrok nezastavíš</h2>
<p>Předně mi nedá nepozastavit se nad rozhodnutím autorů Javy 8, kteří pro mě nepochopitelně zařadili tuto kontrolu jako default s možností vypnutí namísto volitelného zapnutí. Java tím po dvou dekádách naprosté benevolence úplně otočila přístup ke kontrole struktury javadoc komentářů. Dosud v nich mohlo být téměř cokoli a javadoc si maximálně postěžoval warningy, teď rovnou vrátí chybu a shodí tím celý build, často z malicherných důvodů (viz níže).</p>
<p>Šikovný nástroj DocLint a bohulibá snaha o zkvalitnění dokumentace se tak velice rychle stala noční můrou všech projektů s delší historií. Lze dohledat značné množství odkazů na téma doclint, obvykle ve spojení se slovy jako breaks, invalid a disable…</p>
<h2>Velký DocLint tě vidí</h2>
<p>Výsledek kontroly staršího projektu si dovedete představit, ani novější na tom ale nebududou lépe (uvádím jen unikátní chyby, skutečný počet vynásobte stem):</p>
<div id="highlighter_593245">
<p>[source language="xml"]user@hostname:~/www/project/myproject$ mvn javadoc:jar<br />
[ERROR] Failed to execute goal org.apache.maven.plugins:maven-javadoc-plugin:2.9.1:jar (default-cli) on project myproject: MavenReportException: Error while creating archive:<br />
[ERROR] /home/user/www/project/myproject/library/src/main/java/cz/sys/tis/AccidentList.java:181: error: bad use of '&gt;'<br />
[ERROR] * &lt;/element&gt;<br />
[ERROR] ^<br />
[ERROR] /home/user/www/project/myproject/library/src/main/java/cz/sys/tis/ObjectFactory.java:75: warning: no @return<br />
[ERROR] public AccidentList.Accident.ImpactDescriptionList createAccidentListAccidentImpactDescriptionList() {<br />
[ERROR] ^<br />
[ERROR] /home/user/www/project/myproject/library/src/main/java/cz/sys/tis/ObjectFactory.java:83: warning: no @return<br />
[ERROR] public AccidentList.Accident.AlternateSupplyList.AlternateSupplyItem createAccidentListAccidentAlternateSupplyListAlternateSupplyItem() {<br />
[ERROR] /home/user/www/project/myproject/library/src/main/java/com/fg/client/filter/CityOwnerRightsToDocumentFilter.java:125: warning - Tag @see:illegal character: &quot;64&quot; in &quot;{@link CityOwnerRightsToDocumentFilter#getCityCode(String)}&quot;<br />
[ERROR] /home/user/www/project/myproject/library/src/main/java/com/fg/client/model/price_list/PriceList.java:118: warning: no description for @return<br />
[ERROR] * @return<br />
[ERROR] ^<br />
[ERROR] /home/user/www/project/myproject/library/src/main/java/com/fg/client/web/frontend/model/MapMarkerSet.java:35: warning: no description for @param<br />
[ERROR] * @param geolocated<br />
[ERROR] ^[/source]</p>
<p>Pokud vám přijde, že trocha kontroly neuškodí, vězte, že se jedná o kontrolu místy až absurdně přísnou. Je založena na HTML 4.01 specifikaci, která se kontroluje tak, jak ji chápe Oracle, tedy nikoli validací oproti DTD nebo XSD. Pokud se k tomu přičte to, že i oficiální Java nástroje generují neplatné javadoc komentáře (wsimport, xjc), a fakt, že <b>nikde nejsou zdokumentována kontrolovaná pravidla</b> (maximálně se dají vyčíst ze<a href="http://grepcode.com/file/repository.grepcode.com/java/root/jdk/openjdk/8-b132/com/sun/tools/doclint/Checker.java">zdrojového kódu kontrolující třídy</a> a <a href="http://grepcode.com/file/repository.grepcode.com/java/root/jdk/openjdk/8-b132/com/sun/tools/doclint/HtmlTag.java">něco-jako-DSL zápisu pravidel pro HTML tagy</a>), dává to dohromady zaručený recept na katastrofu. Z pravidel, která jsem našel, jsou to například:</p>
<ul>
<li>Zakázaný znak &lt;, ale co víc, i &gt; (který je jinak povolený!) - potěší zvláště ty, kteří jsou zvyklí každou třídu podepisovat jako <code>@author Franta Brabec &lt;fbr@fg.cz&gt;</code></li>
<li>Chybějící atribut <code>summary</code> nebo element <code>caption</code> u tabulky <code>table</code> - přiznám se bez mučení, že o summary slyším poprvé a caption jsem snad nikdy nikam nepsal</li>
<li>Chybějící nebo nepopsaný (!) <code>@return</code> / <code>@throws</code> u funkcí s návratovou hodnotou nebo kontrolovanou výjimkou.</li>
</ul>
<p>a další více či méně závažné prohřešky proti specifikaci, které zmiňuje v <a href="http://blog.joda.org/2014/02/turning-off-doclint-in-jdk-8-javadoc.html">blog postu o vypnutí doclintu Stephen Colebourne</a>:</p>
<p><em>With JDK 8, you are unable to get Javadoc unless your tool meets the standards of doclint. Some of its rules are:</em></p>
<ul>
<li><em>no self-closed HTML tags, such as &lt;br /&gt; or &lt;a id="x" /&gt;</em></li>
<li><em>no unclosed HTML tags, such as &lt;ul&gt; without matching &lt;/ul&gt;</em></li>
<li><em>no invalid HTML end tags, such as &lt;/br&gt;</em></li>
<li><em>no invalid HTML attributes, based on doclint's interpretation of W3C HTML 4.01</em></li>
<li><em>no duplicate HTML id attribute</em></li>
<li><em>no empty HTML href attribute</em></li>
<li><em>no incorrectly nested headers, such as class documentation must have &lt;h3&gt;, not &lt;h4&gt;</em></li>
<li><em>no invalid HTML tags, such as List&lt;String&gt; (where you forgot to escape using &amp;lt;)</em></li>
<li><em>no broken @link references</em></li>
<li><em>no broken @param references, they must match the actual parameter name</em></li>
<li><em>no broken @throws references, the first word must be a class name</em></li>
</ul>
<p><em>Note that these are errors, not warnings. <b>Break the rules and you get no Javadoc output.</b></em></p>
<p>Nic proti kvalitní dokumentaci, ale tepat autora Java kódu, o který snad jde stále v první řadě, za chyby v generovaném HTML výstupu určeném pro zobrazení ve velmi benevolentních prohlížečích, a ještě o tom nikam nenapsat, <b>to se nám opravdu, ale opravdu nezdá</b>. Místo toho, aby autor byl motivován k tomu, aby javadoc komentářích bylo alespoň něco, vyhrávají totiž ti, kteří tam nenapíšou vůbec nic. Jak z toho tedy ven, aniž by bylo nutné přepisovat několik let staré komentáře?</p>
<h2>Vítězství sestává se ze samých průs…švihů</h2>
<p>Nebyla by to přísná kontrola, kdyby se nedala jednoduše obejít. Javadocu stačí předat parametr <code>-Xdoclint:none</code>. Není to ale zase tak jednoduché, jak by se na první pohled zdálo:</p>
<ul>
<li>Parametr je totiž <b>zpětně nekompatibilní</b>, jeho použití ve starších verzích javy vede k chybě o neznámém parametru a tedy neúspěchu kompilace</li>
<li>Různé buildovací frameworky (Maven, Gradle, Ant) používají javadoc automaticky v rámci pluginů nebo podobných mechanismů a <b>někdy je potíž mu parametr podstrčit</b></li>
<li>V Mavenu nastává problém pouze při <code>release</code> nebo <code>javadoc</code> pluginu (nikoli při <code>install</code> nebo <code>deploy</code>).</li>
<li>V FG Forrest releasujeme často z lokálních strojů, kde není jednoduché předem určit, jaká Java bude použita, maven ji detekuje (alespoň pro mě) nevyzpytatelně.</li>
</ul>
<p>Podařilo se mi najít <a href="https://github.com/dropwizard/dropwizard/blob/master/pom.xml#L265-L273">řešení, které umožní build ve všech verzích Javy</a>, aniž by bylo nutné nějak hýbat s konfigurací. Využívá profily a silent parametry pluginů. Stačí v pom.xml v sekci <code>project/profile</code> uvést profil, který se aktivuje pro Java 8 (a vyšší) a definuje property.</p>
<p>[source language="xml"]<br />
&lt;profile&gt;<br />
 &lt;id&gt;java8-disable-strict-javadoc&lt;/id&gt;<br />
 &lt;activation&gt;<br />
 &lt;jdk&gt;[1.8,)&lt;/jdk&gt;<br />
 &lt;/activation&gt;<br />
 &lt;properties&gt;<br />
 &lt;javadoc.doclint.none&gt;-Xdoclint:none&lt;/javadoc.doclint.none&gt;<br />
 &lt;/properties&gt;<br />
&lt;/profile&gt;<br />
[/source]</p>
<p>Potom v konfiguraci pluginu <code>maven-javadoc-plugin</code>, který javadoc v rámci releasu spouští, předat tento parametr s <code>quiet=true</code>, aby si build nestěžoval, pokud ho v nižších verzích Javy nebude mít.</p>
<p>[source language="xml"]&lt;plugin&gt;<br />
   &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;<br />
   &lt;artifactId&gt;maven-javadoc-plugin&lt;/artifactId&gt;<br />
   &lt;configuration&gt;<br />
      &lt;additionalparam&gt;${javadoc.doclint.none}&lt;/additionalparam&gt;<br />
      &lt;quiet&gt;true&lt;/quiet&gt;<br />
   &lt;/configuration&gt;<br />
&lt;/plugin&gt;[/source]</p>
<p>Celá konfigurace tedy může vypadat takto:</p>
<p>[source language="xml"]&lt;profiles &gt;<br />
     &lt;profile &gt;<br />
     &lt;id &gt;basic &lt;/id &gt;<br />
     &lt;build &gt;<br />
       &lt;plugins &gt;<br />
         &lt;plugin &gt;<br />
         &lt;groupId &gt;org.apache.maven.plugins &lt;/groupId &gt;<br />
         &lt;artifactId &gt;maven-javadoc-plugin &lt;/artifactId &gt;<br />
         &lt;configuration &gt;<br />
         &lt;additionalparam &gt;${javadoc.doclint.none} &lt;/additionalparam &gt;<br />
         &lt;quiet &gt;true &lt;/quiet &gt;<br />
         &lt;/configuration &gt;<br />
         &lt;/plugin &gt;<br />
       &lt;/plugins &gt;<br />
     &lt;/build &gt;<br />
     &lt;/profile &gt;<br />
     &lt;profile &gt;<br />
     &lt;id &gt;java8-disable-strict-javadoc &lt;/id &gt;<br />
     &lt;activation &gt;<br />
       &lt;jdk &gt;[1.8,) &lt;/jdk &gt;<br />
     &lt;/activation &gt;<br />
     &lt;properties &gt;<br />
       &lt;javadoc.doclint.none &gt;-Xdoclint:none &lt;/javadoc.doclint.none &gt;<br />
     &lt;/properties &gt;<br />
     &lt;/profile &gt;<br />
 &lt;/profiles&gt;[/source]</p>
<h2>TL;DR - vypnout a psát, jako by to bylo zapnuté</h2>
<p>Jediné rozumné řešení je myslím doclint vypnout. Přepisovat nic nemá smysl a generované věci teprve ne. Ne všechna pravidla jsou ale k ničemu - v zájmu budoucích generací i v zájmu kvality dokumentace na ně pokud možno pamatujte a řiďte se jimi, alespoň těmi smysluplnými. Nikdy totiž nevíme dne ani hodiny, kdy Oracle odstraní i možnost vypnutí kontroly.</p>
</div>
