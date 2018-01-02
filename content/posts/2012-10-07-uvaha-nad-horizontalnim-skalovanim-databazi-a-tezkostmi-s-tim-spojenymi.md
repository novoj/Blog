---
status: publish
published: true
title: Úvaha nad horizontálním škálováním databází a těžkostmi s tím spojenými
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft size-thumbnail wp-image-2295\" title=\"Replication\"
  src=\"http://blog.novoj.net/binary/2012/10/revolve-150x150.jpg\" alt=\"\" width=\"150\"
  height=\"150\" />Škálování databází je velké téma a já rozhodně nejsem takový odborník,
  abych tady rozebíral kdovíjaké detaily. Zcela jistě znáte termíny jako je sharding,
  o kterém <a href=\"http://www.dagblog.cz/2007_12_23_archive.html\" target=\"_blank\">psal
  Dagi už před 5 lety</a>, popřípadě znáte termín <a href=\"http://cs.wikipedia.org/wiki/Partition_(datab%C3%A1ze)\"
  target=\"_blank\">partitioning</a>, který nám nabízejí některé DB stroje \"<a href=\"http://dev.mysql.com/doc/refman/5.1/en/partitioning.html\"
  target=\"_blank\">zadarmo</a>\" a jiné \"<a href=\"http://www.oracle.com/cz/products/database/options/partitioning/index.html\"
  target=\"_blank\">za peníze</a>\". Alternativním způsobem horizontálního škálování
  je <a href=\"http://dev.mysql.com/doc/refman/5.0/en/replication-solutions-scaleout.html\"
  target=\"_blank\">škálování pomocí sady replik pro čtení</a>, o kterém lze uvažovat
  v případě, že máte aplikaci, které řádově méně zapisuje do databáze než z ní čte.
  Konkrétně se jedná o to, že máte několik databázových strojů v režimu MASTER-SLAVE(S),
  který se často nasazuje už jen z důvodu <a href=\"http://www.percona.com/doc/percona-xtrabackup/howtos/setting_up_replication.html\"
  target=\"_blank\">hot-backupu</a> (tj. v případě výpadku master databáze je možné
  velmi rychle z repliky učinit nový master a pokračovat v běhu aplikace).\r\n\r\nJelikož
  já i moji kolegové jsme šetřiví, napadlo nás, že by nemuselo být od věci repliku,
  kterou naše Operations nasadili právě z důvodu hot-backupu využít i pro zrychlení
  / škálování aplikace. Jsme si samozřejmě vědomi, že tento přístup má svoje riziko
  - v případě výpadku jedné z databází a přepnutím master databáze na záložní repliku
  půjdou všechny dotazy původně rozdělené na dva stroje na jeden. Pokud bychom tedy
  uvažovali o tomto druhu škálování bylo by lepší se bavit o dvou replikách nebo by
  musela být záloha naddimenzovaná oproti master stroji.\r\n\r\nProblém, na kterém
  jsme se však vždy zarazili, byl spojen s tím, že nemáte garantováno, kdy se v replice
  objeví stejná data jako na masteru. Zpoždění replikace se může pohybovat pouze v
  milisekundách, ale může nabývat i vyšší hodnoty. Pokud bychom tedy používali MASTER
  pouze na zápisy a některý ze SLAVE na čtení, budeme mít problém s tím, že data,
  která v jednom requestu uživatel vytvoří nemusí nutně v dalším requestu vidět. Ať
  si kdo chce co chce říká o <a href=\"http://en.wikipedia.org/wiki/Eventual_consistency\"
  target=\"_blank\">eventuální konzistenci</a> - tohle je z pohledu <a href=\"http://cs.wikipedia.org/wiki/BFU\"
  target=\"_blank\">BFU</a> zcela jasná chyba, kterou nám bude reportovat a požadovat
  její odstranění.\r\n\r\nNapadaly nás různé možnosti kompenzačních technik, ale všechny
  byly dost pracné - zvlášť v kombinaci s tradiční relační databází, kdy má uživatel
  často k dispozici plnou škálu funkcí jako je ad-hoc třídění, filtrování, seskupování
  atp. Tento týden jsem ale dostal nápad, jak by mohlo být možné relativně jednoduše
  tento problém řešit a otevřít nám tak cestu k využití replik pro škálování. V tomto
  článku bych se chtěl o něj s Vámi podělit a třeba přijdete na nějaká úskalí, která
  mě nedošla a nápad půjde do koše. Když na žádná nepřijdete budu mít větší jistotu,
  že je nápad životaschopný.\r\n\r\n"
wordpress_id: 2293
wordpress_url: http://blog.novoj.net/?p=2293
date: '2012-10-07 09:09:30 +0200'
date_gmt: '2012-10-07 08:09:30 +0200'
categories:
- Programování
- Java
- Spring Framework
- Databáze
- Úvahy
tags: []
comments:
- id: 96949
  author: Filip Jirsák
  author_email: filip@jirsak.org
  author_url: ''
  date: '2012-10-07 10:08:40 +0200'
  date_gmt: '2012-10-07 09:08:40 +0200'
  content: "Podle mne vycházíte z předpokladu, že se transakce provádějí jedna po
    druhé v nějakém pořadí, a že se ve stejném pořadí provedou i na replice. Což platí
    pro lokální databázi jen v případě izolace transakcí serializable, v případě replikované
    databáze bych si tím nebyl jist ani při této úrovni izolace transakcí.\r\n\r\nPokud
    by se nepoužívala časová značka, ale sekvence, stačila by možná úroveň izolace
    repeatable read. Ale pořád se tam budou prát všechny transakce o jednu sekvenci,
    takže to bude mít dopad na výkon. A hlavně je otázka, co vlastně zaručuje ta replikace
    -- jestli vůbec něco zaručuje ve vztahu k transakcím a jejich izolaci."
- id: 96957
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-10-07 10:28:43 +0200'
  date_gmt: '2012-10-07 09:28:43 +0200'
  content: "Ano, z tohohle předpokladu vycházím. Stačí mi, aby bylo zaručeno pořadí
    transakcí vzhledem k aktuálnímu uživateli = requestu = 1 vláknu. Pokud vím, tak
    replikace se děje tak, že master zapisuje sekvenčně do binárního logu, ze kterého
    čtou i repliky. Tj. jak se transakce do logu zařadí, tak by jí měl i slave zpracovat
    - tj. tady je ta relativní sekvenčnost vzhledem k jednomu uživateli zachovaná.\r\n\r\nPravdpodobně
    narážíte na problém, kdy bych při nějakém výpočtu četl data z replik a použil
    je pro výpočet nějaké nové hodnoty, kterou zapíšu do masteru. Tím bych zanedbal
    možné aktualizace jiných uživatelů v master databázi. To je samozřejmě pravda,
    ale v případě, že celou podobnou operaci (včetně čtení) uzavřu do jedné transakce
    (což bych měl tak jako tak), která díky svému zápisovému charakteru (produkuje
    nějaký zápis na závěr) musí jít do master databáze, budou se proti master databázi
    provádět i ta čtení, takže si myslím, že princip zůstává funkční i pro tento případ.\r\n\r\nMožná
    máte na mysli ještě něco jiného, co jsem nepochopil? Nějaký use-case? ... díky"
- id: 96961
  author: vitsoft
  author_email: Pavel.Srubar@gmail.com
  author_url: http://about.me/vitsoft
  date: '2012-10-07 10:38:04 +0200'
  date_gmt: '2012-10-07 09:38:04 +0200'
  content: "<b>Replikace neprobíhají atomicky</b>\r\nMůže se stát, že user vložil
    nová data v čase T+0, tabulka v master s timestampem bude zreplikována jako první
    (v čase T+1),  mezitím se budou zdlouhavě replikovat další tabulky (dokončení
    replikačního cyklu v čase T+3), ale uživatel chce vidět jím vložená data už v
    čase T+2, kdy ještě na replikách nejsou, přestože porovnáním T+0 a T+1 se budeme
    mylně domnívat, že ano."
- id: 96974
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-10-07 11:32:51 +0200'
  date_gmt: '2012-10-07 10:32:51 +0200'
  content: "Hmm, to nějak neodpovídá mému poznání světa (vycházím z MySQL) - můžete
    to podložit nějakými odkazy do dokumentace? Napíšu vám, z čeho vycházím já:\r\n\r\n-
    jsou dva druhy replikace row-based a statement-based: http://www.ovaistariq.net/528/statement-based-vs-row-based-replication/\r\n-
    zápisy do binlogu jdou v pořadí, v jakém jsou commitovány: http://dev.mysql.com/doc/refman/5.6/en/replication-options-binary-log.html#sysvar_binlog_order_commits\r\n-
    slave provádí statementy / aktualizace row podle sekvenčně za sebou, jak je dostává
    z relay-logu = kopie bin-logu: http://www.xaprb.com/blog/2007/01/20/how-to-make-mysql-replication-reliable/\r\n\r\nUvádím
    citaci z posledně jmenovaného zdroje:\r\n\r\n<cite>However, these queries are
    serialized to the binlog in order of transaction commit, so they are run serially
    on the slave. The slave doesn’t read ahead in the binlog and execute multiple
    queries simultaneously. To keep the updates consistent, the queries must be executed
    in the order they’re in the binlog.</cite>\r\n\r\nNikde jsem nenašel informaci
    o tom, že by row-based replikace neměla dodržovat pořadí commitů. Nikde jsem nenašel
    informaci o tom, že by replikace probíhala samostatně na úrovni tabulek - tj.
    nedodržovala pořadí commitů.\r\n\r\nZa předpokladu, že aktualizaci \"master timestampu\"
    provedu po dokončení uživatelské transakce a budu pracovat s touto hodnotou, měl
    bych mít možnost se spolehnout, že jakmile se objeví v replice, předchozí commitnutá
    transakce s uživatelskými daty už tam bude.\r\n\r\nPokud máte někde odkaz na něco,
    co vysvětluje opak, budu vám za to velmi vděčen."
- id: 96982
  author: Martin Hruška
  author_email: martin@suremail.info
  author_url: ''
  date: '2012-10-07 12:03:43 +0200'
  date_gmt: '2012-10-07 11:03:43 +0200'
  content: "Tohle mi celé přijde jako hloupost. Proč vymýšlet vlastí hloupé řešení
    problému, který je milionkrát zdokumentován a milionkrát funkčně vyřešen?\r\n\r\nJe
    vidět, že jste si s analýzou problematiky nedal žádnou práci. Jinak byste naříklad
    nepřišel s tou timestamp, když máme seconds_behind_master!"
- id: 96983
  author: vitsoft
  author_email: Pavel.Srubar@gmail.com
  author_url: http://about.me/vitsoft
  date: '2012-10-07 12:04:14 +0200'
  date_gmt: '2012-10-07 11:04:14 +0200'
  content: "Pokud jsou transakce skutečně serializovány a replikovány chronologicky,
    tak by to fungovat mělo, ostatně riziko je poměrně malé - v nejhorším případě
    user neuvidí svá data hned, ale až když po chvilce nadávání dá refresh.\r\nJá
    jsem vycházel z chování své primitivní table-based netransakční replikace, kterou
    jsem kdysi dávno implementoval."
- id: 96984
  author: kepler
  author_email: c2851344@pjjkp.com
  author_url: ''
  date: '2012-10-07 12:07:07 +0200'
  date_gmt: '2012-10-07 11:07:07 +0200'
  content: |-
    odporucam pozriet Percona XtraDB Cluster:
    http://www.percona.com/software/percona-xtradb-cluster
    alebo Postgres-XC:
    http://postgres-xc.projects.postgresql.org/
- id: 97005
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-10-07 14:24:41 +0200'
  date_gmt: '2012-10-07 13:24:41 +0200'
  content: "Díky za názor. Budu velmi rád, když mě nasměrujete k jednomu z milónů
    funkčních řešení. S analýzou problematiky jsem si mohl určitě dát větší práci
    - vždycky si můžete s něčím dát ještě větší práci - nicméně zrovna v souvislosti
    se seconds_behind_master je situace poněkud složitější. Detaily v článku: http://mysqldatabaseadministration.blogspot.cz/2006/06/investigating-reasons-why-slaves-get.html\r\n\r\nKonkrétně
    cituji z dokumentace MySQL:\r\n\r\n<cite>This field is an indication of how “late”
    the slave is:\r\n\r\nWhen the slave SQL thread is actively processing updates,
    this field is the number of seconds that have elapsed since the timestamp of the
    most recent event on the master executed by that thread.\r\n\r\nWhen the SQL thread
    has caught up to the slave I/O thread and is idle waiting for more events from
    the I/O thread, this field is zero.\r\n\r\nIn essence, this field measures the
    time difference in seconds between the slave SQL thread and the slave I/O thread.\r\n\r\nIf
    the network connection between master and slave is fast, the slave I/O thread
    is very close to the master, so this field is a good approximation of how late
    the slave SQL thread is compared to the master. If the network is slow, this is
    not a good approximation; the slave SQL thread may quite often be caught up with
    the slow-reading slave I/O thread, so Seconds_Behind_Master often shows a value
    of 0, even if the I/O thread is late compared to the master. In other words, this
    column is useful only for fast networks.</cite>\r\n\r\nNenašel jsem bohužel, že
    by existovala proměnná, která by obsahovala poslední replikovanou timestamp a
    byla vždy spolehlivě naplněná správným údajem. Navíc, ve chvíli, kdy neběží replikační
    vlákno na slave, zdá se, že proměnná seconds_behind_master obsahuje NULL hodnotu,
    což nemá nijak vypovídající hodnotu.\r\n\r\nDalší věc, která do jisté míry protiřečí
    tomu, co jste zde napsal je to, že škálování pomocí čtení z replik je jeden ze
    \"standardních\" způsobů horizontálního škálování: http://dev.mysql.com/doc/refman/5.0/en/replication-solutions-scaleout.html"
- id: 97011
  author: lopatin
  author_email: lopatin@net.net
  author_url: ''
  date: '2012-10-07 16:05:14 +0200'
  date_gmt: '2012-10-07 15:05:14 +0200'
  content: Já bych BFU moc neřešil, když už jste takový puntičkáři, tak by možná stačilo
    prostě odhadnout v jakých situacích by takové případy mohly nastat a v těchto
    případech nastavit dobu, po kterou by se četlo z masteru i při dalších requestech.
    Další možnost je např. už na stránce uložení prostě počkat až se to dostane na
    slaves a mezitím uživateli točit kolečkem.
- id: 97109
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-10-07 20:50:51 +0200'
  date_gmt: '2012-10-07 19:50:51 +0200'
  content: "Vím, že naše Operations MySQL Cluster po diskusi zamítli s tím, že víc
    věcí komplikuje než řeší (detaily neznám). Pročetl jsem dokumentaci Percona XtraDB
    Cluster a zatím se tváří jako stříbrná kulka, což je samo o sobě podezřelé :)\r\n\r\nNašel
    jsem nějaké zmínky o nečekaných dead-lock: http://www.mysqlperformanceblog.com/2012/08/17/percona-xtradb-cluster-multi-node-writing-and-unexpected-deadlocks/\r\n\r\nHledal
    jsem i nějaké porovnání výkonnosti XtraDB Clusteru (semi-synchronní replikace)
    a čistě asynchronní replikace v setupu master-slave a našel jsem následující graf
    ukazující signifikantní propad výkonu:\r\n\r\nhttp://www.mysqlperformanceblog.com/wp-content/uploads/2011/10/semisync.png\r\n\r\nNicméně
    je to určitě věc, která stojí za zvážení.\r\n\r\nV tomto článku mne však zajímalo,
    zda je navržený princip uplatnitelný pro master-slave setup či ne.\r\n\r\nDíky
    za komentář."
- id: 97329
  author: Michal Franc
  author_email: michal.franc@gmail.com
  author_url: ''
  date: '2012-10-08 08:33:37 +0200'
  date_gmt: '2012-10-08 07:33:37 +0200'
  content: Nepovazuju se za velkeho db guru, ale pokud by nebyla zajistena posloupnost
    akci, tak by db prece nemohla garantovat referencni integritu, ne?
- id: 97335
  author: Dagi
  author_email: pichlik@seznam.cz
  author_url: http://www.dagblog.cz/
  date: '2012-10-08 09:21:22 +0200'
  date_gmt: '2012-10-08 08:21:22 +0200'
  content: "Novoji, ja bych se velmi zamyslel nad tim, jestli vam to za ty komplikace
    stoji. To ze muzete cist z replika serveru neznamena, ze to budete delat. Potrebujete
    opravdu skalovat ready, mate efektivne zmerene o kolik vam to pomuze? Z tveho
    popisu se zda, ze chcete pouzivat replika ready pouze na data uzivatele tj. nikdy
    se nedelaji dotazy (joiny) pres tabulky, kde mohou zapisovat i jini uzivatele
    resp. vim ze pokud uzivatel neco zapise a nacte, neovlivni vraceny vysledek zapis
    jinych uzivatelu. V takovem pripade je spise otazka, proc ty data necacheovat
    primo na aplikacni urovni, odpadla by tim cela ta chytristika na zjistini jestli
    se data zreplikovala. Navic by odpadnul roundtrip do DB. \r\n\r\nMimochodem pouziti
    session/cookies predpoklada, ze uzivatel nebude pouzivat vasi aplikace ve vicero
    browserech/tabech najednou."
- id: 97364
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-10-08 11:26:17 +0200'
  date_gmt: '2012-10-08 10:26:17 +0200'
  content: "Trošku jsem doufal, že se, Dagi, taky zapojíš do diskuse :)\r\n\r\nPřiznávám,
    že tohle je ve fázi co by kdyby - tj. jednou ráno jsem se vzbudil s tímhle nápadem
    v hlavě. Co se týká jistoty jestli a jak nám to pomůže žádná čísla nemám - otázka
    je, jestli se dají odhadnout jinak než to zkusit nasadit. Za jistých předpokladů
    bych třeba dokázal zjistit statistické rozložení write vs. read, ale nakonec bude
    přeci jen záviset na tom, jak jsou ready s writama provázané, takže takováhle
    statistika mi přijde jako nevypovídající.\r\n\r\nJediná vypovídající statistika
    by podle mého názoru šla udělat jedině tehdy, kdybychom reálně do aplikace zavedly
    ty změny, které by určovaly, jestli by transakce mohla jít do repliky nebo do
    masteru a nasadili ji na nějaký systém, kde se doposud pracuje jen s masterem,
    v módu statistického sledování. Z toho pak teprve zjistit, kolik zátěže by šlo
    delegovat na repliky a jak bychom masteru ulevili (jak říkám, zatím ty naše databáze
    stíhají v pohodě všechno co mají, ale spíš se tak mentálně připravuju na budoucnost
    :) ).\r\n\r\nV souvislosti s tou interakcí mezi uživateli jsi mě přivedl na myšlenku,
    že bychom naráželi na druhotný problém:\r\n \r\nReplika má T-1\r\nJá zapíšu v
    T+0 - user_write_timestamp je T+0\r\nKolega zapíše v T+1 - já jeho zápis vidím,
    protože díky tomu, že replika má T-1 dotazuju MASTER\r\nReplika dožene master
    T+0\r\nJá si obnovím stránku a jdu už do repliky a vidím svůj zápis (T+0), ale
    zmizí mi zápis kolegy, protože ten je T+1 a na jeho timestampu se nečeká\r\n\r\nCache
    se podle mého dají těžko považovat za řešení ... pokud máš na data více pohledů
    - např. zkobinované s dalšími daty (JOINy) nebudou tyhle pohledy mezi sebou korelovat,
    pokud nebudou cache vygenerovány ve shodný čas. Tohle jsme právě probírali docela
    intenzivně a připadá nám tohle asi jako nejpracnější varianta - výhodou je ten
    odpadající roundtrip do DB.\r\n\r\nTo, že v jiné session stejný uživatel viděl
    sem tam maličko starší data, myslím, není problém. Většina lidí pracuje v jedné
    session - třeba si otevírá odkazy do nových tabů, ale session sdílí. Tohle už
    se obhájit myslím dá.\r\n\r\nAle dík moc za nakopnutí ohledně těch víc uživatelů."
- id: 97387
  author: Dagi
  author_email: pichlik@seznam.cz
  author_url: http://www.dagblog.cz/
  date: '2012-10-08 12:15:09 +0200'
  date_gmt: '2012-10-08 11:15:09 +0200'
  content: "Moje rada: nepoustet se do toho pokud to neni uzke hrdlo aplikace :-)\r\n\r\nJe
    skoda, ze pomer mezi read/write operacemi neznas. Ja bych rozhodne zacal tim,
    ze bych si zkusil napsat nejake sondy, abych tohle rozlozeni zjistil. To vam umozni
    vyvazat nektere zbytecne write operace viz to servisni volani, kterym aktualizujete
    stav uzivatele. To by mohlo pomoci v procisteni kodu aplikace v kazdem pripade,
    bez ohledu na to jakou strategii zvolite. \r\n\r\nJeste dve poznamky k tem replika
    reads:\r\n\r\n1.)  Obecne musi pro transakci platit, ze jakykoliv zapis do masteru
    musi implikovat read z masteru a naopak, aby to bylo konzistenti, ale to je myslim
    zrejme a pocitas s tim.\r\n\r\n2.)  Se casto pouzivaji na operace, kde eventual
    konzistence nevadi napr. reporting. Nesnazil bych se to tedy zapinat pro celou
    aplikaci ale pro mista kde to vyrazne pomuze. To jest nedelal bych to transparentne."
- id: 97412
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-10-08 13:59:55 +0200'
  date_gmt: '2012-10-08 12:59:55 +0200'
  content: "Ad 1) s tím se skutečně v návrhu počítá\r\nAd 2) zdá se, že tohle je asi
    konsenz většiny komentujících\r\n\r\nCo se týká poměru read/write operací - tušení
    je, že poměr readů bude vysoký, ale dokud chybí jasná čísla nedá se na tom stavět.\r\n\r\nDíky"
- id: 97416
  author: kepler
  author_email: c2851344@pjjkp.com
  author_url: ''
  date: '2012-10-08 14:14:23 +0200'
  date_gmt: '2012-10-08 13:14:23 +0200'
  content: "MySQL cluster je strasne zavadzajuce meno -- je to in-memory databaza
    ktora je urcena na uplne nieco ine.\r\n\r\nVsetko od Percona je bleeding-edge:
    zoberu MySQL aplikuju vsemozne patche z Googlu / Facebooku, otestuju a pustia
    von. Vacsinou to funguje ale ked potrebujes nieco specificke tak nachdzas len
    same bugy. XtraDB Cluster nie je ziadna vynimka... \r\n\r\n XtraDB Cluster ma
    zopar problemov:\r\n- pridavanie nodov a crash recovery je trochu tazkopadne\r\n-
    z casu na cas zacne odmietat nove spojenia (ale velmi ziedka)\r\n- je to MySQL..."
- id: 97418
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-10-08 14:19:35 +0200'
  date_gmt: '2012-10-08 13:19:35 +0200'
  content: Super, díky moc ... toto jsou hodně cenné názory. Dneska jsem probíral
    XtraDB cluster s našimi Operations a ti jsou v souvislosti s daty VELMI konzervativní.
    Což se ve světle těchto informací ukazuje jako správná cesta.
- id: 98086
  author: Filip Jirsák
  author_email: filip@jirsak.org
  author_url: ''
  date: '2012-10-10 09:19:10 +0200'
  date_gmt: '2012-10-10 08:19:10 +0200'
  content: "Šlo mi o to, že ani tohle nezaručuje, že uživatelův zápis už v replice
    je. Protože v replice může časovou značku zvýšit zápis jiného uživatele, který
    se do repliky dostane dřív, než zápis „můj“.\r\n\r\nNebo-li můžete mít dvě transakce,
    transakce A bude mít časovou značku 1, transakce B časovou značku 2. Do transakčního
    logu se ale mohou zapsat v pořadí B, A. Pak může nastat okamžik, kdy v replice
    už bude transakce B (takže podle časových značek „novější“ transakce), ale A tam
    nebude. Nebo-li uživatel stejně neuvidí svá data, protože v replice ještě nejsou,
    přestože tam jsou data z „novějších“ transakcí.\r\n\r\nPokud nechcete všechny
    transakce tvrdě seřadit za sebe, byla by ještě možnost transakce číslovat a do
    pomocné tabulky si ukládat přehled transakcí, které proběhly. Takže repliky byste
    se pak neptal na časovou značku, ale na to, zda má v tabulce transakcí záznam
    o transakci X. Samozřejmě je to náročnější na výkon, protože v té tabulce se bude
    muset hledat. Na druhou stranu tam potřebujete jen záznamy o aktuálních session,
    takže počet záznamů té tabulky by byl zhruba stejný, jako počet souběžně otevřených
    session. Ostatní záznamy by bylo možné průběžně mazat. Ale vůbec nemám představu,
    jaký dopad na výkon by něco takového mělo."
- id: 98087
  author: Filip Jirsák
  author_email: filip@jirsak.org
  author_url: ''
  date: '2012-10-10 09:28:47 +0200'
  date_gmt: '2012-10-10 08:28:47 +0200'
  content: Záleží na tom, zda „pořadí commitů“ je stejné pořadí, v jakém je vidí všechna
    spojení k databázi (obecně to neplatí, je možné, že MySQL je v tomhle specifická
    a tohle chování zaručuje). I kdyby to tak bylo, je potřeba jako časovou značku
    použít čas commitu transakce, což nevím, jestli jde nějak zjistit.
- id: 98670
  author: Herbi
  author_email: herbi2@seznam.cz
  author_url: ''
  date: '2012-10-13 00:01:17 +0200'
  date_gmt: '2012-10-12 23:01:17 +0200'
  content: "Nestačila by daleko primitivnější strategie čtení z master/slave ?\r\n-
    vše se čte ze slave\r\n- při prvním zápise se přepne na master a dále se čte z
    master\r\n- zpět na slave přepnout pokud byl uživatel neaktivní dobu T (neposílal
    requesty) \r\nKde T je empiricky zjištěná max. doba \"seconds_behind_master\"
    + nějaká rezerva.\r\n\r\nPři vhodném(velkém) poměru reads/writes by to mohlo fungovat.
    \r\nPokud jsou uživatelé kteří nezapisují, mohla by strategie fungovat i bez posledního
    bodu."
- id: 148466
  author: "&raquo; Šestý rok Myšlenek dne otce Fura Myšlenky dne otce Fura"
  author_email: ''
  author_url: http://blog.novoj.net/2013/01/01/sesty-rok-myslenek-dne-otce-fura/
  date: '2013-01-01 00:02:33 +0100'
  date_gmt: '2012-12-31 23:02:33 +0100'
  content: "[...] Úvaha nad horizontálním škálováním databází a těžkostmi s tím spojenými
    [...]"
---
<p><img class="alignleft size-thumbnail wp-image-2295" title="Replication" src="http://blog.novoj.net/binary/2012/10/revolve-150x150.jpg" alt="" width="150" height="150" />Škálování databází je velké téma a já rozhodně nejsem takový odborník, abych tady rozebíral kdovíjaké detaily. Zcela jistě znáte termíny jako je sharding, o kterém <a href="http://www.dagblog.cz/2007_12_23_archive.html" target="_blank">psal Dagi už před 5 lety</a>, popřípadě znáte termín <a href="http://cs.wikipedia.org/wiki/Partition_(datab%C3%A1ze)" target="_blank">partitioning</a>, který nám nabízejí některé DB stroje "<a href="http://dev.mysql.com/doc/refman/5.1/en/partitioning.html" target="_blank">zadarmo</a>" a jiné "<a href="http://www.oracle.com/cz/products/database/options/partitioning/index.html" target="_blank">za peníze</a>". Alternativním způsobem horizontálního škálování je <a href="http://dev.mysql.com/doc/refman/5.0/en/replication-solutions-scaleout.html" target="_blank">škálování pomocí sady replik pro čtení</a>, o kterém lze uvažovat v případě, že máte aplikaci, které řádově méně zapisuje do databáze než z ní čte. Konkrétně se jedná o to, že máte několik databázových strojů v režimu MASTER-SLAVE(S), který se často nasazuje už jen z důvodu <a href="http://www.percona.com/doc/percona-xtrabackup/howtos/setting_up_replication.html" target="_blank">hot-backupu</a> (tj. v případě výpadku master databáze je možné velmi rychle z repliky učinit nový master a pokračovat v běhu aplikace).</p>
<p>Jelikož já i moji kolegové jsme šetřiví, napadlo nás, že by nemuselo být od věci repliku, kterou naše Operations nasadili právě z důvodu hot-backupu využít i pro zrychlení / škálování aplikace. Jsme si samozřejmě vědomi, že tento přístup má svoje riziko - v případě výpadku jedné z databází a přepnutím master databáze na záložní repliku půjdou všechny dotazy původně rozdělené na dva stroje na jeden. Pokud bychom tedy uvažovali o tomto druhu škálování bylo by lepší se bavit o dvou replikách nebo by musela být záloha naddimenzovaná oproti master stroji.</p>
<p>Problém, na kterém jsme se však vždy zarazili, byl spojen s tím, že nemáte garantováno, kdy se v replice objeví stejná data jako na masteru. Zpoždění replikace se může pohybovat pouze v milisekundách, ale může nabývat i vyšší hodnoty. Pokud bychom tedy používali MASTER pouze na zápisy a některý ze SLAVE na čtení, budeme mít problém s tím, že data, která v jednom requestu uživatel vytvoří nemusí nutně v dalším requestu vidět. Ať si kdo chce co chce říká o <a href="http://en.wikipedia.org/wiki/Eventual_consistency" target="_blank">eventuální konzistenci</a> - tohle je z pohledu <a href="http://cs.wikipedia.org/wiki/BFU" target="_blank">BFU</a> zcela jasná chyba, kterou nám bude reportovat a požadovat její odstranění.</p>
<p>Napadaly nás různé možnosti kompenzačních technik, ale všechny byly dost pracné - zvlášť v kombinaci s tradiční relační databází, kdy má uživatel často k dispozici plnou škálu funkcí jako je ad-hoc třídění, filtrování, seskupování atp. Tento týden jsem ale dostal nápad, jak by mohlo být možné relativně jednoduše tento problém řešit a otevřít nám tak cestu k využití replik pro škálování. V tomto článku bych se chtěl o něj s Vámi podělit a třeba přijdete na nějaká úskalí, která mě nedošla a nápad půjde do koše. Když na žádná nepřijdete budu mít větší jistotu, že je nápad životaschopný.</p>
<p><a id="more"></a><a id="more-2293"></a></p>
<p>Můj nápad je stojí na znalosti přesné timestamp posledního zápisu uživatele a timestamp posledního synchronizovaného záznamu v replice. Zjednodušeně řečeno - jediné riziko čtení dat z repliky spočívá v tom, že tam ještě nemusí být data, která uživatel právě zapsal. Pokud mám jistotu, že tam data již jsou použiji ke čtení repliku, pokud vím, že tam nejsou použiji ke čtení zase master a budu tak dělat až do doby, než se mi data objeví na replikace. Pak přepnu čtení na repliku. Za předpokladu, že uživatel výrazně více čte z databáze než do ní zapisuje bude z master databáze číst jen velmi málo uživatelů po velmi omezenou dobu.</p>
<h2>Jak by to mohlo fungovat</h2>
<p>Pro zjištění toho, o kolik je replika zpožděná se používá jednoduchý princip - v master databázi se periodicky updatuje v nějaké tabulce řádek s timestamp. Tato aktualizace je samozřejmě také součástí replikace a tudíž, když si z této tabulky na replice timestamp přečteme, víme přesně o kolik je její obrázek světa pozadu - například víme, že replika má data z doby 5 sekund zpět oproti master databázi.</p>
<p>Na druhé straně si v aplikaci udržuji informaci o tom, kdy uživatel provedl poslední zápisovou operaci - opět pomocí timestamp. Potom vím, že když replica_timestamp &gt;= user_write_timestamp mohu bezpečně používat repliku pro čtení, jinak musím pro čtení používat master databázi. Je samozřejmě nutné pracovat s datumem a časem, který vidí databáze (např. pomocí <strong>select now() as user_write_timestamp</strong>) a nikoliv aplikační server (data se mohou lišit).</p>
<p>Princip jsem zachytil na následujícím activity diagramu:</p>
<p><a href="http://blog.novoj.net/binary/2012/10/Horizontal-scaling.png"><img class="aligncenter size-large wp-image-2299" title="Horizontal scaling" src="http://blog.novoj.net/binary/2012/10/Horizontal-scaling-1024x763.png" alt="" width="627" height="467" /></a></p>
<p>Jak je z nákresu vidět musíme mít možnost splnit následující předpoklady:</p>
<ol>
<li>musíme si udržovat <strong>user_write_timestamp</strong> někde v session uživatele</li>
<li>musíme si dokázat odlišit, jestli v transakci budeme mít zápis nebo ne</li>
<li>musíme přesně vědět o kolik je replika pozadu oproti masteru</li>
</ol>
<h2>Představa o konkrétním nasazení v našem prostředí</h2>
<p>Pokud bych chtěl výše uvedený princip aplikovat na druh aplikací, které vytváříme (web aplikace) nad vývojářským stackem, který používáme (Spring), mohl bych technicky implementovat mechanismus takto:</p>
<ol>
<li>user_write_timestamp udržovat v session uživatele a pomocí servlet filtru jej nastavovat a čistit v nějaké <a href="http://docs.oracle.com/javase/6/docs/api/java/lang/ThreadLocal.html" target="_blank">ThreadLocal</a> proměnné (dejme tomu <strong>UserDatabaseContext</strong>), která je dostupná pomocí statické metody odkudkoliv z aplikace</li>
<li>zápisové transakce detekovat přes výskyt Spring anotace <a href="http://static.springsource.org/spring/docs/3.0.x/api/org/springframework/transaction/annotation/Transactional.html" target="_blank">@Transactional</a> pomocí AOP Pointcutu, který opět do nějaké <a href="http://docs.oracle.com/javase/6/docs/api/java/lang/ThreadLocal.html" target="_blank">ThreadLocal</a> proměnné uloží příznak, že se jedná o zápis a po ukončení metody opět ThreadLocal vyčistit (je nutné ovšem projít aplikační vrstvu a ověřit, že neexistuje nějaká jednoduchá metoda, která by zapisovala data do databáze bez použití @Transactional anotace - např. když prováděla pouze jediný SQL příkaz)</li>
<li>implementovat proxy nad <a href="http://docs.oracle.com/javase/6/docs/api/javax/sql/DataSource.html" target="_blank">DataSource</a>, která by při prvním dotazu v rámci requestu (využití existující proměnné <strong>UserDatabaseContext</strong>) zjistila zpoždění a použitelnost repliky a při volání <em>getConnection</em> metody by buď vracela připojení do master databáze nebo do databáze repliky</li>
</ol>
<div>Ze všech předchozích nápadů mi tento připadá jako jediný rozumně realizovatelný (myslím v kontextu existující rozsáhlé codebase), jelikož se dá z větší části implementovat jednotně na nízké úrovni aplikace a ponechá stávající aplikační logiku více-méně beze změny.</div>
<h2>Problémy, které mne napadají</h2>
<h3>V aplikaci máme logiku, která dělá časté "infrastrukturální" zápisy do databáze</h3>
<p>Například si ke každému uživateli pravidelně ukládáme informaci jestli je připojen on-line - tj. jestli s aplikací aktivně pracuje tak, že si ukládáme do databáze (třeba ne pokaždé, ale dost často) timestamp jeho posledního požadavku na aplikaci. Jedná se sice o zápisovou operaci, ale vůči uživateli je "neviditelná" - on sám neví, že se díky jeho činnosti v databázi něco aktualizovalo a proto ani v UI nečeká žádná data nebo efekty s tím spojené (operace má vliv pouze na ostatní uživatele, kde nám zpoždění tolik nevadí - když není moc velké). Přesto by nám tyto časté zápisy zvyšovaly pravděpodobnost, že uživatel bude číst data z master aplikace místo replik.</p>
<p>Napadá mne řešení si tyto specifické operace označit další anotací @UserInvisibleSideEffect, která by zamezila aktualizaci <strong>user_write_timestamp</strong> a tudíž by nevynucovala čtení z master databáze.</p>
<h3>Máme bezestavovou aplikaci</h3>
<p>A tedy není kam ukládat <strong>user_write_timestamp</strong>. V tuhle chvíli mne napadá leda použít nějakou zástupnou informaci, která by nám dokázala zjistit datum poslední aktualizace datasetu, ke kterému se vztahuje příchozí request. V tomto případě ale musíme provést minimálně jeden hit do master databáze, abychom se k podobnému údaji dostali a proto by se tento přístup vyplatil asi jen tehdy, kdyby nám stačilo zjistit jediné datum poslední aktualizace a otevřeli bychom si tím cestu k velkému množství čtení z repliky. Nebo kdyby zjištění data poslední aktualizace bylo velmi levné oproti následujícím dotazům pro čtení dat. Prostě, aby se nám to vůbec vyplatilo.</p>
<h3>Update 10. října 2012</h3>
<p>Tento článek posloužil svému účelu - v komentářích se vyskytlo několik zajímavých postřehů, které vedou k závěru, že tento přístup není bezpodmínečně bezpečný a má také svá slabá místa ...</p>
