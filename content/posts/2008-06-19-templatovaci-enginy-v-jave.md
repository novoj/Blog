---
status: publish
published: true
title: Exkurz do templatovacích enginů v Javě
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Templatovací jazyky v Javě mají poměrně dlouhou minulost. První a zřejmě
  nejznámnější jsou JSP, které jsou součástí javy. Jsou nejstarší z rodiny templatovacích
  jazyků a přestože jsou masivně používány dodnes, mnoho lidí k nim má své výhrady:\r\n\r\n<ul>\r\n
  \  <li>psaní JSP je obtížné pro ne-java programátory - přestože původní myšlenkou
  bylo, aby JSP psali odborníci na web (tedy \"webdevelopeři\") tato myšlenka zcela
  jistě minula realitu; praxe je taková, že JSP píší z různých důvodu opět Java developři,
  jejichž je jednak nedostatek a jednak jejich zaměření je spíš na aplikační kód než
  na validitu a použitelnost HTML výstupu</li>\r\n   <li>JSP stránky nejsou použitelné,
  díky životnímu cyklu JSP (JSP -&gt; .java -&gt; .class), mimo servletový kontejner
  - to znamená, že teprve servletový kontejner po nadeployování web aplikce JSP převede
  na implementace Servletů a přeloží je do binární podoby. Dopady tohoto mechanismu
  jsou poměrně jasné\r\n   <ul>\r\n      <li>JSP stránky mají své pevné umístění -
  hledají se vždy na filesystemu v adresáři web aplikace; nelze je umístit na classpath
  (a učinit je tak součástí přenositelných knihoven), nelze je načítat z jiného zdroje
  - např. databáze (a umožnit tak vznik nových stránek za běhu na systémech, kde nemáme
  přístup na filesystém), nelze definovat jakoukoliv složitější logiku načítání stránek
  krom dodání Erorr 404 stránky (např. custom logika ve smyslu neexistuje-li primární
  šablona, použij záložní, neexistuje-li ani ta, zobraz chybu)</li>\r\n      <li>JSP
  stránky není možné jednoduše testovat - jejich výstup získáme teprve až dotazem
  na servletový kontejner</li>\r\n      <li>JSP nelze použít pro skládání jiného výstupu
  než do web browseru - např. pro skládání  těl emailů musíme volit jiný templatovací
  engine</li>\r\n      <li>debugování JSP nebylo poměrně dlouho možné a ani dnes to
  není zcela samozřejmá a jednoduchá věc (co se setupu týče)</li>\r\n      <li>chybové
  hlášky JSP stránek jsou při určitém (často standardním) nastavení kontejnerů nečitelné
  (vztahují se k vygenerovaným servletům a nikoliv k původní template) - změna tohoto
  nastavení typicky vyžaduje stop/start kontejneru</li>\r\n   </ul>\r\n   </li>\r\n
  \  <li>JSP stránky díky možnosti psaní scriptletů vybízejí k míchání aplikační logiky
  do prezentační vrstvy - s tím se myslím setkal každý z nás a leckdo se k tomu někdy
  i uchýlil</li>\r\n   <li>v případech některých kontejnerů je při změně JSP a požadavku
  na její opětovné vyrenderování znatelná časová prodleva - kompilace JSP vyžaduje
  nějaký čas (možná se jedná jen o zlomky vteřiny, maximálně vteřiny, ale při ladění
  nějakých drobnostní na stránce se jakákoliv prodleva počítá)</li>\r\n</ul>\r\n\r\nReakcí
  na zmíněné nevýhody byl vznik interpretovaných templatovacích jazyků. V tomto příspěvku
  bych se chtěl podívat na zoubek dvěma nejznámnějším - Apache Velocity a FreeMarkeru.\r\n\r\n"
wordpress_id: 74
wordpress_url: http://blog.novoj.net/2008/06/19/templatovaci-enginy-v-jave/
date: '2008-06-19 07:07:17 +0200'
date_gmt: '2008-06-19 06:07:17 +0200'
categories:
- Java
- Web
tags: []
comments: []
---
<p>Templatovací jazyky v Javě mají poměrně dlouhou minulost. První a zřejmě nejznámnější jsou JSP, které jsou součástí javy. Jsou nejstarší z rodiny templatovacích jazyků a přestože jsou masivně používány dodnes, mnoho lidí k nim má své výhrady:</p>
<ul>
<li>psaní JSP je obtížné pro ne-java programátory - přestože původní myšlenkou bylo, aby JSP psali odborníci na web (tedy "webdevelopeři") tato myšlenka zcela jistě minula realitu; praxe je taková, že JSP píší z různých důvodu opět Java developři, jejichž je jednak nedostatek a jednak jejich zaměření je spíš na aplikační kód než na validitu a použitelnost HTML výstupu</li>
<li>JSP stránky nejsou použitelné, díky životnímu cyklu JSP (JSP -&gt; .java -&gt; .class), mimo servletový kontejner - to znamená, že teprve servletový kontejner po nadeployování web aplikce JSP převede na implementace Servletů a přeloží je do binární podoby. Dopady tohoto mechanismu jsou poměrně jasné
<ul>
<li>JSP stránky mají své pevné umístění - hledají se vždy na filesystemu v adresáři web aplikace; nelze je umístit na classpath (a učinit je tak součástí přenositelných knihoven), nelze je načítat z jiného zdroje - např. databáze (a umožnit tak vznik nových stránek za běhu na systémech, kde nemáme přístup na filesystém), nelze definovat jakoukoliv složitější logiku načítání stránek krom dodání Erorr 404 stránky (např. custom logika ve smyslu neexistuje-li primární šablona, použij záložní, neexistuje-li ani ta, zobraz chybu)</li>
<li>JSP stránky není možné jednoduše testovat - jejich výstup získáme teprve až dotazem na servletový kontejner</li>
<li>JSP nelze použít pro skládání jiného výstupu než do web browseru - např. pro skládání  těl emailů musíme volit jiný templatovací engine</li>
<li>debugování JSP nebylo poměrně dlouho možné a ani dnes to není zcela samozřejmá a jednoduchá věc (co se setupu týče)</li>
<li>chybové hlášky JSP stránek jsou při určitém (často standardním) nastavení kontejnerů nečitelné (vztahují se k vygenerovaným servletům a nikoliv k původní template) - změna tohoto nastavení typicky vyžaduje stop/start kontejneru</li>
</ul>
</li>
<li>JSP stránky díky možnosti psaní scriptletů vybízejí k míchání aplikační logiky do prezentační vrstvy - s tím se myslím setkal každý z nás a leckdo se k tomu někdy i uchýlil</li>
<li>v případech některých kontejnerů je při změně JSP a požadavku na její opětovné vyrenderování znatelná časová prodleva - kompilace JSP vyžaduje nějaký čas (možná se jedná jen o zlomky vteřiny, maximálně vteřiny, ale při ladění nějakých drobnostní na stránce se jakákoliv prodleva počítá)</li>
</ul>
<p>Reakcí na zmíněné nevýhody byl vznik interpretovaných templatovacích jazyků. V tomto příspěvku bych se chtěl podívat na zoubek dvěma nejznámnějším - Apache Velocity a FreeMarkeru.</p>
<p><a id="more"></a><a id="more-74"></a></p>
<h3>Apache Velocity</h3>
<p><a href="http://technorati.com/claim/gjjyxtxp8" rel="me">Technorati Profile</a></p>
<p>Jako první si vezmu na paškál Velocity. Nevím, zda je to pouze moje zkušenost, ale zdá se mi, že Apache Velocity je hned po JSP nejpoužívanějším templatovacím jazykem v Javě. Možná je to dáno tím, že je vývojově starší a také proto, že je vždy propagováno jako velmi jednoduché k osvojení.</p>
<p>Skutečně Velocity je velmi jednoduché a dokážete jej nasadit a používat týž den, kdy s tímto jazykem začnete. Velocity interpretuje rovnou originální šablonu (respektive si z šablony vytváří vlastní <a href="http://en.wikipedia.org/wiki/Abstract_syntax_tree" target="_new">AST</a>) - bez mezikroku kompilace do Java kódu, což urychluje první zobrazení po změně.</p>
<p>Pro vývojáře je podstatné, že umožňuje dodat vlastní implementaci ResourceLoaderu - respektive vybrat si nejvíce vyhovující z již existujících implementací (ClasspathResourceLoader, DataSourceResourceLoader, FileResourceLoader, JarResourceLoader, StringResourceLoader, URLResourceLoader).</p>
<div style="margin: 10px; padding: 5px; border: 1px solid white; background-color: #333333; font-size: 90%">
Pokud se zabýváte modulárními web systémy, brzy narazíte na problém, jak spolu s modulem dodávat jeho prezenační vrstvu. Jedním z možných rešení (avšak velmi nepěkným) je mergování WAR archívů popsané v <a href="http://blog.softeu.cz/maven-a-zavislost-na-waru/" target="_new">postu na SoftEU blogu</a>. Druhým je použití templatovacího nástroje, který vám umožní dodávat šablony z classpath modulu, který pak může zůstat obyčejným JARem. Rozhraní ResourceLoaderu vám však umožňuje daleko víc - načítání šablon může být klidně i podmínečné, takže jednoduše dokážete implementovat logiku načítání šablon podle priority (např. nejdříve se hledá šablona na disku a teprve, když není nalezena bere se výchozí šablona z classpath). To všechno jsou věci, které s JSP nedokážete.
</div>
<p>Templatovací <a href="http://velocity.apache.org/engine/releases/velocity-1.5/user-guide.html" target="_new">jazyk je velmi jednoduchý</a> a asi není jej třeba nějak do detailu rozebírat. Jednoduchá šablona ve Velocity může vypadat třeba takto:</p>
<p>[source:html]<br />
<HTML><br />
    <HEAD><br />
      <TITLE>Hello World!</TITLE><br />
    </HEAD><br />
    <BODY><br />
      <CENTER><br />
      <B>We've reached $downloadCount of Firefox 3!</B><br />
      <BR/><br />
      We are proud to announce that we've achieved new Guiness record.<br />
      <BR/><br />
      Top countries in download were:<br />
      <TABLE><br />
        #foreach($country in $countryList)<br />
          <TR><br />
            <TD>$velocityCount.</TD><br />
            <TD>$country</TD><br />
          </TR><br />
        #end<br />
      </TABLE><br />
      <BR/><br />
      <I>Stay loyal!</I><br />
      </CENTER></p>
<p>    </BODY><br />
</HTML><br />
[/source]</p>
<p>Vygenerování výsledného výstupu z Javy může vypadat například takhle:</p>
<p>[source lang="java"]<br />
/*  first, get and initialize an engine  */<br />
VelocityEngine ve = new VelocityEngine();<br />
ve.init();<br />
/*  next, get the Template  */<br />
Template t = ve.getTemplate( "helloworld.vm" );<br />
/*  create a context and add data */<br />
VelocityContext context = new VelocityContext();<br />
context.put("downloadCount", new Integer(10000000));<br />
List topCountries = new ArrayList();<br />
topCountries.add("United States of America");<br />
topCountries.add("Germany");<br />
topCountries.add("Spain");<br />
context.put("countryList", topCountries);<br />
/* now render the template into a StringWriter */<br />
StringWriter writer = new StringWriter();<br />
t.merge( context, writer );<br />
/* show the World */<br />
System.out.println( writer.toString() );<br />
[/source]</p>
<p>Velocity vám poskytne základní věci, které byste od šablonovacího enginu čekali: include (parse) direktivy pro skládání šablon, makra, jednoduchou práci s objekty, se kterými pracujete v Java - tzn. JavaBeanami apod. Pro přenášení dat do a z šablon slouží kontext, což je takový kbelík na data, se kterými se v šabloně pracuje - příjemné je, že i z šablony mohou vzejít nějaká data, o která byste mohli mít zájem v javovském kódu (a ty právě najdete ve zmíněném kontextu).</p>
<p>Knihovna má také již připravený <a href="http://velocity.apache.org/engine/releases/velocity-1.4/api/org/apache/velocity/servlet/VelocityServlet.html" target="_new">vlastní servlet</a>, který vyrenderuje výstup šablony přímo do HttpResponse.</p>
<p>Podívejme se však o vývojový stupeň dál.</p>
<h3>Freemarker</h3>
<p>Už předchozí věta je trochu hozením rukavice. Po zkušenosti s oběma knihovnami však musím konstatovat, že FreeMarker je skutečně o vývojovou etapu dál. Můžete od něj očekávat to samé co od velocity, ale řeší také plno nedostatků výše zmíněné knihovny. Na tyto nedostatky bych se chtěl podívat na následujících řádcích:</p>
<p><strong>Detalní chybové hlášení</strong></p>
<p>Jedním z palčivých problémů Velocity jsou chybová hlášení. Ještě nedávno byly ve Velocity problémem <a href="http://blog.hibernate.org/Bloggers/Everyone/Year/2006/Month/02/Day/03#a_story_about_freemarker_and_velocity%3Cbr%20/%3Ehttp://www.javaworld.com/javaworld/jw-11-2007/jw-11-java-template-engines.html?page=3" target="_new">chybová hlášení</a> - ani u základních chyb nebylo lehce rozeznatelné v jaké šabloně se jaká chyba vyskytuje. V tomto ohledu již Velocity udělalo pokrok, nicméně výstup FreeMarkerových chyb se mi zdá pro webdevelopry daleko srozumitelnější. Výhoda také je, že FreeMarker vypíše i stack volání jednotlivých template, takže se dá velmi jednoduše orientovat i v chybách uvnitř maker, nebo nestovaných šablon.</p>
<p><strong>Užívání namespace pro linkované knihovny maker nebo JSP tagů</strong></p>
<p>Ve velocity jsou všechna makra házena do na jednu kupu. Pokud byste se tedy vášnivě pustili do výraznějšího vývoje ve Velocity, za chvíli byste začali narážet na konflikty jmen. FreeMarker zavádí pro makra a proměnné <a href="http://freemarker.sourceforge.net/docs/dgui_misc_namespace.html" target="_new">namespace</a>, přes které se na ně dá odkázat. To výrazně zpřehledňuje strukturu šablon.</p>
<p><strong>Podpora JSP tagů</strong></p>
<p>Jedna ze zásadních věcí ve FreeMarkeru je možnost používat JSP tagy. Pokud tedy přecházíte z JSP (jako jsme přešli my), jistě uvítáte možnost zachovat beze změny všechen kód v připravených JSP tazích. FreeMarker zvládne najít všechny tagy v odkazovaných TLD z web.xml a také dokonce všechny tagy v TLD souborech v META-INF na classpath. Jediné co FreeMarker neinterpretuje jsou JSP EL funkce definované v TLD. Tato funkcionalita nám ušetřila mraky času.</p>
<p><strong>Direktivy pro práci s whitespace</strong></p>
<p>Ve Velocity je velkým problémem dodržet vzhed výsledného textu ve smyslu odřádkování a odsazení. Velocity neumožňuje nijak odstraňovat nepotřebný whitespace, který ve výsledném textu nepůsobí dobře, ale ve v šabloně je kvůli přehlednosti naopak potřeba (v souvislosti se strukturou řídících direktiv apod.). <a href="http://freemarker.org/docs/dgui_misc_whitespace.html" target="_new">FreeMarker tyto direktivy nabízí</a>.</p>
<p><strong>Metaprogramování</strong></p>
<p>Ve FreeMarkeru můžete <a href="http://fmpp.sourceforge.net/freemarker/ref_directive_assign.html" target="_new">přiřadit kód šablony do proměnné</a>, kterou pak dále používat. Interpretace obsahu proběhne pouze jednou a v dalších "použitích" se jen vypíše již interpretovaný obsah proměnné.</p>
<p>Jednoduše lze také interpretovat kód v libovolné proměnné - např. mějme třídu:</p>
<p>[source lang="java"]<br />
public class Test {</p>
<p>   public String getFreemarkerSnippet() {<br />
      return "${x}";<br />
   }</p>
<p>}<br />
[/source]</p>
<p>A potom freemarker šablonu (<a href="http://freemarker.sourceforge.net/docs/ref_builtins_expert.html" target="_new">viz. dokumentace</a>):</p>
<p>[source:html]<br />
<#assign x = "something"><br />
Test: ${test.freemarkerSnippet?interpret}<br />
[/source]</p>
<p>Výsledkem bude potom tento výstup:</p>
<p>[source:html]<br />
Test: something<br />
[/source]</p>
<p><strong>Výkon</strong></p>
<p>FreeMarker je <a href="http://www.javaworld.com/javaworld/jw-11-2007/jw-11-java-template-engines.html?page=3" target="_new">podle některých statistik</a> rychlejší jak Velocity. Každopádně jak píší v <a href="http://freemarker.sourceforge.net/docs/app_faq.html#faq_question_24" target="_new">dokumentaci k FreeMarkeru</a> - FreeMarker pravděpodobně nikdy nebude úzkým hrdlem vaší aplikace. Nejnáročnější operací je parsování do AST, které je pak už ale cachované, takže se provádí už jen processing šablony a ten by se v rychlosti dal jistě s JSP srovnat. Pokud tedy narazíte na výkonnostní problémy - buď máte vypnutou cache, nebo bude váš problém ležet ve vrstvách níže.</p>
<h3>Závěrem</h3>
<p>Pokud jste nikdy nevyzkoušeli žádný z templatovacích enginů, doporučuji některý z nich určitě vyzkoušet. Pokud používáte Apache Velocity - což je pravděpodobnější případ - doporučuji rozhodně kouknout na FreeMarker, protože vás bude čekat příjemné překvapení. FreeMarker zvládnete nasadit za den, stejně jako Velocity, ale odmění se vám daleko širšími možnostmi použití a hlavně se vám s ním bude lépe pracovat.</p>
<p>Zajímavé jsou zkušenosti ostatních vývojářů, které lze na webu najít (pár jich uvádím v užitečných odkazech na konci článku). Poměrně zajímavé je konstatování, že valná většina lidí, která přešla od Velocity k FreeMarkeru už u FreeMarkeru zůstala. <a href="http://www.howardism.org/thoughts/001511.html" target="_new">Ti kteří šli opačnou cestou</a> od FreeMarkeru k Velocity se zase hodně rychle vrátili. Už jen to o něčem svědčí.</p>
<p>Zajímavé závěry lze také udělat z <a href="http://wiki.apache.org/velocity/RoadMap" target="_new">roadmapy k Velocity v. 2</a> - jistě si všimnete, že v plánovaných vylepšeních jsou věci, které ve FreeMarkeru už nějaký ten pátek máme.</p>
<p>Pro FreeMarker <a href="http://freemarker.sourceforge.net/editors.html" target="_new">dostante podporu ve většině IDE</a>. Do nejlepšího z nich ;-) se <a href="http://www.jetbrains.net/confluence/display/IDEADEV/Diana+First+EAP+Release+Notes" target="_new">podpora teprve chystá</a> (měla by být do konce roku 2008). Velocity nemá takové zastoupení v Java editorech, nicméně je <a href="http://wiki.apache.org/velocity/VelocityEditors" target="_new">daleko větší podpora v jednodušších editorech</a> (které jsou naopak více používány mezi webaři). V tomto ohledu má tedy FreeMarker ještě co dohánět.</p>
<h3>Užitečné odkazy</h3>
<ul>
<li><a href="http://nb.vse.cz/~zelenyj/it442/eseje/xbarj49/velocity.htm" target="_new">Krátký úvod do Apache Velocity v češtině</a></li>
<li><a href="http://nb.vse.cz/~zelenyj/it380/eseje/xrohj04/freemarker.htm" target="_new">Krátký úvod do FreeMarkeru v češtině</a></li>
<li><a href="http://blog.hibernate.org/Bloggers/Everyone/Year/2006/Month/02/Day/03#a_story_about_freemarker_and_velocity<br />
http://www.javaworld.com/javaworld/jw-11-2007/jw-11-java-template-engines.html?page=3" target="_new">Srovnání FreeMarker a Velocity na InRelationTo Blogu jedním z Hibernate týmu</a></li>
<li><a href="http://freemarker.blogspot.com/2007/12/velocity-of-freemarker-looking-at-5.html" target="_new">Pohled na 5 let historie FreeMarkeru - ohlédnutí směrem k Velocity</a></li>
<li><a href="http://freemarker.org/fmVsVel.html" target="_new">Porovnání s Velocity na FreeMarker website</a></li>
<li><a href="http://www.jivesoftware.com/community/blogs/clearspace/tags/jsp" target="_new"></a></li>
<li><a href="http://article.gmane.org/gmane.comp.web.freemarker.user/2984" target="_new">Osobní zkušenosti s FreeMarkerem vůči použití JSP</a></li>
<li><a href="http://wiki.apache.org/velocity/RoadMap" target="_new">RoadMap Velocity - zajímavé jsou fíčury ve verzi 2.0 - kdo vidí FreeMarker jako já? :-) </a></li>
</ul>
