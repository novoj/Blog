---
status: publish
published: true
title: Nástroje pro vývoj web aplikací ve Forrestu
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft\" title=\"beyond-social-media-monitoring\" src=\"http://blog.novoj.net/binary/2012/08/beyond-social-media-monitoring-300x214.jpg\"
  alt=\"\" width=\"210\" height=\"150\" />Pod ladícím nástrojem si většina Java vývojářů
  představí Java debugger. O něm však v tomto článku řeč nebude. Chtěl bych vám tu
  představit náš přístup k doprovodným nástrojům pro tvorbu webové vrstvy a podívat
  se kolem sebe, jestli jsme v tomto ohledu originální či nikoliv.\r\n\r\nNápad vytvořit
  specifické nástroje se znalostí interních mechanismů použitého frameworku je již
  poměrně starý. V českém PHP frameworku <a href=\"http://nette.org\" target=\"_blank\">Nette</a> vznikla
  tzv. Laděnka někdy na začátku roku 2008 (vycházím ze zmínky na <a href=\"http://latrine.dgx.cz/ladenka-jak-se-vam-libi\"
  target=\"_blank\">blogu Davida Grudla</a>).\r\n\r\nPro některé Javové frameworky
  najdeme také podobné nástroje - Wicket má svůj <a href=\"http://wickeria.com/blog/12-05-23-par-tipu-pro-praci-s-apache-wicket\"
  target=\"_blank\">Debug Bar</a> od roku 2009, Tapestry má <a href=\"http://tapestry.apache.org/tapestry3/doc/DevelopersGuide/inspector.html\"
  target=\"_blank\">Inspector</a> snad od roku 2003, Grails mají <a href=\"http://www.grails.org/Debug+Plugin\"
  target=\"_blank\">Debug plugin</a> někdy od roku 2008 a takto bychom mohli pokračovat
  dál. Se vzrůstající složitostí webových aplikací a frameworků se zdá být užitečné
  mít po ruce nástroj, který vývojářům dokáže odkrýt vnitřní mechanismy a informace
  zpracování požadavků browseru. V některých případech se mi zdá, že nástrojem se
  snaží autoři frameworku pomoci vývojářům lépe kontrolovat jeho slabá místa - v případě
  Wicketu velikost stavových objektů v session, v případě Nette třeba problematická
  práce s vyjímkami v PHP. My našeho webového Inspektora a související nástroje vyvíjíme
  postupně již od začátku roku 2009 a v tomto článku bych vám rád popsal co mají naši
  vývojáři k dispozici a proč.\r\n\r\n"
wordpress_id: 2178
wordpress_url: http://blog.novoj.net/?p=2178
date: '2012-09-04 07:10:53 +0200'
date_gmt: '2012-09-04 06:10:53 +0200'
categories:
- Programování
- Java
tags: []
comments:
- id: 91064
  author: Guido
  author_email: vit.kotacka@gmail.com
  author_url: http://www.sw-samuraj.cz/
  date: '2012-09-09 10:05:46 +0200'
  date_gmt: '2012-09-09 09:05:46 +0200'
  content: "To je moc hezký nástroj! Myslím, že jste to dotáhli mnohem, mnohem dál,
    než nabízí jakýkoliv jiný framework (co znám).\r\n\r\nJá mám přímou zkušenost
    z projektu s Wicketem. Vzhledem k tomu, že jsme do session serializovali minimum
    objektů a měli aplikaci hodně založenou na Ajaxu, tak spíš než <i>debug bar</i>
    jsme používali <i>Wicket Ajax Debug</i>. Každopádně, tyhle nástroje, které umožní
    nahlédnou \"dovnitř\" hodně napomáhají řešení problémů a často i pomůžou vyřešit
    nějaký vnitřní design komponenty.\r\n\r\nKromě těch frameworkových nástrojů poměrně
    intenzivně používám <i>Chrome Developer Tools</i>. Tam se to sice zastaví na úrovni
    webové vrstvy/prohlížeče, ale je to super nástroj pro ladění JavaScriptů, CSS
    a (vlastností a stavů) HTML elementů."
- id: 91084
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-09-09 12:02:21 +0200'
  date_gmt: '2012-09-09 11:02:21 +0200'
  content: Díky, já už si vývoj bez tohoto nástroje taky už nedokážu představit. Chrome
    developer tools taky používám, ale nějak jsem si víc přivykl na Firebug a pořád
    si nedokážu úplně zvyknout na jiný přístup v Chrome. A to i přesto, že Chrome
    používám jako svůj hlavní prohlížeč.
- id: 100456
  author: "&raquo; Jak jsem organizoval Forrestí hackathon Myšlenky dne otce Fura"
  author_email: ''
  author_url: http://blog.novoj.net/2012/10/21/jak-jsem-organizoval-forresti-hackathon/
  date: '2012-10-21 19:48:46 +0200'
  date_gmt: '2012-10-21 18:48:46 +0200'
  content: "[...] se nám jich podařilo zrealizovat osm a tak se od pondělí můžeme
    těšit z nového pluginu pro Inspektora v Google Chrome, vylepšenou práci s lokalizačním
    nástrojem v něm, zbrusu novou sadou [...]"
---
<p><img class="alignleft" title="beyond-social-media-monitoring" src="http://blog.novoj.net/binary/2012/08/beyond-social-media-monitoring-300x214.jpg" alt="" width="210" height="150" />Pod ladícím nástrojem si většina Java vývojářů představí Java debugger. O něm však v tomto článku řeč nebude. Chtěl bych vám tu představit náš přístup k doprovodným nástrojům pro tvorbu webové vrstvy a podívat se kolem sebe, jestli jsme v tomto ohledu originální či nikoliv.</p>
<p>Nápad vytvořit specifické nástroje se znalostí interních mechanismů použitého frameworku je již poměrně starý. V českém PHP frameworku <a href="http://nette.org" target="_blank">Nette</a> vznikla tzv. Laděnka někdy na začátku roku 2008 (vycházím ze zmínky na <a href="http://latrine.dgx.cz/ladenka-jak-se-vam-libi" target="_blank">blogu Davida Grudla</a>).</p>
<p>Pro některé Javové frameworky najdeme také podobné nástroje - Wicket má svůj <a href="http://wickeria.com/blog/12-05-23-par-tipu-pro-praci-s-apache-wicket" target="_blank">Debug Bar</a> od roku 2009, Tapestry má <a href="http://tapestry.apache.org/tapestry3/doc/DevelopersGuide/inspector.html" target="_blank">Inspector</a> snad od roku 2003, Grails mají <a href="http://www.grails.org/Debug+Plugin" target="_blank">Debug plugin</a> někdy od roku 2008 a takto bychom mohli pokračovat dál. Se vzrůstající složitostí webových aplikací a frameworků se zdá být užitečné mít po ruce nástroj, který vývojářům dokáže odkrýt vnitřní mechanismy a informace zpracování požadavků browseru. V některých případech se mi zdá, že nástrojem se snaží autoři frameworku pomoci vývojářům lépe kontrolovat jeho slabá místa - v případě Wicketu velikost stavových objektů v session, v případě Nette třeba problematická práce s vyjímkami v PHP. My našeho webového Inspektora a související nástroje vyvíjíme postupně již od začátku roku 2009 a v tomto článku bych vám rád popsal co mají naši vývojáři k dispozici a proč.</p>
<p><a id="more"></a><a id="more-2178"></a>Pro vývoj webových aplikací používáme vlastní komponentově orientovaný webový framework integrovaný do <a href="http://www.edee-cms.cz/" target="_blank">Edee CMS</a>. Důvodem proč jsme nešli cestou existujících frameworků jsou naše specifické požadavky na vývoj, kdy aplikaci vyvíjí společně Java vývojáři i tzv. web developeři (což jsou experti na HTML a CSS, ale nejsou to svým zaměřením programátoři) a tato platforma nám umožňuje efektivně dělit i sdílet práci. V zásadě jde o to, že aktuálně jsou naši web developeři vytvořit webovou aplikaci bez účasti Java vývojářů, kteří se primárně zabývají business vrstvou aplikace. V místech, kde je potřeba volat nějaké specifické akce nebo dotahovat data z jádra aplikace se použijí záslepky, které Java vývojáři zamění za reálnou logiku, jakmile je hotova.</p>
<p>Vývoj by se dal přirovnat k tomu, který znáte z Wicket frameworku s tím rozdílem, že u nás práce web developerů nekončí u přípravy statických HTML šablon + CSS, ale sahá dál až k funkčnímu prototypu cílové aplikace - tj. šablony jsou již rozparcelovány do znovupoužitelných komponent, mezi stránkami funguje navigace, texty jsou lokalizované do různých jazyků a formuláře jsou včetně většiny validací funkční. To vše bez jediné čárky Java kódu - pouze s využitím deklarativního DSL v XML formátu, se kterým jsou webdevelopeři sžití.</p>
<p>S rozšířením kompetencí našich web developerů bylo potřeba dát jim k dispozici taky nástroj, pomocí kterého by dokázali nahlédnout pod kapotu toho, co vlastně vytvářejí a používají. Řada věcí se totiž poslepu dělala velmi komplikovaně - kupříkladu určení správného umístění <a href="http://freemarker.sourceforge.net/" target="_blank">Freemarker</a> šablony, odhadnutí klíče lokalizovaného textu nebo odhalení triviálních chyb v konfiguraci způsobených překlepy. Častokrát nezbylo než požádat o pomoc Java vývojáře s debuggerem, který přes socket pomohl problém odladit. To ale zdržovalo všechny a ne vždy bylo jednoduché se debuggerem na rozjetý projekt napíchnout. Vytvoření pomůcky pro ladění bylo tedy jen logickým krokem k řešení této bolesti.</p>
<h2>Jak inspektor vypadá</h2>
<p>Inspektor je malá webová aplikace napsaná ve stejné technologii, které umožňuje introspekci a je dostupná pouze ve <a href="http://blog.novoj.net/2009/08/07/odlisujete-v-aplikaci-vyvojove-testovaci-a-produkcni-prostredi/" target="_blank">vývojovém a testovacím prostředí</a>. V těchto režimech jsou ke každé web stránce, která je renderovaná připsány dodatečné cookies, které obsahují URL na jednotlivé části inspektora. Na tyto cookies reaguje náš jednoduchý Firefox plugin, který zobrazuje lištu a kontextové nabídky integrované přímo v prohlížeči. Ten potom při kliknutí na konkrétní tlačítko zobrazí nové popup okno s odpovídající webovou adresou vybraného pohledu inspektora. Představu si můžete udělat z tohoto obrázku:</p>
<p style="text-align: center;"><a href="http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/firefox_plugin/" rel="attachment wp-att-2194"><img class="aligncenter" title="Firefox plugin" src="http://blog.novoj.net/binary/2012/08/firefox_plugin-1024x818.jpg" alt="" width="627" height="500" /></a></p>
<p>Výhodou tohoto přístupu je, že webový vývojář má ladící nástroj při práci rychle po ruce. Aktuálně zvažujeme i implementaci pluginu pro Chrome, jelikož ten se i u nás prosazuje čím dál víc. Tím, že je plugin do prohlížeče velmi tenký (v podstatě se jen integruje do nabídek, čte cookies a zobrazuje popup okno) nebude portace do dalších prohlížečů obtížná.</p>
<h2>Co inspektor umí?</h2>
<p>Základem našeho inspektora, který jsme postupně rozvíjeli, bylo zobrazení stromu komponent aktuálně prohlížené stránky. Jak je vidět z přiloženého obrázku - vlevo je přehledně zobrazená struktura stránky, napravo potom detail konfigurace konkrétní vybrané komponenty. Kromě základních identifikačních informací je zde k dispozici náhled nastavených metadat, konvertorů uživatelských dat na Javovské datové typy a také specifické validace, které se k datům komponenty vztahují. Detail se samozřejmě adaptuje podle typu vybrané komponenty - pokud komponenta neumožňuje vstup uživatele, odpovídající sekce zmizí. Při výběru celé stránky se opět zobrazí jiné relevantní informace:</p>
<p style="text-align: center;"><a href="http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/snimek-obrazovky-2012-08-29-232535/" rel="attachment wp-att-2197"><img class="aligncenter" title="Inspektor #1" src="http://blog.novoj.net/binary/2012/08/Snímek-obrazovky-2012-08-29-232535-1024x531.png" alt="" width="627" height="325" /></a></p>
<p>Záložka <strong>Dokumentace</strong> zobrazuje aktuální popis vzatý z JavaDoc konkrétní třídy ve verzi, která je na daném projektu nasazená. Dokumentaci vytahujeme automatizovaně pomocí knihovny <a href="http://qdox.codehaus.org/index.html" target="_blank">QDox</a> rovnou z odpovídajících zdrojových souborů, které si podle Maven identifikátorů (groupId, artifactId a version) uložených v bundlovaném JARu stáhneme na pozadí online z naší firemní repository.  Používání aktuální dokumentace z JavaDocu vychází z mé úvahy v článku <a href="http://blog.novoj.net/2011/03/16/zamysleni-nad-tvorbou-programatorske-dokumentace/" target="_blank">Zamyšlení nad tvorbou programátorské dokumentace</a> a tam je také myšlenka rozvedena do větších podrobností.</p>
<p>V popisu konkrétního objektu (komponenty, stránky, akce, validace, konverze atp.) je i seznam jejich vlastností a metod, které jsou rozdělené na 2 části - dokumentované -tj. ty, u kterých se počítá s použitím našimi webdevelopery a nedokumentované, které jsou určené spíše pro Java vývojáře a které by výpis znepřehledňovaly a cílovku zbytečně mátly. Ukázka dokumentace validátoru <em>imageFormat</em> vypadá následovně:</p>
<p style="text-align: center;"><a href="http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/snimek-obrazovky-2012-08-31-220111/" rel="attachment wp-att-2209"><img class="aligncenter" title="Dokumentace #1" src="http://blog.novoj.net/binary/2012/08/Snímek-obrazovky-2012-08-31-220111.png" alt="" width="572" height="491" /></a></p>
<p>V záložce <strong>Šablony </strong>je vypsán seznam umístění Freemarkerových šablon seřazený prioritně podle toho, jak je webový framework vyhledává. Přetěžování šablon je jednou z unikátních vlastností, které nám umožňují pro konkrétní komponentu definovat univerzální vzhled pro celou aplikaci, ale stále mít možnost ji na konkrétních specifických částech systému přetížit a upravit dle potřeb. Webdeveloperům stačí jen na správném (prioritnějším) místě vytvořit soubor s odpovídajícím názvem a po refreshi stránky se použije nová šablona. Bohužel bez vizualizace nebylo dříve jednoduché odhadout, jak systém vypočetl seznam umístění pro konkrétní šablony.</p>
<p style="text-align: center;"><a href="http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/snimek-obrazovky-2012-08-29-232738/" rel="attachment wp-att-2208"><img class="aligncenter" title="Inspektor #3" src="http://blog.novoj.net/binary/2012/08/Snímek-obrazovky-2012-08-29-232738-1024x531.png" alt="" width="627" height="325" /></a></p>
<p>Vkládání lokalizovaných textů do webových stránek probíhá standardní Javovskou cestou - přes Property bundly. V tomto směru využíváme skvělé podpory Springu ve formě ReloadableResourceBundle, jak jsem jej <a href="http://blog.novoj.net/2009/01/27/prekonany-resourcebundle-spring-messagesource-vitezi-v-prvnim-kole-ko/" target="_blank">popsal v tomto článku</a>. Díky pár úpravám jsme schopni monitorovat, jaká oblast stránky používá které lokalizované klíče a zobrazit je v záložce <strong>Lokalizace</strong>. U dlouhých stránek je možné zúžit výpis výběrem konkrétní komponenty (kontejneru) na stránce.</p>
<p>U jednotlivých klíčů se využívá podobného mechanismu jako ve Spring MVC - tj. každý klíč má vícero variant od té nejvíce specifické až po tu nejobecnější. Je možné tak mít obecné texty pro celý web, které je možné na konkrétních stránkách upravovat dle konkrétních potřeb. Taktéž známe kompletní seznam všech Properties bundlů, které se při vyhledávání lokalizovaných textů berou v úvahu a dokážeme přesně provázat nalezený text se zdrojovým souborem, ve kterém se nachází. Lepší představu si uděláte z následujícího screenshotu:</p>
<p style="text-align: center;"><a href="http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/snimek-obrazovky-2012-08-29-232822/" rel="attachment wp-att-2220"><img class="aligncenter" title="Inspektor #3" src="http://blog.novoj.net/binary/2012/08/Snímek-obrazovky-2012-08-29-232822-1024x531.png" alt="" width="627" height="325" /></a></p>
<h2>Slovníky dostupných komponent</h2>
<p>Další položkou v naší vývojářské liště jsou <strong>Slovníky</strong>. Ta zobrazuje seznam dostupných objektů, které mohou webdevelopeři při tvorbě webu použít. Najdou zde kompletní seznam akcí, validátorů, poskytovatelů dat a dalších typů objektů včetně dokumentace, která je přímo vytažená z Javadoců odpovídajících tříd (stejným principem, jaký byl již popsán výše).</p>
<p>Zásadní je ovšem to, že tento dialog čerpá informace přímo z interní struktury webového frameworku, takže poskytuje úplný a přesný obrázek toho, co je skutečně k dispozici. Pokud tedy náš Javista vytvoří novou implementaci poskytovatele dat pro stránkovaný seznam - tj. vytvoří novou třídu, která implementuje konkrétní rozhraní, a uvede ji v konfiguraci slovníku nějakého modulu, objeví se web developerům v tomto seznamu včetně dokumentace, kterou pro ně Javista zanechal v JavaDocu. Tento "publikační" proces nelze obejít - protože jinak by webdeveloper danou implementaci ani nemohl použít - tj. v tomto principu je obsažen jak funkční tak i samodokumentační faktor.</p>
<p style="text-align: center;"><a href="http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/snimek-obrazovky-2012-08-29-233107/" rel="attachment wp-att-2225"><img class="aligncenter" title="Slovníky" src="http://blog.novoj.net/binary/2012/08/Snímek-obrazovky-2012-08-29-233107-1024x531.png" alt="" width="627" height="325" /></a></p>
<p>Slovníky je možné definovat na různých místech stromové struktury stránek, vzájemně mezi sebou dědí, je možné je importovat napříč touto strukturou a webdevelopeři je mohou sami doplňovat či upravovat. Ve výchozím stavu je zobrazen slovník, který přináleží aktuálně zobrazované aplikační stránce v prohlížeči. K navigaci mezi slovníky a zúžení výběru zobrazovaných položek slouží ovládací prvky v horní části přiloženého screenshotu (<em>vybrat jiný slovník</em> a <em>zobrazit pouze lokální položky</em>).</p>
<h2>Dokumentace</h2>
<p>Pod položkou dokumentace se skrývá jednak referenční dokumentace ke všem dostupným klíčovým slovům, tagům, Freemarkeru a dalším základním stavebním kamenům webové části aplikace a také <a href="http://blog.novoj.net/2011/03/16/zamysleni-nad-tvorbou-programatorske-dokumentace/" target="_blank">tématická dokumentace</a> k jednotlivým oblastem frameworku, která se dá číst jako knížka a dá programátorům dobrý vhled do různých zákoutí funkcionality. Dokumentace je psána s použitím jednoduchých HTML tagů a je uložena přímo v JARech našich knihoven. Tím pádem se vývojářům zobrazuje dokumentace odpovídající té verzi frameworku, který právě používají k vývoji své aplikace a nemusíme se dlouze zabývat verzováním dostupnosti konkrétních nastavení a funkcí.</p>
<p style="text-align: center;"><a href="http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/snimek-obrazovky-2012-08-29-233244/" rel="attachment wp-att-2226"><img class="aligncenter" title="Dokumentace" src="http://blog.novoj.net/binary/2012/08/Snímek-obrazovky-2012-08-29-233244-1024x748.png" alt="" width="627" height="458" /></a></p>
<h2>Lokalizační nástroj</h2>
<p>Pro zjednodušení a urychlení tvorby lokalizovatelných textů je k dizpozici tlačítko lokalizace, které zobrazí seznam všech klíčů na vykreslované stránce, pro které se nepodařilo najít odpovídající lokalizovaný text. Vývojáři stačí většinou jen naskládat komponenty na stránku (popřípadě si vytvořit vlastní specifické šablony a použít v nich tagy pro použití lokalizovaných textů), jednou si nechat stránku vyrenderovat a pak otevřít tento dialog pro usnadnění lokalizace, ve kterém se mu zobrazí všechny klíče, které je třeba zlokalizovat. Klíče zkopíruje do některého z property bundlů a přeloží je. Po refreshi stránky se již zobrazí správně zlokalizované varianty.</p>
<p style="text-align: center;"><a href="http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/snimek-obrazovky-2012-08-29-233319/" rel="attachment wp-att-2238"><img class="aligncenter  wp-image-2238" title="Lokalizace" src="http://blog.novoj.net/binary/2012/09/Snímek-obrazovky-2012-08-29-233319.png" alt="" width="607" height="418" /></a></p>
<h2>Ladička</h2>
<p>Ladička je posledním nástrojem na naší paletě a umožňuje se dívat na průběh zpracování jednotlivých HTTP požadavků. Dala by se přirovnat k <a href="http://getfirebug.com/" target="_blank">Firebugu</a> s tím rozdílem, že představuje pohled ze strany serveru. Tj. vidíme, jaké všechny HTTP požadavky dorazily do naší aplikace, jaké měly vstupy, jaký modul je zpracovával, jaké byly hodnoty cookies, hlaviček požadavku atp.</p>
<p><a href="http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/snimek-obrazovky-2012-08-29-233436/" rel="attachment wp-att-2237"><img class="aligncenter size-large wp-image-2237" title="Debugger #1" src="http://blog.novoj.net/binary/2012/09/Snímek-obrazovky-2012-08-29-233436-1024x587.png" alt="" width="627" height="359" /></a></p>
<p>Na druhé záložce je zobrazen průběh zpracování requestu frameworkem. Je vidět jakými fázemi životního cyklu zpracování prochází, jak dlouho jednotlivé části zpracování trvají, jaké akce se volají, jaké hodnoty jsou vráceny poskytovateli dat na dané stránce. Tato stránka je užitečná především ve chvíli, kdy aplikace nedělá, co jako vývojáři očekáváme. Dá se zde odhalit použití prezentační cache (která je neoddělitenou součástí frameworku) místo očekávaného volání aplikační logiky, načítání a zapisování dat do komponent, skrývání / odkrývání podmínečně zobrazovaných částí stránky apod. Často se také hodí introspekce Java objektů (podobná té, kterou znáte ze svého IDE), které se v průběhu zpracování použily (ikona lupy).</p>
<p><a href="http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/snimek-obrazovky-2012-08-29-233500/" rel="attachment wp-att-2241"><img class="aligncenter size-large wp-image-2241" title="Debugger #2" src="http://blog.novoj.net/binary/2012/09/Snímek-obrazovky-2012-08-29-233500-1024x587.png" alt="" width="627" height="359" /></a></p>
<p>Poslední záložka je interaktivní konzole, ve které je možné si nechat vyhodnotit v kontextu vybraného HTTP requestu (i historicky) konkrétní výraz našeho výrazového jazyka - tzv. RJEL. Tento výrazový jazyk je velmi podobný <a href="http://static.springsource.org/spring/docs/3.0.0.M3/reference/html/ch07.html" target="_blank">SpEL</a>, který byl, bohužel pro nás, zveřejněn až rok po tom, co jsme my ten náš už produkčně používali. Aktuálně zvažujeme, jestli a jak by bylo možné náš RJEL přetavit ve variantu SpEL, který je z hlediska syntaxe a možností o řád bohatší.</p>
<p>Výsledek ve formě introspektovaných Java objektů zobrazuje ve spodní části obrazovky. Pomocí výrazového jazyka si můžeme nechat zobrazit hodnoty uložené v session, vytáhnout si informace z libovolného ze zaregistrovaných poskytovatelů dat, zobrazovat si hodnoty stavů konkrétních komponent atp.</p>
<p><a href="http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/snimek-obrazovky-2012-08-29-233742/" rel="attachment wp-att-2242"><img class="aligncenter size-large wp-image-2242" title="Debugger #3" src="http://blog.novoj.net/binary/2012/09/Snímek-obrazovky-2012-08-29-233742-1024x587.png" alt="" width="627" height="359" /></a></p>
<p>Pomocí této konzole se můžeme dívat do střev běžící aplikace a dá se tímto způsobem odhalit plno problémů, aniž bychom museli zprovozňovat a používat Java debugger.</p>
<h2>A naše zkušenosti po 3 letech používání?</h2>
<p>Několik desítek hodin investovaných do Inspektora se nám už několikrát vrátilo ačkoliv přínos je obtížně měřitelný. Některé funkcionality doposud ještě nejsou využívány, tak jak bych si představoval - především část dokumentace, která dlouho pokulhávala (a ještě stále pokulhává) za rozsahem dostupné funkcionality a tak si svoji důvěru teprve získává. Nejvíce využívané funkce jsou ty, které přímo šetří práci - třeba lokalizační dialog nebo záložka inspektora s přístupem k Freemarker šablonám. Interaktivní konzole RJEL, přestože je v sadě nástrojů nejmladší, si svoji oblibu získala taky poměrně rychle.</p>
<p>Celou řadu ostatních funkcí využívám ale pouze já a kolegové Javisti, když na dálku poskytujeme podporu našim webdeveloperům. Při množství projektů, které Forrest realizuje, je úspora času při této činnosti veliká. Dříve jsme si kvůli různorodým verzím použitých knihoven museli stáhnout projekt z VCS, zprovoznit v IDE, pokusit se vzdáleně háknout na JVM, kde projekt běžel, a debuggovat konkrétní třídy. Na řadě míst byl remote debugging nemožný a proto jsme si museli projekt rozjíždět lokálně (např. na testovacích prostředích nám JVM neběží v debug režimu nebo když webdeveloper sedí na jiné pobočce a je potřeba ladit na verzi v jeho lokálním prostředí). Často taková situace představovala třeba 2 hodiny na zprovoznění projektu, kde se během 10 minut oddebugoval a odhalil triviální problém. V současnosti jsme schopni většinu problémů odhalit pomocí inspektora, což kromě času šetří spoustu nervů.</p>
<p>Vím, že naše použití a potřeby jsou poměrně specifické, ale vzhledem k tomu, že podobné nástroje najdete i v jiných frameworcích, možná i vy používáte také nějaký takový nástroj pro podporu vývoje webové vrstvy. Pokud ano, budu rád, když se o své názory a zkušenosti podělíte v komentářích.</p>
