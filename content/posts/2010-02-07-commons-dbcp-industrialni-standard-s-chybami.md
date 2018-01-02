---
status: publish
published: true
title: Commons DBCP industriální standard s chybami
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "V rámci zátěžových testů, které jsem v minulém týdnu prováděl jsem přišel
  na jednu zajímavou věc. Při velké zátěži došlo k \"zaseknutí\" Tomcatu, ze kterého
  se systém již nedokázal zotavit. Průvodním jevem byly otevřené konekce na databázi,
  přes které neprocházely žádné dotazy (tj. databáze nic nedělala), nulové zatížení
  procesoru Tomcatem, žádné Exception v logu. Příznaky nasvědčovaly tomu, že problém
  vězel v nějakých deadloccích - buď při práci s konekcemi do databáze nebo mezi aplikačními
  vlákny.\r\n\r\nPo nějaké době nikam nevedoucího pátrání v našem kódu jsem si napsal
  jednoduché wrappery nad DBCP DataSourcem a vracenou Connection, ve kterých jsem
  si ukládal stacktrace threadu i odkaz na vlastní thread, který si konekci z DataSourcu
  vybíral. Dál jsem zavedl monitor toho, zda thready používají vždy pouze jedinou
  connection a nesnaží se získat další, pokud ještě tu původní nevrátily (to by mohla
  být cesta k deadlockům).\r\n\r\nPři opětovném nasimulování problému mi monitor vypsal
  krásných 50 (tj. maximum poolu) vláken čekajících na uvolnění zámku s nasledujícím
  stacktracem (uvádím pouze pár nejdůležitějších řádků):\r\n\r\n<pre>\r\nat org.apache.commons.pool.impl.GenericKeyedObjectPool.returnObject
  (GenericKeyedObjectPool.java:870)\r\nat org.apache.commons.dbcp.datasources.KeyedCPDSConnectionFactory.connectionClosed
  (KeyedCPDSConnectionFactory.java:268)\r\nat com.mysql.jdbc.jdbc2.optional.MysqlPooledConnection.callListener
  (MysqlPooledConnection.java:209)\r\nat com.mysql.jdbc.jdbc2.optional.ConnectionWrapper.close
  (ConnectionWrapper.java:857)\r\nat com.mysql.jdbc.jdbc2.optional.ConnectionWrapper.close
  (ConnectionWrapper.java:480)\r\n</pre>\r\n\r\n"
wordpress_id: 783
wordpress_url: http://blog.novoj.net/?p=783
date: '2010-02-07 20:48:31 +0100'
date_gmt: '2010-02-07 19:48:31 +0100'
categories:
- Programování
- Databáze
tags:
- DBCP
- C3P0
comments:
- id: 18396
  author: Lucie Rut Bittnerova
  author_email: lucie@rut.cz
  author_url: ''
  date: '2010-02-08 09:16:18 +0100'
  date_gmt: '2010-02-08 08:16:18 +0100'
  content: Pekny clanek, jen bych mela drobnou poznamku, ze i programator muze psat
    jako normalni clovek, ba dokonce jako Cech :-) Vetsina anglickych terminu ma sve
    ceske varianty. Obzvlaste ceske sklonovani slova  "deadlock" v 6. pade a vyraz,
    ze "aplikace procesila" me dost tahaly za oci.
- id: 18399
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-02-08 09:58:13 +0100'
  date_gmt: '2010-02-08 08:58:13 +0100'
  content: Rád se nechám poučit - když jsem se kouknul na http://cs.wikipedia.org/wiki/Deadlock
    nepřišlo mi, že by české alternativy byly pro čtenáře jednoznačně vypovídající,
    kdežto deadlock ano. Hmm, a aplikace procesila - pravda, uznávám, že v tomhle
    ohledu by mě moje češtinářka asi nepochválila. Díky za kritiku - v dalších článcích
    na to pokusím soustředit.
- id: 18400
  author: uf
  author_email: ufak@seznam.cz
  author_url: ''
  date: '2010-02-08 10:33:34 +0100'
  date_gmt: '2010-02-08 09:33:34 +0100'
  content: "V odborne reci se vic pouziva anglicky termin. Pokukd se nekde vyskytuje
    cesky termin, doporucuju jako standard uvest v zavorce anglilcky termin (alespon
    u prvniho a pak dalsiho vzdaleneho vyskytu). \r\n\r\nCeske terminy byvaji dost
    casto paskvily. \r\n\r\nje fakt, ze Papa ma hroznou cestinu, ale jeho sloh, obraty
    a novotvary obcas pobavi a osvezi. To se mi na IT literature vzdy libilo, ze je
    odlehcena.\r\nUf"
- id: 18401
  author: Jméno
  author_email: info@example.com
  author_url: ''
  date: '2010-02-08 10:48:40 +0100'
  date_gmt: '2010-02-08 09:48:40 +0100'
  content: Zajímalo by mě vaše nastavení C3P0. Nemůžete se podělit?
- id: 18402
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-02-08 11:19:55 +0100'
  date_gmt: '2010-02-08 10:19:55 +0100'
  content: "Pro zátěžové testy jsem používal:\r\n\r\nminPoolSize: 50\r\nmaxPoolSize:
    50\r\nnumHelperThreads: 10\r\npreferredTestQuery: select now()\r\nidleConnectionTestPeriod:
    60"
- id: 18408
  author: ao
  author_email: ondrus@lesipa.sk
  author_url: ''
  date: '2010-02-08 15:06:25 +0100'
  date_gmt: '2010-02-08 14:06:25 +0100'
  content: "Ďakujem za článok.\r\n\r\nNie je v ňom uvedené o aké verzie knižníc sa
    jedná. Predpokladám, že ide o verzie:\r\n- DBCP 1.2.2\r\n- c3p0 0.9.1.2\r\n\r\nNemýlim
    sa?"
- id: 18409
  author: Juraj
  author_email: juraj.misur@gmail.com
  author_url: ''
  date: '2010-02-08 15:08:28 +0100'
  date_gmt: '2010-02-08 14:08:28 +0100'
  content: Jeden maly hint - pri podozreni na deadlock by som ako prvu moznost vyskusal
    pripojit sa k procesu pomocou jconsole, ktora vie vypisat zoznam vlakien a ich
    aktualny stacktrace. Velmi rychle takto zistite, kde su vlakna zablokovane.
- id: 18422
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-02-08 15:31:38 +0100'
  date_gmt: '2010-02-08 14:31:38 +0100'
  content: "Verze:\r\n\r\nDBCP - 1.2.2\r\nC3P0 - 0.9.1 (čtvrté číslo jsem z JARu nezjistil)\r\n\r\nDíky
    za tip JConsole jsem nevěděl."
- id: 18504
  author: soulfly
  author_email: soulfly1983@gmail.com
  author_url: ''
  date: '2010-02-10 13:53:18 +0100'
  date_gmt: '2010-02-10 12:53:18 +0100'
  content: S DBCP som si uzil tiez svoje .. koho by napadlo ze kniznica z apache commons
    moze byt taky shit
- id: 19004
  author: Jakub Exner
  author_email: ex1@seznam.cz
  author_url: ''
  date: '2010-02-15 18:37:37 +0100'
  date_gmt: '2010-02-15 17:37:37 +0100'
  content: Včera byla vydána nová verze DBCP. Prošel jsem v rychlosti "podezřelé"
    JIRA issues ze seznamu opravených chyb http://commons.apache.org/dbcp/changes-report.html#a1.4
    a vypadá to, že problémy byly opraveny, včetně DBCP-44, viz poznámka u http://issues.apache.org/jira/browse/DBCP-270.
    Prakticky vyzkoušenu tuto novou verzi nemám.
- id: 19006
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-02-15 20:46:12 +0100'
  date_gmt: '2010-02-15 19:46:12 +0100'
  content: Jestli budu mít chvilku, zkusím na té mé testovací instalaci nastavit znovu
    DBCP a projet zátěžový test (tam jsem dosahoval deadlocků se 100% úspěšností).
    Zkusil bych sem výsledky dát ...
---
<p>V rámci zátěžových testů, které jsem v minulém týdnu prováděl jsem přišel na jednu zajímavou věc. Při velké zátěži došlo k "zaseknutí" Tomcatu, ze kterého se systém již nedokázal zotavit. Průvodním jevem byly otevřené konekce na databázi, přes které neprocházely žádné dotazy (tj. databáze nic nedělala), nulové zatížení procesoru Tomcatem, žádné Exception v logu. Příznaky nasvědčovaly tomu, že problém vězel v nějakých deadloccích - buď při práci s konekcemi do databáze nebo mezi aplikačními vlákny.</p>
<p>Po nějaké době nikam nevedoucího pátrání v našem kódu jsem si napsal jednoduché wrappery nad DBCP DataSourcem a vracenou Connection, ve kterých jsem si ukládal stacktrace threadu i odkaz na vlastní thread, který si konekci z DataSourcu vybíral. Dál jsem zavedl monitor toho, zda thready používají vždy pouze jedinou connection a nesnaží se získat další, pokud ještě tu původní nevrátily (to by mohla být cesta k deadlockům).</p>
<p>Při opětovném nasimulování problému mi monitor vypsal krásných 50 (tj. maximum poolu) vláken čekajících na uvolnění zámku s nasledujícím stacktracem (uvádím pouze pár nejdůležitějších řádků):</p>
<pre>
at org.apache.commons.pool.impl.GenericKeyedObjectPool.returnObject (GenericKeyedObjectPool.java:870)
at org.apache.commons.dbcp.datasources.KeyedCPDSConnectionFactory.connectionClosed (KeyedCPDSConnectionFactory.java:268)
at com.mysql.jdbc.jdbc2.optional.MysqlPooledConnection.callListener (MysqlPooledConnection.java:209)
at com.mysql.jdbc.jdbc2.optional.ConnectionWrapper.close (ConnectionWrapper.java:857)
at com.mysql.jdbc.jdbc2.optional.ConnectionWrapper.close (ConnectionWrapper.java:480)
</pre>
<p><a id="more"></a><a id="more-783"></a></p>
<p>Žádná chyba v našem kódu tedy nebyla - při vracení konekce zpátky do DBCP poolu docházelo k deadlockům. Po tomto překvapivém zjištění jsem začal pátrat po zkušenostech s DBCP a ouha - Google mi vrátil celou řádku článků, které narážejí na to, že v DBCP skutečně k deadlockům dochází. Je to o to překvapivější, že jsem dosud Commons DBCP považoval za odladěný industriální standard (integrovaný např. v Tomcatu). Pátrání mě navedlo k <a href="http://issues.apache.org/jira/secure/IssueNavigator.jspa?reset=true&&query=deadlock&summary=true&description=true&body=true&pid=12310469" target="blank">již hlášeným (a opraveným chybám)</a>.</p>
<p>Podobné dotazy proběhly i Tomcat Dev mail konferencí. Velmi zajímavá je <a href="http://www.mail-archive.com/dev@commons.apache.org/msg11139.html" target="_blank">reakce jednoho z ?vývojářů? Tomcatu</a> z července 2009:</p>
<p><cite><br />
<b>I encountered an issue that looks similar to Bug DBCP-270.<br><br><br />
1) Is it the same bug or a new one?</b><br />
Yes, that is DBCP-270<br />
</cite></p>
<p><cite><br />
<b>2) Which patch can I apply and how to apply it?</b><br />
You'd need to apply the patch for DBCP-270 to a local copy of DBCP and then<br />
build Tomcat with your modified DBCP sources.<br />
</cite></p>
<p><cite><br />
<b>3) Will setting testWhileIdle="false" avoid the problem?</b><br />
No. You'd need to completely disable the evictor thread. Note that there are<br />
other potential deadlocks not related to the evictor that you may still hit.<br />
</cite></p>
<p>Nakonec jsme z aplikace vypárali DBCP a vyzkoušeli implementaci nad C3P0. Při obodbných nastaveních a stejném zátěžovém testu jsme k deadlocku již nedošli. Aplikace se z přetíženého stavu po nějakém čase zotavila a standardně procesila požadavky dál.</p>
<p>Přestože je tedy C3P0 podle zdrojů, které jsme našli na internetu pomalejší než DBCP, stabilita a spolehlivost aplikace je pro nás výrazně důležitější, než pár milisekund při práci s poolem. Diagnostika zatuhlého Tomcatu a následný restart stojí totiž výrazně větší "service leak" než drobné navýšení zátěže.</p>
<h2>Reference</h2>
<ul>
<li><a href="http://javatech.org/2007/11/c3p0-vs-dbcp-the-straight-dope/" target="blank">Porovnání C3P0 a DBCP - především s ohledem na rychlost</a></li>
<li><a href="http://stackoverflow.com/questions/520585/connection-pooling-options-with-jdbc-dbcp-vs-c3p0" target="blank">StackOverflow Q&A - názory zmiňující deadlocky při práci s DBCP</a></li>
<li><a href="http://jolbox.com/" target="blank">Jeden z nejnovějších connection poolingů BareCP - ačkoliv asi nejrychlejší, prozatím nedostatečně prověřený praxí</a></li>
<li><a href="http://blogs.nyu.edu/blogs/nrm216/sakaidelic/2007/12/difference_between_dbcp_and_c3.html" target="blank">Další pojednání o rychlosti a deadloccích v DBCP</a></li>
<li><a href="http://forum.springsource.org/showthread.php?t=45575" target="blank">Diskuse na fóru SpringSource  na téma Connection poolingu</a></li>
</ul>
