---
status: publish
published: true
title: Prolomení šifrovaného protokolu HTTPS
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft wp-image-3266\" src=\"http://blog.novoj.net/binary/2017/01/prolomeni-sifrovaneho-protokolu-https-e1485882377456-300x274.jpg\"
  alt=\"\" width=\"166\" height=\"171\" />Vyděsil vás titulek článku? Vlastně to bylo
  tak trochu cílem. Mnoho z nás totiž žije v klamné představě, že nasazení důvěryhodného
  SSL certifikátu a správná konfigurace webového serveru postačuje k zajištění důvěryhodného
  a nečitelného přenosu dat mezi serverem a klientem. Naše přesvědčení potvrzuje fakt,
  že na tomto předpokladu staví celý svět online byznysu.\r\n\r\n"
wordpress_id: 3264
wordpress_url: http://blog.novoj.net/?p=3264
date: '2017-01-31 18:03:45 +0100'
date_gmt: '2017-01-31 17:03:45 +0100'
categories:
- Programování
- Bezpečnost
tags: []
comments:
- id: 158542
  author: Filip Jirsák
  author_email: filip.jirsak@gmail.com
  author_url: https://plus.google.com/+FilipJirsák-CZ
  date: '2017-02-04 20:28:30 +0100'
  date_gmt: '2017-02-04 19:28:30 +0100'
  content: Asi jsem nepochopil, jak chcete pracovat s tím CSRF zamaskovaným XORem.
    Když mám konstantní CSRF=abc, salt=def a abc XOR def dává 753, pak také def XOR
    753 dává abc. Útočník zná def i 753, může tedy vypočítat abc – a pak si může vymyslet
    vlastní salt a vypočítat požadovanou hodnotu. Abych tomu zabránil, musel bych
    si pamatovat, ke které stránce patří který salt, ale to už to můžu rovnou použít
    jako CSRF.
- id: 158543
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2017-02-05 11:42:05 +0100'
  date_gmt: '2017-02-05 10:42:05 +0100'
  content: "To už je třetí reakce v podobném duchu (na různých portálech) - tak jsem
    to asi nevysvětlil dostatečně srozumitelně. XOR v tomto případě neslouží jako
    šifra - to by byl samozřejmě VELKÝ nesmysl. XOR zde slouží jen k tomu, aby se
    hodnota CSRF v response zamaskovala.\r\n\r\nCelý útok spočívá v tom, že útočník
    sleduje side channel, kterým si odvozuje, jak daleko se trefil do nějakého řetězce,
    který je ve výstupu stránky. \r\n\r\nÚtočník nemůže přímo přečíst obsah CSRF kvůli
    Cross-origin politice browseru, nemůže ani použít ani MITM útok, protože je použito
    HTTPS. Nicméně díky kompresi může zjistit, nakolik trefil shodný řetězec z toho,
    jak rychle se mu vrátí odezva serveru (tzn. jestli se vešel nebo nevešel do X
    TCP packetů).\r\n\r\nTj. když bude zkoušet hádat CSRF token, který je obalen v:\r\n\r\n&lt;input
    type=\"hidden\" name=\"_csrf\" value=\"ABC\"/&gt;\r\n\r\nTak si nejdřív zjistí,
    kolik musí poslat znaků, aby zarovnal odezvu na hranici X TCP packetů a potom
    bude zkoušet:\r\n\r\n&lt;input type=\"hidden\" name=\"_csrf\" value=\"A ... trefa,
    vešel se do X packetů\r\n&lt;input type=\"hidden\" name=\"_csrf\" value=\"AA ...
    netrefa, nevešel se do X packetů\r\n&lt;input type=\"hidden\" name=\"_csrf\" value=\"AB
    ... trefa, vešel se do X packetů\r\n&lt;input type=\"hidden\" name=\"_csrf\" value=\"ABA
    ... netrefa, nevešel se do X packetů\r\n&lt;input type=\"hidden\" name=\"_csrf\"
    value=\"ABB ... netrefa, nevešel se do X packetů\r\n&lt;input type=\"hidden\"
    name=\"_csrf\" value=\"ABC ... trefa, vešel se do X packetů\r\n\r\nA to tak dlouho,
    až získá celý CSRF token.\r\n\r\nPokud ale na serveru zamaskujeme CSRF token náhodným
    saltem přes XOR, tak výstup bude při shodném CSRF tokenu v každém výstupu vždy
    odlišný, takže útočník bude mít smůlu.\r\n\r\nTento přístup nám navíc nijak nezkomplikuje
    práci na serveru - i když díky partial update obnově obsahu stránek dostaneme
    v rámci requestu nějaký starší zašifrovaný token, dokážeme původní CSRF snadno
    rekontruovat, protože v tokenu jde i původní varianta saltu.\r\n\r\nJe to takto
    už srozumitelnější?!"
- id: 158544
  author: Filip Jirsák
  author_email: filip.jirsak@gmail.com
  author_url: https://plus.google.com/+FilipJirsák-CZ
  date: '2017-02-05 17:08:37 +0100'
  date_gmt: '2017-02-05 16:08:37 +0100'
  content: Jasně, XOR je tam proto, aby byl výstup pokaždé jiný, čímž se prakticky
    znemožní útok přes kompresi. Už to chápu, díky!
- id: 158545
  author: novoj
  author_email: novotnaci@gmail.com
  author_url: ''
  date: '2017-02-06 15:53:47 +0100'
  date_gmt: '2017-02-06 14:53:47 +0100'
  content: Super, to jsem rád. Poučení pro mě, že na srozumitelnosti článků musím
    dále pracovat.
---
<p><img class="alignleft wp-image-3266" src="http://blog.novoj.net/binary/2017/01/prolomeni-sifrovaneho-protokolu-https-e1485882377456-300x274.jpg" alt="" width="166" height="171" />Vyděsil vás titulek článku? Vlastně to bylo tak trochu cílem. Mnoho z nás totiž žije v klamné představě, že nasazení důvěryhodného SSL certifikátu a správná konfigurace webového serveru postačuje k zajištění důvěryhodného a nečitelného přenosu dat mezi serverem a klientem. Naše přesvědčení potvrzuje fakt, že na tomto předpokladu staví celý svět online byznysu.</p>
<p><a id="more"></a><a id="more-3264"></a></p>
<p>Jak by řekli matematici – použití HTTPS protokolu je pro zajištění takové komunikace nutná, nikoliv však postačující podmínka. Díky tomu, že je HTTPS protokol páteří seriózního internetu, je také velmi zajímavý pro útočníky, kteří by jeho prolomením hodně získali.</p>
<p>Předpokládejme nyní, že jste na váš web nasadili SSL/TLS certifikát – třebas i ten zdarma poskytovaný iniciativou <a href="https://letsencrypt.org/">Let’s Encrypt</a>. Svědomitě jste nastavili svůj webový server tak, že si z <a href="https://www.ssllabs.com/ssltest/">SSL testu</a> odnášíte známku ne menší než A+. Vaše stránky tím pádem nastavují i hlavičku <a href="https://cs.wikipedia.org/wiki/HTTP_Strict_Transport_Security">HSTS</a>. Možná jste vaši doménu zavedli i do <a href="https://hstspreload.org/">preload listu</a> prohlížečů, která zajistí, že vaši návštěvníci nepadnou do pasti „man-in-the-middle“ útočníka, který by je o HTTPS protokol připravil.</p>
<p>Zkrátka a prostě,  co se týká ochrany svých zákazníků, jste opravdu pečliví. A teď si představte, že přes to přese všechno existuje způsob, jak se může útočník k obsahu přenášených dat dostat.</p>
<h4>Heist &amp; Breach přichází na scénu</h4>
<p>K citlivým údajům uživatele operujícího na vašem webu se útočník s největší pravděpodobností dostane pomocí kombinace dvou útočných technik zvaných Heist (anglický ekvivalent slova „loupež“”, zveřejněna v srpnu 2016) a Breach (anglický ekvivalent slova „průlom“, zveřejněna v srpnu 2013). A co k tomu potřebuje?</p>
<ul>
<li>Vaši neznalost problému</li>
<li>nasazení <a href="https://cs.wikipedia.org/wiki/Komprese_HTTP">kompresního algoritmu</a> na odpovědi webserveru</li>
<li>stránku zrcadlící hodnotu vstupního parametru, která zároveň obsahuje utajovaný „citlivý údaj“</li>
</ul>
<p>Schválně se zamyslete, jestli náhodou tyto podmínky nesplňujete.</p>
<p>Trochu vám s přemýšlením pomůžeme. Kompresi nejspíš na webserveru nasazenou máte, dělají to tak (téměř) všichni – dost to totiž zrychluje odezvy webu, hlavně na mobilních sítích. Přece jen je rozdíl stahovat 2MB nebo 400kB. Nejspíš budete používat <a href="https://cs.wikipedia.org/wiki/Gzip">gzip</a>, možná <a href="https://cs.wikipedia.org/wiki/SPDY">SPDY</a> nebo novější <a href="https://en.wikipedia.org/wiki/HTTP/2">HTTP/2</a>, koneckonců si to můžete <a href="http://www.whatsmyip.org/http-compression-test/">hned teď ověřit</a>.</p>
<p>Teď potřebujeme na vašem webu najít nějakou stránku, co otiskne do svého těla obsah vstupního parametru, který jí předáme. Velmi vhodnými adepty jsou např. vyhledávací formuláře, které do výstupní stránky typicky napíší, jaký vyhledávaný výraz byl vložený a kolik výsledků mu vyhovuje. Ideální stránky jsou takové, kde parametr dokážeme protlačit GET požadavkem, ale i s POSTem si útočník hravě poradí. Každý větší web má podobných stránek či URL desítky.</p>
<p>A nyní už nám stačí jen najít ty, kde se zároveň nachází nějaký „citlivý údaj“. Asi nejsme tak bláhoví, abychom někde zobrazovali celá čísla platebních karet, ale pro někoho může být citlivým údajem třeba číslo občanského průkazu, rodné číslo nebo jen adresa bydliště.</p>
<p>To, po čem útočník nejspíš půjde, bude tzv. CSRF token, kterým chráníte provedení všech důležitých akcí na vašem webu (pokud ne, zapomeňte na tento článek, protože máte daleko větší problém). Tento token bývá platný pro sezení uživatele a pokud jej útočník získá, může na vašem webu jménem přihlášeného uživatele provádět libovolné akce nechráněné sekundárním ověřením (opětovným zadáním hesla, potvrzením přes SMS či e-mail apod.). Ano mluvíme zde o útoku typu <a href="https://cs.wikipedia.org/wiki/Cross-site_request_forgery">Cross-Site-Request-Forgery</a>, před kterým vás má právě CSRF token chránit.</p>
<h4>Jak bude takový útok vypadat z pohledu uživatele?</h4>
<p>Uživatel vejde na váš web, přihlásí se a následně záložku zavře bez odhlášení, případně  ji nechá otevřenou, ale vedle otevře novou záložku prohlížeče, v níž dál pracuje. Jinými slovy, váš server má pro uživatele stále otevřené sezení, ve kterém je přihlášen.</p>
<p>V jiné záložce samozřejmě prochází další weby a buď rovnou přijde na web útočníka, nebo otevře web, který má ve svém těle vloženou HTML5 reklamu (sic!) z běžného inzertního systému, do něhož útočník vložil vedle oživení reklamy i speciální JavaScriptový kód využívající výše zmíněné techniky útoku.</p>
<p>Jakmile uživatel přijde na web s takto napadenou reklamou, útočný kód v několika vteřinách vyextrahuje cílenými HTTP dotazy na konkrétní stránku vašeho webu citlivý údaj uživatele. Pokud se jedná o CSRF token, provede následně dalšími HTTP požadavky na pozadí aktivní operace ve jménu daného uživatele a to všechno aniž by uživatel  něco tušil.</p>
<p>Jediná věc, která hraje ve váš prospěch, je to, že útok musí být skutečně dobře zacílený na váš web a útočník jej musí velmi dobře znát. Provozovatelé populárních CMS/e-commerce systémů jsou v tomto samozřejmě v nevýhodě, protože čím víc je systém rozšířený, tím je pro útočníky zajímavější.</p>
<h4>Jak je to všechno možné?</h4>
<p>Teď maličko zabředneme do technikálií.</p>
<h4>Breach</h4>
<p><a href="https://raw.github.com/dionyziz/rupture/develop/etc/Black%20Hat%20Asia%202016/asia-16-Practical-New-Developments-In-The-BREACH-Attack-wp.pdf">Breach</a> využívá základního principu fungování kompresních algoritmů, které vyhledávají duplicity v původním obsahu a zjednodušeně je nahrazují „odkazem“ na první výskyt.</p>
<p>Pokud máme řetězec unikátních znaků ABCD, není možné z něj nic odebrat, aniž by došlo ke ztrátě informace. Řetězec ABCDAB je již možné zkrátit o poslední dva znaky nahrazením duplicitního řetězce AB odkazem na první dva znaky textu (tedy na 1CD1, kde 1 zastupuje kombinaci AB).</p>
<p>Pokud nám tedy útočník dokáže vnutit parametr, který server otiskne do výstupní odpovědi dané stránky a čirou náhodou bude obsah tohoto parametru shodný s nějakou jinou částí výstupní stránky (třeba s naším tajemstvím), musí být výsledná délka komprimovaného obsahu stránky o patřičný počet znaků menší.</p>
<p>Pro útočníka je na této technice skvělé to, že se nemusí snažit hádat celé tajemství najednou – to by bylo stále kombinačně příliš náročné (např. už 4 znakové tajemství v Base32 dává něco málo přes milion kombinací). Tento princip totiž funguje už i na jeden jediný znak tajemství, takže nám jej může vykrást postupně po jednom znaku, což je daleko jednoduší (v našem příkladě 4znakového tajemství v Base32 mu bude stačit max. 4×32 = 128 pokusů).</p>
<p>Nevěříte? Tak se koukněte na <a href="https://ruptureit.com/">instruktážní video</a> Athénské univerzity.</p>
<h4>Heist</h4>
<p>Druhým do party je <a href="https://www.blackhat.com/docs/us-16/materials/us-16-VanGoethem-HEIST-HTTP-Encrypted-Information-Can-Be-Stolen-Through-TCP-Windows-wp.pdf">Heist</a>, který umožní útočníkovu JavaScriptu ZMĚŘIT odezvu serveru, na který útočí. Prohlížeč mu samozřejmě neumožní přistoupit k informaci o počtu bajtů komprimované odezvy serveru. Nicméně pomocí <a href="https://developer.mozilla.org/cs/docs/Web/API/Performance">performance API</a> lze zjistit čas mezi prvním a posledním doručeným bajtem odpovědi a při znalosti fungování sítí je z toho možné odvodit, jak byla zakomprimovaná odpověď velká.</p>
<p>Zní to jednoduše, ale je to pokročilá magie, která využívá nízkoúrovňových detailů, jako jsou velikosti TCP oken – jejich pomocí se útočník může dopátrat, jak velké množství výplňového textu je nutné vygenerovat k tomu, aby klient (útočník) donutil server rozdělit odpověď do více TCP oken v případě neduplicitního znaku a méně v případě správně uhodnutého znaku. Časový rozdíl mezi TCP okny je totiž již měřitelný a odlišitelný z pohledu JavaScriptového kódu.</p>
<p>Celá technika je komplexní a hraje v ní roli řada dalších detailů. V nouzi je třeba pomoci si i statistikou, ale vše jsou to pro chytrou hlavu řešitelné věci. Milióny tupějších hlav budou schopny útok využít v podobě zabaleného exploitu.</p>
<h4>Jak se proti tomu lze bránit?</h4>
<p>A jsme u meritu věci. Bránit se tomu nedá, respektive pouze omezeně. Stoprocentní ochrana je prakticky nepoužitelná. Co radí objevitelé Breach útoku?</p>
<ul>
<li>Vypnout HTTP kompresi – to nechcete.</li>
<li>Oddělit chráněné informace od reflektovaných vstupů – to se dělá dost obtížně, např. CSRF token dost úzce souvisí s parametry odesílanými uživatelem.</li>
<li>Zajistit náhodný obsah chráněných informace v každé odpovědi – nepoužitelné např. u čísla občanského průkazu – nebo jej maskovat další šifrou.</li>
<li>Přidávat ke každé odpovědi náhodný počet náhodných znaků – jenže druhým dechem autoři dodávají, že to útočníka pouze trochu zdrží, ale stejně mu nezabrání citlivá data nakonec získat.</li>
<li>Omezit počet požadavků klienta – opět to útočníka jen zdrží, ale nezastaví.</li>
</ul>
<p>Ze všech možností připadá v úvahu pouze ta třetí a to jen někde.</p>
<h4>Aspoň trošku…</h4>
<p>Řekněme, že na webu nejsou žádné přímo viditelné citlivé údaje zákazníka, po kterých by útočník mohl bažit. Zbude nám CSRF token, který potřebujeme, abychom mohli uživatele chránit proti CSRF útokům. Tento token naštěstí před výše popsaným útokem ochránit dokážeme.</p>
<p>Pro každý požadavek můžeme generovat unikátní CSRF token. Tento nápad už tu byl, ale bohužel se ukázal jako velmi nepraktický (např. při pohybu v historii prohlížeče zpět nebo při částečných aktualizacích obsahu stránek ajaxem začne pracovat proti nám).</p>
<p>Proto je lepší v každém požadavku zamaskovat CSRF token platný pro celé sezení uživatele jednoduchou XOR šifrou s náhodným saltem, který povede k naprosto rozdílnému obsahu CSRF tokenu pro každou odpověď, ale při zpětném poslání na server budeme schopni z maskované varianty a saltu původní CSRF token zpětně odvodit.</p>
<p>Maskovaný CSRF token bude vypadat takto:</p>
<p>CSRF_TOKEN xor SALT + SALT</p>
<p>Tj. při konstantním CSRF = "abc" a náhodným SALT = "def" a výsledkem XOR operace = "753" do stránky otiskneme "753def". Z tohoto řetězce jsme schopni na straně serveru znovu vypočíst původní CSRF token "abc". V dalším requestu nám vyjde náhodný SALT = "123", což změní XOR na "b9f" a výsledná hodnota potom na "b9f123", ze které ale opět dostaneme jednoduše původní CSRF tokendefdefdefdefdefdef "abc".</p>
<p>Nechce-li se vám to programovat, sáhněte třebas po <a href="https://gist.github.com/novoj/504b3cb80ebc31e31ad58f3892bae4aa">naší Java implementaci</a> výše uvedeného algoritmu. Používáte-li <a href="https://projects.spring.io/spring-security/">Spring Security</a>, počkejte si na verzi 5.x, kde uvedený algoritmus (snad) <a href="https://github.com/spring-projects/spring-security/issues/4001">zaimplementují</a> přímo do této knihovny.</p>
<h4>Nemůže to vyřešit někdo za vás?</h4>
<p>Zatím se neví o ničem, co by bylo možné implementovat do webových serverů nebo prohlížečů a dokázalo efektivně odstínit Heist/Breach útok. IETF právě pracuje na draftu, který by nás mohl definitivně zbavit hrozby CSRF útoků. Draft se jmenuje <a href="https://github.com/mikewest/internetdrafts/tree/master/first-party-cookies">First-Party-Only-Cookies</a> a prozatím je implementován v prohlížečích <a href="http://caniuse.com/#feat=same-site-cookie-attribute">Chrome a Opera</a> (další budou <a href="https://bugzilla.mozilla.org/show_bug.cgi?id=795346">přibývat</a>). Draft počítá s tím, že cookies, které váš web označí příznakem SameSite, nebude prohlížeč posílat ze stránek pocházejících z jiné domény, než pro jaké je cookie platná.</p>
<p>Pokud tedy příznakem SameSite označíte session cookie, budou všechny požadavky z externích stránek na váš web vypadat jako dotazy anonymního uživatele, tj. nebudou sdílet přihlášení uživatele, který má váš web otevřený v jiném tabu, nebo jej opustil neodhlášený. Tím pádem nikdo zvenčí nebude moci zneužít jeho autentizace k nekalým operacím na pozadí.</p>
<h4>Máte z toho těžkou hlavu?</h4>
<p>My taky :-)</p>
<p><em>Článek byl publikován na <a href="https://www.fg.cz/cs/deje-se/prolomeni-sifrovaneho-protokolu-https-10930">firemním webu FG Forrest</a>.</em></p>
