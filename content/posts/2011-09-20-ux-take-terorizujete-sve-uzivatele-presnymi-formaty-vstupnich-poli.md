---
status: publish
published: true
title: UX - také terorizujete své uživatele přesnými formáty vstupních polí?
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img src=\"http://blog.novoj.net/binary/2011/09/datetime.png\" alt=\"\"
  title=\"datetime\" width=\"161\" height=\"78\" class=\"alignleft size-full wp-image-1630\"
  /> Od začátku letošního roku pracujeme na drobných vylepšeních, které mají za cíl
  zlepšení uživatelské zkušenosti s našimi webovými aplikacemi. Kromě řady dalších
  věcí se naši UX odborníci zaměřili i na formuláře, které jsou standardní součástí
  většiny webů. O správném designu webových formulářů už toho bylo napsáno mnoho (viz.
  <a href=\"#sources\">reference na konci článku</a>) a v tomto článku je nechci opakovat.
  Jedním z požadavků, které dostali jako první byly automatické korekce zjevně špatných
  vstupů uživatele na místech, kde to je možné. Uvedu pár příkladů, které jste ještě
  donedávna mohli najít i na našich webech:\r\n\r\n<ul>\r\n   <li>hodnota s desetinnou
  čárkou vyžadovala použití čárky a nikoliv tečky (nebo obráceně, podle nastaveného
  locale) - řada uživatelů ovšem jednou napíše to a podruhé ono (což souvisí častokrát
  i s nastavením klávesnice)</li>\r\n   <li>zadání vložené adresy vyžaduje správný
  formát - tj. aby text začínal např. protokolem http:// - uživatelé ovšem většinou
  protokol nepíší a často nepíší ani prefix www</li>\r\n   <li>datum a čas vyžadoval
  přesné zadání podle specifikovaného formátu (d.M.yyyy) a vložení mezery na nesprávné
  místo nebo lehce jiný formát datumu na vstupu ústil v selhání validace</li>\r\n</ul>\r\n\r\nVyřešení
  dvou prvně jmenovaných problémů byla hračka, s datumem jsem se ovšem docela potrápil.
  V době, kdy jsem konverzi implementoval jsem nenašel žádný parser datumu, který
  by uměl \"heuristicky\" rozeznávat různé formáty, takže jsem tuto logiku implementoval
  sám (viz. další část článku). Od té doby se mi ale dostal do rukou odkaz na knihovnu
  <a href=\"http://www.pojava.org/\" target=\"_blank\">POJava</a>, která podobnou
  implementaci v <a href=\"http://www.pojava.org/site/pojava-2.7.0/apidocs/org/pojava/datetime/DateTime.html\"
  target=\"_blank\">DateTime třídě</a> má.\r\n\r\n"
wordpress_id: 1626
wordpress_url: http://blog.novoj.net/?p=1626
date: '2011-09-20 16:28:57 +0200'
date_gmt: '2011-09-20 15:28:57 +0200'
categories:
- Programování
- Java
- User Experience
tags: []
comments:
- id: 51244
  author: koudi
  author_email: koudelka.j@gmail.com
  author_url: ''
  date: '2011-09-20 18:42:53 +0200'
  date_gmt: '2011-09-20 17:42:53 +0200'
  content: "\"Respektive ideálně se úplně zbavit komentáře u daného pole formuláře
    ve smyslu: „vložte datum ve formátu XY“\"\r\n\r\nTady bych si dovolil lehce nesouhlasit.
    Spousta lidi uz je zvykla, ze datum jsou problematicky a (bohuzel) je potreba
    je zadavat v danem formatu. Bez popisku tak budou muset premyslet, jak to asi
    autor pozaduje, protoze nevi, ze na tom nezalezi. Proto by tam podle me nejaky
    popisek byt mel - bud ukazky prijatelnych formatu nebo klidne neco jako \"zadejte
    jak se vam zlibi\"."
- id: 51247
  author: Kalda
  author_email: jirka@kalensky.cz
  author_url: ''
  date: '2011-09-20 20:10:26 +0200'
  date_gmt: '2011-09-20 19:10:26 +0200'
  content: Jen chci podpořit Koudiho - předělávali jsme nějaké formuláře, které se
    jevili jako problematické. Nově bral systém téměř všechny myslitelné formáty,
    tj. nenapsala se k nim nápověda. První, na čem uživatelé již při testech "zatuhávali"
    bylo, že nevěděli, jak to zapsat...
- id: 51250
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-09-20 20:26:57 +0200'
  date_gmt: '2011-09-20 19:26:57 +0200'
  content: "Dík za tip. Pravda je, že kolegové mě na to taky upozorňovali. V návrzích
    na vylepšení od našich ux byla i pravidla pro zobrazování nápovědy - např. formou
    HTML5 placeholdrů (http://jnjnjn.com/144/html5-input-placeholders-eas-form-hints/)
    nebo vedle inputu atd.\r\n\r\nTo jsou ale, z hlediska programátorské podpory,
    už jen takové bonbónky, které nestojí skoro žádnou práci."
- id: 51251
  author: xxx
  author_email: email@nesdeluji.cz
  author_url: ''
  date: '2011-09-20 20:52:44 +0200'
  date_gmt: '2011-09-20 19:52:44 +0200'
  content: "A není lepší nedat uživateli šanci zadat datum blbě?\r\nNapř:\r\n3 selecty
    (den, měsíc, rok) Zadávat se dá z klávesnice a oproti textovému vstupu stačí místo
    tečky (a po tečce by správně měla následovat i mezera) zmáčknout tabulátor.\r\n\r\nPS:
    Datum bez data ( http://www.pravidla.cz/hledej.php?qr=datum )"
- id: 51253
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-09-20 21:13:45 +0200'
  date_gmt: '2011-09-20 20:13:45 +0200'
  content: |-
    Osobně si myslím, že selecty nejsou ideální z několika důvodů:

    - v případě plného data s časem se uživatel uselectuje (jestli počítám správně je to 6 selectů)
    - v selectech obtížně zajistíte nemožnost zadání např. 30.2.2011 - takto uživatel stejně chybu dokáže vyrobit
    - některé selecty budou obsahovat velké množství položek (roky třeba)
    - špatně se kombinují s existujícími JS date pickery
- id: 51257
  author: Petr
  author_email: nechci@zadat.cz
  author_url: ''
  date: '2011-09-20 22:37:10 +0200'
  date_gmt: '2011-09-20 21:37:10 +0200'
  content: U zadávání data je nejhorší, když někdo (jako třeba zde v komentářích)
    otočí měsíc a den. Pokud je den nad 12, tak se to uhodne, ale 5.6. a 6.5. je problém.
    Pak je mi na 2 věci i vaše nápověda "použije se ..." protože by mě nikdy nenapadlo,
    že datum oddělené tečkami v ČR bude mít na prvním místě měsíc, jako to máte zde.
- id: 51286
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-09-21 05:31:18 +0200'
  date_gmt: '2011-09-21 04:31:18 +0200'
  content: "Z čeho vyvozujete, že jako první číslo oddělené tečkami máme měsíc? V
    příkladech používám formát český (tj. evropský) - kdy jako první číslo je vždy
    den. Nevím, jestli zmatení nemohlo způsobit to, jak jsem ve videu zadával datum
    2010-05-06, ale pak se aplikuje opět evropský styl data yyyy-mm-dd.\r\n\r\nPokud
    bych jako primární formát data nadefinoval d.MMMM yyyy, tak by se potom v nápovědě
    zobrazovaly texty jako: \r\n\r\nPoužije se \"6. květen 2010\"\r\n\r\nA to je v
    podstatě už bez diskuse.\r\nVy ale jistě narážíte na to, že 5/6 a 6/5 jsou v podstatě
    nejednoznačně zadaná data. Máte pravdu, ale aktuálně je preferován evropský styl,
    kdy den předchází měsíci. Tj. aplikačně to jednoznačné je - uživatel pak vidí
    výsledné plné datum v té nápovědě napravo, takže z toho by měl usoudit, jestli
    dostává, to co chtěl."
- id: 51289
  author: Petr
  author_email: nechci@zadat.cz
  author_url: ''
  date: '2011-09-21 06:20:35 +0200'
  date_gmt: '2011-09-21 05:20:35 +0200'
  content: Nepřečetl jste si závorku.. Já narážím na "09.21.2011 v 5:31" zde v komentářích.
    Pokud to někdo dokáže takhle "spáchat" na cz webu, pak nemám vůbec jistotu, jestli
    "použije se 5.6.2011" znamená 5. června nebo 6. května a vlastně v kontextu toho
    webu ani nevím, co bych měl zadat já. Samozřejmě "použije se 6. květen 2011" by
    to řešilo, pokud bych si toho všiml a pokud by se to tam vůbec objevilo, protože
    když zadám hodnotu celou a program si myslí, že to je jednoznačné, nápověda není.
- id: 51291
  author: Filip Jirsák
  author_email: filip@jirsak.org
  author_url: ''
  date: '2011-09-21 07:09:18 +0200'
  date_gmt: '2011-09-21 06:09:18 +0200'
  content: Souhlasím s tím, že poznámka by u políčka měla zůstat – spousta uživatelů
    bude stejně o formátu přemýšlet dopředu, protože neví, že tam máte nějakou heuristiku.
    Pro ně pak není vhodná ani poznámka „zvolte formát, jaký chcete“, protože pak
    stejně budou muset vybírat, jaký asi tak bude vhodný. Takže je lepší rovnou nějaký
    vhodný formát doporučit. Doporučený formát bych pak nepopisoval maskou (d.m.rrrr),
    kterou uživatel musí dekódovat, ale příkladem (ze kterého bude zřejmé, co je den,
    měsíc, rok). Do třetice – dlouhou celovětou poznámku bych si ponechal pro případ,
    kdy je potřeba něco podrobně vysvětlit (např. cizinci místo rodného čísla zadají
    datum narození, sériové číslo výrobku najdete … atd.) Formát data bych uvedl jen
    stručně jako příklad, takže vedle políčka pro datum bude jen „např. 31.12.2011“
    nebo „např. 31.12.2011, +0 (dnes), +1 (zítra)“ (vysvětlení v závorce samozřejmě
    nějak méně výrazně). Kdo chce poradit jeden univerzální formát, měl by ho najít
    na prvním místě, pokročilí se můžou naučit vychytávky z dalších příkladů.
- id: 51293
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-09-21 07:34:10 +0200'
  date_gmt: '2011-09-21 06:34:10 +0200'
  content: "Předem díky za všechny komentáře, protože obsahují to, co jsem si představoval
    - jiný pohled na věc.\r\n\r\nAd Petr) díky za upozornění na formáty datumu na
    blogu - zabíralo nějaké defaultní nastavení WordPressu, který pro blog používám,
    a tak byly pro nás evropany skutečně divné ... opraveno\r\n\r\nU toho jednoznačného
    tvaru se skutečně nápověda nezobrazuje - ono by to bylo trochu dvousečné - tyhle
    živé poznámky napravo chceme používat spíš jen \"výjimečně\", tj. ve chvílích
    kdy není něco úplně standardní. Kdybychom to začali používat příliš často, myslím,
    že bychom docílili jen toho, že by to uživatel začal ignorovat.\r\n\r\nAd Filip)
    Souhlas ... dobrá inspirace."
- id: 51297
  author: em
  author_email: mmmiloss@seznam.cz
  author_url: ''
  date: '2011-09-21 08:52:15 +0200'
  date_gmt: '2011-09-21 07:52:15 +0200'
  content: Myslím, že nejlepší ulehčení pro datum je umožnit vynechat tečky, ale pak
    vyžadovat nulu u měsíce. Já osobně pro sebe používám datum RRRR-MM-DD nebo RRRRMMDD_HHMM
- id: 51301
  author: Filip Jirsák
  author_email: filip@jirsak.org
  author_url: ''
  date: '2011-09-21 09:57:39 +0200'
  date_gmt: '2011-09-21 08:57:39 +0200'
  content: 'em: Škoda, že jste ten komentář nenapsal už včera :-) 20092011 by byla
    krásná ukázka nejednoznačnosti formátu data bez oddělovačů.'
- id: 51350
  author: Honza Hommer
  author_email: iam@honzahommer.cz
  author_url: http://www.honzahommer.cz
  date: '2011-09-22 07:00:37 +0200'
  date_gmt: '2011-09-22 06:00:37 +0200'
  content: "Honzo, jak už jsem říkal, tak dobrá myšlenka. Stačí to opravdu dotáhnou
    co se týče upozornění (lepší možná uživatele neupozornit a datum uložit v \"opraveném
    formátu\".\r\n\r\nCo mi pořád přece jenom vadí je, že když po uživateli chceme
    kompletní datum (den, měsíc a rok) a uživatel zadá jenom rok, validátor za něj
    navrhne například 1. 1. téhož roku. To mi přijde jako zvěrstvo. Pokud je uživatel
    takový retard, nemá právo projít formulářem dál a opravdu ten den a měsíc musí
    zadat."
- id: 51352
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-09-22 07:33:02 +0200'
  date_gmt: '2011-09-22 06:33:02 +0200'
  content: "Ahoj Honzo, diskusi si pamatuji a vím co ti vadí. U toho roku je to hodně
    markantní - tu heuristiku můžeme samozřejmě ještě potunit. Nicméně obdobný příklad
    je třeba čas - požadován je formát H:mm a když zadáš jen jediné číslo vezme se
    jako hodina a minuty se doplní jako 00. Tohle ti taky přijde nelogické?\r\n\r\nNavíc,
    když vezmeš v úvahu druhý faktor téhle funkcionality a to je urychlení práce v
    případech často vyplňovaných formulářů?"
- id: 51353
  author: Honza Hommer
  author_email: iam@honzahommer.cz
  author_url: http://www.honzahommer.cz
  date: '2011-09-22 08:08:55 +0200'
  date_gmt: '2011-09-22 07:08:55 +0200'
  content: "Z pohledu aplikace mi to nelogické nepřijde. Asi je to osobní pocit, ale
    pokud po uživateli chci \"dva údaje\" a on vyplní jenom jeden, je to špatně. \r\n\r\nOpravdu
    hlavní a vynikající přínos je ukládání dat do databáze v konzistentním formátu,
    aniž bychom uživatele otravovali využívat přesných konvencí.\r\n\r\nTo doplňování
    data a času, které mi tak vadí, je vhodné případně pro nějaké interní systémy,
    kde jsou uživatelé s touto \"akcí\" seznámeni a (hlavně) denně v kontaktu."
- id: 51436
  author: gsdgtwertwe
  author_email: plan-9@seznam.cz
  author_url: ''
  date: '2011-09-23 20:23:32 +0200'
  date_gmt: '2011-09-23 19:23:32 +0200'
  content: "technicka diskuze je zajimava.\r\nale mam z toho dojem, ze uzivatele blbnout
    kdyz neumi zadat datum a programatori\r\nmusi byt zas o to chytrejsi.\r\nmy mame
    v nasem softu funkci, ze staci zadat cislo dne, treba 23 a dohleda se blizsi\r\ndatum
    vpred ci vzad, 23.10. nebo 23.9."
- id: 51498
  author: NkD
  author_email: michal.nikodim@gmail.com
  author_url: ''
  date: '2011-09-25 00:45:06 +0200'
  date_gmt: '2011-09-24 23:45:06 +0200'
  content: 'V nasem softu (webova app) mame zdavani datumu nasledovne: podle zvoleneho
    jazyka se voli maska pro zobrazeni datumu v ramci cele aplikace. Napriklad CZ:
    DD.MM.YYYY  EN: YYYY-MM-DD . Takhle to uzivatel vidi vsude v tabulkach i na formularich
    a tedy nam to i tak zada. Problem nastal, kdyz prisel pozadavek od uzivatelu:
    "ale my nechceme psat tecky (nebo pomlcky), to nas zdrzuje". Takze validni vstup
    je i CZ: DDMMYYYY EN: YYYYMMDD  a jako bonus i CZ:DDMMYY  a EN: YYMMDD pricemz
    pokud je YY &lt;= abs(2000 - current_year) tak je pricteno 2000 jinak 1900. Na
    lost_focus na poli dojde k rozepsani datumu na puvodni CZ: DD.MM.YYYY (nebo EN..)
    a tak uzivatel vidi jestli zadal spravne. Validace mame na on_change a podbarvujeme
    background textoveho pole + tooltip s error message. Takze po napsani 010202 zmeni
    policko barvu z cervene (v pripade ze bylo required) na bilou a uzivatel vidi
    ze uz je validni vstup. Po opusteni policka se hodnota prepise na 01.02.2002 (CZ).
    Tot vse.'
- id: 51511
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-09-25 08:15:46 +0200'
  date_gmt: '2011-09-25 07:15:46 +0200'
  content: "Zajímavé - tohle už tu trochu výše padlo. My jsme se všude drželi principu:
    \"uživateli se do dat nesahá\". Tj. v tom políčku zůstane vždycky vyplněné to,
    co tam uživatel zapsal - jím vložené hodnoty nikdy nepřepisujeme. Tu naši zkonvertovanou
    / domyšlenou hodnotu zobrazíme read-only napravo nebo pod tím vstupním políčkem
    taky na onblur.\r\n\r\nV tom odkazovaném dokumentu trochu varovali před onchange
    reakcí formuláře - vyžaduje to od uživatele větší soustředění na to, co se vyplňuje,
    než když analýza probíhá až na onblur. Což byla pro mě taky velmi zajímavá a nová
    informace.\r\n\r\nBtw. ta grafika ve videu je velmi jednoduchá - jedná se jen
    o nějaký náš prototyp. Na zákaznických projektech budou ty hlášky graficky i pocitově
    doladěnější.\r\n\r\nDík za komentář."
- id: 51512
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-09-25 08:25:08 +0200'
  date_gmt: '2011-09-25 07:25:08 +0200'
  content: |-
    Ještě bych se rád zeptal, co za aplikaci to (NkD) vyvíjíte? Je to něco bližšího nějakému IS s úzkým okruhem uživatelů, kteří ji používají velmi často a tak preferují zkratky. Nebo nějaká aplikace otevřená na internet, kde není jisté, co za člověka přijde?

    Jak uživatelé reagují na ten onchange? Dokázal bys třeba potvrdit nebo vyvrátit ty teze z odkazovaného článku? Dík
- id: 51545
  author: NkD
  author_email: michal.nikodim@gmail.com
  author_url: ''
  date: '2011-09-25 23:04:43 +0200'
  date_gmt: '2011-09-25 22:04:43 +0200'
  content: "Ten zmineny princip \"uzivateli se do dat nesaha\" je mi blizky. Taktez
    ho vsemozne obhajuju a snazim se aby nas software nebyl chytrejsi nez inspektor
    Trachta. Casto se mi to nedari. Nekdy uplne rezignuju. Nekdy bojuju o kompromis.
    Velmi vyjimecne uplne vyhraju. Ale k veci. To co delame je pouzivano uzkou skupinou
    lidi. Jde v podstate o vnitropodnikovy system, bezici jako tenky klient. Takze
    v podstate si sve uzivatele skolime na to jak to maji pouzivat. Jde o HRMS, kdy
    je nas soft pouzivan k vykonavani outsourcingu pro ruzne firmy. Takze pro tebe
    asi ne moc berna mince. \r\nUI je postavene na Eclipse RAP a tak se to podoba
    desktopove aplikaci a zaroven si na javascript vubec nesahnem (zaplatpanbuh).
    Eclipse RAP je slusnej nastroj, ale i tak par veci delame po svem. Preklady, validace,
    formularove prvky, dataProvidery, sbernice. No kdyz to tak po sobe ctu :-) tak
    v podstate z RAPu potrebujem jen  vyhodnoceni delty pro odeslani na klienta (klient
    qooxdoo), plus eventy, plus theme, plus wrap nad EclipseRCP (hlavne JFace). Je
    to slozity povidani... ja mam na starosti prave UI vrstvu (jeden na OSGi) a obcas
    je to i docela zabava.  Nekdy bysme meli dat rec nad pivem... uz jsme se potkali
    na JOS (prvni rocnik), ale tam jsem byl v podstate jen diky Dagimu (zadne prednasky
    jsem nemel, jen jsem se opajel pocitem, ze jsem mezi elitou) ;-)"
- id: 51547
  author: NkD
  author_email: michal.nikodim@gmail.com
  author_url: ''
  date: '2011-09-25 23:11:03 +0200'
  date_gmt: '2011-09-25 22:11:03 +0200'
  content: Jooo. a k tomu onchange. Asi bych mohl udelat kus videa, ale jsem na to
    levej.. Takze zkusim popsat. Dulezite je ze veskerou validaci mame jako podbarveni
    background-color na textboxu. Takze uzivatel otevre formular por zadavani (v nasem
    pride wizard) a vidi treba 10 poli, pricemz 3 jsou nutne vyplnit a 2 jsou doporucene,
    zbytek nepovinny. Takze vidi 3 policka red-backgound, 2 yellow-background a zbytek
    bile (je to trosku jinak barevne, ale pro priklad staci). Na wizardu talcitko
    finish/ulozit/upravit/smazat (podle situace) je enabled=false. Uzivatel zacne
    typovat red-background a v urcitem okamziku (onChange) mu pole zbela. Kdyz to
    udela uz vsech cervenych, tak se wizard button finish prepne do enabled=true a
    uzivatel tak muze pokracovat. Cela situace je slozitejsi o to ze wizard muze (a
    casto je) nekolika krokovy a tak si preved vyse popsane na button "next" kdy az
    kdyz vsechny stranky wizardu porhlasi ze je vse ok, povoluje se zmineny finish.
    Pak nasleduji kontroly, ktere nelze delat na onChange a uzivatel to vnima jako
    dalsi stranku wizardu. No spatne se to popisuje....
- id: 51566
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-09-26 05:59:28 +0200'
  date_gmt: '2011-09-26 04:59:28 +0200'
  content: "Setkání nad pivem se vůbec nevyhýbám ;-) ... to bývají jedny z nejlepších
    diskusí. Lidi tam na sebe mají víc času a s druhým pivem se nestydí říct názory,
    které si jinak nechávají pro sebe ;-) . Jen ten JOS je krapet daleko. Třeba se
    ale příležitost naskytne.\r\n\r\nDík za konkrétnější info o tom cílovém použití.
    Myslím, že to jak to funguje jsem z popisu docela dobře vyrozumněl. Musím přiznat,
    že mě hodně ovlivnil zmiňovaný článek: http://www.alistapart.com/articles/inline-validation-in-web-forms/\r\n\r\nTam
    v kapitole Testing when to show inline validation\L je hezky popsané, jaké měli
    zkušenosti s inline validacemi BEFORE, WHILE a AFTER. S tím, že standardně jim
    vyšlo jako uživatelsky nejpřívětivější používat AFTER (tolik nedrobí pozornost)
    a na některá vyjímečná pole, kde se předpokládá vysoká chybovost (např. zadání
    unikátního uživatelského jména) WHILE validace."
- id: 51757
  author: Maaartin
  author_email: grajcar1@seznam.cz
  author_url: ''
  date: '2011-09-28 15:33:39 +0200'
  date_gmt: '2011-09-28 14:33:39 +0200'
  content: "Prima clanek, ale tak nejak se spoustou veci nesouhlasim:\r\n\r\nZmenit
    2011 na 1.1.2011 mi prijde nepouzitelny: Bud uzivatel presnejsi datum nevi nebo
    nechce zadat a pak je to problem. Nebo staci rok a pak je mozna chyba ptat se
    na vic. Nebo opravdu myslel den po silvestru ale to ma pravdepodobnost jiste mensi
    nez 1:356, to uz spis myslel 20.11. U casu mi to naopak prijde v pohode, 17 je
    proste 17:00:00.000, protoze tak se casy stanovuji (schuzky bezne zacinaji v 5
    a ne v 5:09:13) a casto vetsi presnost potreba neni.\r\n\r\nPrincip \"uzivateli
    se do dat nesaha\" se mi libi, ale mam pocit ze se ho nedrzis. Sice mu nezmenis
    to co napsal ale zpracuje se neco jineho, coz bych s velkou nadsazkou oznacil
    jako \"uzivateli se do dat saha tak aby to nevidel\". Ono se to sice ukaze hned
    vedle, ale on to nejpis nikdo necte, zvlaste kdyz je to zelene. Pokud jde o vyhledavaci
    formular nebo treba kalendar tak je to celkem jedno, pokud jde o neco kde spatne
    zadany datum muze byt velky prusvih, tak bych tak tolerantni radeji nebyl.\r\n\r\nVzhledem
    k tomu jaky je v tech datumech (spravny ale matouci tvar \"datech\" nepouzivam
    umyslne) gulas, tak asi univerzalni reseni neexistuje. Locale resi vetsinu uzivatelu
    ale co kdyz nekdo ma vsecko anglicky a pouziva cesky datum (jako treba ja)? Vzdy
    se nekdo takovy najde, proto jsou heuristiky potreba, ale zadna spolehliva neexistuje.
    Mozna bych jich zkusil nekolik a v pripade ze vysledek neni jednoznacny, tak bych
    uzivatele terorizoval aby si z nich explicitne vybral. Tu heuristiku co ho vyprodukovala
    bych pak pouzil na vsechny datumy toho uzivatele. Taky to nejspis ma svoje mouchy."
---
<p><img src="http://blog.novoj.net/binary/2011/09/datetime.png" alt="" title="datetime" width="161" height="78" class="alignleft size-full wp-image-1630" /> Od začátku letošního roku pracujeme na drobných vylepšeních, které mají za cíl zlepšení uživatelské zkušenosti s našimi webovými aplikacemi. Kromě řady dalších věcí se naši UX odborníci zaměřili i na formuláře, které jsou standardní součástí většiny webů. O správném designu webových formulářů už toho bylo napsáno mnoho (viz. <a href="#sources">reference na konci článku</a>) a v tomto článku je nechci opakovat. Jedním z požadavků, které dostali jako první byly automatické korekce zjevně špatných vstupů uživatele na místech, kde to je možné. Uvedu pár příkladů, které jste ještě donedávna mohli najít i na našich webech:</p>
<ul>
<li>hodnota s desetinnou čárkou vyžadovala použití čárky a nikoliv tečky (nebo obráceně, podle nastaveného locale) - řada uživatelů ovšem jednou napíše to a podruhé ono (což souvisí častokrát i s nastavením klávesnice)</li>
<li>zadání vložené adresy vyžaduje správný formát - tj. aby text začínal např. protokolem http:// - uživatelé ovšem většinou protokol nepíší a často nepíší ani prefix www</li>
<li>datum a čas vyžadoval přesné zadání podle specifikovaného formátu (d.M.yyyy) a vložení mezery na nesprávné místo nebo lehce jiný formát datumu na vstupu ústil v selhání validace</li>
</ul>
<p>Vyřešení dvou prvně jmenovaných problémů byla hračka, s datumem jsem se ovšem docela potrápil. V době, kdy jsem konverzi implementoval jsem nenašel žádný parser datumu, který by uměl "heuristicky" rozeznávat různé formáty, takže jsem tuto logiku implementoval sám (viz. další část článku). Od té doby se mi ale dostal do rukou odkaz na knihovnu <a href="http://www.pojava.org/" target="_blank">POJava</a>, která podobnou implementaci v <a href="http://www.pojava.org/site/pojava-2.7.0/apidocs/org/pojava/datetime/DateTime.html" target="_blank">DateTime třídě</a> má.</p>
<p><a id="more"></a><a id="more-1626"></a></p>
<h2>Nenuťte uživatele přemýšlet</h2>
<p>Ve smyslu této věty chceme zajistit, aby v případě, že vývojář požaduje datum ve formátu "d.M.yyyy H:mm" mohl uživatel zadat datum i v pozměněné podobě. Respektive ideálně se úplně zbavit komentáře u daného pole formuláře ve smyslu: "vložte datum ve formátu XY" a přizpůsobit se formátu, který vloží uživatel. Pro tyto účely jsem vytvořil třídu <a href="https://github.com/novoj/Utilities/blob/master/src/main/java/org/novoj/utils/datePattern/DatePatternConverter.java" target="_blank">DatePatternConverter</a>, ve které jsem implementoval (žádnou velkou chytristiku nečekejte) vlastní verzi heuristického rozpoznávání datumů. Variabilnost vstupů dobře dokumentuje test <a href="https://github.com/novoj/Utilities/blob/master/src/test/java/org/novoj/utils/datePattern/DatePatternConverterTest.java" target="_blank">testGetDate</a>.</p>
<p>[source lang="java"]<br />
/**<br />
* Tries to recognize date / time pattern from arbitrary string. Uses several decomposition patterns to recognize<br />
* proper value. It tries to make up missing parts in the natural way (current or initial date / time).<br />
*<br />
* @param dateAsString - user entered string<br />
* @param dateRequested - true if you expect some date value<br />
* @param timeRequested - true if you expect some time value<br />
* @param locale - locale used to parse string (passed to the SimpleDateFormat object)<br />
*/<br />
public Date getDate(String dateAsString, boolean dateRequested, boolean timeRequested, Locale locale) {<br />
   ...<br />
}<br />
[/source]</p>
<p>Integrace v naší aplikaci pak spočívá v tom, že vývojář pouze specifikuje základní datumový formát, který očekává (tj. např. "d.M.yyyy H:mm") a konvertor se primárně pokusí datum parsovat proti tomuto formátu. Pokud konverze selže, normalizuje vstup uživatele do zjednodušené podoby a pokusí se aplikovat další "standardní" datumové formáty. Pokud se datum nepodaří z řetězce získat, vrací se NULL hodnota.</p>
<p>Parser se snaží domyslet si konvenčním způsobem chybějící hodnoty. Tj. pokud očekáváte plné datum - d.M.yyyy a uživatel zadá pouze řetězec "2011", vy jako vývojář dostanete celou hodnotu - pokud vložený rok odpovídá aktuálnímu, doplní se jako den a měsíc dnešní den jinak se použije 1. leden. Vzhledem k tomu, že nečekáte časovou hodnotu bude v Date objektu čas vynulován.</p>
<p>Vzhledem k tomu, že takto se snaží "počítač" přemýšlet za uživatele, může se jednoduše stát, že datum neuhodne správně. Měli bychom tedy uživateli ještě před finálním použitím hodnoty (např. uložení do databáze) oznámit, jak jsme si jeho vstup domysleli, aby mohl případně svou hodnotu dále doplnit nebo napsat správně, když se naše logika netrefila do toho, co uživatel zamýšlel.</p>
<p><i><strong>Pozn. na okraj:</strong><br />
Možná si říkáte, zda není toto řešení v době různých sexy javascript datePickerů zbytečné, ale my často narážíme na případy, kdy je použití datePickeru kontraproduktivní - třeba v případě, že očekáváme datumy, které jsou daleko v minulosti nebo v budoucnosti (typicky třeba datum narození). V takových případech je výběr datumu přes datePicker spíš pro zlost. Navíc ve formulářích, které se používají často, je vložení datumu přes klávesnici (pokud nemusím myslet na formát) často rychlejší než zběsilé klikání v datePickeru.</i></p>
<p>Pokud vás zajímá, jak to celé vypadá v praxi, přeskočte <a href="#demo">na poslední odstavec</a> tohoto článku.</p>
<h2>Integrace Javy a jQuery UI DatePicker</h2>
<p>Druhý problém, který jsem v souvislosti s předěláním práce s datumy řešil, byl převod Java formátu datumu na JavaScriptový formát používaný v jQueryUI komponentě datePicker. Když se podíváte na dokumentaci (<a href="http://docs.jquery.com/UI/Datepicker/formatDate" target="_blank">datePicker</a>, <a href="http://trentrichardson.com/examples/timepicker/" target="_blank">timePicker addon</a>), brzy zjistíte, že formáty požadované JavaScriptovými komponentami se od Javovských liší a tudíž musí vývojáři zadávat buď datumové formáty 2x nebo musíte zajistit konverzi jednoho formátu do druhého.</p>
<p>Jelikož nám jde o zrychlení vývoje, nechci po dalších vývojářích, kteří budou používat moji datumovou komponentu, aby znali implementační detaily a studovali dokumentaci ze tří zdrojů. Vydal jsem se tedy cestou konverze - v třídě <a href="https://github.com/novoj/Utilities/blob/master/src/main/java/org/novoj/utils/datePattern/DatePatternConverter.java" target="_blank">DatePatternConverter</a> najdete tyto metody:</p>
<ul>
<li>javaToJavascriptDatePatternConversion</li>
<li>javaToJavascriptTimePatternConversion</li>
<li>getDateAndTimeDelimiter</li>
</ul>
<p>Ty se starají o konverzi Java SimpleDateFormat patternu na cílové patterny pro výše zmíněné dvě JavaScriptové komponenty. Třetí metoda vám vrátí případný řetězec, který má datum a čas spojovat dohromady. Použití a funkcionalita je nejlépe čitelná z <a href="https://github.com/novoj/Utilities/blob/master/src/test/java/org/novoj/utils/datePattern/DatePatternConverterTest.java" target="_blank">JUnit testů</a>.</p>
<p>Musím přiznat, že s touto věcí jsem se bavil celý jeden den. Na první pohled to ale nevypadá jako složitý úkol, že?</p>
<h2 id="demo">Ukázka funkcionality na prototypu</h2>
<p>Na tomto videu se můžete podívat jak to celé funguje v praxi. Při použití těžíme z tzv. živé validace, která na pozadí provádí komunikaci se serverem a validuje hodnoty hned jak je uživatel zadá. Tím mu dokážeme okamžitě také propagovat návrhy oprav ze strany serveru:</p>
<div align="center">
<iframe width="425" height="349" src="http://www.youtube.com/embed/1jwVKEDVtiE?hl=cs&fs=1" frameborder="0" allowfullscreen></iframe>
</div>
<p>To, co se mě na tom celém líbí nejvíc, je to, že vývojáři, který bude formuláře nakonec skládat, stačí jen hezky ostylovat zprávy zobrazující se vedle vstupních polí a na serverové straně deklarovat použité validace. Všechno ostatní už dostává zadarmo.</p>
<h2 id="sources">Zdroje</h2>
<p>V závěru bych rád uvedl několik odkazů na články, které nás přinutily k sebereflexi a změně práce s formuláři. Minimálně bych rád doporučil první článek, na jehož základě jsem v podstatě postavil principy naší živé validace (a které obdobně respektuje i <a href="http://bassistance.de/jquery-plugins/jquery-plugin-validation/" target="_blank">jQuery Validation</a> plugin):</p>
<ul>
<li><a href="http://www.alistapart.com/articles/inline-validation-in-web-forms/" target="_blank">Výsledky uživatelského testování inline (živé) validace</a></li>
<li><a href="http://manwithnoblog.com/2011/05/09/bad-interfaces-getting-dates-wrong/" target="_blank">Práce s datumy ve formulářích</a></li>
<li><a href="http://www.lukew.com/resources/articles/EventApart_WebForms_120809.pdf" target="_blank">Obecné praktiky při návrhu formulářů a jejich dopady (slidy z prezentace)</a></li>
</ul>
