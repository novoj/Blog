---
status: publish
published: true
title: Názvy argumentů metod v reflexi
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Člověk neznalý věci by mohl nabýt dojmu, že přes reflexi v Javě půjdou získat
  všechny informace, které se v signaturách tříd a metod nacházejí. Reflexe v Javě
  je skutečně velmi mocná, nicméně k některým informacím se nedostává jednoduše (<a
  href=\"http://blog.novoj.net/2010/03/19/orisek-v-reflexni-analyze-generik/\" target=\"_blank\">jak
  jsme si ukázali v minulém článku</a>) a k některým se bohužel nedokážete dostat
  vůbec. Do té posledně jmenované kategorie právě patří názvy argumentů metod. A právě
  o nich se chci dnes rozepsat.\r\n\r\n"
wordpress_id: 871
wordpress_url: http://blog.novoj.net/?p=871
date: '2010-04-26 11:29:13 +0200'
date_gmt: '2010-04-26 10:29:13 +0200'
categories:
- Programování
- Java
tags:
- reflection
comments:
- id: 22244
  author: Maaartin
  author_email: grajcar1@seznam.cz
  author_url: ''
  date: '2010-04-26 12:39:48 +0200'
  date_gmt: '2010-04-26 11:39:48 +0200'
  content: "Tentokrat se da jen souhlasit. Soucasna situace neni dobra a hned tak
    se nezlepsi. Zajimalo by me jestli ty jmena pouzivas jen u vlastnich trid nebo
    i u cizich. Myslim ze pouzivat to u cizich je nebezpecny a zbytecny, mam pravdu?\r\n\r\nSun
    ma pravdu v tom, ze timto se jmena parametru stavaji soucasti signatury. No ale
    kdyz je to potreba, tak s tim mel neco delat.  Me by se libilo zavest annotaci
    (pro metody i pro cely tridy), ktera by rekla, ze tomu tak je a v tom pripade
    zpristupnit jmena parametru v reflexi. Tim by to bylo jasne dany a namitky Sunu
    by padly. Nevim jestli by to takhle stacilo, zkusenosti s tim nemam."
- id: 22245
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-04-26 13:02:25 +0200'
  date_gmt: '2010-04-26 12:02:25 +0200'
  content: "No jde pouze o vlastní třídy - typicky metody mého vlastního DAO objektu,
    v Grails se může jednat o parametry metody opět vlastního controlleru pro automatické
    injektování parametrů z HTTP requestu a podobně. Tj. skutečně bych řekl, že ve
    valné většině případů člověk cizí obecně použitelná knihovna má zájem na čtení
    argumentů \"klientského\" kódu - tedy toho co píšu já. Stěží to bude někdo chtít
    dělat obráceně.\r\n\r\nTy anotace by byly řešením, věřím, že když by si na to
    pár mozků dalo ten čas, tak se třeba přijde i s lepším řešením. Ale evidentně
    není vůle."
- id: 22253
  author: Michael
  author_email: email@example.com
  author_url: ''
  date: '2010-04-26 20:48:33 +0200'
  date_gmt: '2010-04-26 19:48:33 +0200'
  content: "Na 101 % suhlasim, hlavne co sa tyka tych poslednych bodov a prikladu
    ACEGI, neskutocne co clovek zazije kym to dostane tam kam chce :)\r\n\r\nTreba
    sa ale pozriet na vec aj inym pohladom. Nemusi to byt nutne \"zle\" rozhodnutie.
    S velkou pravdepodobnostou je za tym kopec studii. Kazdemu sa stane pri pisani
    kodu, ze niekde\r\nna kraji mu nenapadne \"dobre\" meno nejakeho parametra - pripadne
    nie je cas riesit\r\nnazov ... meno sa zabudne, necha sa tam (u mena metody si
    clovek da zalezat o 26 % viac :))... Problem by to nebol ak by za cely zivotny
    cyklus\r\nspravoval 1 az dvaja ludia. Prax je vsak casto ina - casti systemov
    su pouzivane a customizovane\r\n\"kade - tade\" a casto ani autor sa neodvazi
    zmenit co-i-len nazov public metody, zmazat, ci inak upravit. Nie je to zly management
    kodu - takto to byva. Neda sa preto povedat - \"nechajme to na developerov\" -
    to ozaj nie. Chapem, preco to tvrdis, lebo vies, ze vies, ... lenze ... nie kazdy
    vie.\r\n\r\nTeda nie je zle dat konovi klapky na oci aby siel kam by mal. Poriadok
    je naozaj potrebny.\r\nSamozrejme, ... o vsetkom sa da polemizovat. Treba to vnimat
    ako jednu z vyhod jazyka ...\r\na hned bude svet ruzovejsi :)\r\n\r\nPrilisna
    benevolencia muoze totizto viest k anarchii - a teda treba skuor pozerat na to\r\npreco
    je to tak a nie preco to nie je inak ... tiez netvrdim, ze je vsetko idealne ...\r\n\r\nKeby
    som mal riesit problem potreby nazvou parametrov ja - urcite raz budem - najprv
    si uvedomim\r\npreco vlastne potrebujem nieco take ... casto to naznacuje zlu
    cestu - povedal by som prekrocenie\r\nurovne abstrakcie za \"rozumnu\" hranicu
    ..."
- id: 22255
  author: benzin
  author_email: bendal@quick.cz
  author_url: ''
  date: '2010-04-26 22:18:36 +0200'
  date_gmt: '2010-04-26 21:18:36 +0200'
  content: "Existuje jeste jedna varianta a taky je pomerne prehledna:\r\n\r\n@ParamsNames({\"title\",
    \"description\", \"author\", \"publishedDate\"])\r\nArticle createArticle(String
    title, String description, Author author, Date publishedDate);\r\n\r\nJe to sice
    trosicku ukecanejsim, ale prehledne stejne jako Vas navrh. Navic tu anotaci stejne
    musite osetrovat (v nejake podobe), prave proto aby pri zmene jmena parametru
    se zavyslosti nerozvezly.  Tohle je schopne doplnovat rovnou IDE, nebo prave nejaky
    pridavny predkompilacni tool a tak neni skutecne potreba zasvinovat jazyk necim
    co je resitelne a pritom v drtive vetsine pripadu nepotrebne.\r\n\r\nNavic zapsat
    to treba takhle:\r\n@ParamsNames\r\nArticle createArticle(String title, String
    description, Author author, Date publishedDate);\r\nA pak na to nasadit APT (http://java.sun.com/j2se/1.5.0/docs/guide/apt/GettingStarted.html,
    http://www.javalobby.org/java/forums/t17876.html) vyresi problem taky a nezasvinite
    si specifikaci kvuli mensinovym problemum.\r\n\r\n\r\nA naposled. Standardem jak
    tohle resit v Jave, jsou beany. Proste do metody nevstoupi pet paramteru stejneoh
    typu a ruzneho jmena, ale jedna beana (nebo dve, ci tri), jejichz property odpovidaji
    parametrum puvodni metody.\r\n\r\nDalsi mozne reseni je definovat pro ruzne typy
    parametru ruzne potomky stejne tridy napr.\r\nclass StringHolder {\r\n  getString(...);
    setString(...);\r\n}\r\n\r\nclass Title extends StringHolder{};\r\nclass Description
    extends StringHolder();\r\nclass PublishDate extends Date();\r\natd. \r\n\r\nUzivatel
    vaseho frameworku, pak do dane metody necha vstoupit promene takovych typu, jejichz
    hodnotu potrebuje. Takze vase metoda pak vypada takto:\r\n\r\nArticle createArticle(Title
    title, Description description, Author author, PublishDate publishedDate)\r\n\r\nP.S.:
    Osobne nemam rad frameworky bazirujici na stringovych jmenech, pri preklepu Vas
    pak kompilator neopravi. Chapu ze ne vzdy se tomu da vyhnout, ale je-li cesta
    (napr. generovanim tridyu pro kazdy typ parametru), tak si myslim ze je lepsi."
- id: 22258
  author: Maaartin
  author_email: grajcar1@seznam.cz
  author_url: ''
  date: '2010-04-26 23:08:28 +0200'
  date_gmt: '2010-04-26 22:08:28 +0200'
  content: "&gt; Kazdemu sa stane pri pisani kodu, ze niekde\r\n&gt; na kraji mu nenapadne
    “dobre” meno nejakeho parametra\r\n\r\nStejne tak jako u public metody, i kdyz
    tam ne tak casto. To je ale tim, ze public metody jsou videt zvenku, takze clovek
    si proste da vic bacha. Se tou specialni anotaci co jsem navrhoval by autor zadeklaroval
    ze jmeno parametru patri k signature, takze by se nad nim vice zamyslel.\r\n\r\nA
    o nic vic nejde, chyba se stat muze vzdy, (aspon) jednou se dokonce preklep propracoval
    do standardu (\"http-referer\").\r\n\r\n&gt; Tohle je schopne doplnovat rovnou
    IDE, nebo prave nejaky pridavny predkompilacni tool\r\n&gt; a tak neni skutecne
    potreba zasvinovat jazyk necim co je resitelne a\r\n&gt; pritom v drtive vetsine
    pripadu nepotrebne.\r\n\r\nMe se zas nelibi nechat si zasvinovat zdrojak pomoci
    IDE - prece jen se to vickrat cte nez pise.\r\n\r\n&gt; A pak na to nasadit APT...\r\n\r\nTo
    se mi libi, ale nemyslim si ze by to bylo trivialni udelat. S APT snad nic neni
    trivialni, poptam se na to.\r\n\r\n&gt; Standardem jak tohle resit v Jave, jsou
    beany.\r\n\r\nAno, ale ukecany a pracny. Je pak potreba vsude \"castovat\" String
    na Description a zpet, to by slo v C++ automaticky ale v Jave to znamena dost
    psani. Nekde to muze byt i vyhodou, clovek aspon vi, s cim dela.\r\n\r\nTy beany
    maji jeste jednu nevyhodu: Kdyz nekam predam String, tak vim, ze mi ho (bez pomoci
    Unsafe) nikdo nezmeni, ne tak kdyz pridam Description. Radeji immutables."
- id: 22265
  author: benzin
  author_email: bendal@quick.cz
  author_url: ''
  date: '2010-04-27 07:49:15 +0200'
  date_gmt: '2010-04-27 06:49:15 +0200'
  content: "Ja sem samozrejme navrhl nekolik reseni. Neznam konkretni problem, ktery
    se tim resi.\r\n\r\nCo se toho stringu tyce, tak tam je naprd, to ze se neda ze
    stringu udelat potomek protoze je final jinak by to problem nebyl.\r\n\r\nTo s
    tim ctenim a psanim kodu, s probiralo i u protertie. ja je konkretne pisu takhle:\r\n\r\npublic
    class Trida {\r\n  private String property; public String getProperty() { return
    property; } public void setProperty(String property) { this.property = property;
    }\r\n}\r\n\r\nAniz bych potreboval menit jazyk JAVA, mam property, ktera je napsana
    na jednom radku, je to dobre citelne, protoze proste zbytek radku s get a set
    metodama proste nectu. I tohle je problem spise IDE a formatovani nez jazyka.
    Preci neni vubec problem si \"nepodstatne\" anotace nechat zkryt / sbalit. Navic
    anotace nad metodou s vyctem jmen promenych kod prilis nezneprehledni.\r\n\r\nRuku
    na srdce, je skutecne tohel tak obrovsky a neresitelny problem, aby bylo potreba
    menit specifikaci jazyka? Preci i nevabne smeti se sklada ze spousty jednotlivych
    drobnych odpadku, ktere nevabne nejsou."
- id: 22266
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-04-27 07:56:04 +0200'
  date_gmt: '2010-04-27 06:56:04 +0200'
  content: "Maaartin už stihnul odpovědět v duchu, ve kterém bych odpovídal já a proto
    to nebudu opakovat. Všechny uváděné návrhy jen duplikují informaci, která je již
    obsažená v původní signatuře metody, v názvech argumentů (a některé tedy dost
    pracně). A jak všichni dobře víme, zdvojování informací vede pouze k nepřehlednosti
    a dalším chybám.\r\n\r\nPodle mého názoru stačí pouze jasně říct, v čem je tato
    technika nebezpečná a že i názvy argumentů jsou součástí rozhraní. Argumentování
    tím, že jsem se mohl v názvu argumentu uklepnout a chtěl bych to mít možnost bez
    rizika v dalších verzích opravit je zcestný - stejnou chybu jsem přeci mohl udělat
    i při psaní anotace nebo názvu metody a v takovém případě mám problém už za současné
    situace.\r\n\r\nDalší věc - schválně se zkuste zamyslet nad tím, jestli v názvech
    argumentů chybujete častěji než v názvech metod - já tedy ne. Co se týká zmíněných
    použití (iBatis, Grails atd.) - zde je na první pohled jasné a jasně zdokumentované,
    že názvy argumentů hrají roli, protože se mapují na nějaká externí data (názvy
    sloupců v db, názvy paramterů v URL atd.). Řekněte mi, kdo by se mohl v daném
    případě cítit zmatený? Tady jsou argumenty jasně součástí API, což lze jednoduše
    prověřit testy - ty také zajistí i rychlé zjištění chyb v případě změny API.\r\n\r\nOsobně
    v tom vidím jen riziko v případě, že se to někdo bude snažit zneužívat, jenže
    v takovém případě už máme řadu jiných podobných nástrojů, které se také dají zneužívat
    a také nám nevadí (například setAccessible(boolean) že?).\r\n\r\nOsobně v tom
    faktický problém nevidím, a nutnost současný stav obcházet nějakým šíleným oprogramováváním
    se mi příčí."
- id: 22270
  author: benzin
  author_email: benzin@centrum.cz
  author_url: ''
  date: '2010-04-27 10:45:22 +0200'
  date_gmt: '2010-04-27 09:45:22 +0200'
  content: "4Otec Fura. Kde je problem:\r\n\r\nInterface X Class - Ktere jmeno parametru
    bude mit prednost?\r\nPredek X Potomek - ktery metodu prekryva, nebo implementuje.
    - Ktere jmeno bude mit prednost\r\n2x Interface (stejna metoda, jina jmena promenych)
    \ implementovano jednou tridu - Ktere jmeno bude mit prednost?\r\n\r\nA to vsechno
    jak dopadne kdyz pouzijeme JDK proxy? A kdyz pouzijeme CGLIB proxy? A budou dalsi
    nekompatibility pri zamene techto proxy?\r\n\r\nBude nutne aby jmena v implementaci
    rozhrani byly stejne jaako ve tridach? To ale bude strasne z hlediska zpetne kompatibility.
    A taky se dostanete do problemu pri immplementaci dvou rozhrani s ruznymi jmeny
    promenych, ale stejnym jmenem metody.\r\n\r\nNemyslim, ze je tady pekne reseni."
- id: 22273
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-04-27 12:01:41 +0200'
  date_gmt: '2010-04-27 11:01:41 +0200'
  content: "Ok, to beru jako argument - nicméně pravidlo by mohlo být jednoduché -
    vrátí se mi to na co se zeptám. Kdy si dám class.getSuperClass().getDeclaredMethod(\"blabla\")
    dostanu se k názvům uvedeným v deklaraci předka, když zavolám class.getDeclaredMethod(\"blabla\")
    dostanu názvy argumentů přetížené metody (stejně tak i v případě interfaců).\r\n\r\nNezdá
    se mi to nijak proti srsti. V případě knihoven co jsem jmenoval (iBatis, Grails)
    by byly zajímavé právě jen ty argumenty té konkrétní \"klientské\" třídy - tedy
    té nejníž v chainu dědičnosti. Co se týká JDK Proxy nebo Cglibu, taky by neměl
    být problém."
- id: 22275
  author: benzin
  author_email: benzin@centrum.cz
  author_url: ''
  date: '2010-04-27 12:24:11 +0200'
  date_gmt: '2010-04-27 11:24:11 +0200'
  content: "4Otec Fura: Prave ze bude. protze JDK proxy prebira jmena z interace a
    ne ze tridy. Takze kdyz ti pak do ruky vlitne proxy trida splnujici urcity interace,
    tak se nikdy nedozvis jake jmena metod na proxovana instance. Naproti tomu CGLIB
    proxy to dela  (pokud vim) jako potomka predka, takze se ke jmenum dostat muzes.\r\n\r\nProblem
    je v tom, ze tohle muze mit docela nepekne dopady a neni to az tak trivialni,
    takze se nedivim ze se to odklada. Protoze vzdycky tu bude reseni vyhovujici jednem
    a nevyhovoujici druhym. Navic tu porad existuje reseni sice ukecane, ale exsituje.
    A konkretne property, ktere trapi daleko vetsi mnozstvi vyvojaru, porad nenaslo
    uspokojive resen (pokud teda vim). Podobne je tomu s generikama, ze se k nim nedostanes
    za behu, to mi prijde taky jako daleko vetsi problem nez jmena parametru."
- id: 22277
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-04-27 13:02:40 +0200'
  date_gmt: '2010-04-27 12:02:40 +0200'
  content: "Ano JDK Proxy staví pouze na interfacech, kdežte Cglib odvozuje ze superclass
    + umožňuje implementovat libovlné ifacy - tj. v tomto případě bych s instancí
    vůbec neoperoval. U proxy dopředu nikdy nevíš co vlastně wrapují a jestli něco
    wrapují. Tohle se mi nechce moc brát jako argument.\r\n\r\nNicméně souhlasím s
    tebou, že nic není triviální, jak se na první zdá. Určitě by se komplikace našly.
    Je otázka jak problematicky jsou řešitelné. Skutečně už je v Javě dost znát ta
    stále narůstající koule s nálepkou zpětná kompatibilita.\r\n\r\nCo se týká generik,
    tak ty přes reflexi v runtime dostupné jsou. Jen se nedostaneš na konkrétní hodnoty
    wildcard generik - tam máš k dispozici jen \"bounds\". Viz. minulý článek."
- id: 22292
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-04-28 04:47:55 +0200'
  date_gmt: '2010-04-28 03:47:55 +0200'
  content: "@benzin teď mi dochází, že v případě dynamických proxy, které musí implementovat
    jmenované interfacy by muselo dojít pro implementované metody k reflexní analýze
    původních argumentů, tak aby implementované metody držely stejné názvy. Tohle
    mi při psaní minulého příspěvku úplně nedocvaklo, ale principielní problém to
    řekl bych neznamená."
- id: 22299
  author: benzin
  author_email: benzin@centrum.cz
  author_url: ''
  date: '2010-04-28 12:26:57 +0200'
  date_gmt: '2010-04-28 11:26:57 +0200'
  content: "4Otec: No ale dost to omezuje pouziti takovych jmen. Protoze musis vzdycky
    jeste nejak ziskat puvodni klasu. Nemuzes se spolehnout ze ta kterou ziskas z
    obektu ti staci. Je to podobny problem jako u anotaci. V podstate by stacilo jenom
    pri buildovani automaticky prihodit anotaci se jmenama promenych k metode. Ale
    to by presne mel resit ATP.\r\n\r\nMne spise vadi absence aspektu v zakladni jave
    a k tomu samozrejme i kontraktovaci api.\r\n\r\nAle ono je toho strasne moc co
    by v jave mohlo byt a neni tam a pritom v jinych jazycich to je. Napr. v Lispu
    je obdoba aspektu od sameho pocatku - tusim se to menuje hook. Na druhou stranu
    sem ale rad, ze je Java porad docela konzervativni. Prave z Pythonem, mam docela
    nepekne zkusenoti prave se zpetnou kompatibilitou, vzhledem k tomu ze dost velka
    cast KDE  a Gnome (a utilit pro neho) je psana v Pythonu, tak sem si prosel peklem,
    kdyz sem nechte upgradoal na novou verzi."
- id: 22302
  author: Maaartin
  author_email: grajcar1@seznam.cz
  author_url: ''
  date: '2010-04-28 13:53:50 +0200'
  date_gmt: '2010-04-28 12:53:50 +0200'
  content: "Ja bych to nekomplikoval a zustal u\r\n&gt; Ok, to beru jako argument
    – nicméně pravidlo by mohlo být jednoduché – vrátí se mi to na co se zeptám.\r\na
    to jen v pripade ze tam je anotace @ParameterNames (v opacnym pripade predpokladam
    ze autor s tim nepocital a ty jmena pripadne nekdy zmeni). Tim odpada i nutnost
    pamatovat si pripadne stary jmena parametru - to je pak stejne absurni jako pamatovat
    si stary jmena public metod.Jen bych to namisto toho APT dal do rovnou Javy, aby
    se na to lezlo pres\r\nString[] Method.getParameterNames()\r\n\r\nDedeni bych
    taky neresil, nedokazu si predstavit, ze by programator nevedel kterym smerem
    v hierarchii se vydat - pokud tam mam dynamicky proxy, tak vim jestli se vygenerovaly
    k mymu interfejsu nebo k my tride. Zadny konflikty by tez nebylo treba resit,
    pripadne by si poresil programator kdyby si je tam nadelal - coz si tez moc neumim
    predstavit.\r\n\r\nVyhodpu oproti APT by byla prenostitelnost (to APT je treba
    delat pro kazdy prekladac znova a muze se bit s jinym APT) a standardizace (rozumnel
    by tomu i Javadoc a jmena patricne zvyraznoval).\r\n\r\n&gt; 4Otec: No ale dost
    to omezuje pouziti takovych jmen....\r\nMe se nezda ze by to byl vubec problem,
    protoze tam kde bych to pouzil bych i presne vedel kam mam jit. Normalne bych
    to pouzil jen pro jeden druh objektu, rekneme pro entity a kdyz jsem je napsal
    jako tridy, tak musim u proxy jit k predkovi, atd. (uz bych se opakoval).\r\n\r\nVic
    mi vadi, ze to nepujde pouzit pro neco jako konstruktor\r\n\r\n@com.google.inject.Inject\r\nArticle(@Named(\"title\")
    String title, @Named(\"description\") String description, Author author,  Date
    publishedDate)\r\n\r\n(to Named jsem schvalne pouzil jen kde je potreba), ale
    k tomu me vazne nic nenapada."
- id: 22330
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-04-29 20:09:03 +0200'
  date_gmt: '2010-04-29 19:09:03 +0200'
  content: "@benzin na tomhle se asi shodneme -  konzervatismus má taky své klady\r\n\r\n@Maartin
    s tou anotací to není úplně špatný nápad, ale kdyby to šlo bez ní, bylo by to
    přeci jen nejlepší - jde mi přeci taky o úsporu kódu, zjištění těch argumentů
    se skutečně může odehrávat podobně jako to v současnosti děláme u anotací, tam
    také musíme skenovat hierarchickou strukturu (a jde to ;-) )\r\n\r\n@vsem díky
    za podnětné komentáře, jsem rád, že se podařilo trošku rozproudit diskusi"
- id: 22377
  author: Maaartin
  author_email: grajcar1@seznam.cz
  author_url: ''
  date: '2010-05-02 03:03:46 +0200'
  date_gmt: '2010-05-02 02:03:46 +0200'
  content: Ta anotace by stacila jedna pro tridu, to neni zrovna moc psani. Nebo pro
    pakaz, kdyz by se dala k package-info.java. Tou anotaci autor prohlasi, ze jmena
    argumentu zustanou stabilni; bez ni by to byla tak trochu ducharina - marne ale
    vzpominam, jestli jsem kdy jmeno argumentu menil.
---
<p>Člověk neznalý věci by mohl nabýt dojmu, že přes reflexi v Javě půjdou získat všechny informace, které se v signaturách tříd a metod nacházejí. Reflexe v Javě je skutečně velmi mocná, nicméně k některým informacím se nedostává jednoduše (<a href="http://blog.novoj.net/2010/03/19/orisek-v-reflexni-analyze-generik/" target="_blank">jak jsme si ukázali v minulém článku</a>) a k některým se bohužel nedokážete dostat vůbec. Do té posledně jmenované kategorie právě patří názvy argumentů metod. A právě o nich se chci dnes rozepsat.</p>
<p><a id="more"></a><a id="more-871"></a></p>
<p>Ve většině scénářů vás názvy parametrů zajímat nebudou, ale pokud byste chtěli koketovat s dynamickým generováním logiky tříd podle signatur metod - podobně jako to dělají například Grails nebo iBatis (a jistě i další), brzy narazíte na to, že by se vám tato znalost velmi hodila. Schválně porovnejte následující ukázkové signatury metod:</p>
<p>[source lang="java"]</p>
<p>Article createArticle(<br />
   String title, String description,<br />
   Author author, Date publishedDate<br />
);</p>
<p>Article createArticle(<br />
              @Param("title") String title,<br />
              @Param("description")String description,<br />
              @Param("author")Author author,<br />
              @Param("publishedDate") Date publishedDate<br />
);</p>
<p>Article createArticleWithTitleDescriptionAuthorPublishedDate(<br />
   String title, String description,<br />
   Author author, Date publishedDate<br />
);</p>
<p>[/source]</p>
<p>Jistě mi dáte za pravdu, že první varianta je nejpřehlednější a má dostatečně vypovídající hodnotu. Jenže zrovna s ní budete mít v Javě problémy. V reflexi se totiž dostanete pouze na typy těchto parametrů - tj. Class[] {String.class, String.class, Author.class, Date.class} a to vám k odvození toho, jakou informaci z parametru do jaké property POJO Article vložit, rozhodně nestačí. Že rozhodně nejste první člověk nepříjemně překvapený z tohoto faktu, zjistíte velmi jednoduše, když se <a href="Java method argument names reflection" target="_blank">zeptáte pana Gůgla</a>.</p>
<p>Kromě řady blogů vám dá asi nejpodrobnější a nejsrozumitelnější přehled <a href="http://paranamer.codehaus.org/" target="_blank">open source projekt s názvem Paranamer</a>. V něm se dočtete, jaké důvody vedly autory Javy k tomu, aby tuto informaci v reflexi nezpřístupnili:</p>
<p><cite>Sun had misgivings about the appropriateness of the this change to Java. It was felt that applications could end up depending on parameter names, and that they essentially became part of constructor/method signatures and could never be changed if you wanted to be backwards compatible.</cite></p>
<p>Vzhledem k tlaku skriptovacích jazyků a knihoven, které by rády tuto funkcionalitu využívaly, Sun nějakou dobu zvažoval doplnění této informace do reflexní části Javy, nicméně v JDK 6 se tak nestalo a podobná funkcionalita není plánována ani do JDK 7. Zdá se tedy, že s tímto faktem budeme muset ještě několik let žít.</p>
<p>Jak z této šlamastyky ven? Naštěstí nejsme první, kdo to řeší - potřeba už dohnala řadu lidí k tvorbě nějakých řešení. Bohužel každé z nich má své mouchy:</p>
<h2>Obohacování byte kódu</h2>
<p>Toto je právě primární způsob řešení zmiňované knihovny <a href="http://paranamer.codehaus.org/" target="_blank">Paranamer</a>. V rámci build procesu přidá do kompilovaných class statické pole __PARANAMER_DATA, do kterého uloží informace o všech metodách třídy, jejich argumentech a především názvech argumentů. Při volání metody:</p>
<p>[source lang="java"]<br />
String[] parameterNames = paranamer.lookupParameterNames(method)<br />
[/source]</p>
<p>potom Paranamer konzultuje právě toto pole, ze kterého získá požadované informace pro danou metodu. Paranamer poskytuje pluginy pro Maven2 a Ant. Co je však poměrně zásadní nedostatek jsou chybějící pluginy do IDE. Pokud budete tedy chtít využívat Paranamer v kombinaci s JUnit testy spouštěnými nad kódem kompilovaným z IDE, budete mít problém. Jinak je tato cesta jedinou skutečně funkční a použitelnou.</p>
<p>Pro parsování Java zdrojového kódu používá Paranamer knihovnu <a href="http://qdox.codehaus.org/" target="_blank">QDox</a>, která v mém případě měla v relativně aktuální verzi (nevím přesně - pravděpodobně to byla 1.9) problémy s některými generikami, což v kombinaci s Paranamer Maven2 pluginem způsobovalo selhávání buildu.</p>
<p>Nicméně vzhledem k současné situaci s JDK doufám, že Paranamer společně s QDoxem zmíněné problémy brzy vyřeší a půjde o obecně použitelný a uznávaný přístup k řešení této situace.</p>
<h2>Čtení debug informací z byte kódu</h2>
<p>Tento přístup je asi nejčastěji používaný - využívá toho, že když zkompilujete zdrojové kódy s debugovacími informacemi (<a href="http://java.sun.com/j2se/1.4.2/docs/tooldocs/windows/javac.html" target="_blank">javac -g</a>) budou názvy argumentů metody přeloženy do těla metody jako lokální proměnné, jejichž název bude možné z byte kódu zjistitelný. Jedná se o alternativní zjišťovací metodu v Paranameru a hlavní zjišťovací metodu ve Spring Frameworku, který se se stejným problémem potýkal také při psaní AOP podpory.</p>
<p>Ve Springu tudíž najdeme rozhranní <a href="http://grepcode.com/file/repo1.maven.org/maven2/org.springframework/spring-core/2.5.6/org/springframework/core/ParameterNameDiscoverer.java" target="_blank">ParameterNameDiscoverer</a> a jeho základní implementaci <a href="http://grepcode.com/file/repo1.maven.org/maven2/org.springframework/spring-core/2.5.6/org/springframework/core/LocalVariableTableParameterNameDiscoverer.java#LocalVariableTableParameterNameDiscoverer" target="_blank">LocalVariableTableParameterNameDiscoverer</a>, které nám právě umožňuje poptat se na názvy argumentů metod nebo konstruktorů. V jeho podání se názvy argumentů zjišťují takto:</p>
<p>[source lang="java"]<br />
//třída si cachuje výsledky a proto je poměrně výhodné držet ParameterNameDiscoverer jako singleton<br />
ParameterNameDiscoverer  pnd = new LocalVariableTableParameterNameDiscoverer();<br />
String[] argNames = pnd.getParameterNames(myMethodOrConstructor);<br />
[/source]</p>
<p>Tento přístup je možné bez dodatečné konfigurace použít jak ze všech build nástrojů (Ant, Maven2 ...), tak i z IDE - má bohužel také svou nevýhodu a to poměrně zásadní. Informace jsou dostupné pouze pro metody, které mají své tělo (tj. implementaci). U metod interfacu, nebo abstraktních metod jsou tyto informace nedostupné (neexistuje tělo metody, neexistují lokální proměnné a tudíž není odkud tuto informaci vzít). Tj. pro případy, kdy existuje pouze definice interface a implementace má vzniknout dynamicky je tento přístup nepoužitelný (např. problém u iBatisu v. 3).</p>
<h2>Čtení informací z JavaDocu</h2>
<p>Toto je poslední z variant, kterou nabízí Paranamer - nicméně zde musíte ke kompilovanému kódu dodat referenci na Javadoc archív (url), což není ve většině produkčních nasazeních možné.</p>
<h2>Závěrem</h2>
<p>Současný stav je tedy poměrně tristní. Jediným inženýrským rozhodnutím od stolu se zadělalo na nehezký problém, který se těžko obchází. Je mi vcelku jasný argument, že umožněním čtení názvů parametrů by se tato informace defakto stala součástí API, kterou není možné jednoduše měnit, aniž bychom se obávali naboření zpětné kompatibility.</p>
<p>Na druhou stranu, je čím dál víc zcela legálních případů, kdy by využití názvů metod vyloženě pomohlo dělat úsporná a přehledná API, čemuž je v současnosti efektivně zamezeno.</p>
<p>Buď jak buď, osobně toto rozhodnutí vnímám jako něco, co bylo rozhodnuto z pozice síly bez ohledu na potřeby Java vývojářů. To že je řešení této potřeby vyjmuto i z JDK 7 můj názor jen potvrzuje. V praxi jsem viděl už řadu podobných rozhodnutí, které ve výsledku vedly jen k daleko horšímu stavu, než kdyby původní autor API nechal uživatelům-vývojářům volnou ruku.</p>
<p>Jsou mi jasné motivy defenzivního návrhu API - co se ovšem stane v případě, že danou věc, kterou vám původní autor blokuje opravdu nutně potřebujete? Sám si odpovím, protože jsem to už párkrát sám musel dělat :</p>
<ul>
<li>přistoupíte k privátním polím a metodám přes reflexi s přenastavením accessible flagu</li>
<li>zkopírujete obsah původní třídy / metody do své vlastní</li>
<li>forknete zdrojové kódy knihovny, provedete nutné vlastní úpravy a vytvoříte si vlastní build</li>
<li>provedete úpravy byte kódu za běhu</li>
<li>zahodíte celou knihovnu a její funkcionality, které by se vám sice hodily, ale pro svůj případ je prostě neohnete</li>
</ul>
<p>Při psaní API podle si podle mého názoru musíme být vědomi toho, že nikdy nejsme z pozice autora schopni odhadnout všechny případy použití, na které bude knihovna ve výsledku použita. Také musíme uvědomit, že pokud naše skvěle defenzivně napsané API nebude konkrétní věc umožňovat, donutíme zoufalého vývojáře použít jakéhokoliv prostředku, aby naši ochranu probil a výsledek bude potom jenom horší. Vše je hnáno motivem zachování zpětné kompatibility, ale zkusme trochu více věřit ostatním vývojářům, zkusme si věřit sobě navzájem.</p>
<p>Skvělé API nemusí být přespříliš defenzivně psané - Spring Framework je toho skvělým příkladem. A pokud mám jmenovat knihovny na opačné straně spektra určitě budu nerad vzpomínat třeba na jCaptchu nebo i na Acegi Security.</p>
<p><a href="http://en.wikipedia.org/wiki/Power_to_the_people_(slogan)" target="_blank">Power to the people!</a></p>
