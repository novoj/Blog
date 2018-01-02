---
status: publish
published: true
title: K čemu je nám užitečný komponentový web framework?
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft size-full wp-image-2516\" title=\"wheel\" src=\"http://blog.novoj.net/binary/2013/03/wheel.jpg\"
  alt=\"\" width=\"240\" height=\"180\" />Nedávno jsem <a href=\"https://twitter.com/novoj/status/315113785704714242\"
  target=\"_blank\">jedním svým twítem</a> vyvolal menší diskusi ohledně toho, co
  nám dovoluje komponentový framework oproti tomu, čeho bychom byli schopni dosáhnout
  s jednoduchým MVC rámcem. Bohužel twitter mi nedává takovou možnost vyjádřit se
  a tak jsem chtěl důvody a výhody, které vidím v komponentách na frontendu, popsat
  trošku obšírněji v tomto článku.\r\n\r\nKomponentový model na webové vrstvě přináší
  oproti <a href=\"http://cs.wikipedia.org/wiki/Model-view-controller\" target=\"_blank\">MVC
  </a>se \"standardním\" šablonovým systémem možnost elegantní znovupoužitelnosti
  částí, které se znovu použít dají. Pro mě jako vyznavače DRY je toto jedna z VELKÝCH
  výhod. Namítnete, že znovupoužitelnosti se přeci dá dosáhnout i v běžném šablonovacím
  systému - co třeba JSP tagy nebo Freemarkerová makra? Touhle cestou jsem si prošel
  a výsledek byl vždycky kostrbatý - obvykle se vám podaří znovupoužít buď vykreslovací
  šablonu nebo aplikační logiku, ale nikdy ne rozumně obojí.\r\n\r\n"
wordpress_id: 2507
wordpress_url: http://blog.novoj.net/?p=2507
date: '2013-03-23 07:32:07 +0100'
date_gmt: '2013-03-23 06:32:07 +0100'
categories:
- Programování
- Java
- Web
- Úvahy
tags: []
comments:
- id: 151674
  author: Daniel Kolman (@kolman)
  author_email: kolman@twitter.example.com
  author_url: http://twitter.com/kolman
  date: '2013-03-23 17:46:06 +0100'
  date_gmt: '2013-03-23 16:46:06 +0100'
  content: "Moc nerozumim kde je ten přínos komponent. V MVC budu reprezentovat stránkovanej
    výpis samozřejmě taky nějakym objektem, něco jako PagedList. View pak na jeho
    vyrenderování může použít *znovupoužitelnou* šablonu, která pomocí *reflexe* vygeneruje
    záhlaví umožňující sortování a filtraci. Rozdíl je v tom, že v MVC je čistý oddělení
    logiky (kde seberu PagedList) od zobrazení (šablony). Reuse je stejnej. Když to
    budu chtít exportovat do XLS, pošlu ten PagedList něčemu, co ho pomocí *reflexe*
    ztransformuje. No a na přidání novýho gadgetu do všech editorů stránek? Předpokládám
    že pokud maj všechny editory aspoň nějakou sdílenou funkcionalitu, bude tam někde
    šablona která bude všude použitá, takže ji prostě změnim a #epic #win.\r\n\r\nMVC
    neznamená že jsme zahodili reuse. Jen striktně oddělujeme práci s daty a jejich
    renderování."
- id: 151675
  author: Daniel Kvasnička (@dkvasnickajr)
  author_email: dkvasnickajr@twitter.example.com
  author_url: http://twitter.com/dkvasnickajr
  date: '2013-03-23 19:16:20 +0100'
  date_gmt: '2013-03-23 18:16:20 +0100'
  content: "Na twitteru je ta diskuse fakt na pendrek :)\n\nSlovicko stateless jsem
    tam zamichal proto, ze dneska je pravidlo (potvrzovane vyjimkami), ze komponentovy
    framework je tezce stateful (session), zatimco obycejne MVC, jako treba Stripes,
    vetsinou neni. Mozna to bylo zavadejici, to je fakt... \n\nKazdopadne zakladni
    myslenka byla ta, ze co popisujes, to skutecne neni o komponentovem vs. MVC, ale
    o tom, co pouzijes za \"V\". Ja napriklad aktualne na svem soukromem projektu
    pouzivam https://github.com/cgrand/enlive a s tim se odvazim tvrdit, ze bych to
    same napsal. Dokonce klidne i 1:1 (pokud to chapu dobre tak, ze vyse uvedena XMLka
    jsou vlozena nekde do HTML v miste, kde ta komponenta ma byt). Pritom ale nepouzivam
    zadny \"komponentovy\" framework a Enlive mam jako view vrstu v klasicke MVC app.
    \n\nA  to me privadi jeste k AOP samotnemu: je to jen jeden zpusob, jak ortogonalni
    concerny resit v klasickem ciste objektovem svete. Jak uz jsem nakousnul na twitteru
    - AOP je v zasade berlicka jazyku, co nemaji funkce vyssiho radu ;) Jinde se to
    da vyresit napr. knihovnami typu https://github.com/technomancy/robert-hooke,
    nicmene v zasade k tomu zadna knihovna potreba neni. Pak se takova vec i jednoduseji
    pasuje vsude mozne...\n\nPak je tu samozrejme jeste argument treti cesty a to
    ten, ze server-side renderovani je uncool a \"so 90s\" a ze to mas stejne mit
    cely napsany v Angularu! :)\n\n(k negativum AOP - celkem dost zprehlednuje situaci
    pouzivani 100% typesafe AOP v Jave EE 6, ty jejich interceptory... neohnes to
    tak brutalne jako pres stringovou definici pointcutu, ale je to relativne bezpecne
    a prehledne)"
- id: 151676
  author: Daniel Kvasnička (@dkvasnickajr)
  author_email: dkvasnickajr@twitter.example.com
  author_url: http://twitter.com/dkvasnickajr
  date: '2013-03-23 19:17:59 +0100'
  date_gmt: '2013-03-23 18:17:59 +0100'
  content: Vidim, ze Dan psal vicemene ve stejnym duchu :)
- id: 151677
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-03-23 19:56:17 +0100'
  date_gmt: '2013-03-23 18:56:17 +0100'
  content: "Při psaní článku jsem se i já trošku zorientoval v pojmech. Oba mluvíme
    o MVC - i komponentové frameworky jsou MVC, komponentové jsou \"pull\", nekomponentové
    jsou \"push\" (viz. http://en.wikipedia.org/wiki/Web_application_framework) ...
    a s tím bych souhlasil.\r\n\r\nStojím si za tím, že v push rámcích máš daleko
    větší práci s reusem, protože ty tě k žádnému zapouzdření nevedou. Když si vezmu
    za příklad Strutsy nebo Spring, tak tam si controller osahá request (nebo mu framework
    zajistí binding), dotáže model, výsledky překouše a nacpe to jako atributy requestu.
    Všechny pěkně na jedné hromadě. Tady se moc o zapouzdřenosti, která vede ke znovupoužitelnosti,
    moc mluvit nedá.\r\n\r\nAd tvoje argumentace - co by v tom případě bylo součástí
    toho PagedListu? Seznam sloupců odpovídající toho co je ve view? Identifikace
    sloupce, podle kterého je setříděno? Nastavení vstupních filtrů? A kdo ten PagedList
    vyrábí? Byznys vrstva? To asi ne, tím bys view zanášel do modelu. Takže výstup
    z byznys vrstvy překoušeš v kontroleru, přesypeš data z jedněch objektů do PagedListu,
    který tedy slouží jen jako DTO. To je krapet fuška řekl bych.\r\n\r\nŠkoda, že
    tohle je moc hutné téma i na diskusi pod článkem. Tohle by chtělo probrat nad
    konkrétními případy - já prostě jen aktuálně cítím, jaké nám dává komponentová
    architektura možnosti. V push MVC modelu jsem toho udělal už hodně a nikdy jsem
    z toho nebyl tak spokojený, jako teď s tím co máme. Ale chápu, že to je těžko
    předatelné :("
- id: 151678
  author: Daniel Kolman (@kolman)
  author_email: kolman@twitter.example.com
  author_url: http://twitter.com/kolman
  date: '2013-03-23 20:51:45 +0100'
  date_gmt: '2013-03-23 19:51:45 +0100'
  content: "Mluvim o \"push\" MVC, protože \"pull\" neni čistý MVC. Za čistý MVC považuju,
    když controller sežene všechny data potřebný pro stránku a view to \"jen\" renderuje,
    a pokud je složený z více šablon, stále jsou šablony relativně hloupý a dělaj
    maximálně různý transformace dat který dostanou, ale rozhodně nemůžou třeba šahat
    na databázi.\r\n\r\nPagedList obsahuje data (řádky) a metadata (seznam sloupců,
    sort, filtry). Jestli jsou metadata definovaný staticky (a dostaneš se k nim reflexí)
    nebo explicitně je celkem fuk. Tyhle informace ti *musí* dát byznys vrstva, protože
    pokud chceš efektivně stránkovat (=na straně databáze), pak jí to musíš předat
    v rámci dotazu.\r\n\r\nDTO je super věc, pokud chceš čistě oddělit vrstvy. Vytvářet
    a plnit je můžeš nějak automaticky. Pro view je navíc dobrý si vytvořit display
    objects, pokud je to nutný. Když to shrnu:\r\n\r\n1. Controller zavolá remote
    facade\r\n2. Remote facade pracuje s business vrstvou, zeptá se jí na objekty
    a přeloží je do DTO, který vrátí controlleru\r\n3. Controller buď jen předá DTO
    do view, nebo pokud vyžaduje zobrazení nějakou logiku, tak nejdřív přeloží DTO
    na Display Object a ten pošle view.\r\n\r\nVypadá to jako \"spoustu práce\" ale
    na velkejch projektech to má jednoznačnej benefit - vrstvy jsou maximálně decoupled,
    krásně se to testuje, máš jasný rozhraní.\r\n\r\nA že controller překouše data
    \"všechny pěkně na jedné hromadě\"? To nemusí bejt pravda, záleží jak to napíšeš:)
    V controllerech je možný provádět určitou kompozici dat a je to vrstva kde je
    možný bejt hodně kreativní;)"
- id: 151679
  author: Borek Bernard (@borekb)
  author_email: borekb@twitter.example.com
  author_url: http://twitter.com/borekb
  date: '2013-03-23 21:30:55 +0100'
  date_gmt: '2013-03-23 20:30:55 +0100'
  content: "Sranda, jak se vy (s Javou, ale to asi není moc podstatné) pomalu dostáváte
    k principu fungování ala ASP.NET Web Forms, zatímco .NETisti se pomalu ale jistě
    přesouvají k MVC.\r\n\r\nJinak mi připadá, že MVC hodně hájí lidi, kteří dělají
    spíš *weby* (ok, třeba mnohastránkové, komplikované, ale stále weby), zatímco
    vy budujete dost komplikovanou modulární *aplikaci*. Ačkoliv lze nepochybně v
    komponentovém frameworku dělat i weby a v MVC aplikace, obráceně je to přirozenější.
    Takže ve vašem případě se vůbec nedivím, že jsi z komponentového přístupu nadšený."
- id: 151680
  author: Daniel Kolman (@kolman)
  author_email: kolman@twitter.example.com
  author_url: http://twitter.com/kolman
  date: '2013-03-23 23:35:39 +0100'
  date_gmt: '2013-03-23 22:35:39 +0100'
  content: Mimochodem to mi přijde jako jeden z nejpřekvapivějších rozdílů mezi javisty
    a .netisty - zatímco javisti tíhnou ke komponentově orientovaným frameworkům,
    .netisti k MVC. Důvody můžeme rozebrat u piva:))
- id: 151681
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-03-24 13:25:45 +0100'
  date_gmt: '2013-03-24 12:25:45 +0100'
  content: "Vyžadování nenažraného state na straně serveru je nedokonalost frameworku,
    nikoliv obecná vlastnost komponentového přístupu. Ale souhlasím, že třeba JSF
    to třeba se stavovostí krutě přehnaly (jiné rámce neznám natolik, abych to mohl
    tvrdit).\r\n\r\nV ohledu XMLek - struktura komponent na stránce se drží odděleně
    od samotných HTML šablon. V podstatě podobně, jako to má Enlive - rozdíl je v
    tom, že šablony můžeme dle potřeby přetěžovat a také šabona se váže ke komponentě.
    Tj. nikde se nenajde kompletní HTML stránka od head až po konec body. HTML je
    rozpalcelované na jednotlivé komponenty, což nám umožňuje zmiňovaný partial update
    a další legrácky. Tohle je trošku o zvyk - člověk si musí zvyknout myslet \"strukturovaně\"
    - ale v zásadě se to dá napasovat na jakékoliv HTML.\r\n\r\nMáš pravdu, že AOP
    je v jistém směru berlička - na druhou stranu v odkazovaném https://github.com/technomancy/robert-hooke
    mi uvedený příklad připadá to samé jako v AOP pointcut:\r\n\r\n(add-hook #'examine
    #'doubler)\r\n\r\nA AOP advice:\r\n\r\n(defn doubler [f &amp; args]\r\n  (apply
    f args)\r\n  (apply f args))\r\n\r\nJen je to forma jiného zápisu a jazyk se \"nehackuje\"
    na úrovni byte-code, ale využívá se vlastnosti funkcionálního přístup. Nicméně,
    principielně mi to připadá dost podobné.\r\n\r\nJo a s tím Angularem ještě uvidíme
    - zatím jsem na server side o dost produktivnější, než kluci s JavaScriptem :)"
- id: 151682
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-03-24 13:57:34 +0100'
  date_gmt: '2013-03-24 12:57:34 +0100'
  content: "No člověk utíká od toho s čím udělal špatnou zkušenost :) ... a tady je
    vidět, že stříbrná kulka neexistuje.\r\n\r\nNe, já proti push MVC nic nemám -
    na běžné aplikace jsou ideální. Nám prostě jen přestaly stačit. Pokud se v push
    MVC dá nějaký reuse udělat, tak jen v rámci jednoho projektu. My děláme desítky
    projektů ročně - od nejmenších až po ty velké a rozhodli jsme se jít modulární
    architekturou, která nám umožňuje sdílet kód napříč projekty docela efektivně.
    A tam bylo s push MVC trápení - furt jsme plno věcí psali znovu a znovu.\r\n\r\nTeď
    jsme schopni pouhým \"zapnutím\" modulu nahodit celé nové (administrační) GUI
    a zpropagovat udělátka na potřebná místa skrz systém pár řádky kódu. Pravda je,
    že to místy začíná být už docela složité domyslet všechny důsledky a zvolit nejvhodnější
    řešení, ale to za ušetření takové spousty kódu docela stojí.\r\n\r\nBtw. s tou
    složitou modulární aplikací se dělají i tyhle jednoduché weby (a kupodivu efektivně):\r\n\r\nhttp://www.supermanie.cz/\r\nhttp://blog.fg.cz/clanky/\r\nhttp://www.cez.cz/etarif/cs/uvod.html"
- id: 151683
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-03-24 14:09:05 +0100'
  date_gmt: '2013-03-24 13:09:05 +0100'
  content: "Pull MVC model nijak nešpiní - šablony zůstávají hloupé (my např. používáme
    FreeMarker a jedno stěžejních prohlášení je, že je stavěný tak, aby neumožňoval
    dělat složité věci v šablonách) - viz. What is FreeMarker zde: http://freemarker.sourceforge.net/\r\n\r\nJde
    jen o to, že pull MVC definuje komponentu jako něco, co v sobě spojuje view a
    část controlleru. A přesně o té sdílení části controlleru nám jde. Java kód komponenty,
    návazné akce, které něco mohou provádět a poskytovatelé dat reprezentují v tomto
    směru C. Kupříkladu akce nebo poskytovatelé dat taky nesmí přímo provádět nějakou
    byznys logiku - ty jen přetransformují požadavky z view na volání byznys vrstvy,
    kde se děje všechno důležité - reprezentují jen takový bridge do byznys vyrstvy,
    která je view agnostická.\r\n\r\nPrincip překladu volání do byznys vrstvy, který
    uvádíš chápu - takhle jsme to dělali. Mě ale kreativita a snaha o reuse v controller
    vrstvě dovedla do komponentové architektury :)"
- id: 151685
  author: Daniel Kvasnička (@dkvasnickajr)
  author_email: dkvasnickajr@twitter.example.com
  author_url: http://twitter.com/dkvasnickajr
  date: '2013-03-24 16:47:48 +0100'
  date_gmt: '2013-03-24 15:47:48 +0100'
  content: Jaky framework teda vlastne pouzivate? Tipuju to na Wicket nebo Tapestry,
    ale spis teda to prvni... :)
- id: 151686
  author: Daniel Kvasnička (@dkvasnickajr)
  author_email: dkvasnickajr@twitter.example.com
  author_url: http://twitter.com/dkvasnickajr
  date: '2013-03-24 17:02:36 +0100'
  date_gmt: '2013-03-24 16:02:36 +0100'
  content: "@Dan: Do diskuse cisty / necisty bych se moc nepoustel, protoze interpretaci
    MVC je milion a nerekl bych, ze existuje jedina svata... Reenskaug, kdyz poprve
    MVC privedl na svet, tak mluvil o pull. Ukolem C nebylo dotlacit data do V. Bylo
    to ale samozrejme tehdy v pripade desktopu, coz je ale taky tak trochu to, co
    se komponentove web. frameworky snazi emulovat... takze bacha, zauberre rasse
    MVC tady v zasade dela Honza :D\r\n\r\nCo se tyka tvych popisovanych 3 bodu, tak
    samozrejme treba v pripade SOA to ani moc jinak nejde. Jinak jsem ale az prilis
    casto videl aplikace, ktere byly psane timhle zpusobem a zvrhly se v proceduralni
    lasagne, ve kterych anemicky objekty litaly nahoru dolu servisama, do kterych
    zgravitovala veskera business logika aplikace... O OOP se uz pak moc neda mluvit,
    o FP ale taky ne... Nemam rad prekladani mezi DTO na kazdym myslitelnym spoji
    v aplikaci. Kdyz jsou ruzne vrstvy zavisle na spolecnem domenovam modelu, mezi
    nimi samotnymi to zadnou zavislost nedela (pokud programator neni überprase).
    Decoupling a cisty rozhrani zustava..."
- id: 151688
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-03-24 20:57:48 +0100'
  date_gmt: '2013-03-24 19:57:48 +0100'
  content: "Teď jsi mě odkopal :) ... používáme vlastní. Je mi jasné, že se najde
    plno lidí, kteří by mě v tuto chvíli začali o hlavu omlacovat NIH, ale ono to
    vzniklo docela spontánně. \r\n\r\nPotřebovali jsme vyvinout něco, co by dokázali
    nasazovat naši webdevelopeři - což nejsou programátoři jako takoví, aby s tím
    dokázali dělat jednoduché formuláře na webech a nemuseli s tím ztrácet čas Javisti.
    A nakonec se to zvrhlo ve full blown web framework :)\r\n\r\nKaždopádně účel nám
    to plní - my Javisti se věnujeme vývoji byznys logiky a níž, pak vytvoříme bridge
    \"poskytovatelů dat\" a \"akcí\" (což jsou ty kontrolery, které jen převolávají
    byznys logiku) a webdevelopeři to potom včetně HTML oživí na view vrstvě. Donutilo
    nás to i vytvořit supportní nástroje, které jsem u jiných frameworků ještě neviděl:
    http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/\r\n\r\nBtw.
    třeba tohle: http://www.supermanie.cz/ ... vyrobil kompletně kolega webař. Za
    mě je tam jen pár Groovy tříd na nějaké validace, akce bylo vymalováno. Vespod
    je nakonec znovupoužitelný modul na galerie napsaný v Javě.\r\n\r\nPodobně s tím
    třeba nás firemní systém poskládal externista, který je kvalitní databázista,
    ale s  webem zatím moc velké zkušenosti neměl. My jsme mu připravili komponenty,
    kostru webu, napojení přes SOAP na jeho Sybase databázi (za nás investice několika
    málo týdnů) a on s tím za rok a půl vytvořil vcelku obstojnou nadstavbu nad krabicovým
    IS (aktuálně víc jak 40-50 unikátních stránek s reportingem, fakturací atp.)\r\n\r\nKdybych
    nevěděl, že to funguje, tak to takhle neobhajuju :)"
- id: 151689
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-03-24 21:02:57 +0100'
  date_gmt: '2013-03-24 20:02:57 +0100'
  content: "Díky všem za náměty - tyhle web frameworky, ty byly vždycky kontroverzní
    :) \r\n\r\nKaždopádně, i když působím zatvrzele vážím si Vašich názorů."
- id: 151693
  author: Zebří policie
  author_email: mnamnouri@seznam.cz
  author_url: ''
  date: '2013-03-25 09:46:45 +0100'
  date_gmt: '2013-03-25 08:46:45 +0100'
  content: Wicket FTW!
- id: 151703
  author: Guido
  author_email: vit.kotacka@gmail.com
  author_url: http://sw-samuraj.cz
  date: '2013-03-27 10:03:28 +0100'
  date_gmt: '2013-03-27 09:03:28 +0100'
  content: "Já už jsem teda frontend léta nedělal. Ale pořád mám dobré vzpomínky na
    komponentové frameworky jako je Wicket nebo Flex. A taky si pamatuju trápení s
    JSF/RichFaces a problémy s AJAXem.\r\n\r\nA to jsme byli v o dost jednodušší situaci,
    protože jsme řešili design a reuse jenom v rámci jednoho projektu. Takže si myslím,
    že vaše \"komponentová cesta\" vede správným směrem.\r\n\r\nNa druhou stranu,
    u komponentového frameworku je potřeba \"udržet míru\". Třeba použít GWT bych
    se docela obával - tam mi to přijde jako už moc velká magie."
- id: 151704
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-03-27 11:15:19 +0100'
  date_gmt: '2013-03-27 10:15:19 +0100'
  content: "No ono okolo komponentových frameworků panuje celá řada předsudků - zrovna
    včera jsme to probírali na NerdDinner. Obecně panuje názor, že komponentový framework
    musí být stateful, že je na složení HTML je potřeba mít odpovídající strukturu
    (která DOM +/- kopíruje) komponentového stromu (tj. např. že pro vykreslení tabulky
    je potřeba komponenta tabulka v ní nutně komponenty pro sloupce), že je nutné
    při každém requestu znova vytvářet strom komponent na straně serveru (i kvůli
    aktualizaci jediného údaje v jedné komponentě) atd.\r\n\r\nTohle všechno jsou
    IMHO jen důsledky špatné implementace, nikoliv vlastnosti komponentového návrhu
    obecně."
---
<p><img class="alignleft size-full wp-image-2516" title="wheel" src="http://blog.novoj.net/binary/2013/03/wheel.jpg" alt="" width="240" height="180" />Nedávno jsem <a href="https://twitter.com/novoj/status/315113785704714242" target="_blank">jedním svým twítem</a> vyvolal menší diskusi ohledně toho, co nám dovoluje komponentový framework oproti tomu, čeho bychom byli schopni dosáhnout s jednoduchým MVC rámcem. Bohužel twitter mi nedává takovou možnost vyjádřit se a tak jsem chtěl důvody a výhody, které vidím v komponentách na frontendu, popsat trošku obšírněji v tomto článku.</p>
<p>Komponentový model na webové vrstvě přináší oproti <a href="http://cs.wikipedia.org/wiki/Model-view-controller" target="_blank">MVC </a>se "standardním" šablonovým systémem možnost elegantní znovupoužitelnosti částí, které se znovu použít dají. Pro mě jako vyznavače DRY je toto jedna z VELKÝCH výhod. Namítnete, že znovupoužitelnosti se přeci dá dosáhnout i v běžném šablonovacím systému - co třeba JSP tagy nebo Freemarkerová makra? Touhle cestou jsem si prošel a výsledek byl vždycky kostrbatý - obvykle se vám podaří znovupoužít buď vykreslovací šablonu nebo aplikační logiku, ale nikdy ne rozumně obojí.</p>
<p><a id="more"></a><a id="more-2507"></a></p>
<p>Vezměte si jen takový <a href="http://www.rokjinak.cz/srv/www/qf/cs/ramjet/requests/requestListing" target="_blank">jednoduchý stránkovaný seznam</a> - v nekomponentovém MVC se logika v controllerech míchá, na view vrstvě si sice můžete pomocí makra vysdílet šablonu, ale přechody mezi stránkami, třídění a filtrování už řešíte v controlleru a ten je z podstaty věci obtížné sdílet mezi různými stránkami. Neříkám, že to je nemožné, ale rozhodně to od vás bude vyžadovat daleko větší invenci, než se vám podaří shodný kód vysdílet. Čím složitější stránka, tím složitější controller a tím větší pravděpodobnost, že ze znovupoužitelnosti nezbude nic. Tento způsob tvorby webové vrstvy na to není prostě stavěný. Má ale zase jiné výhody - je jednoduchý.</p>
<p><a href="http://en.wikipedia.org/wiki/Web_application_framework" target="_blank">Komponentový systém</a> nám umožňuje stránkovaný seznam vzít a obalit jej do jedné komponenty, která spojuje vykreslovací šablonu (kterou musí být jednoduché přetížit v případě potřeby - tady třeba selhává <a href="http://cs.wikipedia.org/wiki/JavaServer_Faces" target="_blank">JSF</a>), logiku, která se stará o třídění a filtrování a od běžného programátora vyžaduje pouze implementaci rozhraní, které komponenta používá pro získávání dat z aplikační vrstvy.</p>
<p>Chceme-li jít ještě dál můžeme (ale nemusíme) i tuto komponentu dále rozdělit na samostatnou subkomponentu pro stránkování, komponenty pro definici sloupců seznamu (s derivací sloupce, podle kterého je možné třídit), filtrovací komponenty atd. Ve standardizovaných případech tedy pracujeme se stránkovanými seznamy na vyšší úrovni abstrakce a při chytrém návrhu máme velké možnosti kompozice komponent do výsledného požadovaného tvaru a tudíž i velké úspěšnosti znovupoužitelnosti.</p>
<p>Ať jen neteoretizujeme na abstraktní úrovni, tady jsou ukázky z našeho <a href="http://cs.wikipedia.org/wiki/Dom%C3%A9nov%C4%9B_specifick%C3%BD_jazyk" target="_blank">DSL</a> s jehož pomocí skládáme webovou vrstvu:</p>
<p>[source lang="xml"]<br />
&lt;recordListing&gt;<br />
   &lt;dataSource class=&quot;com.fg.SomeProvider&quot;/&gt;<br />
&lt;/recordListing&gt;<br />
[/source]</p>
<p>Toto to nejjednoduší možné zapsání seznamu - používáme komponentu recordListing (výpis záznamů) s dodavatem dat <strong>SomeProvider</strong>. Ve vykresovací šabloně nejsme při tvorbě HTML ničím svázáni, ale zase toho moc nevíme k tomu abychom dokázali navrhnout vykreslovací šablonu obecně. Tenhle způsob se ale výborně hodí na specifické layouty seznamů, u kterých víme, že je jejich znovupoužitenost minimální (např. toto je <a href="https://www.okbonus.sk/srv/www/qf/sk/ramjet/activeBonusProgram" target="_blank">ukázka specifického stránkovaného výpisu</a>).</p>
<p>Co když budeme chtít komponentu ještě dále zobecnit a používat ji jako kopyto pro desítky použití (např. pro účely reportingu)? Dekomponujeme si ji dále na sloupce a můžeme ven vyjmout stránkovací logiku například takto:</p>
<p>[source lang="xml"]<br />
&lt;recordListing&gt;<br />
   &lt;dataSource class=&quot;com.fg.SomeProvider&quot;/&gt;<br />
   &lt;column id=&quot;firstName&quot;/&gt;<br />
   &lt;orderableColumn id=&quot;lastName&quot;/&gt;<br />
   &lt;column id=&quot;age&quot;/&gt;<br />
   &lt;pagination/&gt;<br />
&lt;/recordListing&gt;<br />
[/source]</p>
<p>Pokud bychom do toho všeho chtěli umožnit ještě filtraci podle obsahu sloupců, můžeme jít ještě dál:</p>
<p>[source lang="xml"]<br />
&lt;recordListing&gt;<br />
   &lt;dataSource class=&quot;com.fg.SomeProvider&quot;/&gt;<br />
   &lt;column id=&quot;firstName&quot;/&gt;<br />
   &lt;orderableColumn id=&quot;lastName&quot;&gt;<br />
      &lt;columnFilter&gt;<br />
         &lt;textInput id=&quot;filter.byName&quot;/&gt;<br />
      &lt;/columnFilter&gt;<br />
   &lt;/orderableColumn&gt;<br />
   &lt;column id=&quot;age&quot;&gt;<br />
      &lt;columnFilter&gt;<br />
         &lt;textInput id=&quot;filter.fromAge&quot;&gt;<br />
            &lt;validators&gt;&lt;number/&gt;&lt;/validators&gt;<br />
         &lt;/textInput&gt;<br />
         &lt;textInput id=&quot;filter.toAge&quot;&gt;<br />
            &lt;validators&gt;&lt;number/&gt;&lt;/validators&gt;<br />
         &lt;/textInput&gt;<br />
      &lt;/columnFilter&gt;<br />
   &lt;/column&gt;<br />
   &lt;pagination/&gt;<br />
&lt;/recordListing&gt;<br />
[/source]</p>
<p>Nechci zabíhat do přílišných podrobností, které jsou poplatné tomu komponentovému frameworku, který jsme použili - šlo mi jen o to naznačit možnosti kompozice webové vstvy.</p>
<p>Znovupoužitelnost je ale jenom jedna z věcí, kterou jsme tím získali. Dekompozice na logicky uzavřené celky nám otevřela cestu k technice<a href="http://blog.novoj.net/2010/10/02/zrychlete-svoji-webovou-aplikaci-pomoci-partial-update/" target="_blank"> částečného vykreslování (obnovování) stránky</a> pomocí AJAXu.</p>
<p>Tím že v aplikaci máme strukturovaný model webové vrstvy můžeme začít využívat reflexního přístupu k řešení některých problémů. Jak bylo vidět na příkladu výše, můžeme se například v <strong>recordListing</strong> komponentě prohledat subkomponenty na výskyt <strong>columnFilter</strong> a <strong>orderableColumn</strong> komponent a podle jejich aktuálních uživatelských dat odpovídajícím způsobem upravit výsledný dotaz, který jde na backend (tj. do poskytovatele dat <strong>SomeProvider</strong>, který vůbec netuší co všechno se před jeho zavoláním stalo). A můžeme tak udělat i velmi obecně, aniž bychom dopředu museli znát všechna místa a způsoby použití.</p>
<p>Obdobným způsobem jsme třeba realizovali export do XLS na našem firemním intranetu - akce, která generuje přes <a href="http://poi.apache.org/" target="_blank">Apache POI</a> XLS soubor potřebuje v základu minimální množství konfigurace a přesto je dostatečně obecná. Vyhledá si totiž na aktuální stránce komponentu, která zobrazuje stránkovaný seznam, vyčte si z ní konfiguraci sloupců, datové typy a formátování, zjistí si její datový zdroj a vygeneruje Excel ve stejné struktuře s tím rozdílem, že nad datovým zdrojem projde a vypíše všechny dostupné stránky výpisu a nikoliv pouze tu aktuální, jak to dělá webový frontend. Výhodou tohoto provedení je navíc to, že zůstane zachované i uživatelské filtrování a třídění obsahu, jako na webu. Bez reflexe bychom museli odvést daleko větší množství práce, abychom se k rozumně zformátovanému výstupu do Excelu dostali.</p>
<p>Nedávno, když jsme přemýšleli nad stavbou modulárního GUI pro <a href="http://www.edee-cms.cz/cs/demo" target="_blank">Edeeho </a>nás napadlo, že bychom mohli pomocí <a href="http://cs.wikipedia.org/wiki/Aspektov%C4%9B_orientovan%C3%A9_programov%C3%A1n%C3%AD" target="_blank">AOP techniky</a> elegantně řešit publikace nových gadgetů skrz redakční systém. Představte si situaci, kdy máte nasazený redakční systém s celou řadou specifických vstupních editorů stránek. Podobně jako <a href="http://wordpress.org/" target="_blank">WordPress</a> má dva typy obsahu: článek a stránku - i my umožňujeme obsah kategorizovat - nicméně nejsme omezeni pouze na tyto dva typy. Pro každého zákazníka šijeme požadované typy obsahu na míru - pokud si zákazník přeje mít jako obsah <a href="https://www.okbonus.sk/srv/www/qf/sk/ramjet/okmagazin/recipe/detail?id=73" target="_blank">kuchařský recept</a> (s přísadami, obtížností přípravy atd. atd.), <a href="https://www.okbonus.sk/srv/www/qf/sk/ramjet/okmagazin/lifeStyle/detail?id=152" target="_blank">obyčejný článek</a> nebo popis akciového fondu, připravíme mu odpovídající a z hlediska UX optimalizovaný editor.</p>
<p>Na druhé straně připravujeme modul, který umožňuje extrakci statistických údajů z <a href="www.google.com/analytics/" target="_blank">Google Analytics</a> a chtěli bychom, aby se u každého editoru stránky zobrazilo malé <a href="http://cs.wikipedia.org/wiki/Gadget" target="_blank">udělátko</a>, který by uživateli zobrazilo, jak je na tom jeho stránka s počtem přístupů v čase (pěkně pohodlně rovnou v rozhraní našeho produktu).</p>
<p>Otázka nyní zní: jak zpropagovat náš gadget do existujících editorů stránek? Nesmíme zapomenout, že my při tvorbě udělátka ani nevíme, jaké specifické editory na různých zákaznických instalacích vzniknou.</p>
<p>Nasnadě je tupá varianta - udělátko zdokumentovat a na každé instalaci, kde budeme chtít mít modul Google Analytik zapnutý budou muset programátoři obejít všechny editory stránek a ručně do nich podle dokumentace udělátko přidat. Samozřejmě, když by náhodou někdo modul vypnul, budeme mít na všech těchto stránkách zobrazenou chybu.</p>
<p>Ovšem díky tomu, že v systému máme pod kontrolou prototypovou stránku tohoto vstupního editoru, na které se staví dál, a zároveň máme webovou vrstvu strukturovanou do komponent, můžeme celý problém vyřešit daleko elegantněji.</p>
<p>Napíšeme pravidlo (<a href="http://en.wikipedia.org/wiki/Aspect_(computer_programming)" target="_blank">aspekt</a>), které bude aplikováno na každou stránku spravovanou webovým frameworkem a v případě, že bude daná stránka odvozená z našeho prototypového editoru (<a href="http://en.wikipedia.org/wiki/Pointcut" target="_blank">pointcut</a>), najdeme na ní předpřipravené místo pro tato extra udělátka a tam náš Google Analytics gadgetek přidáme (<a href="http://en.wikipedia.org/wiki/Advice_in_aspect-oriented_programming" target="_blank">advice</a>). Kromě jednoduchého přidání komponenty do nějakého kontejneru máme celou škálu dalších operací, které je možné se skladbou komponent dělat. V tomto ohledu kopírujeme většinu možností manipulace, které nám <a href="http://api.jquery.com/category/manipulation/" target="_blank">s DOMem umožňuje jQuery</a> (append, prepend, wrap, remove atd.).</p>
<p>Ani nemusím zmiňovat, že udělátko si s sebou může nést plno funkcionality - přepínat různé typy dat (pageviews, unikátní návštěvníci, délka období atp.), filtrovat atp. Díky zapouzdřenosti komponent není nutné dvakrát koumat, jak vypadá cílová stránka. Vše co komponenta potřebuje, si nese s sebou. To je dar komponentového modelu.</p>
<p>Původně jsme mysleli, že budeme tuto aspektovou rozšiřitelnost používat jen ve velmi výjimečných případech, ale v současné době pozoruji, že tento přístup si získal oblibu a začal se používat na hromadné změny ve stránkách na klientských instalacích poměrně běžně.</p>
<p>Samozřejmě AOP má svá rizika - při extenzivním používání znepřehledňuje vazby v systému (u aspektově přidávaných a modifikovaných věcí nemusí být patrné odkud a proč byla tato modifikace provedena). Pokud se bude AOP na view vrstvě používat opatrně a s rozumem otevírá prostor pro elegantní řešení jinak velmi pracných úprav. Ostatně, když srovnáme toto použití aspektů s <a href="http://en.wikipedia.org/wiki/AspectJ" target="_blank">AspectJ</a>, který se na byznys vrstvě používá už léta, zjistíme, že pozitivní i negativní dopady na systém jsou obdobné.</p>
<p>A abych dokončil ještě svou myšlenku z Twitteru - zkuste si něco podobného s push MVC frameworkem. Tam toto realizovat IMHO nelze, protože model na view vrstvě chybí (modelem zde není myšlen doménový model). Teď už snad ten můj tweet dává logiku :)</p>
