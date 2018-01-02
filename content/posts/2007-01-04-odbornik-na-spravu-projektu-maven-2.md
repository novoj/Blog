---
status: publish
published: true
title: Odborník na správu projektu - Maven 2
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Stále mnoho vývojářů používá pro buildování svého projektu ant nebo maven
  1, někteří si možná píší dokonce své sh nebo bat skripty. Možná o nové verzi Mavenu
  vědí a možná mají důvody proč zůstat u svého \"osvědčeného\" řešení. Sám jsem mezi
  ně patřil, ale přešel jsem - a teď vidím, že jsem udělal dobře, móóóc dobře :).\r\n\r\nJaké
  hlavní výhody Maven 2 přináší?\r\n\r\n"
wordpress_id: 5
wordpress_url: http://blog.novoj.net/2007/01/04/odbornik-na-spravu-projektu-maven-2/
date: '2007-01-04 21:17:16 +0100'
date_gmt: '2007-01-04 20:17:16 +0100'
categories:
- Maven
tags: []
comments:
- id: 3
  author: Tomas Kutin
  author_email: tomas.kutin@gmail.com
  author_url: ''
  date: '2007-01-15 13:49:15 +0100'
  date_gmt: '2007-01-15 12:49:15 +0100'
  content: 'rad bych reagoval na tento clanek tykajici se vyborneho nastroje maven
    2, mam s nim urcite zkusenosti i kdyz ne zase tak velke ale jako prvni vec kterou
    bych chtel vyzdvihnout tak je integrace do vyvojovych prostredi, ja sam to mam
    rozjete v NetBeans a Eclipsu a nemohu si to vynachvalit, pouze si otevrete adresar
    obsahujici pom.xml a vse ostatni uz za vas udela prislusny plugin, tzn. nemusite
    nastavovat zdrojove adresare, slozite hledat knihovny nutne ke kompilaci projektu
    atd...z minuleho zamestnani sem mel prave vzdy se zavedenim projektu do ide postavene
    chlupy na zadech :) (nevim jestli to byla moje chyba....:) ) ale ted pouze otevrete
    projekt a "vetsinou" je bez chyb zkompilovan a pripraven k pouziti..., a kdyz
    potrebujete pridat dalsi knihovny .... pouze pravym tlacitkem add dependency a
    zobrazi se list box s nalezenymi knihovnickami z repositories, dalsi vyhoda alespon
    co se tyce pluginu Maven 2.0 integration pro eclips je jednoduche spousteni jednotlivych
    fazi projektu a navic s definovanymi profily pomoci External Tools...take sem
    privital transitivni zavislosti mezi knihovnami..... pro nekoho muze byt maven
    slozitejsi, ale myslim ze kdyz nekdo dokaze napsat slozity skript v antu tak to  dokaze
    bez vetsich problemu casem i v mavenu : )'
- id: 139
  author: benzin
  author_email: benzin@centrum.cz
  author_url: http://live.jabbim.cz/benzin
  date: '2007-06-05 22:26:36 +0200'
  date_gmt: '2007-06-05 21:26:36 +0200'
  content: "Dneska jsem uz cetl jiny clanek proc pouzivat Maven 2  a ne Anta. S tim
    jsem nesouhlasil, spousta veci tam predkladanych mi neprisli prilis pravdive,
    ale tento clanek mi mluvi z duse.\r\n\r\nJenom na okraj. Pokud pom.xml k damenu
    projektu neexistuje neni problem knihovnu i tak nainstalovat a v pripade ze na
    nejake zavislosti prijdete vy sami muzete je tam docela jednoduse pridat. Takze
    tam kde podpora pro Maven 2 neni neni problem to vyresit.\r\n\r\nS temi zavyslostmi
    jde, ale zaroven i jedna potiz, nektere knohovny maji spoustu zavislsti, ktere
    jsou ale ptrebo jenom v urcitem pripade. Dost casto se pak stane ze sebou tahata
    spostu knihoven o kterych nevite k cemu vlastne sou a nakonec je ani nepotrebujete.
    To se v Antovi nestavalo. Ale pokud nechcete danou aplikaci zrovna dostat na 5.4
    disketu, tak by to nemusel byt az tak zasadni problem :)\r\n\r\nP.S.: Mam trefnejsi
    priklad pro vhodne vyuziti profilu. Je to pro automaticke testy. Napriklad testovani
    databazovych trid je docela zdlouhave, pokud prave nepracujete na objektech, ktere
    by je nejak menili, nebo vyuzivali muzete proste pomoci profilu jednoduse vypnout.\r\n\r\nMy
    osobne mam profil na kompletni testy, na rychle testy a kazdy vyvojar ma jeste
    svuj vlastni profil, ve kterem ma ty nejzhavejsi testy, ktere nejvic potrebuje.
    Docela to zrychli vyvoj."
- id: 140
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-06-06 04:40:17 +0200'
  date_gmt: '2007-06-06 03:40:17 +0200'
  content: "Ta potíž jde docela jednoduše vyvrátit - lze použít tzv. \"optional\"
    dependency (viz. např. knihovny Sprignu), která zajistí, že se tyto dependence
    automaticky nedotáhnou, pokud nebudete chtít. Více informací zde: http://maven.apache.org/guides/introduction/introduction-to-optional-and-excludes-dependencies.html\r\n\r\nJinak
    s těmi profily máte pravdu - příkladů by se dalo najít mrtě. Profily jsou prostě
    boží. :)"
- id: 141
  author: benzin
  author_email: benzin@centrum.cz
  author_url: http://live.jabbim.cz/benzin
  date: '2007-06-06 10:26:42 +0200'
  date_gmt: '2007-06-06 09:26:42 +0200'
  content: "Jo to se samozrejme vyuzit da, jenze kdo ma vedet ce vsechno skutecne
    potrebuje? Nehlede na to ze jedena zavislost si natahne druhou a tak pak dalsi
    dvacitku. Vsechno to prochazet je docela opruz. naopak v Antovi (resp. v direktivnim
    build nastroji) hledate problem az kdyz vam vyskoci chyba ze knihovnu nebylo mozne
    najit.\r\n\r\nJde jen o pristup. Btw. uz jsem narazil na docela blbe resitelny
    problem. Jedena knihovna chtela saxon sedmickove verze a druha sestkovou. A pac
    je to nekompatibilni navzajem se to docela hadalo. Spatne se to dohledava kdyz
    nejednou nevite proc vam webserver nestartuje.\r\n\r\nA dalsi problem ktery vznika
    pri spouste zavislosti, ze nejakou zapisete nchte dvakrat. Z pomu se pak pouziva
    vzdy ta definice ktera byla napsana jako posledni. Takze chcete zmenit knihovnu
    (ja treba jaybird) ze stare na novou verzi. Udelate to samzorejme jenom u prvniho
    vyskytu (to ze je tam druhy vas nenapadne) a problem zustava. Tak hledate dalsi
    tri dny jak debil, co je spatne. Nakonec zjistite pohledem do buildovaneho waru,
    ze je tam porad ta stara verze jaybirda.\r\n\r\nAle to jsou jen dorbne problemy
    k z praxe, ktere zaberou hodne casu na odhaleni kde je zakopany pes, ale nezaberou
    moc casu na opravu."
- id: 142
  author: Jan Novotný
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-06-06 11:53:31 +0200'
  date_gmt: '2007-06-06 10:53:31 +0200'
  content: "No z mých zkušeností bych to neviděl jako úplně zásadní problém. Jednak
    člověk depencence na knihovnách neřeší valnou část projektu - typicky je hodně
    práce při setupu a pak když se něco nového přidá (což je opravdu jen sem tam).
    Po zbuildování se vyplácí si prohlédnout sestavení, jestli se tam nevyskytnou
    některé knihovny 2x. Pak stačí v tom \"hlavním projektu\" což bude typicky war
    nebo ear, dát explicitně závislost pouze na jedné z těch verzí (opět typicky na
    té novější). Maven při sestavování potom upřednostní vámi explicitně uvedenou
    verzi knihovny (v. 2.0.5 Mavenu).\r\n\r\nNaštěstí se Maven 2 neustále zlepšuje,
    takže časem se myslím i tyhle věci vyladí k naší spokojenosti. Ono to totiž ve
    své podstatě vůbec není jednoduchý problém k řešení (myslím tím problematiku sestavování
    projektu a vůbec projektové správy kolem) - už v současném stavu je Maven 2 ve
    správě projektu daleko před Antem."
---
<p>Stále mnoho vývojářů používá pro buildování svého projektu ant nebo maven 1, někteří si možná píší dokonce své sh nebo bat skripty. Možná o nové verzi Mavenu vědí a možná mají důvody proč zůstat u svého "osvědčeného" řešení. Sám jsem mezi ně patřil, ale přešel jsem - a teď vidím, že jsem udělal dobře, móóóc dobře :).</p>
<p>Jaké hlavní výhody Maven 2 přináší?</p>
<p><a id="more"></a><a id="more-5"></a></p>
<ul>
<li><strong>Best Practises</strong></li>
</ul>
<p>Maven je především koncentrátem dobrých zkušeností z oblasti správy projektů. To není jen termín - v jeho případě je to pravda. V praxi to znamená, že jej nepoužíváte jen k sestavování instalačních balíčků, ale že pokrývá všechny oblasti, které se správou projektu souvisí a hlavně - navádí vás, jak je už od začátku dělat správně.</p>
<p>Základem je správná adresářová struktura (ano můžete si ji nadefinovat jinak - ale proč vymýšlet něco co je už vymyšlené a funguje dobře?), způsob ukládání zdrojových kódů do SCM (rozdělení na trunk, releases, tags), automatické spouštění  a organizace testů, release management a mnoho dalšího.</p>
<ul>
<li><strong>Přehlednost, jednotnost, samodokumentační efekt<br />
</strong></li>
</ul>
<p>Snad každý se už setkal s tím, že každý projekt je sestavován tak trochu jinak. Nový vývojář v týmu potom ještě nějakou dobu zjišťuje jak to celé vlastně funguje. Jaké skripty má pouštět a co mu ty skripty provedou (projekt od projektu jinak). Stejné je to i s oblíbeným Antem - na většině projektů si tým vytvoří vlastní targety, pokaždé dělají tak trochu něco jiného, i když v mnoha případech už se alespoň ustálila jmenná konvence. Někde je adresářová struktura odvislá od používaného IDE, vývojář s jiným IDE se potom zase problematicky přizpůsobuje struktuře, která není pro to jeho IDE nativní. Výsledkem je jednoduše řada problémů na místech, kde problémy být nemusí a vývojář se zabývá něčím, za co mu nikdo neplatí.</p>
<p>Maven v tomto směru přinese řadu zlepšení - většinu z nich ne okamžitě. V případě, že většina organizace bude pro správu projektů používat maven, bude pro vývojáře z různých projektů jednoduché orientovat se v jiných projektech. Struktura je stejná, principy sestavování také, názvy cílů jsou všude stejné, rozdíly jsou velmi jednoduše čitelné v jediném konfiguračním souboru projektu a tím je pom.xml.</p>
<p>V tomto souboru lze také nalézt většinu z informací, které jako vývojáři ke své práci potřebujete. Jsou zde cesty k repozitory zdrojových kódu, bug trackeru, adresa integračního serveru, seznam vývojářů, odkazy na mailing listy atd. Řada z těchto informací není jen pasivní, ale Maven je zároveň využívá při vlastní práci při buildování. Všechny tyto informace lze jednoduše a přehledně zobrazit na generované projektové stránce.</p>
<ul>
<li><strong>Tranzitivní závislosti</strong></li>
</ul>
<p>Závislosti knihoven je věc přirozená, ale rozhodně ne triviální. Kupříkladu pokud buildujete s pomocí Antu, řešíte přilinkování závislostí více méně sami. Setkal jsem se například s ukládáním všech knihoven, na kterých byl projekt závislý do SCM (kdo stahoval 30MB přilinkovaných knihoven z SVN spolu se zdrojovými kódy, ví o čem mluvím :) ). Pokud používáte Maven verze 1, máte sice již způsob jak závislé knihovny k projektu připojovat - nicméně se dost napíšete. Kupříkladu pokud chcete použít framework Struts musíte ručně nadefinovat závislost cirka na 20 dalších knihovnách (docela dost práce na jeden framework - a to jsme zatím u tenkých řešení ;)).</p>
<p>Co přináší Maven 2? To samé jako Maven 1 jen už nemusíte tolik psát - stačí nadefinovat závislost na hlavní knihovně Struts a ta sama ve svém pomu definuje další závislosti na dalších knihovnách, ty na dalších knihovnách atd. Ve výsledku vám ta vaše jedna závislost dotáhne požadovaných 20 knihoven, které potřebujete ke spuštění aplikace. Skvělá věc, která se potýká s jedním problémem. Knihovny, které takto přilinkováváte musí mít nadefinovaný vlastní pom = musí být zbuildované s pomocí Maven 2. V současné době snad už většina softwérhausů (Codehaus, OpenSymphony, brzy přibude i Apache Jakarta a další) používá pro buildování Maven, nebo alespoň knihovny s pomocí něj builduje právě pro své zákazníky-vývojáře, kteří Maven používají. Není to ale samozřejmost.</p>
<ul>
<li><strong>Jasně definovaný životní cyklus</strong></li>
</ul>
<p>Další novinkou, kterou jsem dříve považoval za negativum je striktní životní cyklus (striktní ale ne rigidní). Ant řeší různé stupně sestavování postupným převoláváním svých targetů, při složitějších projektech se z toho nakonec stane nepřehledný mišmaš, kterému už jen málokdo rozumí. Maven v první verzi měl také své pluginy pospojované velmi volně a postupným navěšováním pregoal a postgoal skriptů, se z celého buildování mohl stát také velmi nepřehledný proces.</p>
<p>Nový Maven přichází s jasným životním cyklem - nebo spíš sestavovacím procesem složeným z různých úrovní (např. resource-generate, compile, test, install, deploy). Maven při sestavování postupuje sériově podle nich. Tedy pokud chcete spustit automatické testy (fáze test) musí se před tím spustit předcházející fáze např. generate-sources, compile-sources, compile-test-sources atd. (podrobnější popis lze nalézt <a title="rozbor životního cyklu Maven 2" target="_blank" href="http://cvs.peopleware.be/training/maven/maven2/buildLifecyclePhases.html">například zde</a>). Na první pohled možná svazující, na druhý pohled jednoduchý, průhledný a skvěle použitelný mechanismus. Jednotlivé fáze nutně nemusí něco dělat - pokud v projektu nemá smysl automaticky generovat zdrojové kódy, fáze generate-sources proběhne aniž by fyzicky něco provedla. Uvedený životní cyklus je "standardní", ovšem je možné si definovat úplně jiný - vlastní životní cyklus (takový např. definuje <a title="ukázka odlišného životního cyklu" target="_blank" href="http://cvs.peopleware.be/training/maven/maven2/buildLifecyclePhases.html#site">plugin pro buildování projektové site</a>).</p>
<ul>
<li><strong>Tenká a jednoduchá konfigurace</strong></li>
</ul>
<p>Pokud jste někdy psali vlastní buildovací skript třebas v antu nebo shellu, jistě mi dáte za pravdu, že časem vznikla hezká řádka konfiguračních parametrů takového skriptu a v případě, že skript nebyl napsán chytře, často docházelo k tomu, že se uživatel tohoto skriptu trápil s jednotlivými nastaveními, aby mu vše běhalo, jak on požaduje. Navíc pokud jste vy nebyli při psaní poctiví a parametry jste rozumně nezdokumentovali, trápil se ještě čtením vašeho kódu.</p>
<p>Maven v tomto ohledu opět přináší plno výhod. Jelikož v sobě koncentruje pravidla pro organizaci projektu, vývojář musí pro první použití nastavit jen velmi málo věcí - i ty může nastavit pomocí průvodce. Zbytek je vzat z defaultních hodnot, které v 99.9% případů dostačují. Všechny konfigurační informace o projektu se nacházejí v jednom souboru (pom.xml), který je v současné době již velmi dobře zdokumentován, takže vy nemusíte psát vůbec nic a kolegové mají přitom po ruce dostačující dokumentaci ke své práci. V porovnání ke své funkcionalitě je množství informací v pom.xml velmi úsporné - to je již na první pohled znát pokud porovnáte velikost pom.xml s konfiguračními soubory Maven 1, popř. build skripty antu.</p>
<ul>
<li><strong>Profily sestavování</strong></li>
</ul>
<p>Skvělá věc, která je ve verzi 2 jako novinka. Umožňují vám definovat odchylky od standardního procesu. Obtížně se to teoreticky vysvětluje, proto tuto funkcionalitu předvedu na příkladu</p>
<p>Představte si, že máte sestavování projektu vyladěné pro vývoj. Automatické testy běhají jako víno, vše se chová     tak jak má i při deployi na vývojový server a přijde čas prvního reálného release. V tu chvíli se zjistí, že knihovny, které vy pro vlastní vývojové prostředí musíte přilinkovávat v reálném prostředí již existují a do vašeho balíčku se znovu dostat nesmí. Řešením je použít profil - profil je reprezentován svým unikátním jménem a ve svém těle "modifikuje" vybrané části původního pom.xml od kterého se odvozuje. Tzn. lze v něm jednoduše znovu nadefinovat celou deklaraci závislostí (dependencies) podle nových požadavků. Samozřejmě takto je možné modifikovat celou řadu dalších údajů, což vám ve výsledku dává velmi mocný nástroj pro vydávání různých verzí jednoho a téhož balíčku.</p>
<p>Velkými výhodami je krom jiného to, že i potom je celý projekt velmi přehledný a snadno se v něm vyznáte. Není nutné duplikovat stejné informace vícekrát - deklarujete jen ty části, které se mění. Po nějaké době si už ani nedokážete představit, jak jste mohli bez profilů žít ;).</p>
<ul>
<li><strong>Release management</strong></li>
</ul>
<p>Release management je bolístka, kterou není vždy jednoduché vyřešit. Maven vám k tomu dává dobrý návod ve formě release pluginu. Ten vás (a vývojáře vašeho týmu) nutí k tomu dodržovat základní pravidla. Mezi ně patří:</p>
<ol>
<li>přidělení nového čísla verze (nesmí se jednat o SNAPSHOT verzi)</li>
<li>všechny změny commitnuté do SCM, všechny konflikty musí být vyřešeny před vydáním verze</li>
<li>balíček nesmí záviset na žádné vývojové verzi (SNAPSHOT) jiného balíčku</li>
<li>je nakonfigurováno kam se mají ukládat "tagy" SCM před vydáním nové verze</li>
<li>všechny automatické testy před vydáním projdou bez chyby</li>
</ol>
<p>Vlastní plugin potom vyzve uživatele k zadání čísel verzí (nabízí již výchozí správné možnosti), sestaví zkušební balíček, spustí testy, po jejich spuštění zataguje stávající verze zdrojových souborů, provede si checkout do dočasného adresáře a v něm vytvoří finální "release" balíček. V následné fázi potom spustí generování projektové site, včetně všech doprovodných reportů a umístí "release" balíček do repository - čímž vlastně zveřejní všechny potřebné informace pro "veřejnost".</p>
<p>Byť se zdá uvedený mechanismus na první pohled perfektní, při rutinním používání je v něm vidět několik slabin. Plugin má problémy s děděním projektů (vazby parent a modules), je obtížná konfigurace pluginu (např. vypnutí testů z nějakých důvodů) jelikož plugin si sám v sobě pouští nový maven, který nepřebírá parametry spuštění release pluginu a je také obtížné vložit dovnitř release procesu vlastní logiku. Doufám, že se v dalších verzích tyto nedostatky brzy odstraní, protože jinak se jedná o geniální řešení.</p>
<ul>
<li><strong>Základní build schémata "out of the box"</strong></li>
</ul>
<p>V tomto ohledu nenabízí nová verze Mavenu oproti předchozí nic převratného. Oproti antu je to však stále velká přednost - pokud nepracujete na něčem velmi neobvyklém, pravděpodobně budete moci svůj projekt moci sestavit jediným příkazem aniž byste museli kromě Mavenu cokoli dalšího instalovat a konfigurovat. Vše zajistí sada pluginů z plugin repository (nejste samozřejmě omezeni jen na jednu repository, ale můžete si nakonfigurovat libovolný počet - včetně vlastních s vlastními pluginy). Výhodou tohoto systému je také to, že vždy používáte ty nejaktuálnější verze sestavovacích pluginů.</p>
<p><strong>Proč vlastně Maven 2 nepoužívat?</strong></p>
<p>V následujících bodech bych rád rozebral mé pochybnosti a obavy, kvůli kterým jsem sám nechtěl Maven 2 vyzkoušet. Zkuste si je přečíst - možná přemýšlíte o tom samém.</p>
<ol>
<li><em>Je to novinka - co když mě to zavede do situace, kterou nedokážu vyřešit?</em><br />
Až taková novinka to není - Maven 2 vyšel v říjnu 2005. Já sám jsem po půl roce používání zatím nenarazil na situaci, kterou bych nedokázal řešit. Tam, kde jsem se s první verzí Mavenu dostal do úzkých, je často řešení v nové verzi triviální. Zprvu jsem se také obával nedostatku dokumentace, ale zhruba v říjnu 2006 poměrně rozsáhle rozšířili sekci uživatelské dokumentace (<a target="_blank" href="http://maven.apache.org/users/index.html">start guide</a>, <a target="_blank" href="http://maven.apache.org/guides/index.html">kompletní index</a>), takže tuto obavu můžete směle odložit. Pokud například nenajdete ten správný plugin pro Maven 2, který dělá to co potřebujete, můžete si nadefinovat a spustit i části Ant skriptů nebo si napsat vlastní logiku ve formě pluginu přímo v Javě.</li>
<li><em>Na první pohled to celé vypadá složitě.</em><br />
Možná ano, na druhý však nikoliv :). Stačí rychle prolétnout tyto články (<a target="_blank" href="http://maven.apache.org/guides/getting-started/maven-in-five-minutes.html">Maven v 5 minutách</a>, <a target="_blank" href="http://maven.apache.org/guides/getting-started/index.html">Maven ve 30 minutách</a>) a můžete začít pracovat. Do detailů se dostanete časem. Snad mi dáte za pravdu, že proniknout např. do antu není o mnoho jednodušší.<br />
Vaši kolegové pouze vymění jeden příkaz za příkaz jiný (pokud odhlédneme k nutnosti instalovat Maven, což je otázka skutečně pěti minut). Pokud nemají ambice na úpravu buildovacího mechanismu nemusí se nic speciálního učit.</li>
<li><em>Já bych klidně přešel, ale to by musela celá firma a na to já jsem moc malý pán.</em><br />
Nemyslím si, že to je nutně záležitost celé firmy. Podle mého názoru se v pohodě dá začít s jedním projektem - nechte své kolegy se přesvědčit samotné o výhodách Mavenu 2. Je jasné, že vás budou zkoušet - zprvu budete muset promptně řešit jejich požadavky na buildování, čímž jen více proniknete do principů Mavenu. Časem to bude na vás zavést firemní repository atd. Bude vás to stát nějaký ten čas, ale výsledek stojí za to. Ideálním způsobem je pokusit se zavést Maven do nového projektu, kde máte nějaké slovo - např. jako vedoucí programátor, technický vedoucí nebo někdo na podobné pozici. Začátek s Mavenem utáhnete na své autoritě, a časem už obhájí Maven své kvality sám. Staré projekty nechť se buildují po starém způsobu, na nové zkuste nasadit nové řešení.</li>
<li><em>IDE to zatím nepodporují - byla by s tím hrozná práce.</em><br />
Chyba lávky. V současné době existují specifické pluginy pro obvyklá IDE - např. pro NetBeans je to <a target="_blank" href="http://mevenide.codehaus.org/">Mevenide</a>, pro IntelliJ Ideu je to <a target="_blank" href="http://quebbemann.kicks-ass.net/idea-maven-plugin/">Maidea</a>, pro Eclipse je to např. <a target="_blank" href="http://m2eclipse.codehaus.org/">Tycho</a>. Sám mám zkušenosti s Mevenide pro NetBeans a jsem s ním velmi spokojený. Jednou z velkých výhod je především správa závislostí - pokud nějaký váš kolega přidá do pom.xml novou závislost, po update z SCM IDE automaticky detekuje změnu pom.xml a načte si do paměti nové závislé knihovny, takže bez restartu ide, bez úmorného klikání v dialozích máte znovu zkompilovatelný projekt včetně kontextové nápovědy v nových knihovnách. Do IDE je integrováno i spouštění testů a debugging. Integrace Mavenu na úrovni spouštění testů a vlastních projektů je samozřejmě chudší než nativní funkce IDE - nicméně přináší na oplátku jiné výhody (především při práci v týmech).</li>
<li><em>Když jsem to několik let dělal s antem, proč zkoušet něco nového?<br />
</em>Ant jako takový postačuje na buildování projektu, ale dost se s ním nadřete. Maven vám ušetří hodně práce a jeho zprovoznění a použití je antu velmi podobné. Ve chvíli, kdy potřebujete do svého projektu zavést nějakou novinku musíte doplnit do svých skriptů podporu pro tuto technologii. S mavenem máte velkou šanci, že bude existovat plugin, který vaše potřeby vyřeší jedním příkazem pokud dodržíte doporučené best practises. Pokud se chcete zbavit rutinní práce, zkuste Maven.</li>
<li><em>Maven 1 bohatě stačí - na novou verzi jsem neslyšel moc dobré ohlasy.</em><br />
Ano, taky jsem je slyšel - na webu je snadno najdete pod hesly "maven 2 negatives", "maven 2 sucks". Např. <a target="_blank" href="http://coderambling.com/2006/11/27/why-oh-why-i-hate-maven-2-now.aspx">Developer afterthough</a> (tady bych možná uvažoval o tom, že autor použil možná maven brzy na komplexní a rozeběhnutý projekt), <a target="_blank" href="http://blogs.maven.org/brett/2005/06/15/1118790757000.html">RE: Why do you Hate Maven</a> (tento článek se mi zdá poměrně dobře vyvážený a lecos se z něj dozvíte), <a target="_blank" href="http://www.oreillynet.com/cs/user/view/cs_msg/77733"><span class="headline">I really hate to be negative...</span></a> (tady bych spíš doporučil druhý komentář než uvodní pasáž). Jako na každý jiný software o kterém se mluví, i o Mavenu najdete rozporuplné názory. Proto doporučuji pustit se opatrnou cestou nasazení Mavenu na novém projektu, který není příliš rozsáhlý a na něm si osahat jeho vlastnosti. Sami potom uvidíte, jestli je jeho nasazení pro vás přínosem nebo ne.<br />
Z mých vlastní zkušeností snad mohu dát za pravdu v části prvnímu uvedeném článku v tom, že některé knihovny distribuované ve veřejných repository neobsahují informace o tranzitivních dependencích (někde můžete narazit třeba i na chyby) a knihovny od některých dodavatelů se do veřejných repository dostávají nějakou dobu, takže můžete mít potíže se zaváděním nějakých novinek. Opravdu ale záleží na tom, co ke své práci potřebujete - mě to prozatím žádné významné problémy nezpůsobilo.</li>
</ol>
<p><strong>Závěrem</strong></p>
<p>Tento článek by měl být úvodní k problematice Mavenu. Rád bych v blízké budoucnosti pokračoval dalšími články, které by vám pomohly trochu osvětlit problematiku používání Mavenu. Doufejme, že se mi mé plány podaří vyplnit.</p>
<p><strong>Užitečné odkazy</strong></p>
<ul>
<li>Našel jsem odkaz na elektronickou knihu <a target="_blank" href="http://www.mergere.com/m2book_download.jsp">Better builds with Maven</a> zdarma ke stažení. Prozatím jsem ještě neměl čas se na ni podívat, ale třebas to někomu pomůže.</li>
<li>Vhodné nástroje pro vyhledávání knihoven pro Maven 2 jsou vyhledávací stroje např.: <a target="_blank" href="http://mvnrepository.com/">http://mvnrepository.com/</a> nebo <a target="_blank" href="http://maven.ozacc.com/">http://maven.ozacc.com/</a>. S nimi najdete cesty k požadovaným jarům snáze.</li>
<li>Při vytváření vlastní firemní remote repository doporučuji se zamyslet nad nasazením <a target="_blank" href="http://maven-proxy.codehaus.org/">Maven proxy od Codehaus</a>, která zajistí, že vývojáři si nebudou muset konfigurovat více remote repository, ale jen tu vaši firemní. Tam na jednom místě nakonfigurujete odkazy na další remote repository, které chcete prohledávat a dotazy na knihovny, které dosud ve své firemní repository nemáte se přesměrují ven a chybějící knihovny se vám dostáhnou aniž by to klient (tzn. programátor při buildování) zjistil (snad až na trochu delší response time).</li>
</ul>
