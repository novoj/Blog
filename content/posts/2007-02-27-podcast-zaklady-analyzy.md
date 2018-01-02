---
status: publish
published: true
title: 'Podcast: základy analýzy'
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
wordpress_id: 9
wordpress_url: http://blog.novoj.net/2007/02/27/podcast-zaklady-analyzy/
date: '2007-02-27 07:10:53 +0100'
date_gmt: '2007-02-27 06:10:53 +0100'
categories:
- Programování
- Podcast
tags: []
comments:
- id: 19
  author: Pavel Čech
  author_email: pavel.cech@uhk.cz
  author_url: ''
  date: '2007-02-27 07:14:59 +0100'
  date_gmt: '2007-02-27 06:14:59 +0100'
  content: "Ahoj Honzo,\r\nposlechl jsem si záznam tvoji přednášky a myslím, že to
    je opravdu velmi dobré. Je to trochu delší ale dobře se to poslouchá. Možná paradoxně
    právě proto, že se nesnažíš mluvit úplně spisovně a je to takové uvolněné. Z nahrávky
    je znatelné, že mluvíš dost ze zkušenosti a obrazně řečeno víš kde je hlavička,
    do které uhodit:). Především se jedná o rozebrání životního cyklu a jeho jednotlivých
    fází.\r\n\r\nPřipomínek moc nemám. Jsou to spíše takové názory, kdy bych něco
    formuloval jinak ale ve skutečnosti na tom tolik nezáleží. Tedy tady jsou takové
    drobné připomínky:\r\n\r\n1) Ve výkladu bych se asi snažil oddělit pojem metodiky
    a modelu životního cyklu aplikace. Ve výkladu se věnuješ především životnímu cyklu.
    Každá metodika se sice odvíjí od (je postavena na) konkrétního modelu životního
    cyklu ale je to ještě něco navíc a to i přestože se většinou jednotlivé základní
    principy předkládají na pozadí životního cyklu. V metodice mohou být i některé
    záležitost o řízení projektu nebo o určování náročnosti, jak o ni mluvíš na konci.\r\n\r\n2)
    Agilní metodiky se dosti používají v některých firmách; mají své výhody a nevýhody.
    Zkušený analytik nebo projektový manažer by měl určit jaká metodika by pro daný
    projekt byla vhodná.\r\n\r\n3) Někde narazíš na rozdělení požadavků na funkční
    a nefunkční. Nefunkční požadavky představují požadavky na určitou kvalitu nebo
    omezení. Mohou být např. časového, organizačního, technologického, atd. rázu,\r\n\r\n4)
    U vazby \"extend\" v use case diagramu zmiňuješ její význam. Zde je asi největší
    odchylka od správnosti ale není to nic zásadního. Vazba \"extend\" nepředstavuje
    modifikaci dvou typových úloh. Použití je spíše, pokud jedna typová úloha je určitou
    alternativou nebo volitelným rozšířením pro jinou typovou úlohu. Příklad by mohl
    být např. v situaci u mobilního operátora by byl nějaký use case sjednání smlouvy
    a k tomu by mohla být alternativa nákup dotovaného telefonu - nebo něco takového.\r\n\r\n5)
    U sekvenčního digramu nejde ani tolik o detailní popis algoritmu ale o tom jak
    jsou zasílány zprávy mezi jednotlivými objekty v čase (v nějako posloupnosti).
    Význam sekvenčního digramu spočívá zejména pro kontrolu, zda jsou v modelu všechny
    potřebné operace pro provedení určitého use case. Používá se zejména ve spojení
    se scénáři.\r\n\r\n6) V diskuzi na konci má spíše pravdu kolega. Většinou existuje
    něco jako katalogové zpracování požadavků, kde lze rozdělit funkční a nefunkční.
    V use case diagramu se potom dělají jen ty funkční. Některé nefunkční požadavky
    mohou být vyjádřeny jako podmínky pro provedení určité typové úlohy ale technické
    by se tam asi neobjevily. V uml požadavky nejsou přímo ale definuje se tam něco
    jako uživatelsky definovaný element.\r\n\r\nNo snad ti to alespoň trochu pomůže.\r\n\r\nJinak
    je to určitě zajímavé a dám na tebe odkaz do svých odkazů, aby se k tomu dostali
    studenti:).\r\n\r\nZdraví Pavel"
- id: 20
  author: Tomáš Brejla
  author_email: brdloush@brdloush.net
  author_url: ''
  date: '2007-02-28 15:11:26 +0100'
  date_gmt: '2007-02-28 14:11:26 +0100'
  content: "Musím říct, že podcasto-seminář se mi velice líbil. Je vidět, že za tvými
    slovy se skrývají dlouholeté zkušenosti, nic jsi neprezentoval zcestně a všechno
    dávalo smysl. Slajdy jsem neviděl, ale myslim že to ani nebylo nutné. Asi sis
    nějak podvědomě uvědomoval, že obrázky máš popsat tak, aby tomu rozuměli i ti,
    kteří tu prezentaci nemají před sebou ;) Fungovalo to bezvadně. Zbytečně dlouhé
    to určitě nebylo, i když se přiznám, že jsem si to pouštěl \"na dva zátahy\",
    cca půl hodiny před koncem jsem potřeboval na chvilku orazit ;)\r\n\r\nPodcast
    jsem poslechl až poté, co jsem si přečetl komentář Pavla Čecha. Zaujal mě zejména
    bod 6 jeho komentáře, protože o termínu \"katalogové zpracování požadavků\" (či
    jak je zmíněno v podcastu \"katalog uživatelských požadavků\"), jsem zatím neslyšel.
    Asi budu muset trošku zagooglit a vzdělat se ;). Taky mě napadlo, že nefunkční
    požadavky na Use-case jde rozhodně v UML zakreslit (ať už pomocí stereotypu, tagged
    values, constraintů a nebo v nouzi Text notem). Je ale pravda, že se asi můžou
    objevit i požadavky obecné, které se neváží na jednotlivé Use-casy. Kam třeba
    napsat požadavek stylu \"Systém musí mít dostupnost 24/7\", \"musí utáhnout X
    requestů za vteřinu\" a podobně? To by se do UML diagramů cpalo asi hodně  blbě.
    \r\n\r\nJeště dotaz k bodu 4 komentáře Pavla Čecha - osobně mi vazby extends a
    include u Use-case diagramu  moc k srdci nepřirostly a docela pravidelně zapomínám
    na to, jak že by se tyhle 2 potvory měly modelovat. Takže jsem docela rád slyšel
    názor, který sdílím také -- že zrovna tyhle vazby nejsou tak důležité, že prioritou
    je spíš nezapomenout na všechny důležité use-casy. Přijde mi, že na extends a
    include vazbách se lpí jen v literatuře a tak trochu na \"akademické rovině\".
    Prakticky se mi ale zdá, že diagramy to často spíš jen znepřehledňuje a že pokud
    to dokáže celkem solidně mást mě, tak zákazník z toho asi moc moudrej taky  nebude
    ;) \r\n\r\nV průběhu podcastu jsi zmínil i MDA. Osobně bych nad tímhle přístupem
    hůl nelámal. Pokud se použije uváženě, dokáže ušetřit mnoho práce. Viz třeba AndroMDA
    a její cartridge pro modelování perzistentní vrstvy (hibernate nebo EJB nebo EJB3)
    a business vrstvy (spring nebo ejb session beany). Obrovskej problém je ale velice
    špatná až žádná podpora v nástrojích (jak v IDE, tak v UML kreslidlech). Rozhodně
    ale doporučuju nakoupit balík čokolády (na obrnění nervů -- bude potřeba) a vyzkoušet
    si AndroMDA, nebo také třeba OpenArchitectureWare (OAW).. (na \"Software Engineering
    Radio\" je právě o OAW několik MDA-related podcastů). Taky nevěřím na něco jako
    \"úplný MDA přístup\". Ale na využití sémanticky silných modelů pro generování
    některých částí kódu, všelijakých mapovacích a konfiguračních XMLek, tak na to
    už docela věřím. Ale jen do té míry, kdy to je efektivní a přináší to výhody.\r\n\r\nZmínil
    jsi, že nerad kreslíš do modelů věci ve stylu Strutsovských ActionForms (které
    patří ale spíš až do návrhu, ne do analýzy) a podobně. Tady rozhodně souhlas.
    \ Nicméně když se nad tím zamyslíš, tak takové ty všemožné tmelící třídy/metody/...
    dokážeš obvykle se znalostí svého \"částečného  modelu\" a znalostí architektury
    (tj, také znalostí transformačních pravidel z modelu do kódu) domyslet a dokódovat
    ručně.  Takže ono je asi důležité vždy myslet na to, že např. modelovaná  třída
    nemusí nutně ve finále v implementaci odpovídat právě jedné třídě javovského kódu
    a že mnohdy není třeba modelovat 10 elementů, ale třeba jen jeden, který bude
    sémanticky bohatší. Třeba AndroMDA pro &gt; třídy vyplivne tolik zajímavých artefaktů
    (interface + base + impl POJO třídu vč. milých drobností jako equals a hashCode;
    továrnu; mapovací xmlka pro hibernate; ddl skripty pro založení DB schématu; finder
    metody a query; DAO třídy,..), že člověk až žasne, co všechno nemusí transformovat
    z modelu do kódu (čti \"nabušit\" ;)) ručně. A to vše s minimálním usílím -- tu
    a tam něco označíš pevně daným stereotypem..\r\n\r\nCelkově to bylo příjemné a
    zajimavě podané poslouchání -- na první podcast super. Tak snad se brzo objeví
    i nějaký \"opravdický\" podcast ve stylu CZpodcastu nebo Javaposse ;)  Poděkování
    zaslouží Honza Severa, že svolil uveřejnit záznam. Takovýhle pohled šéfa na věc
    se mi líbí.\r\n\r\n--\r\nTomáš\r\n\r\nP.S.: na začátku a konci podcastu by to
    chtělo zlepšit srozumitelnost textu co říkáš. Možná ztlumit hlasitost, snížit
    basy.. je to takové trochu zahuhňané. Semináři samotnému je ale rozumět parádně.
    Můžu se zeptat čím jsi to snímal?\r\n\r\nP.P.S.: magnatune outro \"That was track
    number...\" je mazec ;)"
- id: 21
  author: Novoj
  author_email: novotnaci@megasphera.cz
  author_url: http://blog.novoj.net
  date: '2007-02-28 15:57:03 +0100'
  date_gmt: '2007-02-28 14:57:03 +0100'
  content: "Pane jo, to je komentář. Díky za kladný ohlas - a plno námětů. Zkusím
    na pár z nich reagovat:\r\n\r\n1) ano je to docela dlouhé, taky jsem měl ke konci
    už pěkně těžký jazyk ;)\r\n\r\n2) to co uvádíš (dostupnost, výkonnost) jsou právě
    příklady nefunkčních požadavků - v KUP mají své jasné místo; na základě Pavlových
    připomínek se ještě jednou podívám na vazbu KUP s UML (<a rel=\"nofollow\" target=\"_new\"
    href=\"http://www.sparxsystems.com.au/platforms/requirements_management.html\"
    rel=\"nofollow\">pokud vím tak v  Enterprise Architectu je nějaká možnost evidovat
    \"requirements\" a ty mají své podtypy functional a nonfunctional</a>)\r\n\r\nPár
    zajímavých informací by se možná dalo najít i na blogu p. Katolického (<a target=\"_blank\"
    href=\"http://www.akamonitor.cz/SRM.htm\" rel=\"nofollow\">http://www.akamonitor.cz/SRM.htm</a>)\r\n\r\n4)
    kolega zkoušel AndroMDA a po nějakém tom dni zkoušení říkal, že to stojí hodně
    námahy celé to kolečko rozchodit a ve výsledku nebyl přesvědčen o tom, že ta námah
    stojí za to - zkoušel jsem ho naťuknout a snad si najde čas, aby sem napsal svůj
    komentář k AndroMDA; osobně mám největší hrůzu z opětovného kolečka zpět z kódu
    do UML modelu - ne že bych měl velké zkušenosti z MDA, ale tohle je velký oříšek,
    bez jehož kvalitního rozlousknutí nemá MDA valného smyslu (lépe řečeno pak se
    degraduje na generátor kódu z modelu, a to je jen část MDA principů). Nicméně,
    kdyby byl open source nástroj, který by toto zvládal včetně těch funkcionalit
    co popisuješ, dokážu si představit přínos - lépe řečeno velké ušetření opičí práce.\r\n\r\n5)
    Díky za technické připomínky ... intro a outro zkusím vylepšit. Nicméně neplánuji,
    že bych byl tak aktivní podcaster, jako kluci z CZpodcastu nebo další co jsi zmiňoval.
    Jen podcasting považuji za skvělou formu vzdělávání, která v Čechách ještě není
    nijak moc rozvinuté - proto jsem chtěl také přispět naší malé komunitě svou troškou
    do mlýna."
- id: 22
  author: Tomáš Brejla
  author_email: brdloush@brdloush.net
  author_url: ''
  date: '2007-02-28 17:09:35 +0100'
  date_gmt: '2007-02-28 16:09:35 +0100'
  content: "ad 2.) Jasně, nefunkční požadavky to jsou. Nicméně bych řekl, že i ty
    je ještě potřeba rozlišovat na nefční požadavky use-casu a nefční požadavky systému.
    Ty na use-case by teoreticky šly zahrnout do use-case diagramu některou ze zmíněných
    forem (stereotyp, constraint,..). Ty obecné (na celý systém) rozhodně ne.\r\n\r\nZa
    odkazy díky, mrknu na ně.\r\n\r\nAsi mi uniklo... co je KUP? Narazil jsem jen
    na \" Knowledge Unified Process\", což asi nebude to pravé ořechové ;)\r\n\r\n\r\nad
    4.) \r\n\r\nS tím rozcházením je to opravdu docela síla.. To nelze nez potvrdit.
    Největší problém jsem měl zpočátku s Mavenem, protože je to pro mě i dnes stále
    celkem velká magie, do které oproti antu kolikrát netuším kam hrábnout abych dosáhl
    svého cíle.\r\n\r\n\"Opětovné kolečko\" z kódu do UML ani neočekávej. Popravdě
    jsem zatím nikde v praxi neviděl opravdu fungující (jak MDA tak  neMDA) nástroj,
    který by efektivně uměl zárověň forward i reverse engineering. Celkově reverse
    engineeringu moc nevěřím. Zejména z již zmíněného  důvodu, že vůbec nemusí platit
    onen poměr  1:1 ve smyslu modelovaný_element:výsledný_element. Pokud vím, MDA
    nikde ani nespecifikuje, že by nástroje měly umět reverse.. Primárně mluví o transformacích
    (CIM)-&gt;PIM-&gt;PSM. Transformace \"tam a zpět\" vyloučené nejsou, ale i dnes
    je stále ještě dost problémů s \"jednoduchým\" jednosměrným přístupem.\r\n\r\nOna
    ta \"specifikace\" (manifest) je celkově dost vágní a spíš než o konkrétních postupech
    je MDA definováno jako sada technologií (XML, XMI, MOF, UML, OCL, QVT a bůhví
    co ještě), které umožňují využívat modelů a automatických transformací mezi nimi.
    Dále je na celou věc potřeba nahlížet jako na metodiku - tzn. zejména si zvyknout
    na to, že model je v MDA povýšen na (nad) úroveň kódu. Podobně jako u extrémního
    TDD kód bez testu neexistuje, u MDA přístupu když potřebuješ třeba přidat metodu
    do bussiness logiky, uděláš to na modelu, přegeneruješ příslušné artefakty pomocí
    MDA toolu a pak teprve naimplementuješ onu metodu.\r\n\r\nDruhá věc je i tíhnutí
    k metamodelování -- zamyšlením se nad tím, co momentálně děláš otrocky a šlo by
    zautomatizovat a následně navržení metamodelu, pomocí kterého budeš moct zmíněné
    věci modelovat + transformačních templatů. Takže v řeči AndroMDA je to taková
    myšlenka \"rozvíjej/vytvářej si svoje cartridge podle toho jak potřebuješ\". Pravda
    je, že tohle už tak snadné není a člověk je obvykle placený za implementaci fíčur,
    které chce zákazník a ne za to, že si na to píše vlastní nástroje, které mu pak
    ulehčí práci.. No ale to se už trochu dostáváme k problému \"obhajitelnosti\"
    tohohle postupu -- podobný problém má ale koneckonců i třeba TDD..\r\n\r\nPodle
    mě je to tak, že pokud si zvykneš na takovýhle top-down (či forward) přístup,
    nepotřebuješ nic jako \"reverse engineering\" - synchronizaci modelu podle kódu.
    Ta je koneckonců těžko realizovatelná a mnohdy téměř nemožná. Dost lidí se vyděsí
    při představě častého přegenerovávání kódu -- napadne je, že při tom příjdou o
    své změny v implementaci. Ale i tohle je vyřešeno.. objektově orientované jazyky
    a návrhové vzory dávají dostatek prostředků (viz třeba způsob jak se s tím vypořádává
    AndroMDA - obvykle se generuje interface a base implementace třídy a o tvojí implementaci,
    která dědí baseImpl, už se staráš jen a jen ty sám.). Takže ani forward generování
    bych nezavrhoval..\r\n\r\nKdyby kolega našel čas k sepsání svého komentáře s porodními
    bolestmi s AndroMDA, bych byl určitě rád. Ostatním jedno velké SORRY za mírný
    odklon od tématu ;)\r\n\r\nAd. podcasting: absolutní souhlas. Já jsem si tuhle
    formu vzdělávání/informování hodně oblíbil. Kvůli Javaposse jsem si dokonce pořídil
    mp3 přehrávač a každý týden se těším jak malé děcko na to, až mě RSS čtečka upozorní
    ;)"
- id: 23
  author: Novoj
  author_email: novotnaci@megasphera.cz
  author_url: http://blog.novoj.net
  date: '2007-02-28 20:05:41 +0100'
  date_gmt: '2007-02-28 19:05:41 +0100'
  content: "Ad KUP) Katalog Uživatelských Požadavků - česká alternativa SRM (Software
    Requirements Management viz. p. Katolický). S tímto termínem jsem se setkal kdysi
    na školení ve firmě Komix.\r\n\r\nEvidentně máš s MDA větší zkušenosti než mám
    já. Co jsem zatím já zaslechl, přečetl nebo probral s kolegy u piva zdál se mi
    kvalitní reverse engeneering důležitou součástí MDA. Možná to tak není, ale bez
    něj mi přijde MDA velmi nepoužitelné. Umím si to představit ve stylu one-man-show
    projektu, ale pokud na projektu pracuje tým 5 lidí museli by se při synchronizaci
    modelu a řešení konfliktů v SCM utlouct. Co se týká toho přístupu s tím, že nástroj
    generuje jen base třídy, ze kterých se implementační třídy odvozují (ať přes implementaci
    nebo dědičně), tak s tím mám naprosto reálné zkušenosti. Před 4mi lety jsme ve
    firmě měli projekt, na kterém jsme toto zkoušeli. Pravda - používali jsme nějaký
    prastarý open source UML nástroj, s tím, že jsme si implementovali vlastní generátor,
    který s XMI exportu generoval třídy a který nebyl taky dokonalý - ale výsledek
    byl naprosto hrůzostrašný. Na projektu jsme dělali jen ve dvou lidech, ale dalo
    nám neuvěřitelné množství práce udržet vše v chodu při paralelních změnách. Tato
    zkušenost je v mé paměti natolik živá a hrozivá, že bych nikdy touto cestou už
    nešel.\r\n\r\nJednak ten nástroj měl problematické synchronizování dvou odvozených
    modelů (musely být dva, jelikož na jednom jsem pracoval já, na druhém kolegyně)
    - tzn. toto vyžadovalo dost klikání a přemýšlení. Další věcí bylo, že před každou
    synchronizací se ten druhý model musel dostat fyzicky na tvůj počítač, aby se
    se mohla provést synchronizace (ano šlo to vyřešit uložením obou modelu na sdílený
    síťový disk). Dál jsme museli synchronizovat i vygenerované kódy přes SCM, což
    dalo také hodně práce. Nakonec jsme kapitulovali a dohodli se, že změny bude dělat
    pouze jeden a nebudeme synchronizovat dva modely. To ale nehorázně zpomalilo vývoj,
    protože s každou změnou, na kterou se přišlo při implementaci kódu, se muselo
    za tím jedním z nás, aby to dal do modelu, pak znovu prošlo to hrůzostrašné kolečko,
    commit do SCM a pak se teprve dalo pokračovat s vývojem dál. A to jsme byli dva
    - neumím si to vůbec představit ve více lidech.\r\n\r\nProstě jsem přesvědčen
    že bez kvalitního reverse engeneeringu se model od reálného kódu dříve nebo později
    nevyhnutelně rozjede. A snaha o udržení modelu souhlasicího s reálem je tím dražší,
    čím je model detailnější. Když píšeš o tom, že MDA je takové vágně definované
    s tím, že je to spíše snůška technologií - napadá mě, že se může jednat jen o
    další buzzword, kterých známe už mrtě.\r\n\r\nAd Podcasting) Taky jsem se zamiloval
    do Podcastů - před půlrokem jsem si koupil nový mobil - Sony Ericson W700i, který
    je na podcasty jak stvořený. 250MB na kartě, které je již v základní sadě spolu
    se sluchátky a SW pro synchronizaci s PC jsou naprosto postačující. Navíc, nemusím
    tahat s sebou další hračku - mobil stejně nosím téměř pořád u sebe. Můžu jenom
    doporučit."
---
<p>Na přání svých současných kolegů ve firmě <a target="_blank" href="http://www.fincommaterna.com/">FMC</a> jsem připravil seminář zaobírající se základy analýzy v UML.</p>
<ol>
<li>popisem životního cyklu</li>
<li>cíle analýzy a návrhu</li>
<li>behaviorální diagramy</li>
<li>strukturální diagramy</li>
<li>diagramy vztahů</li>
<li>odhadování časové náročnosti</li>
<li>tipy a triky</li>
</ol>
<p>Obávám se, že jsem v některých částech nebyl úplně přesný, na mnoha místech jsem mohl řadu věcí popsat podrobněji a někde jsem nebyl schopný nalézt ty správné výrazy a obraty. Celou dobu jsem mluvil nespisovně a častokrát ani nedodržel shodu přísudku s podnětem. Pokud se vám zdají některé mé myšlenky zavádějící nebo obtížně pochopitelné, neváhejte a napište mi reakci - pokusím se nejasnosti vysvětlit zde.</p>
<p>Původním záměrem bylo věnovat se hlavně UML diagramům, nakonec to však sklouzlo trošku více k rozebrání životního cyklu. Dále jsem se ve výkladu (po konzultaci s odborníkem na  UML - Pavlem Čechem z Univerzity Hradec Králové)  dopustil některých nepřesností a někde možná i chyb. Proto prosím koukněte na první komentář k tomuto článku. Některá má tvrzení zde budou revidována.<br />
A buďte shovívají, tohle je můj první "podcast". :)</p>
<p><strong>Poděkování:</strong> Jsem rád, že mi bylo umožněno publikovat záznam z tohoto semináře veřejně (tímto děkuji svému šéfovi Honzovi Severovi) a podělit se i s vámi o tyto myšlenky.</p>
<p><strong>Použitá hudba:</strong>  <a href="http://magnatune.com/artists/albums/utopiabanished-night/">Utopia Banished - Night of the Black Wywern</a>, Forshadowing the Endless Quest (<a target="_blank" href="http://magnatune.com/">http://magnatune.com</a>) zveřejněná pod Creative Commons License</p>
<p><strong>Podcast License: </strong><a target="_blank" href="http://creativecommons.org/licenses/by-nc-sa/1.0/"><img align="right" title="Creative Commons - Some Rights Reserved" alt="Creative Commons - Some Rights Reserved" src="http://he3.magnatune.com/img/somerights2.gif" /> Creative Commons</a></p>
<p><a title="MP3 Podcast" href="http://files.novoj.net/ZakladyAnalyzy/zaklady_analyzy_a_navrhu_v_UML.mp3"><img align="left" title="MP3 Podcast" alt="MP3 Podcast" style="margin-right: 10px" src="http://files.novoj.net/button_mp3.gif" /></a> <a title="MP3 Podcast" href="http://files.novoj.net/ZakladyAnalyzy/zaklady_analyzy_a_navrhu_v_UML.mp3"><strong> Podcast</strong></a> [1:38:17] 23,6 MB</p>
<p><a title="Doprovodná prezentace (PDF)" href="http://files.novoj.net/ZakladyAnalyzy/zaklady_analyzy.pdf">Doprovodná prezentace</a> (PDF) 142 KB</p>
