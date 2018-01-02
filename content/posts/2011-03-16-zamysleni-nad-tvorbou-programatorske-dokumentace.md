---
status: publish
published: true
title: Zamyšlení nad tvorbou programátorské dokumentace
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img src=\"http://blog.novoj.net/binary/2011/02/documentation-150x150.jpg\"
  alt=\"\" title=\"Businessman Overwhelmed with Paperwork\" width=\"150\" height=\"150\"
  class=\"alignleft size-thumbnail wp-image-1371\" /> Aktuálně ve <a href=\"http://www.fg.cz\"
  target=\"_blank\">Forrestu</a> revidujeme způsob vytváření dokumentace, nastavení
  standardů a bavíme se o tom, co a jak změnit. \r\n\r\nMotiv je jasný - nejsme spokojeni
  se současným stavem a v některých případech dokonce dost zásadně. Všichni známe
  to staré rčení \"nejlepší dokumentace je zdrojový kód\", které pochází kdoví odkud
  (tipnul bych si, že za ním stojí eXtreme Programming, ale zdroj jsem vážně nenašel)
  - jenže je to omyl. Správná dokumentace může mít dost zásadní vliv na výslednou
  použitelnost / publicitu vašeho produktu / knihovny mezi programátory. \r\n\r\nKvalitní
  (systém) dokumentace má podle mého názoru zásadní pozitivní vliv na rozšíření např.
  <a href=\"http://docs.jquery.com/Main_Page\" target=\"_blank\">jQuery</a> nebo <a
  href=\"http://static.springsource.org/spring/docs/3.1.0.M1/spring-framework-reference/html/\"
  target=\"_blank\">Springu</a>. Naopak negativně se musela dokumentace podepsat na
  adopci <a href=\"http://groovy.codehaus.org/Documentation\" target=\"_blank\">Groovy</a>.
  Přestože se jedná o skvělý jazyk, dokumentace je na tom, co se týká přehlednosti
  a detailnosti, bídně (můj subjektivní dojem).\r\n\r\n"
wordpress_id: 1370
wordpress_url: http://blog.novoj.net/?p=1370
date: '2011-03-16 00:00:46 +0100'
date_gmt: '2011-03-15 23:00:46 +0100'
categories:
- Programování
- Java
tags: []
comments:
- id: 36375
  author: Jakub Vrána
  author_email: jakub@vrana.cz
  author_url: http://php.vrana.cz/
  date: '2011-03-16 09:57:29 +0100'
  date_gmt: '2011-03-16 08:57:29 +0100'
  content: "Výborný přehled. Také se kloním k tomu dokumentovat co nejblíž kódu. A
    ne někde bokem ve Wiki jako to má třeba Nette (a chtělo by se dodat - taky to
    podle toho vypadá).\r\n\r\nS verzováním dokumentace to ale záleží na projektu.
    Např. v oficiálním manuálu PHP jsme taky zvažovali, že dokumentaci rozdělíme podle
    verze PHP, tam by to ale bylo kontraproduktivní, protože jako programátor často
    potřebuji vědět, v kterých všech verzích mi kód bude fungovat. A i když bych třeba
    věděl, že mi projekt poběží na jedné konkrétní verzi PHP, tak ho stejně chci psát
    tak, aby byl dopředně kompatibilní."
- id: 36382
  author: David Skýba
  author_email: david.skyba@centrum.cz
  author_url: ''
  date: '2011-03-16 11:29:13 +0100'
  date_gmt: '2011-03-16 10:29:13 +0100'
  content: |-
    V souvislosti s tematickou dokumentací a tutoriály mi dost pomáhají názory Kathy Sierry (spoluautorka Head First Java a dalších knížek).

    Za přečtení stojí How to get users to RTFM na http://headrush.typepad.com/creating_passionate_users/2006/09/how_to_get_user.html
- id: 36385
  author: Vladka
  author_email: vladkax@volny.cz
  author_url: ''
  date: '2011-03-16 12:03:47 +0100'
  date_gmt: '2011-03-16 11:03:47 +0100'
  content: "Sqelý článek. \r\nPraxe v .NET je však ve spousta firmách tragická. Dokumentaci
    negenerujeme a kvalitní API také neumíme napsat, o to je to horší bez dokumentace.
    \r\nPřitom ja mám takový narcistický sklon si procházet vygenerovanou dokumentaci
    a koukat se jestli je to API dost hezký, intuitivní a popsané. Bohužel tyto mé
    choutky jsou neukojeny a velký podíl na tom má i Microsoft, že dlouho nebyl dostupný
    ekvivalentní nástroj k JAVADOCU.\r\n\r\nA přitom je to přesně jak říkáš, kdo umí
    dokumentovat, tak umí i dobře psát kod."
- id: 36405
  author: Ladislav Thon
  author_email: ladicek@gmail.com
  author_url: ''
  date: '2011-03-16 16:02:34 +0100'
  date_gmt: '2011-03-16 15:02:34 +0100'
  content: "Souhlasím s katastrofálním stavem dokumentace ke Groovy i s tím, že dokumentace
    ke Springu je na skvělé úrovni. Tedy od verze 2, v 1.2 to byl taky dost děs. Ale
    Groovy už patří pod SpringSource dost dlouho na to, aby s tím chlapci něco udělali
    :-)\r\n\r\nJá se momentálně potýkám s naprosto nevyhovující strukturou dokumentace,
    kvůli které musím lidem vysvětlovat spoustu věcí, které by si bývalo stačilo přečíst.
    Takže díky za motivující článek."
- id: 36407
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-03-16 17:12:28 +0100'
  date_gmt: '2011-03-16 16:12:28 +0100'
  content: "@David Skýba: Kathy Sierru mám taky rád: http://blog.novoj.net/2008/05/21/vasnivi-uzivatele/
    ... problém pro mě je překlenout tu propast mezitím, co bych chtěl a co jsem aktuálně
    schopen ;-)\r\n\r\n@Jakub Vrána: chtěl bych to řešit tak, že primárně by měl vývojář
    používat referenční dokumentaci k té verzi, kterou má na své instalaci (taktéž
    i slohovou). Samozřejmě by někde stranou existovala refereční a slohová dokumentace
    i pro nejaktuálnější verzi, kam by bylo možné kdykoliv nahlédnout. Připadá mi
    to přehlednější a jednodušší způsob než časté anotace @since a @deprecated v dokumentačním
    textu.\r\n\r\nDíky všem za postřehy. Jsou pro mě velmi cenné."
- id: 36437
  author: Tomáš Záluský
  author_email: zalusky@centrum.cz
  author_url: ''
  date: '2011-03-17 02:51:17 +0100'
  date_gmt: '2011-03-17 01:51:17 +0100'
  content: "Dík za přínosný článek, umím si představit tu plnou hlavu po takovém brainstormingu
    :-) Ještě bych k tomu dodal:\r\n- “nejlepší dokumentace je zdrojový kód ...  –
    jenže je to omyl.\" - on to není ani tak omyl, spíš neúplná pravda. Tuhle větu
    slýchám často v souvislosti s důrazem na správné pojmenování a v tomto smyslu
    se s ní ztotožňuji, nicméně souhlasím, že není důvodem nedělat ostatní typy dokumentace,
    o kterých jste psal. Jinak než se dostat do stavu: /** @return false */ boolean
    foo() {return true;} - to radši nic.\r\n- překážkou psaní javadocu je také nutnost
    psát v HTML. Podpora v Eclipse pro doplňování tagů není ideální. Často používané
    prvky jsou ul,ol,li a bylo by mnohem pohodlnější, kdyby javadoc akceptoval nějaký
    wiki formát přímo. Tím by bylo vyřešeno i \"aby vás to nelákalo, hrát si s formátováním\"\r\n-
    \"Navíc jsem si potřeboval utřídit myšlenky a psaní mi v tom pomáhá\" - tohle
    se dá aplikovat i na samotné psaní dokumentace. Taky nedokumentuju neusazené API,
    ale zároveň jsem se odnaučil dívat se na nedokumentované API pohledem 'už tomu
    chybí jen ta dokumentace' - potřebu refactoringu často objevím až při psaní dokumentace."
- id: 36449
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-03-17 07:28:01 +0100'
  date_gmt: '2011-03-17 06:28:01 +0100'
  content: "@Tomáš Záluský:\r\n- nejlepší dokumentace je kód: v tomhle směru jsem
    se spíš snažil oslovit ty, kteří se touto větou ohánějí jako výmluvou proč dokumentaci
    nepsat. Nechci zpochybňovat to, ze i přes nejdokonalejší dokumentaci se do kódu
    někdy musí a proto by měl podle toho vypadat.\r\n- formátování: formátování je
    zlo - souhlasím, ze nějaký Wiki nebo APT by mohl být lepší (jenže třeba takový
    zápis tabulky v Apt je taky velmi ošklivá záležitost), důležitá je ale jen změna
    mindsetu - když dokumentuji, soustředím se na obsah a ne na formu\r\n- dokumentace
    hotového API: na tohle mi reagoval jeden kolega z firmy úplně stejně a něco pravdy
    na tom určitě je. Odpovídal jsem mu, ze já obvykle nejsem schopný nastřelit API
    napoprvé správně a ještě nějakou dobu si s ním hraji a masivně refaktoruji. Při
    tomhle stylu vývoje je myslím lepší posunout dokumentaci až ke konci realizace
    - tam je ještě možné API začistit podle toho, co mě napadne při psaní dokumentace,
    ale už vím ze to budou více méně jen kosmetické změny."
- id: 36485
  author: v6ak
  author_email: reknu@nic.cz
  author_url: ''
  date: '2011-03-17 18:15:24 +0100'
  date_gmt: '2011-03-17 17:15:24 +0100'
  content: "\"V tomto centrálním místě by mělo být možné nad libovolnou kapitolou
    diskutovat\"\r\nDobrá poznámka. Máte nějaké tipy na nástroje pro tuto diskuzi?"
- id: 36630
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-03-19 20:06:48 +0100'
  date_gmt: '2011-03-19 19:06:48 +0100'
  content: "@v6ak Tohle je pro nás no-brainer - vzhledem k tomu, že hlavní naší devizou
    je naše CMS: http://www.edee-cms.cz/ , tak je pro nás nejlevnější a nejproduktivnější
    nasadit na tenhle úkol náš vlastní diskusní modul (to by nám nemělo zabrat víc
    jak pár hodin)."
- id: 90025
  author: "&raquo; Nástroje pro vývoj web aplikací ve Forrestu Myšlenky dne otce Fura"
  author_email: ''
  author_url: http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/
  date: '2012-09-04 07:11:55 +0200'
  date_gmt: '2012-09-04 06:11:55 +0200'
  content: "[...] repository.  Používání aktuální dokumentace z JavaDocu vychází z
    mé úvahy v článku Zamyšlení nad tvorbou programátorské dokumentace a tam je také
    myšlenka rozvedena do větších [...]"
---
<p><img src="http://blog.novoj.net/binary/2011/02/documentation-150x150.jpg" alt="" title="Businessman Overwhelmed with Paperwork" width="150" height="150" class="alignleft size-thumbnail wp-image-1371" /> Aktuálně ve <a href="http://www.fg.cz" target="_blank">Forrestu</a> revidujeme způsob vytváření dokumentace, nastavení standardů a bavíme se o tom, co a jak změnit. </p>
<p>Motiv je jasný - nejsme spokojeni se současným stavem a v některých případech dokonce dost zásadně. Všichni známe to staré rčení "nejlepší dokumentace je zdrojový kód", které pochází kdoví odkud (tipnul bych si, že za ním stojí eXtreme Programming, ale zdroj jsem vážně nenašel) - jenže je to omyl. Správná dokumentace může mít dost zásadní vliv na výslednou použitelnost / publicitu vašeho produktu / knihovny mezi programátory. </p>
<p>Kvalitní (systém) dokumentace má podle mého názoru zásadní pozitivní vliv na rozšíření např. <a href="http://docs.jquery.com/Main_Page" target="_blank">jQuery</a> nebo <a href="http://static.springsource.org/spring/docs/3.1.0.M1/spring-framework-reference/html/" target="_blank">Springu</a>. Naopak negativně se musela dokumentace podepsat na adopci <a href="http://groovy.codehaus.org/Documentation" target="_blank">Groovy</a>. Přestože se jedná o skvělý jazyk, dokumentace je na tom, co se týká přehlednosti a detailnosti, bídně (můj subjektivní dojem).</p>
<p><a id="more"></a><a id="more-1370"></a></p>
<p>Nuže - berme, že naším cílem je tvorba dokumentace pro další programátory (tj. nikoliv zadávací, akceptační nebo uživatelská dokumentace). Jak by měla taková dokumentace vypadat, aby byla skutečně funkční? Stačí nabrat inspiraci na <a href="http://en.wikipedia.org/wiki/Software_documentation" target="_blank">Wikipedii</a>:</p>
<h3>Tématická</h3>
<p>O této se my bavíme jako o slohové dokumentaci - po té sáhne nejspíš úplný nováček, který chce pochopit principy skryté za konkrétní funkcionalitou knihovny (lepší příklad tohoto typu dokumentace, než je ve <a href="http://static.springsource.org/spring/docs/3.1.0.M1/spring-framework-reference/html/" target="_blank">Springu</a>, jsem nikde ve své praxi nepotkal).</p>
<p>Bez tohoto typu dokumentace lze možná žít, ale ztěžujeme tak ostatním programátorům rychlý a správný začátek používání knihovny. Lecos je možné si odvodit z dalších dvou typů dokumentace, ale vývojářům může chybět porozumění proč dělají to, co dělají (a to je z dlouhodobého hlediska dost nebezpečná záležitost).</p>
<h3>Tutorialy</h3>
<p>Tento typ dokumentace nazýváme jako funkční příklady. Tj. reálná ukázka použití vaší knihovny nejlépe ve spustitelném tvaru, který si může čtenář ihned vyzkoušet (ještě lépe s ním mít možnost experimentovat). Příklad by měl být samozřejmě okomentovaný a jednoduše zkopírovatelný uživatelem. Protože to je to, co budou čtenáři dělat - kopírovat a upravovat vaše příklady. Urychlíte jim start, zjednodušíte práci a zároveň víte, že stavějí na zdravém základu, za kterým stojíte vy jako autoři. Pro ukázkový příklad bych použil služby, které na podobný účel orientují: <a href="http://jsfiddle.net/" target="_blank">jsFiddle pro JavaScript</a>, <a href="http://groovyconsole.appspot.com/" target="_blank">Groovy Web Console</a> a další. Pro příklad uvedu jQuery - třeba: <a href="http://api.jquery.com/last/" target="_blank">http://api.jquery.com/last/</a>, kde spojují tutorial s referenční dokumentací výborným způsobem (mohou si to dovolit, všechny příklady jsou velmi jednoduché).</p>
<h3>Referenční</h3>
<p>Referenční dokumentace opěrný bod, každého uživatele - bude ji používat úplný začátečník stejně jako zkušený uživatel (nikdo nezná všechno a je to i zbytečné). Referenční dokumentace by měla být úplná a vždy aktuální, měla by být přehledná a dobře strukturovaná. Musí být orientovaná na cílové čtenáře - tj. Java vývojářům odpovídá JavaDoc, JavaScript programátoři uvítají refereční dokumentaci v podobě, jakou má např. <a href="http://docs.jquery.com/Main_Page" target="_blank">jQuery</a> nebo jakou generuje <a href="http://code.google.com/p/jsdoc-toolkit/" target="_blank">jsDoc</a> (<a href="http://www.birt-exchange.com/be/documentation/JavaComponents10/JSAPI-JSdoc/index.html" target="_blank">ukázka</a>) atp. Aby byly splněny výše uvedené podmínky, je ideální, aby byla tato dokumentace generovaná z aktuálního zdrojového kódu. Referenční dokumentace by měla pokrývat jen a pouze veřejné API knihovny.</p>
<p>Nyní, když jsme si rozebrali, jak by měla dokumentace vypadat, podívejme se, s čím se na cestě za dokonalostí velmi pravděpodobně setkáme:</p>
<h2>Hrozby</h2>
<p>Níže se snažím zachytit nejčastější vady dokumentace a zamýšlím se nad jejich možnými příčinami.</p>
<h3>Neúplná dokumentace</h3>
<p>Nejčastěji se setkáme s neúplnou dokumentací (nedej bože, neexistující dokumentací) - tj. dokumentací, kde některé části úplně chybí, nebo jsou nedostatečně popsané. Důvody takového stavu vám obhájí každý vývojář daného projektu - nejčastějším z nich je nedostatek času. Všichni se pachtíme za implementací fíčur a čas na dokumentaci, která žádné nové vlastnosti nepřináší, prostě není. Nikdo v rámci sprintu nezaplánoval čas na tvorbu / aktualizaci dokumentace a / nebo ji zákazník nechce zaplatit. Často také není jasně definované, kdo je vlastně za dokumentaci odpovědný (jasně, že celý tým) nebo nejsou dány jasné mantinely, aby se člověk mohl soustředit na to, CO dokumentovat a ne JAK dokumentovat (tj. bootstrap tvorby dokumentace je velmi náročný, protože daný člověk musí vymyslet celý "ekosystém").</p>
<h3>Neaktuální dokumentace</h3>
<p>Jako důvody neaktuální / neudržované dokumentace mne napadají: složitost vytváření dokumentace a nízká motivace vývojářů pro její aktualizaci či neautomatizované vytváření dokumentace (nebo nefunkčnost automatického procesu). Všichni si uvědomujeme, že psaní dokumentace bude vždy zátěž, která nepřináší okamžitý benefit. Tj. abychom udrželi dokumentaci douhodobě aktuální musí motivace a okamžité benefity z ní plynoucí převýšit náklady na její tvorbu. Čím víc opičí práce je v procesu dokumentace potřebný, tím výše si zvedáme laťku pro motivaci týmu.</p>
<h3>Chybná dokumentace</h3>
<p>Horší než chybějící dokumentace je dokumentace chybná nebo zavádějící. Často může být tento stav paradoxně zapříčiněn tím, že ji tvoříme příliš brzy - ve chvíli, kdy si systém ještě pořádně nesedl a dodatečné modifikace, refaktorizaci kódu již do existující dokumentace zpětně nepromítneme. Možná také za líné vývojáře píše dokumentaci někdo jiný, kdo není autorem algoritmů a základních principů zakotvených v aplikaci a tudíž nemá v hlavě ten správný obraz, který je potřeba ke správné dokumentaci. Dalším možným důvodem je, že vývojáři píšící dokumentaci nemají správné vyjadřovací schopnosti a jejich výstup není dostatečně srozumitelný (svěřili byste ale takovému člověku třeba komunikaci se zákazníkem?).</p>
<h3>Nepřehledná / přebujelá dokumentace</h3>
<p>Firmy / projekty, které si nestěžují na nedostatek dokumentace mohou mít paradoxně úplně jiný problém. Dokumentace sice existuje, ale je jí tolik nebo je tak nepřehledná, že se v podstatě nedá použít. Dřív nebo později tak začne jejich dokumentace zastarávat, protože přidávat další a další části do nepřehledné dokumentace situaci jenom zhorší a motivace k jejímu psaní se sníží pod kritické minimum. Důvodem jsou špatně nastavené procesy pro dokumentaci, strukturování dokumentace, nebo špatné technické zázemí pro její tvorbu. Nechvalně známým příkladem budiž dokumentační "šablony" některých známých českých bank, po jejichž vyplnění nemůže být čtenář o moc moudřejší, než byl na začátku (dokumentace aplikace o 10 jednoduchých pagích na 90 stránkách dokumentace - WTF! - zajímalo by mě, kolik stránek má dokumentace takového internetového bankovnictví).</p>
<h2>Eliminace příčin vadné dokumentace</h2>
<p>Nyní, když jsem se rozepsal, jaké špatné konce nás mohou v souvislosti s dokumentací potkat, je na čase zamyslet se, jestli a jak se dá proti jednotlivým hrozbám bojovat. Nuže, odteď jsou to již jen moje domněnky, protože jak jsem již uvedl - zatím to u nás zrovna ideální není. Snažím se tedy najít cestu, která vede podle mého názoru tudy:</p>
<h3>Nedostatek času na psaní dokumentace</h3>
<p>Tenhle faktor hraje jednu z nejzásadnějších rolí a je těžké s ním bojovat. Podle mého názoru není vhodné dokumentovat, pokud se nám nestabilizovalo API. S refaktorizací metod / tříd totiž v podstatě přicházíme o veškerou dokumentaci, která k nim byla vytvořená - to může vést pouze ke dvěma špatným volbám: nerefaktorizovat nebo nedokumentovat. Lépe tedy: dokumentovat ale až stabilní API.</p>
<p>Tím se nám tedy dokumentace posouvá na konec realizace. Aby se skutečně provedla je nutné ji PLÁNOVAT a vyhradit na ni čas už na úrovni projektového řízení. Líp se nám bude plánovat, když minimalizujeme čas potřebný na její vytvoření (využít co největší možné automatizace a vytěžení existujících dat) a zajistíme další vedlejší přínosy z tohoto procesu (viz. další kapitoly).</p>
<h3>Složitost psaní dokumentace</h3>
<p>Se složitostí se bojovat dá. Psát / udržovat dokumentaci je na obtíž každému, a proto stačí minimální překážka, která se postaví do cesty a výrazně snížíme motivaci k jejímu psaní. Doložím na příkladech - představte si, že pokud chcete zdokumentovat svůj kód musíte:</p>
<ul>
<li>najít na sdíleném disku textový dokument, vyhledat potřebnou kapitolu a doplnit nové informace</li>
<li>otevřít analytický nástroj, doplnit a zdokumentovat patřičné modely (popř. požádat analytika o doplnění příslušných informací)</li>
<li>otevřít Wiki (nebo jinou dokumentační stránku jako je třeba Confluence), přihlásit se, najít odpovídající stránku a tu zaktualizovat</li>
</ul>
<p>Se všemi těmito příklady jsem se osobně v praxi setkal a můžu odpovědně říct, že vedou k podvědomému odkládání povinnosti dokumentovat. Z toho důvodu docházím k závěru, že dokumentace (má-li být psaná a udržovaná) se musí nacházet co nejblíž vlastnímu kódu, ne-li přímo v něm. Ideální se mi tedy zdá pro dokumentační účely využít v co největší míře JavaDocu a zdrojů umístěných přímo v projektovém adresáři (HTML, APT atp.). Tj. vývojář by neměl mít potřebu opustit své IDE aby vytvořil nebo aktualizoval dokumentaci - pokud je k tomu nucen, je to pro něj mentální blok, který bude muset překonat (a řada jej bez přinucení nepřekoná).</p>
<p>S publikací dokumentace nesmí být spojené žádné další ruční úkony. Formát / umístění dokumentace a proces publikace musí být jasně daný a vývojář nesmí být nucen přemýšlet o něčem dalším, než je vlastní dokumentace kódu. Musí stačit pouze napsat odstavec v souboru projektu (JavaDoc v Java class, paragraf v HTML v konkrétním projektovém adresáři atp.) a commit do VCS.</p>
<p>Informace, které jsou jednoduše odvoditelné z výkonné části nesmí být potřeba opisovat znovu do jiné části dokumentace. Musí se posbírat automaticky. Uvedu příklad:</p>
<p>Mějme knihovnu JSP tagů - po přidání nového tagu by nemělo být nutné někde jinde v dokumentaci duplikovat tuto informaci a zavádět nějaký nový odkaz na tento tag apod. Dokumentační proces by měl být schopný přečíst TLD dodávané s projektem a vysát z něj dokumentaci, seznam vlastností atd. (buď přímo z XML nebo z JavaDocu odkazované třídy). Tj. programátor pouze zavede nový tag TLD, což z hlediska funkcionality stejně musí a zdokumentuje třídu pomocí JavaDoc. Tato informace se následně promítne i do generované dokumentace.</p>
<p>I v případě líného programátora se tak dokumentace drží aktuální, protože čerpá přímo z produkčního kódu. Zcela zásadně se musíme držet principu DRY, jinak to nebude fungovat.</p>
<h3>Nízká motivace k psaní dokumentace</h3>
<p>Nemyslím si, že je možné motivaci dlouhodobě udržet nějakými pohrůžkami nebo odměnami. Motivaci ovšem mohou zdvihnout další využití vytvořené dokumentace. Nad dokumentovanými tutoriály / příklady je možné postavit sadu testů, které zvýší kvalitu kódu mezi releasy knihovny. S drobnou prací navíc je tak možné získat i hodnotné integrační testy, které mohou výrazně snížit chybovost základních podporovaných use-case.</p>
<p>Důležitou roli také hraje "komunita" vývojářů. Jednak, pokud evidentně nějaká část dokumentace chybí, je třeba aby vyvíjeli tlak na autora kódu - popřípadě měli jednoduchou možnost dokumentaci sami doplnit nebo navrhnout doplnění. Dokumentace by neměla být tedy pouze v pasivním formátu, ale měla by být integrována někam, kde je možné vkládat příspěvky do diskuse, odeslat autorovi kódu návrh nového odstavce do dokumentace či možnost vytvořit vlastní ukázkové příklady použití (ideálně s testy).</p>
<p>Další důležitou věcí je, aby se dokumentace používala. Jenom u často používané dokumentace je šance, že se udrží aktuální, vychytají se nepřesnosti a chyby a bude nějaká motivace autorů / komunity ji udržovat a rozvíjet. Z toho důvodu musí být dokumentace rychle po ruce (ideálně z místa, kde budou uživatelé funkcionality knihovny používat, by se měli jedním kliknutím dostat k odpovídající dokumentaci).</p>
<h3>Chyby v dokumentaci</h3>
<p>Chybám se nedá úplně vyhnout nikde - v dokumentaci taky budou. Tím spíš u interních knihoven, kde nemáme takových čtenářů, jako má třeba Spring. Chyby jsou dvojího druhu:</p>
<ul>
<li>dokumentace nereflektuje aktuální stav (zastaralá)</li>
<li>dokumentace je nedostatečná</li>
<li>dokumentace má logické chyby</li>
</ul>
<p>Zastarávání dokumentace se lze vyhnout pouze tak, že dokumentaci aktualizujeme spolu s kódem na jednom místě. Tj. pokud upravuji kus veřejného API a vidím, že je v dokumentaci popsána původní funkcionalita (o pár řádek výš), přirozeně mi to nedá, abych spolu s kódem neupravil také dokumentaci. Prostě to bije do očí a většina lidí to tak nenechá být.</p>
<p>Někteří lidé jsou struční a těžko s tím něco uděláme. Tady musí zafungovat "komunitní" prvek a musí přijít někdo další, koho to bude rozčilovat a navrhne doplnění dokumentace. Takovému dobrovolníkovi nesmíme házet žádné klacky do cesty - měl by mít možnost doplnit dokumentaci jednoduše, ideálně kontaktovat rovnou původního autora a mít možnost mu poslat (e-mail by měl stačit) doplněnou dokumentaci k revizi. Jakmile navážou osobní kontakt, už se nestane, že by odvedená práce vyšla vniveč. Navíc bude mít původní autor možnost revidovat logickou správnost navrhované dokumentace a bude vidět, že jeho standardní úroveň dokumentace pro čtenáře nestačí a bude motivován ke zlepšování.</p>
<p>Myslím, že vývojář, který je schopný navrhovat kvalitní API, musí být schopný vyplodit i kvalitní dokumentaci k němu. Podle mého názoru to jde ruku v ruce - člověk, který neumí vyjádřit své myšlenky, těžko dokáže navrhnout použitelné API (polemizujte se mnou :-) ). K chybám tedy často dochází proto, že dokumentaci píše někdo jiný, než původní autor dokumentace, který v hlavě nenosí ten správný obraz a logické souvislosti. Vím, že si odporuji s předchozím odstavcem - proto se tam snažím vtlačit proces revize navrhované dokumentace autorem. Tady chci říct jen toto - nikdo z nás není takový lumen, aby pro něj byla podřadná nějaká práce (jako je třeba psaní dokumentace). Neexistuje podřadná práce a i ta největší esa by se měla věnovat psaní dokumentace stejně jako ti nejposlednější z týmu.</p>
<p>Jako závěrečný bod této kapitoly jsem si nechal verzování dokumentace. V referenční dokumentaci si můžeme pomocí nějakými anotačními nástroji (např. @since v JavaDoc) ale ve slohové dokumentaci /  tutorialech je toto verzování daleko problematičtější. Historicky jsme to řešili poznámkami "na okraj", že tato pasáž "platí od verze XY" - ale celkově to vede pouze ke zhoršení čitelnosti dokumentace (pokud zrovna nejedete na poslední verzi, musíte v hlavě složitě odfiltrovávat všechny pasáže, které se vás netýkají). Z tohoto pekla jsou pouze dvě cesty - buď při releasech knihovny aktuální dokumentaci vystavit na unikátní (neměnnou) URL, nebo ji ukládat přímo dovnitř artefaktů, které jsou součástí releasu. Programátor, který potom používá konkrétní verzi knihovny použije dokumentaci z konkrétního URL (nebo přímo zevnitř knihovny) ve verzi, kterou používá. Nebude tak nutné nic odfiltrovávat, protože v dokumentaci logicky nebudou zdokumentované fíčurky, které ještě neexistují. Jediný problém, který je s tímto spojený, je ten - že někdy dojde k uvolnění nových vlastností, které se nestihnou (i při dobré vůli) zdokumentovat. Do zamrazených verzí dokumentace je potom zpětně už těžké dokumentaci doplňovat - je prostě nutné akceptovat, že dokumentace se prostě objeví třeba až v některých dalších verzích knihovny, i když reálně je daná fíčura dostupná už dříve (tady nás může zachránit automaticky generovaná referenční dokumentace, čerpající z produkčního kódu - i když ta často nemusí být dostatečná).</p>
<h3>Špatně strukturovaná dokumentace</h3>
<p>Tohle je místo, kde se to všechno může zvrtnout. Můžeme vyhodit desítky, ne-li stovky hodin práce na něčem, co ve výsledku nebude fungovat. V hlavě mám představu nějakého jednoduché aplikační nadstavby, která bude agregovat dokumentaci z konkrétních knihoven tak, aby autoři dokumentace už nemuseli myslet na to jak, ale co dokumentovat. Pravidla pro ně by měla být opravdu jen jednoduchá: pište JavaDoc, odkazované obrázky / dokumenty ukládejte v projektovém adresáři sem a odkazujte relativně, slohovou dokumentaci dávejte tuhle a hlavně - tady připravte příklady pro základní use-case, které svým kódem řešíte (samozřejmě s patřičnými integračními testy např. pomocí <a href="http://seleniumhq.org/" target="_blank">Selenia</a>). Kašlete na styly - používejte základní HTML tagy (nebo něco jako APT), aby vás to nelákalo, hrát si s formátováním.</p>
<p>Ty kousky dokumentace, které takto vzniknou, se pak zpřístupní v centralizované dokumentaci, kde se na jednom místě setkají tématická i referenční dokumentace s příklady. V tomto centrálním místě by mělo být možné nad libovolnou kapitolou diskutovat, aby zapůsobil komunitní prvek při řešení problémů s konkrétními funkcionalitami (každý příspěvek v diskusi by šel e-mailem na původního autora dané kapitoly). U každé kapitoly by měl být také formulář (link otvírající e-mail klienta), který umožní komukoliv napsat návrhy na změny v kapitole dokumentace / příkladu atp. původnímu autorovi.</p>
<p>Funkční příklady by měly kombinovat jak interaktivní ukázku dané fíčurky, tak náhledy na důležité části kódu nebo konfigurace, která příklad představuje. Ideálně pokud by měl čtenář nějakou možnost si s kódem v sandboxu pohrát a experimentovat s jeho modifikacemi.</p>
<p>Dokumentace by měla "žít" - tj. mělo by v ní jít fulltextově vyhledávat, nejčastěji navštěvované části dokumentace by měly být někde vysvícené (feedback pro původní autory kódu), stejně tak by měl být přehled o nejčastěji diskutovaných fíčurkách. Příspěvky do diskusí by mělo být možné hodnotit, aby se vyselektovaly nejhodnotnější odpovědi na případné problémy (princip, který stojí za úspěchem <a href="http://stackoverflow.com/" target="_blank">StackOverflow</a>).</p>
<p>Pokud budeme držet požadavky na vlastní dokumentaci na přirozené úrovni a minimalizujeme "omáčku", budeme mít i do budoucna trošku volnější ruce k restrukturalizaci dokumentace, pokud se nám strukturování nepovede hned na poprvé. Změny by se měly týkat pouze toho pojícího systému, ale původní dokumentace autorů by mohla zůstat (s troškou štěstí) bez nutnosti změny.</p>
<h2>Závěr</h2>
<p>To jsem se zase rozepsal, že? Pravda je, že jsem po našem brainstormingu nabitý nápady, které potřebují jít na papír, protože jejich realizace určitě zabere několik měsíců (už jen proto, že dokumentace je vždy až na druhé koleji). Navíc jsem si potřeboval utřídit myšlenky a psaní mi v tom pomáhá (zkuste to někdy taky ;-) ).</p>
<p>Z toho všeho balastu na závěr (i pro sebe) vybírám základní pravidla, které jsou podle mého názoru zásadní:</p>
<ol>
<li>dokumentace musí vznikat v IDE, přímo u kódu</li>
<li>DRY!!! co je vytěžitelné reflexí / analýzou produkčního kódu se dokumentuje "samo"</li>
<li>systém dokumentace musí být dán zvenčí a musí být přirozený - programátor by se měl věnovat jen lokální dokumenaci kódu, jak to dělal vždycky</li>
<li>dokumentování musí mít vedlejší motivátory - např. jednoduché doplnění integračních testů zvedajících o řád kvalitu releasů nových verzí knihovny, možnost využití nápovědy přímo v IDE, využití sandboxovaného příkladu nejen uživateli ale i autory původního kódu k experimentování</li>
<li>podpora komunitního efektu - navázání kontaktu uživatelů s autory, podpora kontribuce v maximální možné míře</li>
<li>dokumentace dosažitelná na jediné kliknutí (jedinou klávesovou kombinaci)</li>
<li>verzovaná dokumentace - nejlépe pomocí prostředků VCS a standardního release procesu</li>
<li>jednoduché a striktní oddělení veřejného a priváního API i na úrovni dokumentace (abychom čtenáře nezahltili nepodstatnými informacemi)</li>
<li>zprovozněná suite integračních testů, kam stačí jednoduše doplnit další</li>
<li>sandbox pro experimentování</li>
<li>živá dokumentace -  automatizovaná detekce "toho kde to žije"</li>
<li>dokumentují se až dokončené fíčury, vyzkoušené praxí</li>
</ol>
<p>Části naznačeného řešení jsou již zrealizované a sbíráme zkušenosti s jejich provozem. Plno toho ovšem hotového není a celkový obrázek, jak uvedená pravidla fungují v praxi nemám. Z technologického hlediska máme většinu pravidel pokrytých (tj. víme jak na to), ale teprve život ukáže, jestli to byla správná cesta a správný způsob realizace nebo ne. Rád bych na tento článek v budoucnu navázal a popsal jak technologickou stránku věci, tak i zkušenosti, které s tím budeme mít.</p>
