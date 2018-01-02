---
status: publish
published: true
title: 7 tipů pro práci v Debug režimu v IntelliJ Idea
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Před lety jsem psal <a href=\"http://blog.novoj.net/2007/04/09/debugging-v-praxi-%E2%80%93-opravdu-samozrejmost/\">článek
  o debugování aplikací v Javě</a>. K mému překvapení jsem se totiž setkal s programátory,
  kteří v Javě k debugování kódu používali System.out(...) místo debug režimu. Po
  letech otvírám stejné téma z jiného pohledu. Jak efektivně používáme nástroje debug
  režimu, které nám naše IDE nabízí? Je totiž plno situací, kdy se můžeme s debugováním
  dost nadřít, nebo ... vědět co a jak v daném okamžiku nastavit tak, abychom se k
  výslednému pochopení problému dostali zkratkou. IntelliJ Idea těchto nástrojů nabízí
  celou řadu a v tomto článku bych rád rozebral několik z nich, které sám rád používám.\r\n\r\n"
wordpress_id: 704
wordpress_url: http://blog.novoj.net/?p=704
date: '2010-01-05 21:06:37 +0100'
date_gmt: '2010-01-05 20:06:37 +0100'
categories:
- Java
- Softwarové nástroje
- IntelliJ Idea
tags: []
comments:
- id: 16545
  author: podlesh
  author_email: podlesh@podlesh.cz
  author_url: ''
  date: '2010-01-06 09:36:33 +0100'
  date_gmt: '2010-01-06 08:36:33 +0100'
  content: S těmi breakpointy na fieldy pozor - nemusí (netestoval jsem všechna JDK)
    zareagovat při nastavení pomocí reflection nebo deserializace :-(
- id: 16556
  author: benzin
  author_email: bendal@quick.cz
  author_url: ''
  date: '2010-01-06 16:56:03 +0100'
  date_gmt: '2010-01-06 15:56:03 +0100'
  content: "No vsechno tohle sem automaticky v Eclipse pouzival az n to prejmenovani
    intanci a stapping. To by mohlo byt pomerne uzitecne (zkusim to najit).\r\n\r\nNo
    ale vedlo mne to k jine myslence. Prilis neholduju buildovani z IDE, obzvlast
    kdyz nad kodem mate navesene dalsi tooly, ktere ho predpripravi nez dojde k samotne
    kompilaci. Pro JavaME je to dost potreba, protoze jinak je vsechno desne praccne.
    No a pokud nema dany tool intergraci pro vase IDE dost se zapotite. No takze by
    to chtelo aby HotSwap sel spustit mimo IDE a pokud mozno primo do rozjeteho emulatoru
    JavaME. Mate s necim takovym zkusenosti? Ted sem nasel jenom maven2-hotswap-plugin,
    ale nevim jestli to tim vyresim (budu zkouset), ale jestli mate nekdo s necim
    takovym zkusenosti, dejte mi prosim vedet."
- id: 16558
  author: Petr Prochazka
  author_email: pprochazka@gk-software.com
  author_url: ''
  date: '2010-01-06 18:11:19 +0100'
  date_gmt: '2010-01-06 17:11:19 +0100'
  content: "Ja jeste hodne casto pri krokovani pouzivam Shift + F7 (Smart Step Into).\r\nZobrazi
    se pop menu se vsemi volanymi metodami na radku. Vetsinou chci skocit do te posledni,
    ktera je volana"
- id: 16560
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-01-06 20:32:23 +0100'
  date_gmt: '2010-01-06 19:32:23 +0100'
  content: "@benzin poslední idea (možná to umí i osmička) má na compiler navěšený
    Annotation processing, nevím, jestli by se to k tomu nemohlo využít. Praktické
    zkušenosti ale nemám - navíc pro mobily jsem zatím nikdy neprogramoval, takže
    tady si nedovolím žádný komentář. Pro naše účely Idea dokáže plně nahradit maven
    build, s tím rozdílem, že je výrazně rychlejší.\r\n\r\n@Petr Prochazka: díky -
    tohle jsem postřehl při brouzdání novinkami v Idee, ale neobjevil jsem nikde zkratku.
    Díky vyzkouším."
- id: 16570
  author: Tomas Zalusky
  author_email: zalusky@centrum.cz
  author_url: ''
  date: '2010-01-07 11:29:00 +0100'
  date_gmt: '2010-01-07 10:29:00 +0100'
  content: Diky za clanek, ne vsechno jsem znal (pouzivam sice Eclipse, ale bylo prijemne
    to v nem objevit :-).
- id: 16576
  author: antaran
  author_email: martin.vician@gmail.com
  author_url: http://www.zont.eu
  date: '2010-01-07 19:43:46 +0100'
  date_gmt: '2010-01-07 18:43:46 +0100'
  content: super clanok...uz mi nebude vrtat hlavou na co tam to "Mark Object" vlastne
    je :), ten breakpoint na NullPointerException si tiez vyskusam :)
- id: 18484
  author: ghost
  author_email: lubos.mifacek@seznam.cz
  author_url: ''
  date: '2010-02-10 10:02:58 +0100'
  date_gmt: '2010-02-10 09:02:58 +0100'
  content: "Super clanek. O tom hotswapu jsem nevedel, jak na to.\r\nNyni resim ale
    tento problem. Pouzivam debugger na vzdalene debugovani web aplikace. Vse funguje
    ok, tak ale zmenim strukturu classy, udelam redeploy, ale dalsi hotswap uz nefunguje,
    jakoby si porad nekde drzela starou nezmenenou classu.. Pomuze jen restart idei\r\nNevite
    nekdo, jak na to?\r\nBuild a (re)deploy resim pres ANT, mimo ideu.."
- id: 18677
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-02-12 09:16:49 +0100'
  date_gmt: '2010-02-12 08:16:49 +0100'
  content: To úplně nechápu ... redeploy znamená, stopnutí a nastartování app serveru?
    Nebo jen stopnutí kontextu, ale app server stále žije? Zkuste trošku blíž popsat,
    co se tam vlastně děje ...
- id: 18686
  author: ghost
  author_email: lubos.mifacek@seznam.cz
  author_url: ''
  date: '2010-02-12 11:04:49 +0100'
  date_gmt: '2010-02-12 10:04:49 +0100'
  content: "Redeploy je asi jen stopnuti kontextu, ostatni aplikace na domene jedou
    dal i v prubehu redeploy. Pouzivame Sun portal na Glassfish 8.1.\r\nPouzivame
    Ant org.apache.tools.ant.taskdefs.optional.sun.appserv.DeployTask, nenina tom
    nic specialniho."
- id: 18703
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-02-12 13:36:03 +0100'
  date_gmt: '2010-02-12 12:36:03 +0100'
  content: "V tom případě bych si tipnul, že po redeploy zmizí tebou původně hotswapovaná
    verze třídy (tříd) a načte se verze z daného WARu. Nicméně novým hotswapem by
    se měl dát normálně zase vyměnit obsah metod. Pokud se tak neděje, tak je to opravdu
    možná nějaká issue Idey.\r\n\r\nAbych pravdu řekl, pro vývoj používám kompilační
    výsledek Idey (při synchronizaci s Mavenem je při standardních buildech identicky
    s buildem spuštěným přes Maven) a restart Tomcata. Tohle je asi nejrychlejší turnaround,
    ke kterému jsem dospěl. Idea má totiž narozdíl od Antu/Mavenu přehled o tom, které
    třídy a jejich závislosti je nutné překompilovat a udělá jen ty. Ant/Maven musím
    slepě překompilovat všechno, protože ty vazby neznají.\r\n\r\nTím pádem používám
    úplně jiný use-case a díky tomu jsem asi na tebou popisovaný problém nenarazil."
- id: 18704
  author: ghost
  author_email: lubos.mifacek@seznam.cz
  author_url: ''
  date: '2010-02-12 13:49:41 +0100'
  date_gmt: '2010-02-12 12:49:41 +0100'
  content: "Ja bych spis rekl, ze se ta nova verze nenacte a to je ten problem. Idea
    si porad mysli, ze byla provedena zmena struktury.. Jde o to vymazat nejak tu
    z idey tu starou strukturu a prekvapive rebuild aplikace nepomuze, ale restart
    idei ano. Zrejme se pouziva nejaka cache..\r\nDiky za tvuj cas."
- id: 18713
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-02-12 17:01:04 +0100'
  date_gmt: '2010-02-12 16:01:04 +0100'
  content: "Ještě mě napadá, jestli by to nemohlo souviset s classloader leakem. Co
    když se při restartu kontextu neuvolnil ten starý classloader a stále je v paměti?
    Bohužel netuším jak funguje při JVM hotswapu nalezení třídy u které se má vyměňovat
    její obsah. Třeba je někde pořád živá reference na tu původní \"už hotswapovanou\"
    classu v neuvolněném classloaderu? Jenže tady už úplně vařím z vody ... tohle
    by chtělo nějaký test.\r\n\r\nOdpojení debug režimu a nové nastartování taky nepomůže?\r\nCo
    restart serveru ... ten asi pomůže stejně jako restart Idey že?"
- id: 19873
  author: Jety
  author_email: mail@jetensky.net
  author_url: http://jetensky.net/blog
  date: '2010-02-23 14:11:22 +0100'
  date_gmt: '2010-02-23 13:11:22 +0100'
  content: "Ahoj Honzo, díky za tipy, určitě se mi hodí ten drop frames, věděl jsem,
    že se v tom bodě dá dívat na proměnné, ale ne že se dá odtud znovu debugovat.\r\n\r\nTaky
    díky za Smart Step Into (z komentáře od Petra Prochazky)."
- id: 48543
  author: Stacie Brostrom
  author_email: Kromm@gmail.com
  author_url: http://www.yahoo.co.uk
  date: '2011-08-12 03:00:26 +0200'
  date_gmt: '2011-08-12 02:00:26 +0200'
  content: I came across your webpage this afternoon and its a really great enlightening
    read however , the font looks somewhat skewed in safari.
---
<p>Před lety jsem psal <a href="http://blog.novoj.net/2007/04/09/debugging-v-praxi-%E2%80%93-opravdu-samozrejmost/">článek o debugování aplikací v Javě</a>. K mému překvapení jsem se totiž setkal s programátory, kteří v Javě k debugování kódu používali System.out(...) místo debug režimu. Po letech otvírám stejné téma z jiného pohledu. Jak efektivně používáme nástroje debug režimu, které nám naše IDE nabízí? Je totiž plno situací, kdy se můžeme s debugováním dost nadřít, nebo ... vědět co a jak v daném okamžiku nastavit tak, abychom se k výslednému pochopení problému dostali zkratkou. IntelliJ Idea těchto nástrojů nabízí celou řadu a v tomto článku bych rád rozebral několik z nich, které sám rád používám.</p>
<p><a id="more"></a><a id="more-704"></a></p>
<h3>1. HotSwapping</h3>
<p>Výměnu tříd v JVM za běhu v debug režimu zná snad každý. Několikrát jsem však musel radit lidem, kterým to "nefungovalo" nebo nevěděli hned jak v IntelliJ Idee, jak na to. HotSwaping i IntelliJ Idee zafunguje tehdy, jste li v debug režimu a zkompilujete třídu (Ctrl + Shift + F9) nebo celý projekt (Ctrl + F9). Následně by měl vyběhnout popup, který vás informuje o počtu vyměněných tříd, popř. o chybě. Chyba nastává v případě, že v třídě provedete <a href="http://www.zeroturnaround.com/jrebel/comparison/">strukturální změnu</a>. Viz. následující obrázek:</p>
<div align="center">
<a href="http://blog.novoj.net/binary//2010/01/hotswap.png"><img src="http://blog.novoj.net/binary//2010/01/hotswap.png" alt="hotswap" title="hotswap" width="362" height="338" class="aligncenter size-full wp-image-733" /></a>
</div>
<p>Pokud se vám zdá, že vám IntelliJ Idea nereaguje - prověřte jednak, že jste skutečně v debug režimu a koukněte také do nastavení debuggeru (Ctrl + Alt + S, Debug, HotSwap), že máte vybranou možnost Always nebo Ask u položky Reload classes after compilation - viz. předchozí obrázek.</p>
<h3>2. Frames - živý stacktrace</h3>
<p>Často využívám okna s názvem frames, kterému říkám živý stacktrace. Pokud v něm kliknete na některý z nižších řádků, automaticky se vám v editoru otevře odpovídající zdrojový soubor a řádek, který řádku v stacku odpovídá. Spolu s tím se vám i obnoví obsah okna variables, ve kterém se vám zobrazí lokální proměnné platné pro dané místo. Pokud na tento řádek kliknete pravým tlačíkem myši a v popupu vyberete volbu Drop frames, vrátíte se jakoby v kódu zpět do daného místa a můžete z něj znovu tracovat až k vašemu breakpointu. Drop frames totiž vyresetuje všechny lokální proměnné framů mezi aktuálním breakpointem a vámi zvoleným framem a umožní vám vrátit execution point zpět. Změny globálních proměnných (tj. těch, které neleží na stacku jsou nevratné, to musíte vzít v úvahu). Tuto vlastnost jsem se snažil znázornit na následujícím obrázku:</p>
<div align="center">
<a href="http://blog.novoj.net/binary//2010/01/stacktrace.png"><img src="http://blog.novoj.net/binary//2010/01/stacktrace-300x121.png" alt="stacktrace" title="stacktrace" width="300" height="121" class="aligncenter size-medium wp-image-739" /></a>
</div>
<p>Tyto funkce jsou skvělé v případě, že informace v místě breakpointu nedostačují k odhalení příčin hledaného problému. Příčiny často leží totiž ve výš v místech, kde je konkrétní kód volán. Tam je tedy obvykle velmi zajímavé analyzovat lokální proměnné a případně použít Expression Evaluation (Alt + F8, Ctrl + Alt + F8 nebo Alt + levé tlačítko myši pro okamžité zobrazení) pro vyhodnocení nějakého konkrétního Java výrazu v lokálním kontextu.</p>
<h3>3. Stepping</h3>
<p>Pokud používáte dynamické AOP, narazíte při debugování na ten problém, že se při procházení kódem často dostáváte do infrastrukturních tříd Cglib / JavaAssist / Spring Frameworku a dalších, což vám pochopení vlastního problému spíš ztěžuje. Brouzdání kódem infrastrukturních knihoven je dobré v případě, že chcete pochopit, jak to uvnitř nich funguje. Pokud vás to ale nezajímá nebo to už víte, neustálé procházení jejich kódu zdržuje a zabírá mentální kapacitu, kterou byste mohli lépe využít na rozlousknutí daného problému. Obvykle totiž chyba neleží v těchto knihovnách, protože ty jsou důkladně otestovány, ale spíš ve vašem kódu.</p>
<p>IntelliJ Idea pro tento případ nabízí skvělou možnost při kráčení v debug režimu vynechávat konkrétní třídy, nebo třídy odpovídající zvolenému patternu (Ctrl + Alt + S, Debug, Stepping) - viz. následující obrázek:</p>
<div align="center">
<a href="http://blog.novoj.net/binary//2010/01/stepping.png"><img src="http://blog.novoj.net/binary//2010/01/stepping.png" alt="stepping" title="stepping" width="272" height="330" class="aligncenter size-full wp-image-742" /></a>
</div>
<p>Při šikovném nastavení tedy při vstupu do metody, která je reálně implementovaná na úrovni dynamické proxy vstoupíte přímo do vlastního kódu - tedy nějaké advice apod. Debugování dynamických tříd se tím krásně zjednoduší.</p>
<h3>4. Vlastní renderery dat</h3>
<p>Tuto funkcionalitu opět využijete jen ve speciálních případech. V našem případě se jednalo o nevypovídající náhled proměnných, které byly představovány Spring dynamickými proxy. V takovém případě se vám totiž zobrazí fieldy dané proxy, ve kterých jsou teprve ukryty vaše objekty, které jsou pro vás zajímavé. Schválně si porovnejte přehlednost následujících dvou zobrazení proměnné:</p>
<div align="center">
<a href="http://blog.novoj.net/binary//2010/01/data-viewer.png"><img src="http://blog.novoj.net/binary//2010/01/data-viewer-300x145.png" alt="data-viewer" title="data-viewer" width="300" height="145" class="aligncenter size-medium wp-image-745" /></a>
</div>
<p>Myšlenka je veskrze jednoduchá - Idea vám nabízí možnost sami si definovat výrazy (Ctrl + Alt + S, Debug, Data Type Renderers), které budou použity při zobrazení proměnných konkrétního typu v okně variables. Můžete si sami přesně určit, co se má vypisovat na úrovni daného uzlu i co se má zobrazit po rozkliknutí nebo dokonce definovat, jestli uzel vůbec bude možné rozkliknout. Na první pohled se to zdá možná jako dost práce, ale v případě často používaných typů s netriviální strukturou se pár minut práce brzy vrátí. Navíc definice expression s code completion, kterou IntelliJ Idea nabízí všude, kde se pracuje s kódem, je směšně jednoduché.</p>
<div align="center">
<a href="http://blog.novoj.net/binary//2010/01/data-viewer-settings.png"><img src="http://blog.novoj.net/binary//2010/01/data-viewer-settings-300x144.png" alt="data-viewer-settings" title="data-viewer-settings" width="300" height="144" class="aligncenter size-medium wp-image-748" /></a>
</div>
<p>Více si o sestavování vlastních rendererů můžete přečíst přímo <a href="http://blogs.jetbrains.com/idea/2008/04/type-renderers/" target="_new">na blogu JetBrains</a>.</p>
<h3>5. Značkování</h3>
<p>Čas od času potřebujete zjistit, zda instance, se kterou se pracuje je skutečně ta stejná instance, se kterou pracujete někde jinde. V podstatě byste si potřebovali udělat něco jako assertSame, jenže ve chvíli, kdy stojíte na breakpointu se nemůžete jednoznačně dobrat té druhé instance, nebo si nejste jisti, že byste dostali tu správnou. První nápad je tedy obvykle ten, poznamenat si někam id reference dané instance a na druhém místě jej porovnat - idčkem myslím kombinaci nazevTridy@cislo, které Idea v zobrazení proměnných uvádí. Tím se ale okrádáte o cenné flow - navíc se časem rychle ztratíte v řadě id poznamenaných na papíře. A přitom stačí jen Idee říct, aby vám konkrétní instanci při výpisech pojmenovala a zvýraznila:</p>
<div align="center">
<a href="http://blog.novoj.net/binary//2010/01/marking.png"><img src="http://blog.novoj.net/binary//2010/01/marking-300x130.png" alt="marking" title="marking" width="300" height="130" class="aligncenter size-medium wp-image-752" /></a>
</div>
<h3>6. Code coverage</h3>
<p>Tento bod s debugováním souvisí pouze okrajově. Pomáhá nám psát testy, které dokáží odhalit co nejvíce chyb - respektive pomáhá nám najít oblasti, které nemáme testy pokryté a které tedy představují potenciální hrozbu.</p>
<p>Integrace pokrytí kódu testy v rámci IDE je obrovská výhoda - okamžitě přímo v editoru ihned po ručním spuštění testu vidíte, které řádky produkčního kódu vám test pokrývá. Obvykle se toto tato funkcionalita nastavuje jako součást Ant nebo Maven buildu a často není úplně triviální. Navíc výsledky potom máte v externím reportu, takže musíte přepínat mezi ním a IDE, nehledě na prodlevu, která je nezanedbatelná. Idea nám naštěstí nabízí nativní integraci code coverage - stačí zvolit Edit configurations v toolbaru a pro konkrétní Debug konfiguraci vybrat záložku Code coverage:</p>
<div align="center">
<a href="http://blog.novoj.net/binary//2010/01/code-coverage-edit-config.png"><img src="http://blog.novoj.net/binary//2010/01/code-coverage-edit-config.png" alt="code-coverage-edit-config" title="code-coverage-edit-config" width="262" height="127" class="aligncenter size-full wp-image-760" /></a>
</div>
<p><br/></p>
<div align="center">
<a href="http://blog.novoj.net/binary//2010/01/code-coverage.png"><img src="http://blog.novoj.net/binary//2010/01/code-coverage-300x273.png" alt="code-coverage" title="code-coverage" width="300" height="273" class="aligncenter size-medium wp-image-755" /></a>
</div>
<p>Pokud byste toto nastavení chtěli propagovat do všech nově vytvořených běhových konfigurací, nakonfigurujte toto nastavení po kliknutí na tlačítko Edit defaults v levé dolní části dialogu.</p>
<p>Detaily o novinkách v IntelliJ Idea 9 při práci s Run/Debug konfiguracemi si <a href="http://blogs.jetbrains.com/idea/2009/10/invoking-rundebug-actions-in-intellij-idea-9/">přečtěte přímo na blogu JetBrains</a>.</p>
<p>Výsledky code coverage po spuštění testů jsou velmi přehledné a můžete z nich rychle usoudit, kde nutně potřebujete rozšířit svou sadu automatizovaných testů:</p>
<div align="center">
<a href="http://blog.novoj.net/binary//2010/01/code-coverage-view.png"><img src="http://blog.novoj.net/binary//2010/01/code-coverage-view-300x119.png" alt="code-coverage-view" title="code-coverage-view" width="300" height="119" class="aligncenter size-medium wp-image-756" /></a>
</div>
<h3>7. Speciální typy breakpointů</h3>
<p>Používání breakpointů je standard - stačí kliknout na nalevo od požadovaného řádku zastavení. Mezi běžné znalosti, řekl bych, patří i nastavení podmínky pro zastavení na daném breakpointu (Ctrl + Shift + F8, Condition) - častokrát byste se totiž uklikali, než byste zastavili na breakpointu v požadované situaci a dynamická podmínka vám takto práci výrazně usnadní.</p>
<p>Co už ale programátoři míň používají, jsou breakpointy definované na polích třídy. Ty jsou velmi efektivní v případě, že potřebujete zjistit, kdo a kdy modifikuje hodnotu fieldu ať už přes setter metodu nebo prostým přiřazením v rámci jiné metody v třídě.</p>
<div align="center">
<a href="http://blog.novoj.net/binary//2010/01/breakpoint-field.png"><img src="http://blog.novoj.net/binary//2010/01/breakpoint-field-300x217.png" alt="breakpoint-field" title="breakpoint-field" width="300" height="217" class="aligncenter size-medium wp-image-763" /></a>
</div>
<p>Velmi zajímavé jsou také breakpointy nad exception. V případě, že se vám zalogovaný stacktrace ztrácí v tuně dalších logovaných informací a nemůžete se dobrat příčiny konkrétní exception, jsou tyto breakpointy nejlepším způsobem jak se velmi rychle dobrat výsledku. Osobně mám vždy nastavený breakpoint na NullPointerException, protože to je vyjímka, která by se ve vyladěném kódu nikdy neměla vyskytnout. Při takto nastaveném breakpointu jsem okamžitě Ideou přesměrován na problémové místo.</p>
<div align="center">
<a href="http://blog.novoj.net/binary//2010/01/breakpoint-exception.png"><img src="http://blog.novoj.net/binary//2010/01/breakpoint-exception-300x217.png" alt="breakpoint-exception" title="breakpoint-exception" width="300" height="217" class="aligncenter size-medium wp-image-764" /></a>
</div>
<h3>Odkazy</h3>
<p>Při tvorbě tohoto článku jsem, kromě svých zkušeností, čerpal detaily z těchto článků:</p>
<ul>
<li><a href="http://codingmatters.blogspot.com/2009/03/misc-intellij-tips.html">Skvělý článek Dmitrie Kandalova s tipy pro používání IntelliJ Idey</a></li>
<li><a href="http://www.jetbrains.com/idea/features/compiler.html">Oficiální dokumentace JetBrains</a></li>
</ul>
<p>Stejně jako v minulém článku vám budu vděčný za další postřehy v komentářích. Příjemných překvapení v Idee je totiž tolik, že bych se velmi divil, kdybych věděl o všech :-) .</p>
