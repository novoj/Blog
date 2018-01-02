---
status: publish
published: true
title: Debugging v praxi - opravdu samozřejmost?!
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<p>V poslední době jsem zjistil, že některé věci, které já považuji za samozřejmé,
  pokud se rozhlédnu kolem sebe, tak úplně samozřejmé nejsou. Jednou z nich je debugování
  Javovského kódu. I v dnešní době, kdy je podpora ze strany technologií na perfektní
  úrovni je mnoho vývojářů, kteří pro rutinní vývoj (nemluvím o řešení problémů po
  nasazení aplikace) a odlaďování kódu debuggování nepoužívají a spoléhají se na záznamy
  z logu. Je pravda, že tento přístup má své výhody – obvykle se tímto způsobem obohatí
  kód dostatečným množstvím logů, že i v produkci je obvykle dost informací k řešení
  problémů, pokud nastanou. Zásadní nevýhodou, kterou v tom spatřuji já je naprosto
  drastické snížení produktivity programování. Problém, který se dá vyřešit během
  půl minuty vložením breakpointu na správné místo v kódu se může v případě procházení
  logů protáhnout klidně i na pět minut. Flow programátora je potom – však vy víte
  kde :).</p>\r\n\r\n<p>Proto tento článek věnuji těm, kteří debugging nepoužívají
  nebo měli nějaké problémy s jeho zprovozněním.</p>\r\n\r\n"
wordpress_id: 13
wordpress_url: http://blog.novoj.net/2007/04/09/debugging-v-praxi-%e2%80%93-opravdu-samozrejmost/
date: '2007-04-09 19:04:49 +0200'
date_gmt: '2007-04-09 18:04:49 +0200'
categories:
- Java
tags: []
comments:
- id: 40
  author: štěpán
  author_email: stepan.vacek@cleverlance.com
  author_url: ''
  date: '2007-04-10 11:20:39 +0200'
  date_gmt: '2007-04-10 10:20:39 +0200'
  content: Myslím si, že debugování a logování se navzájem doplňují. Debugování programátor
    použije, pokud potřebuje odladit chybu nebo problematickou část, a logováním zjistí,
    že chyba (vůbec) nastala a za jakých podmínek - volání metody nebo interakce s
    DB se loguje včetně parametrů. Právě kvalitní logovací data z produkce jsou neocenitelné
    ;-) zkoušet "nasimulovat" chybu, pouze pokud máte informaci z logu že nastala,
    je šílený.
- id: 41
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-04-10 12:38:58 +0200'
  date_gmt: '2007-04-10 11:38:58 +0200'
  content: Ano, souhlasím - nikterak taky logování nezatracuji - naopak. Spíš mi jde
    o to, že ladit aplikaci na vývojovém prostředí pomocí logů se mi zdá hrubě neproduktivní.
    Proto jsem celý tento článek napsal. Bez kvalitních logů se v runtime rozhodně
    nedá obejít.
- id: 42
  author: Petr Ferschmann
  author_email: pferschmann@softeu.com
  author_url: http://blog.softeu.cz/
  date: '2007-04-10 18:33:04 +0200'
  date_gmt: '2007-04-10 17:33:04 +0200'
  content: "Zdravím,\r\n\r\nmusím říct, že jsem -Djava.compiler=NONE nikdy nepoužíval
    a funguje mi vše i bez něj. Prostě to funguje jak by člověk čekal. Určitou eliminaci
    nepoužívaného kódu už dělá Java Compiler a tak už to obvykle v době běhu JIT odstraněné
    je."
- id: 48
  author: david
  author_email: bmfv@seznam.cz
  author_url: ''
  date: '2007-04-12 19:59:55 +0200'
  date_gmt: '2007-04-12 18:59:55 +0200'
  content: "Dik za zajimavy clanek...Chtel bych se jen zeptat, proc volite tenhle
    vzdaleny debug misto debugu u sebe na localhostu? Po pravde jsem se s tim setkal
    poprve, proto by me zajimalo, jaky to prinasi vyhody... \r\nDik za odpoved"
- id: 49
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-04-13 05:29:55 +0200'
  date_gmt: '2007-04-13 04:29:55 +0200'
  content: "A to je právě jedna z věcí, které jsem se snažil v článku trochu osvětlit
    - ale asi se mi to moc nepovedlo. On totiž není žádný \"remote\" a \"local\" debugging
    (tedy v tom základním slova smyslu). To co jsem v článku popsal je totiž ten \"standardní\"
    a \"jediný\" způsob debuggingu v té podobě, v jaké skutečně funguje. Pokud si
    prohlédnete ta videa, tak i já jsem debuggoval kód na lokálním Tomcatu.\r\n\r\nNa
    první pohled by se mohlo zdát, že existují i \"jiné\" způsoby jak debuggovat než
    ten co jsem uvedl - vždyť v IDE obvykle můžu vybrat přímo typ web / aplikačního
    serveru a ten si z IDE spustit a zároveň i debuggovat. Jenže v reálu to znamená,
    že IDE jen udělá automaticky to, co jsem já v ukázkách dělal ručně. Když spustíte
    např. Tomcat z IDE - spustí se vám nová instance Tomcatu, která je v seznamů procesů
    systému viditelná jako samostatný proces (odpovídá tomu, jako byste ručně spustili
    catalina.bat nebo catalina.sh). Pokud si z IDE nadeployujete a spustíte v debug
    režimu svou aplikaci do Tomcatu - IDE jen automaticky provede to, co já jsem ukázal
    \"ručně\". \r\n\r\nTen \"remote debugging\" výraz jsem vzal z termínu IDE IntelliJ
    IDEA, která tím označuje způsob připojení se k již existující instanci java aplikace
    v debug režimu (např. k tomu Tomcatu) - v Netbeans to je Attach Listener a v Eclipsu
    to bude asi zase něco jiného. Ale to remote nemá skutečný význam v tom, že bych
    debugoval kód na jiném serveru (i když bych mohl a fungovalo by to).\r\n\r\nJe
    však dobré vědět, co se děje na pozadí a jak to ve skutečnosti funguje, protože
    někdy můžete mít v IDE problémy s předpřipravenou podporou serverů. Například
    jsem si stáhnul poslední vývojovou verzi Netbeans a tam vůbec nebylo možné spustit
    externí instalaci Tomcatu a deploynout do ní aplikaci - díky tomu nešel ani ten
    \"jednoduchý\" debugging. Nebo můžete mít takový aplikační server (či jeho verzi),
    kterou IDE nepodporuje - ale to neznamená, že nemůžete debugovat. Ruční způsob
    vám půjde vždy.\r\n\r\nTo je to co jsem se snažil článkem říct (mimo jiné ;)).
    Tak doufám, že se mi to po reperátu už podařilo :)."
- id: 50
  author: david
  author_email: bmfv@seznam.cz
  author_url: ''
  date: '2007-04-13 17:41:21 +0200'
  date_gmt: '2007-04-13 16:41:21 +0200'
  content: Aha, toho localu jsem si  ve videu nevsiml.:)  Ted uz mi to dava smysl...
    Pokud jde o ty netbeansy, tak ja ten posledni milestone (8) pouzivam taky(lepsi
    editor, ale porad dost chyb:() a myslim, ze tahle funkce bude az v tech dalsich
    milestonech. Ten bundle tomcat ale funguje bez problemu. Diky
- id: 51
  author: Brdloush
  author_email: brdloush@brdloush.net
  author_url: ''
  date: '2007-04-14 23:46:08 +0200'
  date_gmt: '2007-04-14 22:46:08 +0200'
  content: "Zdravím. Jojo, také kolikrát nestíhám koukat kolik relativně samozřejmých
    věcí ostatní (a často já sám) neznají. Sám jsem byl docela překvapen, když jsem
    jednou v naší aplikaci, která vesele deadlockovala, věnoval čas přečtení výpisu,
    který získáte, když ji breaknate v konzoli pomocí Ctrl+Pause(Break).  Break vypíše
    do konzole tak zajímavé informace, že se mnohdy deadlock docela slušně dohledáte.
    Až se pak člověk diví, že v IDE tahle možnost ani není (nebo jo?).\r\n\r\nHot
    redeploy je věc úplně super, nicméně na můj vkus až příliš často ho dostanete
    do stavu, kdy je nutné restartnou server a začít debugovat znovu. Většinou stačí
    drobnost v podobě změny  struktury třídy (třeba přidat/odebrat/přejmenovat field)
    a je vymalováno. Tady bych osobně uvítal trošku větší vylepšení do dalších verzí
    protože hot redeploy je k nezplacení a věřím že by ještě šel  pořádně vylepšit
    (i když bůh ví, jak moc reálné to je - nikdy jsem se tím nijak zvlášť nezaobíral).\r\n\r\nJeště
    ad tracování respektive spíše produkční sledování - na posledních  Sun Tech Days
    mě docela hodně překvapil Solaris.. nejen kvůli suprovému filesystému ZFS, ale
    také kvůli moc fajn nástroji DTrace. Bohužel jsem neměl ještě dostatek času si
    Solaris někam dlouhodoběji nainstalit a ozkoušet, nicméně alespoň 2 linky k dobru
    pro představu co s DTracem lze dosáhnout:\r\n\r\nhttp://blogs.sun.com/blaze/entry/dtrace_my_mysql_application\r\nhttp://www.brendangregg.com/DTrace/smc.html\r\n\r\nUž
    je to nějaká doba co jsem to četl, ale vím, že mě zmíněné linky vcelku mile překvapily
    a zaujaly. Tak třeba i vás."
- id: 52
  author: Honza Novotný
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-04-16 20:16:37 +0200'
  date_gmt: '2007-04-16 19:16:37 +0200'
  content: "Tak to se zase přiznám neznám já - nechcete někde popsat postup (a výsledky?!).
    Přiznám se, že pokud bych narazil na deadlocky asi bych sáhnul po profileru z
    NetBeans - i když nevím jestli ten je na vyhledávání deadlocků nejlepší.\r\n\r\nHot
    redeploy je fakt docela užitečná věcička. Rozhodně postačuje na takové ty rychlé
    opravy. Pokud se vyvíjí na nějakém \"rozumě\" rychle startujícím serveru ala Tomcat
    s několika málo web aplikacemi - dají se časté restarty ustát. Ovšem jakmile to
    přesáhne určitou mez už to je problém - tím větší, čím víc se ladí klikáním po
    web aplikaci. Tady bych chtěl vyzdvihnout vývoj pomocí automatických testů, protože
    v takovém případě se vám začínají vyplácet i pro samotnou rychlost vývoje.\r\n\r\nPřiznám
    narovinu, že se Solarisem jsem přišel do styku jen velmi povrchově. Trošku jsem
    si hrál s Ubuntu, ale žádný extra odborník na Linux taky nejsem. Je jasné, že
    pokud jste odborník, dokážete na Linuxu získat daleko více informací o tom, co
    se děje v systému než na M$ Windows - ale k tomu budu potřebovat ještě hodně času
    ;).\r\n\r\nKaždopádně díky za linky i za reakci (mmch, ten postup s konzolí by
    mě fakt zajímal)."
- id: 53
  author: Brdloush
  author_email: brdloush@brdloush.net
  author_url: ''
  date: '2007-04-16 23:03:30 +0200'
  date_gmt: '2007-04-16 22:03:30 +0200'
  content: "My na deadlocky narazili při vytváření swingovského wysiwig word-like
    editoru. Byl to problém se zamykáním dokumentu versus update GUI. Zavolání setVisible()
    poslalo celou aplikaci kvůli deadlocku do kolen - docela pěkný oříšek.  \r\n\r\nZagooglil
    jsem a docela pěkně a jednoduše popsané, jak na věc, je třeba tady: http://wiki.eclipse.org/index.php/How_to_report_a_deadlock\r\n\r\nNa
    vyzkoušení se může hodit nějaký ten deadlock ;) http://jroller.com/page/skavish?entry=how_to_create_a_guaranteed
    \r\n\r\nNB Profiler je moc fajn vecicka, u nas jsem ale na hledani memory leaku
    jsem ale uzivil spise HAT - https://hat.dev.java.net/.  Hat totiž ukazuje nejen
    jaké objekty vám leží v paměti, ale i jaká třída je alokovala atd atd.. Má toho
    zkrátka k analýze mnohem víc než NBProf. (což je vcelku logické, NBProf jede v
    reálném čase, hat dělá velký snapshot heapu..) Používal jsem ho jen krátce ale
    i tak se hodně osvědčil. A na průzkum chyceného heapu to má to dokonce i webové
    GUI :)\r\n\r\nO DTrace vim zatim bohuzel hodne malo  a nemam vubec cas to zmenit
    :( Co jsem zatim pochopil/zaslechl, je to  podpora pro dynamicke tracovani zabudovane
    tracovani primo do systemu (momentálne asi jen solaris).  Takze uz kdyz poustite
    na produkcnim solarisu binarku java, automaticky se v ni pak muzete hrabat dtracem
    - bez nutnosti jakehokoliv zasahu (nejake parametry pro virtual machine apod).
    Vyhodou je zejmena fakt, ze dtracovat muzete i neco, co treba bezi 24/7 na produkci..
    s zivymi daty, bez nejakeho zpomaleni. Solarisaci se chlubi, ze je to zatracene
    dobre napsane a brutalne rychle. Z příkladu s tracováním mysql to vypadá hodně
    flexibilně a použitelně. \r\n\r\nDoporučuju si opravdu najít 5 minut a přečíst
    si ten krátký blog entry o dtracovani mysql aplikace. Způsob jakým si dotyčný
    krásně intuitivně dohledá,co potřebuje zjistit, až zavání genialitou. Ono holt
    opravdu platí že v jednoduchosti je síla. Když jsme se nedavno snažili  zjistit,
    jaké dotazy posílá WebSphere Commerce server na OracleDB v rámci jednoho requestu,
    tak jsem při vzpomínce na existenci DTrace jen tiše skřípal zuby a Solarisákům
    záviděl :)\r\n\r\nHolt si na ten solaris někdy musím najít čas.. ale vzhledem
    k blížícím se státnicím mám teď trochu jiné problémy ;) Jinak jsem taky na Ubuntu
    a jak říkáte - do odborníka mám také zatraceně hodně daleko :)"
- id: 54
  author: Honza Novotný
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-04-17 07:51:15 +0200'
  date_gmt: '2007-04-17 06:51:15 +0200'
  content: "Díky za linky - ta informace o konzoli je hodně zajímavá včetně odkazu
    na HAT. Díky za přínosný komentář. Ono dělat zkoumat cokoliv na provozním serveru
    je oříšek - v mé předchozí firmě jsme měli odborníky na Solaris a kolikrát jsem
    koukal co dokázali na Sun Serverech provést a zjistit.\r\n\r\nUpřímě řečeno dlouho
    jsem žil v domění, že Solaris běží výhradně na Sunovských serverech - což už evidentně
    dávno není pravda (viz. tabulka na konci stránky http://en.wikipedia.org/wiki/Solaris_Operating_System)."
- id: 55
  author: Brdloush
  author_email: brdloush@brdloush.net
  author_url: ''
  date: '2007-04-17 18:19:33 +0200'
  date_gmt: '2007-04-17 17:19:33 +0200'
  content: Už dlouho to tak není. Solaris (příp. opensolaris) není problém nainstalit
    pěkně k klídku doma, ať už to VMware nebo regulérně. Nejjednodušší na vyzkoušení
    je asi livecd distro Belenix (http://www.genunix.org/distributions/belenix_site/).
    I tak jsem v tom ale dobře plaval, nějak my chyběly klávesové zkratky na přepínání
    textových konzolí, backspace nefachal tak jak má atd.. No časem tomu dám druhý
    pokus a uvidíme ;)
- id: 56
  author: benzin
  author_email: benzin@centrum.cz
  author_url: http://live.jabbim.cz/benzin
  date: '2007-04-19 07:42:17 +0200'
  date_gmt: '2007-04-19 06:42:17 +0200'
  content: "Vidite to, ja pouzival v Delphi jenom debuger a logovani vubec. S prechodem
    na Java jsem se rozhodl, ze pouzivani Logu je dost super. V posledni dobe me logovaci
    silenstvi dostoupilo takove krajnosti, ze dneska uz v podstate debuger nepouzivam.
    Jde totiz o metodu vyvoje kterou pouzivate. Ja napriklad pouzivam TDD (testy rizeny
    vovj), trochu mixly XP. Takze ke vsemu mam testy a logy. Zadna moje metoda (pokud
    jenom nenastavuje sadu parametru) nema pres deset radku. A vkazde metode mivam
    nekolik logu. \r\n\r\nKdyz dojde k problemu vim uplne presne kde se vyskytl a
    v jake podobe byly  v danou chvili parametry. Vetsinou pak uz neni problem a chybu
    opravim primo, bez dabugingu.\r\n\r\nBtw. jsem asi jeden z mala ktery pise testy
    pred samotnou metodou. A musim rict, ze v podstate nepotrebuju pouzivat Debuger."
- id: 57
  author: Brdloush
  author_email: brdloush@brdloush.net
  author_url: ''
  date: '2007-04-19 08:12:41 +0200'
  date_gmt: '2007-04-19 07:12:41 +0200'
  content: "Ze by nova metodika vyvoje - LDD -Log Driven Development? :-) Je pravda,
    ze kazdy by mel vyvyjet takovym zpusobem, jak to uzna za vhodne a efektivni. Takze
    pokud vam vyhovuje logovat jak o zivot, proc ne. \r\n\r\nMuzete trochu rozvest
    jakym zpusobem logujete? Nejak si ted nedovedu predstavit,ze bych skoro do kazde
    metody pral rucne logovaci hlasky, natoz pak jeste vypis parametru. Mozna to tam
    dotlacit skrze AOP - to bych jeste zkousnul, ale upravovat to rucne pri kazdem
    refaktoringu, to bych se asi osypal :-) Druha vec je jestli pak neni log plny
    textu - jak se v nem pak rozumne vyznat?\r\n\r\nOsobne bych se debuggeru rozhodne
    nevzdal. Rozumne logovani je fajn a pokud usetri nejake to debugovani, tak je
    to jen dobre. Ale debugovani je podle me trochu o necom jinem. Je mnohem flexibilnejsi.
    Breakpointy, watche, podminene breakpointy (ty taky dost lidi nezna, pritom je
    to tak super vec) atd atd. Hlavni vyhodu vidim v tom, ze se pekne za behu muzu
    rozhodovat co chci sledovat a co nikoliv. Logovani je na muj vkus prilis staticke
    a compile-time.\r\n\r\nAle urcite se rad se necham poucit. ;)\r\n\r\nLogovani
    imho nahradit debugging  nemuze nikdy a ja osobne ho povazuju za neco nepostradatelneho.
    Kdyz si predstavim,jakym zpusobem obvykle \"debuguji\" svuj kod phpckari, jde
    mi mraz po zadech :-)"
- id: 58
  author: Honza Novotný
  author_email: novotny@fg.cz
  author_url: http://blog.novoj.net
  date: '2007-04-19 09:21:29 +0200'
  date_gmt: '2007-04-19 08:21:29 +0200'
  content: "Mám úplně stejné důvody proč se držím debugování. Vyvíjím také pomocí
    testů. Ale upřímě řečeno testy píšu ve chvíli, kdy mám dokončenou myšlenku v kódu,
    abych si ji ověřil ... při psaní kódu refaktoruju v podstatě neustále, takže se
    mi často mění rozhraní. Pokud jsem psal testy před napsáním kódu, tak jsem testy
    neustále přepisoval, takže nakonec jsem na tom strávil plno \"hluchého\" času,
    než když to dělám obráceně. Vím, že z pohledu TDD to není to pravé ořechové, ale
    nepodařilo se mi najít jiný efektivní způsob (pro můj styl psaní).\r\n\r\nDalší
    věcí je, že píšu testy obvykle pouze na úrovni business vrstvy a to většinou testy
    integrační - tedy včetně propojení na vrstvu datovou. Po zkušenostech s testováním
    webové vsrstvy jsem zanechal psaní testů pro ni, jelikož se musely neustále opravovat
    a ten efekt jsem nějak neviděl. Webovou vrstvu tedy ladím přímo klikáním, a tam
    se mi HOT REDEPLOY opravdu hodně hodí - šetří plno času v kolečkách: nalezení
    chyby, oprava, deployment, otestování. Ve výsledku mám tedy obvykle vyladěnou
    business vrstvu pomocí testů a pouze GUI ladím tím \"starým\" ručním způsobem.\r\n\r\nSouhlasím
    s Brdloushem, že debugger je skvělá věc, kterou řada jazyků prostě nemá. Tento
    článek měl právě vést k zamyšlení, jestli skutečně využíváme těch výhod, které
    nám Java nabízí. Leta jsem vyvíjel v prostředí, kde jsem debugger nemohl použít
    a tam opravdu nezbývalo než se spolehnout na logování - taky to jde, ale efektivita
    je prostě někde jinde. Jak jsem psal - ve většině případů vám debugging ušetří
    enormní množství času - a to i v případě, že vyvíjíte pomocí testů - vždyť přeci
    i při spuštění testů si můžete dát breakpoint (já používám IntelliJ IDEA a ta
    podpora to toto je naprosto úžasná) a přijdete na problém mnohem dřív."
- id: 59
  author: filemon
  author_email: jf@jirifabian.net
  author_url: http://www.jirifabian.net
  date: '2007-04-20 09:12:29 +0200'
  date_gmt: '2007-04-20 08:12:29 +0200'
  content: Jelikoz casto naskakuju do projektu v pulce, vyuzivam debugging nejvice
    pri studiu chovani aplikace. Co se tyce logovani - nezapominejte, ze napr. na
    produkcni stroj se debuggerem nejspise nepripojite a u sebe take vzdy simulovat
    nelze (napr. bug vznikly rozdilnymi daty). Takze huste logovani je pro maintenance
    spasa.
- id: 60
  author: benzin
  author_email: benzin@centrum.cz
  author_url: http://live.jabbim.cz/benzin
  date: '2007-04-22 17:50:40 +0200'
  date_gmt: '2007-04-22 16:50:40 +0200'
  content: "Brdloush: No zatim jsem nepouzivl nic jineho nez log4j a apacha logging.
    do kazde tridy skopnu tohle:   /** Logger for this class and subclasses */\r\n
    \ private static final Log LOGGER = LogFactory.getLog(JStudentDAO.class);\r\n\r\nA
    zmenim tridu. Pak zu jenom Tam kde se to jevi vhodne soupnu LOGGER.debug. V log4j.properties
    mam udelane loggery pro kazdy balik zvlast. Takze mam nekolik log souboru a tri
    hlavni (textovy, na konzoli a html). Hlasky mam rozsypane po ruznych mistech.\r\n\r\nK
    debugingu musim sahnout kdyz dojde k chybe, tam kde jsem ji necekal. Necekal jsem
    chybu jenom tam kde nejsou testy. Dejde-li k chybnemu chovani, dochazi k nemu
    v nejake metode, naprosto vzdy se da pouhou uvahu urcit ktera metoda to spousti.
    Takze do testu nasadim data, ktera tvorila chybu a projedu testy. Okamzite vidim,
    kde dochazi k chybam. A co chcete v deseti radkove metode debuggerovat?\r\n\r\nJak
    rikam, obcas k nemu sahnu, vetsinou, ale jenom tehdy, kdyz se framework (spring
    nebo hivernate), nechova tak jak jsem cekal a nechce semi psat testy frameworku.
    Takze tak jak rika filemon na pochopeni ciziho kodu.\r\n\r\nHonza Novotný: Co
    refaktorujete na jednoucelove metode? Presouvate ji do jine tridi? No pak musite
    presunout i test. Menite nekdy chovani jednoucelovych metod? U mne se to stava
    jen zridka, spis proste nektere metody se stanou deprecated, ale proto nemusism
    jeste prepisovat testy. Takze u mne se stava jenom ze proste test smazu, protoze
    jsem smazal metodu. Neuvedomuji si, ze bych nekdy menil chovani testu, protoze
    jsem zmenil chovani metody. To se mi snad jeste nestalo. Proste metoda ma jmeno,
    ktere v podstate urcuje co dela, jeden dva parametry, nejaky vystup a slus. Kdyz
    ji nepotrebuju smazu ji a napisu metodu novou. Je-li chybna, oprvim ji. Je umistena
    ve spatne tride? Presunu ji i prislusny test. Tot vse."
- id: 61
  author: benzin
  author_email: benzin@centrum.cz
  author_url: http://live.jabbim.cz/benzin
  date: '2007-04-22 17:55:36 +0200'
  date_gmt: '2007-04-22 16:55:36 +0200'
  content: Btw. neberte to tak, ze bych snad brojil proti debugingu. Jenom proste
    tvrdim, ze z kazdodeni prace casem vymyzel. Takze ma cesta smerovala od debuggeru
    k logu a testum. Ale urcite je to dano i typem aplikaci, ktere vytvarim.
- id: 62
  author: Honza Novotný
  author_email: novotny@fg.cz
  author_url: http://blog.novoj.net
  date: '2007-04-22 20:44:54 +0200'
  date_gmt: '2007-04-22 19:44:54 +0200'
  content: "Rád bych tady ještě jednou napsal, že v žádném případě nebrojím proti
    logování. Dle komentářů se mi zdá, jako by to tak vyznělo, ale to jsem neměl v
    žádném případě na mysli. Co chci říct, že logování i debuging má při vývoji v
    Javě své místo - každé ale trochu jinde.\r\n\r\nPravda je, že si myslím, že ladění
    kódu pomocí \"asynchroně\" pomocí logovacích záznamů v čase vývoje se mi zdá jako
    neefektivní. Nicméně, každý z nás je originál - a je klidně možné, že vy s pomoců
    logů hledáte chyby rychleji než já s pomocí debuggeru. Co jsem však v praxi poznal
    byl naprostý opak - minutové analyzování dlouhých debug logů tam, kde mě s debuggerem
    stačí 15 - 30 vteřin. Nutnost redeploye (restartu serveru) tam, kde mne stačí
    překompilování třídy a HOT REDEPLOY. To co se snažím v článku obhajovat je pouze
    efektivita vývoje na úrovni, kterou může ovlivnit každý programátor. Opravdu to
    neberte jako zpochybňování vašich zvyků vývoje, v podstatě se hlavně jedná o moji
    zkušenost.\r\n\r\nDalší skvělá vlastnost debuggeru, kterou logy těžko efektivně
    nahradíte je ad hoc vyhodnocování Java výrazů za běhu, v kontextu běžící aplikace.
    \r\n\r\nCo se týká průzkumu cizího kódu - souhlasím a také to praktikuji. Je opravdu
    rozdíl, traverzovat kódem místo snažení se naslepo otestovat a pochopit black
    box. Tady už to kolikrát neznamená jen ztrátu času - ale rozdíl mezi proniknutím
    do logiky nebo ne. Mmch. např. z Acegi Security jsem se hodně naučil o Springu
    a je tam i zajímavá dekompozice systému k okouknutí. To zvenku prostě nepoznáte.
    Někdy je však problém donutit IDE aby vám ve zdrojácích cizích tříd (připojených
    jako JARy) procházelo - v IntelliJ Idea se mi to zdá asi nejjednoduší k rozchození.
    V Netbeans jsem měl svého času problémy nastavit breakpointy - muselo se to nastavovat
    jako v otevřeném class a nikoliv v samotném source file (mám ten dojem, že když
    si tam dáte GoTo Class a dáte název cizí třídy - zobrazí se vám 2x - jednou jako
    source a jednou jako class, ať vyberete cokoliv, otevře se source, ale breakpointy
    fungují jen když vyberete class). V Eclipsu jsem se nějak beznadějně ztratil ...
    ale tam se mi to stávalo pořád.\r\n\r\nAd testování a refaktoring: Tady jde asi
    především o styl vývoje. Například já o sobě vím, že programovat pomocí UML diagramů
    (a jsou lidé, kterým tento styl vývoje vyhovuje, jinak by nevzniklo MDA) není
    pro mne. Class diagramy sice v pohodě nakreslím, ale nemyslí mi to v nich - v
    kódu obvykle zjistím, že existuje elegantnější řešení a původní představu třebas
    dvakrát překopu než jsem spokojen (mluvím o složitějších částech aplikace - na
    jednoúčelových metodách není co vymýšlet - jde spíš o dekompozici a výsledné poskládání
    \"jednoúčelových metod\"). Faktem je, že při tomto stylu vývoje na začátku přesně
    nevím, jak bude vypadat výsledné řešení, takže na konci je z původních třech tříd,
    tříd deset - v metodách klidně polovina parametrů ubyde, protože úkoly převzala
    jiná metoda volaná mimo tuto metodu atd. atd. \r\n\r\nPo přečtení knihy Extrémní
    programování od Kenta Becka jsem taky psal nejdřív testy, ale po nějaké době jsem
    toho nechal, protože jsem byl dost neefektivní. Prostě jsem strávil plno času
    přepisováním testů. Je jasné, že pokud se jen metoda přesunuje není problém -
    horší je, jakmile se vám mění kontrakt metody - najednou část toho co dělala původní
    metoda, dělají třebas dvě metody jiných tříd. Pak se třebas logika přípravy prostředí
    pro test dost špatně přenáší - rozhodně ale do testu už musíte sáhnout.\r\n\r\nDost
    v tomhle mohou pomoci mock objekty, které kladou minimální nároky na přípravu
    okolního prostředí - v podstatě si ho můžete celé nasimulovat a pak už ty náklady
    se změnamy už nejsou tak veliké. Ale s pomocí mock objektů se také nedá testovat
    všechno (stejně musíte mít nějaké integrační testy).\r\n\r\nBuďto tedy něco dělám
    zásadně špatně (doufám že ne), nebo je to zase jen důsledek toho, že jsme každý
    jiný, a každý má tak trochu ten svůj osobitý styl vývoje."
- id: 63
  author: benzin
  author_email: benzin@centrum.cz
  author_url: http://live.jabbim.cz/benzin
  date: '2007-04-22 21:36:13 +0200'
  date_gmt: '2007-04-22 20:36:13 +0200'
  content: "4Honza Novotny: No ja diky tomu, ze mam unit testy nemusim restartovat
    cely server (v mem pripade by to byl jetty). Navi diky springu nepouzivam zadny
    kontejner, ale delam vsechno pres spring. Takze jde jenom o nacteni kontextu,
    ale i to delam jenom v pripade testu DAO trid. Jinak vsechno jede pres mock objekty,
    na ktere z casti vyuzimva Mockobjects a z casti si je pisu sam. To podle toho
    jake vlastnosti po nich pozaduju.\r\n\r\nBtw. integracni test, je myslim, jenom
    pro DAO. Btw. GUI jsem se jeste testovat nenaucil, takze to testuji skutecne rucne
    :(. Myslim, ze by se situace vyrazne zmenila, kdybych nepouzival spring a aplikaci
    spoustel v kontejneru. to by pak integracni testovani vyzadovalo kde co.\r\n\r\nZkuste
    se zamyslet nad tim, jestli delate dobre kdyz vase metody maji vice nez jednu
    funkci. Resp. kdyz mam metodu od ktere povazuji dve funkce, tak to provedu tak
    ze zavolam dve metody, ktere maji vzdy jednu funkci. Tim si vyrazne zjednodusite
    praci jak s testama, tak s pripadnym prepisovanim testu. \r\n\r\nBtw. jde urcite
    o typ aplikace, kteoru vytvarite. Delate-li aplikaci jen pro jednoho zakaznika,
    muzete si dovolit chybu, protoze kdyz se na chybu narazi opravite ji a velmi snadno
    dostanete k zakaznikovi. Kdyz ale mate zakazniku spousty, tak Vam oprava chyby
    \ zabere spoustu casu. A to nejvic na zvedani telefonu, protoze ti zakaznici pouzivaji
    ve stejnem obdovi stejnou funkci a tudiz vsichni vam volaji v jednu chvili. Z
    toho spousta z nich zvladne vypnout automatickou aktualizaci, ale uz nezvladne
    jednosduse pravidelne aktualizovat :). \r\n\r\nTakze jak rikam, jde o to jakou
    aplikaci vyvyjite a jake prostredky jste nucen pouzit."
- id: 64
  author: Honza Novotný
  author_email: novotny@fg.cz
  author_url: http://blog.novoj.net
  date: '2007-04-23 08:38:08 +0200'
  date_gmt: '2007-04-23 07:38:08 +0200'
  content: "No aplikace se přeci neskládá jen z \"jednoúčelových\" metod. Pak máte
    metody, které tyto \"jednoúčelové\" metody spojují a přidávají třebas ještě něco
    dalšího -&gt; na oko tedy jako by plní více funkcí naráz - i když ve skutečnosti
    tuto odpovědnost delegují dál. Typicky právě tyto funkce představují business
    logiku aplikace a ty se také vyplatí testovat integračně - tzn. tak aby se ověřilo,
    že kompozice součástí je bezchybná. Ale tady už opravdu jdeme do detailů a mohli
    bychom se přít o drobnostech do nekonečna.\r\n\r\nShodneme se určitě na tom, že
    záleží na konkrétní situaci. S tímto bych to tedy asi uzavřel ;)."
- id: 65
  author: benzin
  author_email: benzin@centrum.cz
  author_url: http://live.jabbim.cz/benzin
  date: '2007-04-23 10:34:45 +0200'
  date_gmt: '2007-04-23 09:34:45 +0200'
  content: "Novotny: Nikdy nepridavaji nic noveho. Jenom spojuji. To je podstatne.
    A integracni testy  vice modulu chcete jako delat jak? Kdyz delate jeden modul,
    nemate k dispozici moduly dalsi. Jedine co muzete udelat je napsat test pro dany
    modul, kde rozhrani trid z jineho modulu mockujete a pak napsat abstrakni testy
    (myslim, se jim rika akceptacni), ktere pak dedi testy v danem modulu a tim otestuji,
    ze jsou kompatibilni s vasim modulem.\r\n\r\nTakze ne, nedelam integracni test
    nikde jinde, nez tam kde neuspeju s mockem. A s mockem jsem zatim neuspel, jenom
    na urovni databaze. (btw. dao objeckt pro potreby trid normalne mockuju, ale pri
    testovani samotne implementace dao objektu, je potreba testovat jej proti databazi)."
- id: 66
  author: Honza Novotný
  author_email: novotny@fg.cz
  author_url: http://blog.novoj.net
  date: '2007-04-23 11:40:38 +0200'
  date_gmt: '2007-04-23 10:40:38 +0200'
  content: "I v pouhém spojení je logika - přeci nemáte jen sekvenční metody, kde
    se vždy vykonává jedna posloupnost. Mám dojem, že tady si spíš nerozumíme, než
    cokoliv jiného.\r\n\r\nBTW: o modulech jsem přeci nemluvil ne?!\r\n\r\nVaroval
    bych se přeceňování mock testování. jak odhalíte např. chybu sestaveného projektu?
    Celek přeci není jen součet částí - části mohou samostatně fungovat jak víno,
    ale po sestavení tam mohou být třecí plochy, které způsobí, že to nakonec jako
    celek nefunguje.\r\n\r\nTypicky např. když v mock objektech pracujete jen se svými
    \"vymyšlenými\" daty. Nakonec si zkusíte udělat integrační test nad reálnými daty
    v DB, na úrovni business vrstvy a klidně zjistíte, jak vám to hezky padne na hubu,
    jenom proto, že jste ve svých mock objektech vždy vracel konkrétní \"ozkoušená\"
    testovací data, se kterými business objekty počítaly. S reálnými daty, ale mohou
    klidně vyhořet. A není to tím, že byste něco podcenil, nebo špatně programoval
    - prostě se jen nedá vždy 100% počítat se všemi variantami. Tohle vím, protože
    jsem si to ozkoušel na vlastní kůži - od té doby integrační testy nepodceňuji.\r\n\r\nSpíš
    je otázka, kde leží ten správný poměr mezi testy.\r\n\r\nMožná, když pracuje člověk
    na projektu sám, tak se dá tento problém minimalizovat (a záleží na velikosti
    projektu). Ale stejně bych integrační testy, jdoucí napříč aplikací nepodceňoval.
    Nemusí být složité - správná funkcionalita je zajištěna unit testy - ale často
    odhalí, že při konkrétním použití (v kombinaci) se generují chyby."
- id: 174
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-07-04 05:28:56 +0200'
  date_gmt: '2007-07-04 04:28:56 +0200'
  content: "Přidal jsem zajímavý odkaz na článek od Borůvka o HotSwap v prostředí
    Eclipse. Mj. začátek článku, popisuje přesně ty důvody, kvůli kterým se prostě
    vyplatí rozhozením debugu zabývat.\r\n\r\nhttp://www.boruvka.net/blog/2007/07/eclipse-nefunkn-hot-code-replace.html"
---
<p>V poslední době jsem zjistil, že některé věci, které já považuji za samozřejmé, pokud se rozhlédnu kolem sebe, tak úplně samozřejmé nejsou. Jednou z nich je debugování Javovského kódu. I v dnešní době, kdy je podpora ze strany technologií na perfektní úrovni je mnoho vývojářů, kteří pro rutinní vývoj (nemluvím o řešení problémů po nasazení aplikace) a odlaďování kódu debuggování nepoužívají a spoléhají se na záznamy z logu. Je pravda, že tento přístup má své výhody – obvykle se tímto způsobem obohatí kód dostatečným množstvím logů, že i v produkci je obvykle dost informací k řešení problémů, pokud nastanou. Zásadní nevýhodou, kterou v tom spatřuji já je naprosto drastické snížení produktivity programování. Problém, který se dá vyřešit během půl minuty vložením breakpointu na správné místo v kódu se může v případě procházení logů protáhnout klidně i na pět minut. Flow programátora je potom – však vy víte kde :).</p>
<p>Proto tento článek věnuji těm, kteří debugging nepoužívají nebo měli nějaké problémy s jeho zprovozněním.</p>
<p><a id="more"></a><a id="more-13"></a></p>
<p>JVM se pro ladění spouští ve speciálním režimu (tzn. se speciálními parametry), aby bylo možné jeho chod ovlivňovat. V debug režimu bude Java pravděpodobně o dost pomalejší, takže tyto parametry si dovolte použít pouze na vývojovém prostředí.</p>
<p>Pro spuštění Javy v debug módu stačí do parametrů spuštění přidat následující parametry (je navíc třeba zajistit, že se vám volá java z instalace SDK a ne pouze standardního JRE):</p>
<pre>
<code>
-Xdebug -Xnoagent -Djava.compiler=NONE -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=5005
</code>
</pre>
<p>Kde jednotlivé parametry znamenají zhruba následující:</p>
<ul>
<li><b>-Xdebug</b><br>zapíná podporu pro debugování v JVM</li>
<li><b>-Xnoagent</b><br>vypíná <a href="http://java.sun.com/j2se/1.3/docs/tooldocs/win32/oldjdb.html" target="_new">"starou" verzi</a> java debuggeru</li>
<li><b>-Djava.compiler</b><br>vypíná JIT (just in time) compiler - tedy HotSpot optimalizaci (logicky usuzuji, že pokud by zůstala zapnuta, mohly by díky optimalizaci některé řádky prostě vyzmizet, což pro debugging není úplně optimální - nicméně dle <a href="http://forum.java.sun.com/thread.jspa?threadID=5134045&tstart=0" target="_new">tohoto záznamu v Sun fóru</a>, by to zas až tak veliký problém být neměl - ašak nejsem odborník, abych mohl polemizovat)</li>
<li><b>-Xrunjdwp</b><br>nahrává knihovny pro debugging a stanovuje druh přenosu
<ul>
<li><b>transport:</b> typ přenosu - v podstatě existují dva:
<ol>
<li>dt_socket: připojení přes socket - vyžaduje nastavení portu</li>
<li>dt_shmem: připojení přes sdílenou paměť (pouze pro MS Windows platformu) - vyžaduje nastavení názvu</li>
</ol>
</li>
<li><b>server:</b> stanovuje, která strana (JVM nebo debugovací klient) je tou aktivní stranou - pokud server=y - JVM čeká až se klient aktivní připojí k serveru, v opačném případě se JVM okamžitě zkusí připojit k debugovacímu klientovi na stanovené adrese (paramtr address)</li>
<li><b>suspend:</b> má smysl dávat asi jen "y" - zajistí, že JVM pozastaví výkon všech vláken v případě, že dojde k debugovací události</li>
<li><b>address:</b> v případě použití dt_socket by se zde mělo zadat číslo portu, kde bude JVM naslouchat na připojení debug klienta</li>
<li><b>name:</b> v případě použití dt_shmem stanovuje název úseku sdílené paměti (ale radši si to ověřte, tady si nejsem moc jistý)</li>
</ul>
</li>
</ul>
<p>V podstatě je pouze důležité abyste potom v IDE nastavili také stejné parametry (důležitá je hlavně adresa = port a transportní režim - doporučuji socket). K takto spuštěnému JVM se potom můžete odkudkoli připojit a debugovat jeho kód. Je klidně možné takto debugovat i kód na serveru, který fyzicky leží úplně na jiném místě – jen si musíte dát pozor, aby firewally propustily komunikaci na portu, který je otevřen pro debugging (také je komunikace odpovídajícím způsobem zpomalená, takže debugování není tak plynulé).</p>
<p>Toto je obecný způsob nastavení javy pro debugování – lze použít jak pro debugování webových aplikací uvnitř web kontejnerů, pro klientské aplikace a můžete tím klidně krokovat i zdrojáky Javy samotné nebo třebas i zdrojáky aplikačních serverů, pokud je máte k dispozici (a věřte mi tímhle způsobem se můžete do jejich fungování dostat daleko rychleji než pasivním studiem kódu).<br />
Ukažme si nyní spuštění javy v debugging režimu při použití web kontejneru Tomcat 5.0 a Javy 1.4.2 a pokus o odkrokování jednoduché webové aplikace (jednoduchého servletu).</p>
<p><b><a href="http://files.novoj.net/Debugging/idea-debug.avi">AVI ukázka remote debuggingu v prostředí IntelliJ IDEA 6.0.4</a></b><br />
<br><br />
<b><a href="http://files.novoj.net/Debugging/netbeans-debug.avi">AVI ukázka remote debuggingu v prostředí NetBeans 6.0 m8</a></b><br />
<br><br />
<a href="http://www.sweb.cz/pichlik/archive/2006_04_30_archive.html" target="_blank">Tady je něco pro Eclipsisty od Dagiho</a><br />
<br><br />
<a href="http://www.boruvka.net/blog/2007/07/eclipse-nefunkn-hot-code-replace.html" target="_blank">A tady je zajímavý příspěvek od Borůvka o HotSwap v prostředí Eclipse</a></p>
<p>Celé se to ještě dále zjednodušit. IDE mají obvykle v sobě přímou podporu pro základní webové či aplikační kontejnery a obvykle stačí jen vytvořit novou konfiguraci pro tyto kontejnery s uvedením cesty, kde je nainstalován a IDE se postará o vše ostatní.<br />
Nicméně je vhodné znát procesy, které se stejně dějí na pozadí, aby to celé pro nás nebyla taková magie – znalost se hodí obvykle ve chvíli, kdy to celé nefunguje tak jak má.</p>
<p>Z mého pohledu je skvělou věcí HOT REDEPLOY funkcionalita, kterou poskytuje IDE (v IntelliJ IDEA je to velmi jednoduché – s Netbeansy, které jsem používal před půl rokem se mi to nějak nepovedlo rozchodit, možná je to tím, že NetBeansy pro buildování a deploy používají interně Anta, takže je pro ně obtížné zjistit, které třídy se změnily a provést HOT REDEPLOY pouze na nich). Stačí abyste měli Javu spuštěnou v debug režimu a při překompilování tříd / projektu Idea sama zjistí, které třídy se od posledního deploye změnily a podhodí je JVM k výměně. Ani nepotřebujete mít chod aplikace zastavený na nějakém breakpointu v dané třídě – stačí být jen „připojený“ k JVM. Tím se celé kolečko „nalezení problému – oprava – deploy – vyzkoušení opravy“ minimalizuje na opravdu jen pár vteřin a celý vývoj se může opravdu velmi urychlit. Zvláště pak v případech, kdy programátor nepoužívá k vývoji hlavní funkcionality automatické testy (tzn. je odkázán na ruční oklikání v testovacím prostředí) – což bohudík není můj případ ;).</p>
<p><b>Pozn. 27.5.2007:</b> Tak jsem NetBeansům křivdil - v debug módu je prý v toolbaru k dispozici funkce "apply code changes", která by mělá právě HOT REDEPLOY provést.</p>
