---
status: publish
published: true
title: Mock testing - Potěmkinovy vesnice
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Řada z vás možná už na výraz Mock testing narazila, někteří ne. Pro ty z
  vás, kteří Mock přístup v testování nepoužili je tento článek. Pro ostatní může
  být zajímavá ukázka této techniky na knihovně EasyMock.\r\n<ul>\r\n\t<li><strong>Co
  jsou to mock objekty?</strong></li>\r\n</ul>\r\nJedná se vlastně o techniku psaní
  určitého druhu automatických testů. V podstatě se jedná o nahrazení reálného objektu
  testovací fasádou, která neprovádí žádnou funkcionalitu nahrazovaného objektu -
  jen se jako tento objekt tváří. Místo původní logiky objektu je vloženo chování,
  které ve svém testu potřebujete.\r\n\r\nNejlepší bude teorii provázat s praxí. Pokud
  píšete automatické testy, jistě jste narazili na situaci, kdy k napsání jednoduchého
  testu musíte velmi složitě a pracně připravovat okolní podmínky. Např. testujete
  metodu v business objektu, který se dotazuje interně DAO objektů na data v databázi.
  To ale znamená, že před tím, než začnete testovat logiku tohoto business objektu,
  musíte připravit správná data v databázi. Musíte také zajistit, že se tam omylem
  nedostanou další data, která by test zhatila (např. v SELECT dotazu vrátila více
  řádků) a tudíž obvykle zase musíte po sobě uklízet. Ošetření okolních podmínek spuštění
  testu vás nakonec může stát několkrát více času, než potřebujete k napsaní vlastní
  testovací logiky.\r\nExistují různé techniky, jak toto zajistit - setkal jsem se
  např. s použitím HSQL databáze, která byla celá v paměti a po každém testu se kompletně
  dropla a před novým opět vytvořila a dosadila se příslušná testovací data (tím,
  že se vše odehrávalo pouze v paměti byly testy velmi rychlé). Ovšem lehčí je dle
  mého názoru právě použít techniku mock objektů.\r\n\r\nPři použití této techniky
  se soustředíte na testování pouze logiky business objektu a předpokládáte že okolní
  objekty fungují správně tak jak mají. Potom v našem příkladě za DAO objekty dosadíte
  pouze \"prázdné\" ulity, které mají stejné rozhraní, ale místo vlastní logiky obsahují
  logiku takovou, kterou potřebujete pro vlastní test. Tzn. ve chvíli, kdy se business
  objekt zeptá DAO na konkrétní data, neproběhne dotaz do databáze, ale vy mu rovnou
  vrátíte data, která v daném testu potřebujete.\r\n\r\nTo je celý princip mock objektů.
  Nic víc, nic míň. Pokud se chcete dozvědět něco víc, pokračujte ve čtení.\r\n\r\n"
wordpress_id: 6
wordpress_url: http://blog.novoj.net/2007/01/19/mock-testing-potemkinovy-vesnice/
date: '2007-01-19 07:22:25 +0100'
date_gmt: '2007-01-19 06:22:25 +0100'
categories:
- Java
- Testování
tags: []
comments:
- id: 4
  author: komofei
  author_email: komornik@linux.sk
  author_url: ''
  date: '2007-01-22 15:14:44 +0100'
  date_gmt: '2007-01-22 14:14:44 +0100'
  content: "Velmi pekny clanok. \r\nAle mam problem s pochopenim testu c. 2. Ako to
    dopadne pri verify() ? Zliha to,a lebo je to OK ?  Nepochopil som presne ako sa
    zachova konstrukcia: expectLastCall().andThrow(new SenderException) . Vysvetli
    mi to niekto? Vdaka."
- id: 5
  author: Novoj
  author_email: novotnaci@megasphera.cz
  author_url: http://blog.novoj.net
  date: '2007-01-22 17:12:53 +0100'
  date_gmt: '2007-01-22 16:12:53 +0100'
  content: "Všechny testy ve zdrojových kódech projdou bez chyby. V metodě verify
    se skutečně ověřuje pouze to, co jsem uvedl v bodě #6. Konstrukce \"expectLastCall().andThrow(new
    SenderException())\" říká přesně toto. Výsledek posledního instruovaného volání
    (což je v našem případě #4) bude exception, která je uvedená v parametru.\r\n\r\nTzn.
    když je zavolána objektem tested metoda performBusinessLogic (#8) a ten uvnitř
    svého vykonávání zavolá na messageMocku metodu send, EasyMock místo \"simulace\"
    vykonání vyhodí exception SenderException.\r\n\r\nObdobně by se dal mock instruovat
    k vrácení návratové hodnoty (pokud by metoda send měla nějakou návratovou hodnotu,
    jako že v našem ukázkovém příkladě nemá) deklarací (uvažujme boolean):\r\n\r\nexpectLastCall().andReturn(Boolean.TRUE)\r\n\r\nPokud
    by stále byly nějaké pochybnosti, doporučuji stáhnout si přiložený projekt a celé
    si to oddebugovat. Tam nejlépe poznáte, co se kdy jak volá a s jakými výsledky.\r\n\r\nA
    propo. Děkuji za kladnou reakci - taková věc člověka vždycky potěší."
- id: 6
  author: Satai
  author_email: ondra@nekola.cz
  author_url: http://www.nekola.cz/
  date: '2007-01-22 19:56:05 +0100'
  date_gmt: '2007-01-22 18:56:05 +0100'
  content: "Ajaj, také jsem se chystal napsat něco o EasyMock. Objevil jsem je před
    nedávnem a dost mi zjednodušily život.\r\nVětšinou testuji stav, ale někdy je
    opravdu lepší testovat procesy a na to je EasyMock jako dělaný. Našel jsem i další
    knihovny jako je JMock, ale přišly mi příliš komplexní pro 95% použití. A určitě
    musím pochválit EasyMock za žikovné použití Javy5 v v nových versích knihovny."
- id: 7
  author: Jsem Šedý &raquo; Blog Archive &raquo; Mock testing - Potěmkinovy vesnice
  author_email: ''
  author_url: http://www.nekola.cz/satai/technologie/it/programovani/java/2007/01/22/mock-testing-potemkinovy-vesnice/
  date: '2007-01-22 20:21:10 +0100'
  date_gmt: '2007-01-22 19:21:10 +0100'
  content: "[...] Před pár týdny jsem objevil skvělou knihovnu EasyMock. Chystal jsem
    se o ní něco málo blognout, ale Otec Fura mne předběhnul. Rozhodně si jeho post
    přečtěte. Nazajde moc do hloubky, ale na první dojem to stačí. [...]"
- id: 9
  author: Andrej
  author_email: huhu@huhu.hu
  author_url: ''
  date: '2007-01-24 15:28:58 +0100'
  date_gmt: '2007-01-24 14:28:58 +0100'
  content: zdrojaky ako png - to je pomerne velka vzacnost!
- id: 10
  author: Novoj
  author_email: novotnaci@megasphera.cz
  author_url: http://blog.novoj.net
  date: '2007-01-24 15:53:25 +0100'
  date_gmt: '2007-01-24 14:53:25 +0100'
  content: ":) výsledek je lepší než jako zdroják vložený textově. Zkoušel jsem to.\r\n\r\nNicméně
    kompletní zdrojáky je možné si stáhnout jako ZIPko, takže pokud máte zájem o detaily,
    originály jsou k dispozici."
- id: 11
  author: Old ShatterKuna
  author_email: radiq@centrum.cz
  author_url: ''
  date: '2007-01-25 10:19:51 +0100'
  date_gmt: '2007-01-25 09:19:51 +0100'
  content: Moc ty mock objekty nechápu. Teď mám nějaké automatické testy, které dynamicky
    vytvoří SQL dotaz a vyberou něco z databáze. Já pak potřebuju zjistit, jestli
    ten SELECT něco vrací nebo ne. Těchto testů probíhá za sebou několik a vždy se
    hrabe do databáze a tahá to data, což dělá testy poněkud zdlouhavými, protože
    je tam hodně záznamů. Dá se pro tento problém použít nějaký mock objekt, který
    dobu provádění zkrátí? Já si teda myslím, že ne, protože zde se jedná o kontrolu
    dat a ne o kontrolu přístupu k databázi. Mám pravdu?
- id: 12
  author: Novoj
  author_email: novotnaci@megasphera.cz
  author_url: http://blog.novoj.net
  date: '2007-01-25 10:33:26 +0100'
  date_gmt: '2007-01-25 09:33:26 +0100'
  content: "Mock objekty se typicky nehodí na testování \"datové vrstvy\" - tzn. pokud
    potřebujete testovat, zda jste složil správně SQL dotaz, tak v takovém případě
    vám nezbyde než se skutečně dotázat databáze a počkat si na reálné výsledky. S
    tím souvisí i nutná příprava testovacích dat.\r\n\r\nMock objekty se hodí na testování
    aplikační vrstvy (viz. příklad s business objektem). Vrstva obsahující aplikační
    logiku obvykle pracuje s datovou vrstvou, ze které získává data pro své operace.
    Za předpokladu, že máme již datovou vrstvu otestovanou a funkční - můžeme si ušetřit
    práci při testování aplikační vrstvy použitím mocků.\r\n\r\nA) původní přístup:\r\nchci
    testovat aplikační objekt, ten se dotazuje datové vrstvy -> před vlastním testem
    musím naplnit data v databázi, tak aby, když se aplikační objekt zeptá datového,
    vrátily správná data. Je to dost práce, ale testuju tím vlastně najednou několik
    věcí (integrační test): vlastní aplikační objekt, objekty datové vrstvy, spolupráci
    aplikačního objektu s datovou vrstvou\r\n\r\nB) přístup s mocky:\r\nchci testovat
    aplikační objekt, ten se dotazuje datové vrstvy -> v testu si vytvořím virtuální
    mock objekty datové vrstvy a nainstruuji jim jejich chování - tzn. řeknu jim,
    že až se jich aplikační objekt zeptá, mají vrátit konkrétní testová data. Žádné
    dotazy do databáze neproběhnou. Výsledkem je daleko méně práce při psaní testů
    a izolovaný (unit) test, při kterém testuji jen a jen aplikační objekt. Samozřejmě
    musím někde jinde otestovat zvlášť datovou vrstvu, abych zamezil chybám na tomto
    místě. Myšlenkou je, že i když budu izolovaně psát testy na více objektů (zvlášt
    aplikační a zvlášt datová vrstvaj), zabere mi to méně práce a bude to lépe otestované,
    než kdybych se pokoušel psát pouze integrační (složité) testy. V unit testech
    mám totiž větší možnosti jak otestovat i různé niance daného volání, což bych
    při volání ob jeden objekt obtížně testoval."
- id: 4077
  author: Tomas Jurman
  author_email: tomasjurman@gmail.com
  author_url: ''
  date: '2008-10-24 20:35:50 +0200'
  date_gmt: '2008-10-24 19:35:50 +0200'
  content: Díky moc za super článek.
- id: 4854
  author: bjbj
  author_email: jiri.billig@volny.cz
  author_url: ''
  date: '2008-11-19 00:26:25 +0100'
  date_gmt: '2008-11-18 23:26:25 +0100'
  content: Test č. 1 chápu - je jasný a srozumitelný. V podstatě testujeme if příkaz
    ve výkonné metodě business objektu. Ale test č. 2 nechápu - jak autor článku správně
    píše, je to simulace, ne test. Kdy ho tedy spouštět ? Když nepojede internet a
    spustění business classy naostro by tedy způsobilo logování, pustíme místo toho
    simulaci (test č. 2) s tím, že předpokládáme, že se spůstí logování a v tomto
    případě prohlásíme test za úspěšný ? V takovém případě ale test sám o sobě závisí
    ještě na okolním prostředí (stavu internetu) a sám se nemůže vyhodnotit jako úspěšný
    nebo neúspěšný - nebo je to úplně jinak ???
- id: 4867
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2008-11-19 08:42:51 +0100'
  date_gmt: '2008-11-19 07:42:51 +0100'
  content: "No - nevím jestli jsem pochopil dotaz správně. Tento článek rozebírá automatické
    testování aplikace, které se provádí v průběhu vývoje aplikace. S vlastním produkčním
    během nemá nic společného.\r\n\r\nJde nám o to, abychom si při vývoji ověřili,
    jak se bude chovat naše aplikace (v tomto příkladě konkrétně business objekt)
    chovat v konkrétních situacích. Otestovat si chování business objektu tak, že
    si lokálně aplikaci spustíme a vytáhneme drát ze zdi není ideální způsob testování
    ze dvou důvodů:\r\n\r\n- existují situace, kdy danou situaci z její podstaty nemůžeme
    reálně na vývojovém prostředí vůbec navodit\r\n- takový test musíme provádět ručně
    - nám jde ale o to aby ani při dalších změnách v aplikaci nemohlo dojít k zanesení
    nějaké chyby, která by měnila chování naší aplikace v dané situaci\r\n\r\nProto
    používáme automatické testy, které pouštíme jak lokálně při vývoji aplikace, tak
    ideálně i na nějakém integračním serveru, který je společný pro celý tým. S vlastním
    produkčním během aplikace nemají testy \"vůbec nic společného\", krom toho, že
    výrazně zvýší její kvalitu (a to tím, že jsme si mohli ještě před nasazením plno
    situací, které mohou potenciálně nastat, vyzkoušet).\r\n\r\nTzn. v druhém testu
    nám skutečně stačí ověřit to, že při potenciálním výpadku internetu by se aplikace
    zachovala tak, že by chybu jednoduše zalogovala a vyjímku by \"spolkla\". Test
    je pro nás úspěšný, protože se v dané situaci chová tak jak jsme chtěli (v reálném
    případě bychom mohli chtít dělat něco jiného, než jen chybu zalogovat, ale pro
    účely příkladu nám toto zjednodušené chování postačuje). \r\n\r\nDoufám, že jsem
    tímto aspoň trochu odpověděl na poslední dotaz?!"
- id: 153711
  author: Testování Java aplikací at blog glog blopt
  author_email: ''
  author_url: http://blog.janbouchner.cz/?p=407
  date: '2014-10-28 13:17:34 +0100'
  date_gmt: '2014-10-28 12:17:34 +0100'
  content: "[&#8230;] http://blog.novoj.net/2007/01/19/mock-testing-potemkinovy-vesnice/
    [&#8230;]"
---
<p>Řada z vás možná už na výraz Mock testing narazila, někteří ne. Pro ty z vás, kteří Mock přístup v testování nepoužili je tento článek. Pro ostatní může být zajímavá ukázka této techniky na knihovně EasyMock.</p>
<ul>
<li><strong>Co jsou to mock objekty?</strong></li>
</ul>
<p>Jedná se vlastně o techniku psaní určitého druhu automatických testů. V podstatě se jedná o nahrazení reálného objektu testovací fasádou, která neprovádí žádnou funkcionalitu nahrazovaného objektu - jen se jako tento objekt tváří. Místo původní logiky objektu je vloženo chování, které ve svém testu potřebujete.</p>
<p>Nejlepší bude teorii provázat s praxí. Pokud píšete automatické testy, jistě jste narazili na situaci, kdy k napsání jednoduchého testu musíte velmi složitě a pracně připravovat okolní podmínky. Např. testujete metodu v business objektu, který se dotazuje interně DAO objektů na data v databázi. To ale znamená, že před tím, než začnete testovat logiku tohoto business objektu, musíte připravit správná data v databázi. Musíte také zajistit, že se tam omylem nedostanou další data, která by test zhatila (např. v SELECT dotazu vrátila více řádků) a tudíž obvykle zase musíte po sobě uklízet. Ošetření okolních podmínek spuštění testu vás nakonec může stát několkrát více času, než potřebujete k napsaní vlastní testovací logiky.<br />
Existují různé techniky, jak toto zajistit - setkal jsem se např. s použitím HSQL databáze, která byla celá v paměti a po každém testu se kompletně dropla a před novým opět vytvořila a dosadila se příslušná testovací data (tím, že se vše odehrávalo pouze v paměti byly testy velmi rychlé). Ovšem lehčí je dle mého názoru právě použít techniku mock objektů.</p>
<p>Při použití této techniky se soustředíte na testování pouze logiky business objektu a předpokládáte že okolní objekty fungují správně tak jak mají. Potom v našem příkladě za DAO objekty dosadíte pouze "prázdné" ulity, které mají stejné rozhraní, ale místo vlastní logiky obsahují logiku takovou, kterou potřebujete pro vlastní test. Tzn. ve chvíli, kdy se business objekt zeptá DAO na konkrétní data, neproběhne dotaz do databáze, ale vy mu rovnou vrátíte data, která v daném testu potřebujete.</p>
<p>To je celý princip mock objektů. Nic víc, nic míň. Pokud se chcete dozvědět něco víc, pokračujte ve čtení.</p>
<p><a id="more"></a><a id="more-6"></a></p>
<ul>
<li><strong>Stub objekty a Mock objekty</strong></li>
</ul>
<p>Pokud chcete použít tuto techniku při testování, potřebujete vyřešit dva problémy:</p>
<ol>
<li><em>možnost nastavit testovanému objektu mock objekt zvenčí - princip IoC</em><br />
V podstatě to znamená, abyste mohli nahradit původní reálný objekt náhražkou např. přes setter metodu, konstruktor nebo jako parametr testované metody. Velmi prosté, ale v některých případech, kdy nemáte pod kontrolou API testovaného objektu, to vylučuje samotné použití této techniky.</li>
<li><em>možnost nahradit originální logiku nahrazovaného objektů testovací logikou - princip OOP</em><br />
Tzn. testovaný objekt nesmí poznat, že pracuje s náhražkou. Musí být zachováno rozhraní původního objektu a objekty musí být typově stejné.<br />
To se dá v Javě udělat jen dvěma způsoby: děděním nebo implementací interface. Vytvářet mocky děděním bych nedoporučoval, jelikož potom máte v mock objektu fragmenty původní logiky, což vám to může mnohokrát akorát celé zamotat. Ideální je tedy nadefinovat rozhraní, se kterým testovaný objekt pracuje a dané rozhraní je implementováno dvěmi třídami - tou reálnou a falešnou "mock" implementací. Je to trochu pracnější způsob, ale čistší.</li>
</ol>
<p>Ve vlastním testu potom jednoduše vytvoříte testovaný objekt, nastavíte mu místo původní reálné implementace testovací náhražku a zajistíte, aby ta vracela data, která ve svém testu požadujete.</p>
<p>Můžete se vydat cestou tzv. stub objektů - což znamená že vytvoříte fyzicky třídy, které obsahují logiku, kterou od nich požadujete v testech. Je to asi jednodušší cesta pro někoho, kdo s tímto způsobem testů ještě nepřišel do styku, ale cesta dosti pracná.</p>
<p>Dalším vývojovým stupněm jsou tzv. mock objekty. Jejich použití je možná obtížnější, zato přinášejí jednu zásadní výhodu. Dynamické mock objekty jsou vytvářeny přímo testem a existují pouze virtuálně. Tzn. není třeba fyzicky implementovat vlastní mock třídu a navíc vám zdarma poskytnou řadu funkcionality, kterou byste do svých stub objektů pracně implementovali. Příklad použití mock objektů si ukážeme na použití knihovny EasyMock.</p>
<ul>
<li><strong>EasyMock knihovna a vytvoření jednoduchého testu s použitím mock objektu</strong></li>
</ul>
<p>Dejme  tomu, že máme tento business objekt, který chceme testovat.</p>
<p><a title="Klikněte pro zvětšení" href="http://files.novoj.net/EasyMockTesting/BusinessObject.png"><img align="middle" title="BusinessObject zdrojový kód" alt="BusinessObject zdrojový kód" src="http://files.novoj.net/EasyMockTesting/BusinessObject.png" /></a></p>
<p>Ten používá ke své činnosti dvě rozhraní - IMessageSender a ILogger. Vlastní logika business objektu je velmi prostá, pokud dojde číslo menší jak 10, pošle email příjemci jedna. Pokud je číslo větší, pošle mail příjemci dva. Pokud se nepodaří odeslat email, tuto chybu zaloguje. Uvedená dvě rozhraní jsou zobrazena níže.</p>
<p><a href="http://files.novoj.net/EasyMockTesting/IMessageSender.png"><img align="middle" alt="IMessageSender - zdrojový kód" title="IMessageSender - zdrojový kód" src="http://files.novoj.net/EasyMockTesting/IMessageSender.png" /></a></p>
<p><a href="http://files.novoj.net/EasyMockTesting/IMessageSender.png"><img align="middle" alt="ILogger zdrojový kód" title="ILogger zdrojový kód" src="http://files.novoj.net/EasyMockTesting/ILogger.png" /></a></p>
<p>Výše uvedenou logiku bychom normálně obtížně testovali, ale s použitím mock objektů to bude triviálně jednoduché. Kompletní zdrojové kódy jako Maven 2 projekt naleznete na konci článku. V něm je implementace testů jak pomocí Mock, tak i Stub objektů. Nuže, jak vypadá testování s knihovnou EasyMock?</p>
<p><em>Test první:</em></p>
<p>V prvním testu chceme otestovat, že pokud je vstupní hodnota 1 odešle se email prvnímu příjemci a zároveň se nezaloguje žádná chyba (odeslání se podaří).</p>
<p><a href="http://files.novoj.net/EasyMockTesting/Test1.png"><img align="middle" alt="Test1 zdrojový kód" title="Test1 zdrojový kód" src="http://files.novoj.net/EasyMockTesting/Test1.png" /></a></p>
<p>Ve výše uvedeném kódu je několik zajímavých míst.</p>
<p><strong>#1</strong> - zde se vytváří virtuální mock objekt implementující specifikované rozhraní; fakticky zde v tuto chvíli knihovna EasyMock vytvoří novou třídu implementující vaše rozhraní a instanciuje objekt této virtuální třídy;</p>
<p><strong>#2</strong> - zde zavoláme metodu našeho rozhraní stejně, jako bychom to udělali s reálným objektem; v tomto případě, však pouze instruujeme mock objekt, že má očekávat (po odstartování skutečného testu - viz. bod #3) volání metody send s uvedenými parametry</p>
<p><strong>#3</strong> - zde řekneme knihovně EasyMock: až do tohoto bodu jsme programovali tvé chování pro daný test; od této chvíle se chovej dle našich instrukcí (viz. bod #2)</p>
<p><strong>#4</strong> - nastavíme mock objekty do testovaného objektu - tzn. místo původních reálných implementací mu podstrčíme kukaččí vejce v podobě našich mock objektů</p>
<p><strong>#5</strong> - zavoláme testovanou metodu business objektu - ta proběhne standardním způsobem a business objekt při svém chodu zavolá metodu rozhraní IMessageSender na našem mock objektu - volání proběhne bez problémů, tudíž si business objekt myslí, že vše proběhlo v pořádku (náš mock objekt se tvářil jako reálný objekt)</p>
<p><strong>#6</strong> - verifikace mock objektů - toto je hlavní pasáž mock testování; zde EasyMock prověří, zda celá akce proběhla tak, jak jste ho před replay fází naučili; tzn. ověří, že mezi replay a verify došlo k jednomu volání metody send na messageMock objektu a že vstupní parametry odpovídaly (equals) vámi definovaným hodnotám z bodu #2; pokud by k volání nedošlo, nebo došlo vícekrát, či některá z hodnot se lišila od vámi specifikovaných, dojde zde k vyjímce a celý test selže; taktéž si povšimněte že součástí verify je i loggerMock objekt, u kterého jsme neprováděli žádnou "instruktáž" - v takovém případě ve fázi verify ověří EasyMock knihovna, že nebyla zavolána žádná metoda tohoto rozhraní (což je dobře, protože v takovém případě by se business objekt zachoval špatně)</p>
<p><em>Test druhý:</em></p>
<p>V druhém testu chceme simulovat chybu odeslání zprávy. Objekt implementující IMessageSender rozhraní by v metodě send měl vyvolat chybu SendException. Business objekt by na to měl reagovat zalogováním chyby rozhraním ILogger.</p>
<p><a href="http://files.novoj.net/EasyMockTesting/Test2.png"><img align="middle" title="Test2 zdrojový kód" alt="Test2 zdrojový kód" src="http://files.novoj.net/EasyMockTesting/Test2.png" /></a></p>
<p><strong>#1</strong> - vytvoříme business objekt</p>
<p><strong>#2</strong> - opět vytvoříme virtuální mock objekty</p>
<p><strong>#3</strong> - nyní instruujeme EasyMock, že má očekávat volání metody logError na objektu loggerMock - přičemž první parametr musí být ne null objekt (String) a druhým parametrem má být objekt přetypovatelný na třídu SendException (v této části vidíte, že argumenty nemusíte uvádět exaktně přesně - EasyMock poskytuje abstraktnější výrazové prostředky)</p>
<p><strong>#4</strong> - zde instruujeme EasyMock, že má očekávat volání metody send na objektu messageMock s konkrétními vstupními hodnotami (obdobně jako v testu 1)</p>
<p><strong>#5</strong> - zde je další novinka, zde říkáme EasyMocku aby v posledním volání (viz. bod #4) vyhodil jako výsledek volání exception SendException (obdobně bychom mohli EasyMocku říct, aby poslední volání vrátilo konkrétní návratovou hodnotu záměnou andThrow voláním metody andReturn)</p>
<p><strong>#6</strong> - nyní řekneme knihovně EasyMock: až do tohoto bodu jsme programovali tvé chování pro daný test; od této chvíle se chovej dle našich instrukcí<br />
<strong>#7</strong> - nastavíme mock objekty do testovaného objektu - tzn. místo původních reálných implementací mu podstrčíme kukaččí vejce v podobě našich mock objektů</p>
<p><strong>#8</strong> - zavoláme testovanou metodu business objektu - ta proběhne standardním způsobem a business objekt při svém chodu zavolá metodu rozhraní IMessageSender na našem mock objektu - při volání metody send náš mock vyhodí SendException a náš business objekt by se měl patřičně zareagovat zalogováním chyby</p>
<p><strong>#9</strong> - verifikace mock objektů - EasyMock ověří, zda na messageMock objektu byla zavolána právě jednou metoda send a parametry volání odpovídaly (equals) předpisu z kroku #4; dále ověří, že na objektu loggerMock byla právě jednou zavolána metoda logError s prvním ne nullovým parametrem a druhým parametrem přetypovatelným na SendException</p>
<ul>
<li><strong>Další možnosti knihovny EasyMock</strong></li>
</ul>
<p>Výše uvedené příklady prezentují pouze základní a jednoduché možnosti knihovny EasyMock. V druhé verzi má již poměrně rozsáhlé možnosti "imitace" a ověřování požadovaného chování. Například umožňuje parametry porovnávat ne jen na ekvalitu, ale má řadu výrazových prostředků z nichž jsme uvedli pouze dva (např. je / není null, test na regulární výraz, aritmetické operátory >,<,= nebo spojování podmínek přes logické operátory and, or). Počet volání metod lze definovat přesně (např. právě jedno jako v našich testech) nebo v určitém limitu - alespoň jednou, od - do, libovolně. Umožňuje ověřovat pořadí volání konkrétních metod a naopak. Dokáže vytvořit mock objekty v různých režimech - strict mock (očekává volání jen vámi předepsaných metod - jinak generuje UnexpectedCallException), nice mock (umožňuje libovolné volání metod na tomto objektu - u neinstruovaných metod vrací "výchozí" hodnoty - null, 0 nebo false).</p>
<p>V druhé verzi je také novinkou Class Extension knihovna, která vám umožňuje generovat mock objekty nikoliv pouze na základě rozhraní, ale i na základě normálních tříd (tzn. není potřeba mít definovaný interface). Tento způsob vám také umožní nechat některé implementace metod mock objektů nepřekryté knihovnou EasyMock - tzn. budou obsahovat původní logiku reálné třídy.</p>
<ul>
<li><strong>Pozitivní dopady mock testování</strong></li>
</ul>
<p>Testy jsou poměrně velmi přehledné, jednoduše se píšou a ušetří vám plno práce s nastavováním prostředí pro test. Navíc  vám umožní testovat funkcionalitu, která je jen velmi obtížně testovatelná (např. že váš skript odešle v určitou chvíli email).</p>
<ul>
<li><strong>Negativní dopady mock testování</strong></li>
</ul>
<p>Je potřeba si uvědomit, že objekty, které nahrazujete se vlastně netestují. Použití mock objektů vám umožňuje vytváření izolovaných unit testů - ty jsou sice jednodušší a přehlednější, ale nemají takovou cenu pro vlastní testování jako testy integrační. Integrační testy vám pomohou objevit chyby na úrovni rozhraní různých komponent - tzn. ne pouze, komponenta A se chová tak jak má, ale že komponenta B používá komponentu A jak má. Ve výsledku totiž uživatel aplikace nepracuje pouze s komponentami jednotlivě, ale s celým systémem komponent a chyba komunikace mezi komponentami je pro něj úplně stejná jako chyba jedné konkrétní komponenty. Prostě to nefunguje.</p>
<ul>
<li><strong>Zdroje</strong></li>
</ul>
<p><a target="_blank" href="http://files.novoj.net/EasyMockTesting/EasyMockTest.zip">Zdrojové kódy příkladu ke stažení jako projekt Maven 2<br />
</a></p>
<p><a target="_blank" href="http://www.mockobjects.com/">Mock Objects</a> - úvod do techniky mockování<br />
<a target="_blank" href="http://www.easymock.org/">EasyMock</a> - knihovna pro podporu dynamických mock objektů (viz. příklady v článku)<br />
<a target="_blank" href="http://www.jmock.org/">jMock</a> - alternativa k EasyMock, abyste si mohli vybrat ;)</p>
