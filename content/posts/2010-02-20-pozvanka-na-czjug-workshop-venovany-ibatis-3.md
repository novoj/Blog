---
status: publish
published: true
title: Pozvánka na CZJUG Workshop věnovaný iBatis 3
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Rád bych vás všechny pozval na workshop na téma <a href=\"http://ibatis.apache.org/java.cgi\"
  target=\"_blank\">iBatis 3</a> konaný 3. března 2010 od 18 hodin v rámci CZ JUG
  setkání (pozor tato praktická setkání se konají v Národní technické knihovně v Praze
  - Dejvicích - viz. mapka dole). <a href=\"http://ibatis.apache.org/java.cgi\" target=\"_blank\">iBatis</a>
  je framework pro mapování dat uložených v relační databázi na Java objekty. Už po
  několik let je zajímavou alternativkou k ORM frameworkům postaveným na JPA (jehož
  typickým představitelem je <a href=\"https://www.hibernate.org/\" target=\"_new\">Hibernate</a>).
  Mottem <a href=\"http://ibatis.apache.org/java.cgi\" target=\"_blank\">iBatisu</a>
  je zjednodušit vývojářům práci s databází a přitom zůstat tak jednoduchý, jak jen
  to je možné. Právě jednoduchostí a nízkoúrovňovým přístupem k databázi si získal
  celou řadu vývojářů a v řadě případů poráží i daleko silnější frameworky.\r\n\r\nNa
  workshopu si budete moci sami vyzkoušet práci s <a href=\"http://ibatis.apache.org/java.cgi\"
  target=\"_blank\">iBatisem 3</a>, který právě spatřil světlo světa. Kromě novinek
  v <a href=\"http://ibatis.apache.org/java.cgi\" target=\"_blank\">iBatisu</a> bude
  k vyzkoušení jeho integrace do Spring Frameworku 3.1. Obě dvě záležitosti ještě
  nemají své stabilní verze, takže budou k vyzkoušení opravdu žhavé novinky. V průběhu
  bude vyhlášena soutěž o jednu licenci vývojového prostředí <a href=\"http://www.jetbrains.com/idea/\"
  target=\"_new\">IntelliJ Idea 9 Ultimate Edition</a>, kterou věnovala společnost
  <a href=\"http://www.jetbrains.com/\" target=\"_new\">JetBrains</a>.\r\n\r\n"
wordpress_id: 807
wordpress_url: http://blog.novoj.net/?p=807
date: '2010-02-20 22:03:55 +0100'
date_gmt: '2010-02-20 21:03:55 +0100'
categories:
- Programování
- Java
- iBatis
- Databáze
tags: []
comments:
- id: 19741
  author: Libor
  author_email: l.prenek@gmc.net
  author_url: ''
  date: '2010-02-22 07:44:22 +0100'
  date_gmt: '2010-02-22 06:44:22 +0100'
  content: "Nazdar, workshop me hodne zajima, ale bohuzel nemuzu se zucastnit. Bude
    z teto akce porizeno video?\r\nDik"
- id: 19743
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-02-22 08:46:17 +0100'
  date_gmt: '2010-02-22 07:46:17 +0100'
  content: Nejsem si jistý - spíš bych řekl, že ne. Workskop bych chtěl ještě opakovat
    někdy v květnu / červnu pro studeny Univerzity Hradec Králové (dám vědět minimálně
    přes twitter přesný termín). Nicméně, cvičení jsou ke stažení již teď, řešení
    doplním cca týden po workskopu.
- id: 19898
  author: Dagi
  author_email: pichlik@seznam.cz
  author_url: http://sweb.cz/pichlik
  date: '2010-02-23 17:57:24 +0100'
  date_gmt: '2010-02-23 16:57:24 +0100'
  content: Workshopy bohuzel nejsou nahravany.
- id: 20417
  author: Tomáš Záluský
  author_email: zalusky@centrum.cz
  author_url: ''
  date: '2010-03-02 17:35:01 +0100'
  date_gmt: '2010-03-02 16:35:01 +0100'
  content: "Stáhnul jsem si projekt a importoval do Eclipse jako Maven projekt,\r\nale
    mvn package vypíše problém u jmxtools a jmxri. \r\n\r\n[DEBUG] Connecting to repository:
    'java.net' with url: 'https://maven-repository.dev.java.net/nonav/repository'.\r\nDownloading:
    https://maven-repository.dev.java.net/nonav/repository/com.sun.jdmk/poms/jmxtools-1.2.1.pom\r\n[DEBUG]
    attempting to create parent directories for destination: jmxtools-1.2.1.pom.tmp\r\n357b
    downloaded  (jmxtools-1.2.1.pom)\r\n[WARNING] *** CHECKSUM FAILED - Checksum failed
    on download: local = 'b662aa01d49d8a571aa79f67a1d4a92a7d9c6359'; remote = '&lt;!DOCTYPE&#039;
    - RETRYING\r\n\r\nV lokální repository jsou soubory .jar a .pom, ale jejich obsah
    je HTML s chybou 301:\r\n\r\nMoved Permanently\r\nThe document has moved <a href=\"http://download.java.net/maven/1/com.sun.jdmk/jars/jmxtools-1.2.1.jar\"
    rel=\"nofollow\">here</a>.\r\n\r\nDělám něco špatně nebo je chyba v tom, že artefakt
    není v pořádku v centrální repository? Zkoušel jsem dát do pomu repository s navrhovaným
    URL, ale chyba přetrvávala. Nakonec jsem to vyřešil tak, že jsem .jar soubory
    přepsal v repository těmi z adresáře lib ze zipu pro workshop. Ale zajímalo by
    mě, zda je to správně, koukám, že na nich závisí jen log4j. Testy v packagi init
    mi pak prošly (ty ostatní ne, ale předpokládám, že je budeme na workshopu \"opravovat\").\r\n\r\nDíky!"
- id: 20418
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-03-02 17:42:40 +0100'
  date_gmt: '2010-03-02 16:42:40 +0100'
  content: V trunku je to již v pom.xml excludováno. Kdy sis to z GitHubu stahoval?
- id: 20467
  author: Tomas Zalusky
  author_email: zalusky@centrum.cz
  author_url: ''
  date: '2010-03-03 08:58:33 +0100'
  date_gmt: '2010-03-03 07:58:33 +0100'
  content: Včera v 16:18. Ale i dnes ráno stahuji stejný zip. Stahoval jsem to jako
    zip přes Download source. V zipu je stejný pom jako na http://github.com/novoj/iBatisWorkShop/blob/master/pom.xml
    - log4j obsahuje exclusion jen na mail a jms.
- id: 20470
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-03-03 09:11:13 +0100'
  date_gmt: '2010-03-03 08:11:13 +0100'
  content: Opravdu, tyhle jsem nevyjmul. Pom jsem doupravil. Teď už by je to chtít
    nemělo.
- id: 20590
  author: Brdloush
  author_email: brdloush@brdloush.net
  author_url: ''
  date: '2010-03-04 10:05:11 +0100'
  date_gmt: '2010-03-04 09:05:11 +0100'
  content: "Ahoj, ten problém s jmxtools jsem včera řešil taky. Narazil jsem na tohle:
    http://jira.codehaus.org/browse/MEV-649?page=com.atlassian.streams.streams-jira-plugin%3Aactivity-stream-issue-tab.
    Šel jsem cestou 3 a zafungovalo to ok:\r\n\r\nSolution (3) - the best one. Use
    version log4j 2.1.14 instead. It seems to be OK."
- id: 20605
  author: Jarda Jirava
  author_email: jarda@jirava.net
  author_url: http://jirava.net/blog
  date: '2010-03-04 14:41:12 +0100'
  date_gmt: '2010-03-04 13:41:12 +0100'
  content: "Díky za včerejší workshop, ať zarytý .netista, tak jsem byl zvědav, jak
    iBatis v Javě pokročil a na co se mohu těšit nového v iBatis.NET.\r\nCo mě mrzí,
    že mi unikl začátek, přeci jen se rozkoukat v jave, byt v pekne pripravenem projektu
    bylo při sledování výkladu složitější.\r\nPřesto díky, moc pěkně připraveno a
    určitě je to inspirací, jak také vést UG v .NETu.\r\nJarda"
- id: 20608
  author: Tomas
  author_email: tomas.bublik@gmail.com
  author_url: ''
  date: '2010-03-04 15:30:07 +0100'
  date_gmt: '2010-03-04 14:30:07 +0100'
  content: "Na jaky e-mail mame posilat resene testy?\r\nDiky"
- id: 20617
  author: Jirka
  author_email: jiri.samek@post.cz
  author_url: ''
  date: '2010-03-04 17:24:26 +0100'
  date_gmt: '2010-03-04 16:24:26 +0100'
  content: Bohuzel jsem si taky nezapsal email na jaky mame posilat resene testy.
- id: 20629
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-03-04 20:59:41 +0100'
  date_gmt: '2010-03-04 19:59:41 +0100'
  content: "Řešení možné odeslat na libovolný z:\r\n\r\nnovotnaci zavináč gmail tečka
    com\r\nnovotny zavináč fg tečka cz\r\n\r\nDíky za všechny ohlasy."
---
<p>Rád bych vás všechny pozval na workshop na téma <a href="http://ibatis.apache.org/java.cgi" target="_blank">iBatis 3</a> konaný 3. března 2010 od 18 hodin v rámci CZ JUG setkání (pozor tato praktická setkání se konají v Národní technické knihovně v Praze - Dejvicích - viz. mapka dole). <a href="http://ibatis.apache.org/java.cgi" target="_blank">iBatis</a> je framework pro mapování dat uložených v relační databázi na Java objekty. Už po několik let je zajímavou alternativkou k ORM frameworkům postaveným na JPA (jehož typickým představitelem je <a href="https://www.hibernate.org/" target="_new">Hibernate</a>). Mottem <a href="http://ibatis.apache.org/java.cgi" target="_blank">iBatisu</a> je zjednodušit vývojářům práci s databází a přitom zůstat tak jednoduchý, jak jen to je možné. Právě jednoduchostí a nízkoúrovňovým přístupem k databázi si získal celou řadu vývojářů a v řadě případů poráží i daleko silnější frameworky.</p>
<p>Na workshopu si budete moci sami vyzkoušet práci s <a href="http://ibatis.apache.org/java.cgi" target="_blank">iBatisem 3</a>, který právě spatřil světlo světa. Kromě novinek v <a href="http://ibatis.apache.org/java.cgi" target="_blank">iBatisu</a> bude k vyzkoušení jeho integrace do Spring Frameworku 3.1. Obě dvě záležitosti ještě nemají své stabilní verze, takže budou k vyzkoušení opravdu žhavé novinky. V průběhu bude vyhlášena soutěž o jednu licenci vývojového prostředí <a href="http://www.jetbrains.com/idea/" target="_new">IntelliJ Idea 9 Ultimate Edition</a>, kterou věnovala společnost <a href="http://www.jetbrains.com/" target="_new">JetBrains</a>.</p>
<p><a id="more"></a><a id="more-807"></a></p>
<p>Zjednodušený program workshopu:</p>
<ul align='left'>
<li>agenda a základní popis iBatis</li>
<li>zprovoznění iBatis na projektu - ukázka integrace do Spring 3.X</li>
<li>základní použití: CRUD</li>
<li>podpora immutable objektů</li>
<li>práce se sekvencemi</li>
<li>asociace a kolekce
<ul>
<li>lazy loading (N+1 problém)</li>
<li>join selecty</li>
</ul>
</li>
<li>dynamické SQL</li>
<li>použití anotací</li>
<li>diskriminátory a typehandlery</li>
</ul>
<p><strong>Kde:</strong> <a href="http://www.mapy.cz/#mm=ZP@sa=s@st=s@ssq=n%C3%A1rodn%C3%AD%20technick%C3%A1%20knihovna@sss=1@ssp=113925228_121581260_156654700_156528332@x=133005408@y=136011649@z=15" target="_new">Národní technická knihovna, Praha - Dejvice</a><br><br />
<strong>Místnost:</strong> <a href="http://www.techlib.cz/cs/sluzby/konferencni-sluzby-a-pronajmy/konferencni-prostory-ballinguv-sal/" target="_new">Ballingův sál</a><br />
<strong>Kdy:</strong> 3. března 2010, od 18:00 do 19:30<br><br />
<strong>Přednášející:</strong> Jan Novotný (FG Forrest)</p>
<h3>Příprava na workshop</h3>
<p>Na sále je k dispozici volné WiFi připojení, nicméně doporučuji si předem stáhnout materiály z adresy:</p>
<ul>
<li>GIT klient: git://github.com/novoj/iBatisWorkShop.git</li>
<li>HTTP: <a href="http://github.com/novoj/iBatisWorkShop/tree/master" target="_blank">http://github.com/novoj/iBatisWorkShop/tree/master</a> (v menu odkaz Download sources)</li>
</ul>
<p>Dále si, pokud možno předem, zprovozněte projekt ve svém oblíbeném IDE. Pokud používáte Apache Maven mělo by vám stačit importovat projekt do IDE a měli byste mít hotovo. V opačném případě naleznete všechny potřebné knihovny v podadresáři LIB, zdrojové kódy nastavte na adresáře <b>src/main/java</b> a <b>src/main/resources</b>, adresáře pro testy na adresáře <b>src/test/java</b> a <b>src/test/resources</b>.</p>
<p>Pokud vám všechny testy z package <b>cz.novoj.ibatis.init</b> projdou, jste připraveni a budu se těšit na Vaši účast.</p>
