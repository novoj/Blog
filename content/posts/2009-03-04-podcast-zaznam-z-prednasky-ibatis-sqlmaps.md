---
status: publish
published: true
title: 'Podcast: Záznam z přednášky iBatis SqlMaps'
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Tento týden proběhla na Univerzitě v Hradci Králové přednáška na téma iBatis
  SqlMaps. V přednášce jsem se snažil projít všemi základními funkcionalitami iBatisu
  a porovnat jej krátce s několika dalšími přístupy k implementaci datové vrstvy (plain
  JDBC, JPA / Hibernate) a podívat se co nového nás čeká v nové verzi iBatis číslo
  3.\r\n\r\nKvůli omezenému rozsahu (1,5 hodiny) nemohlo dojít na trošku sofistikovanější
  záležitosti jako je použití diskrimintárů a resultObjectFactory, integrace se Springem,
  dávkovému zpracování dotazů do databáze a použití iBatoru. Pokud byste měl kdokoliv
  nějaké otázky týkající se těchto oblastí, neváhejte je napsat do komentářů k tomuto
  postu, a já se je pokusím zodpovědět a popřípadě publikovat i další příklady.\r\n\r\n"
wordpress_id: 408
wordpress_url: http://blog.novoj.net/?p=408
date: '2009-03-04 18:26:55 +0100'
date_gmt: '2009-03-04 17:26:55 +0100'
categories:
- Java
- Podcast
- iBatis
tags: []
comments:
- id: 6727
  author: Pavel Stastny
  author_email: pavel.stastny@gmail.com
  author_url: ''
  date: '2009-03-05 10:41:55 +0100'
  date_gmt: '2009-03-05 09:41:55 +0100'
  content: "Dobra prace ;-)  \r\n\r\nDiky. \r\n\r\n -happy"
- id: 6729
  author: Tomáš Homola
  author_email: tomas.homola@gmail.com
  author_url: ''
  date: '2009-03-05 10:52:42 +0100'
  date_gmt: '2009-03-05 09:52:42 +0100'
  content: Dobrá přednáška... bude někdy nějaký pokračování? třeba rozšíření informací
    co tam právě nebyly řečeni integrace se springem atd? Nebo přednáška věnovaná
    Hibernate?
- id: 6735
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-03-05 13:39:50 +0100'
  date_gmt: '2009-03-05 12:39:50 +0100'
  content: "No o Hibernatu se asi neodvážím moc hovořit - v této oblasti bych řekl
    nemám dost znalostí ani zkušeností. Radši přednáším o věcech, ve kterých mám alespoň
    1-2 roky praxi, abych mohl říct i o praktických zkušenostech a dopadech.\r\n\r\nPokračování
    neplánuji - možná až vyjde iBatis 3, mohl bych nějakým způsobem provést update,
    protože tento release vypadá opravdu zajímavě.\r\n\r\nPokud byste měl nějaký konkrétní
    dotaz k těm věcem co jsem vynechal, stačí napsat a já se pokusím odpovědět."
- id: 6750
  author: Petr
  author_email: Petr.Charvat@gmail.com
  author_url: http://pcharvat.blogspot.com/
  date: '2009-03-06 13:33:56 +0100'
  date_gmt: '2009-03-06 12:33:56 +0100'
  content: Super přednáška. Potvrzuji, že učící křivka se počítá na hodiny. Používal
    jsem iBatis ve spojení se springem, který také řídil transakce a nezaznamenal
    jsem jediný problém. Jako náhrada JdbcTemplate je ideální.
- id: 6804
  author: Jety
  author_email: mail@jetensky.net
  author_url: http://jetensky.net/blog
  date: '2009-03-09 15:30:34 +0100'
  date_gmt: '2009-03-09 14:30:34 +0100'
  content: "Ahoj Honzo, díky za přednášku. Mám dotaz, jakou má výhodu syntaxe $parameter$
    oproti #parameter#.  Jinými slovy zda se dá obecně říct \"Vždy používejte syntaxy
    #parameter# a nikdy $parameter$, abyste neriskovali SQL injection?\".\r\n\r\nBtw.
    Ten powerpoint je příjemně přehledný, tuším, že to dalo dost práce.\r\nJety"
- id: 6807
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-03-09 17:40:26 +0100'
  date_gmt: '2009-03-09 16:40:26 +0100'
  content: "No ten #parameter# je vždy bezpečný - jenomže ho nemůžeš použít na všech
    místech v tom SQL - pokud potřebuješ napsat dynamickou ORDER BY klauzuli, tak
    se bez $parameter$ neobejdeš. Skutečně si to stačí v hlavě představit, jak to
    bude přeložené do toho JDBC zápisu. Tzn. k výše uvedenému zápisu - není možné
    zapsat SQL:\r\n\r\nselect * from TABULKA order by ? ?\r\n\r\nTo by JDBC zařvalo
    - to akceptuje parametry jen skutečně na místech, které jsou pro parametry platné
    (tzn. např where podmínky \"where sloupec = ?\" apod.). \r\n\r\nPro ty dolarové
    zápisy je teda dobré to dělat tak, že pokud ti jde parametr z url, tak si při
    přípravě vstupů do mapované query iBatisu uděláš:\r\n\r\nif (\"asc\".equalsIgnoreCase(urlParameter))
    {\r\n   iBAtisParameters.put(\"type\", \"asc\"));\r\n} else {\r\n   iBAtisParameters.put(\"type\",
    \"desc\"));\r\n}\r\n\r\nJe to sice trošku víc psaní, ale jednodušeji to podle
    mého nejde, aniž by ses nevystavil SQL Injection. Na druhou stranu, tohle by asi
    iBatis nemohl dost dobře suplovat."
- id: 6832
  author: lzap
  author_email: lzap@seznam.cz
  author_url: ''
  date: '2009-03-10 12:40:38 +0100'
  date_gmt: '2009-03-10 11:40:38 +0100'
  content: "Ty ajaxový SNAPSHOTY jsou odporný, jak to vypnout? Furt se mi to tady
    objevuje.\r\n\r\nPěkná přednáška."
- id: 6835
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-03-10 13:11:06 +0100'
  date_gmt: '2009-03-10 12:11:06 +0100'
  content: Vypnul jsem je. Kdysi se mi zdály jako dobrej nápad, ale už se mi taky
    moc nepozdávají - tvůj komentář byla poslední kapka ;-)
- id: 6846
  author: benzin
  author_email: bendal@quick.cz
  author_url: http://live.jabbim.cz/benzin
  date: '2009-03-11 08:30:55 +0100'
  date_gmt: '2009-03-11 07:30:55 +0100'
  content: 'P.S.: Jeste k tomu ## a $$ je dobre podotknout ze nejenom SQL Injection
    to resi. Resi to taky kompilaci SQL dotazu a delku logu. Kdyz totiz rvete hodnoty
    primo do SQL musi serve pokazde znovu kompilovat dotaz a pokazde si o nem udela
    zapis do logu, kdezto kdyz pouzijete ?, tak ke kompilaci dojde (v idealnim pripade)
    jenom jednou a i logu se tim hodne ulevi.'
- id: 6848
  author: Ex1
  author_email: jexner@centrum.cz
  author_url: ''
  date: '2009-03-11 12:25:40 +0100'
  date_gmt: '2009-03-11 11:25:40 +0100'
  content: Dobře udělané a informativní. Díky.
- id: 12968
  author: Tomáš Procházka
  author_email: atom@atomsoft.cz
  author_url: ''
  date: '2009-10-06 06:38:43 +0200'
  date_gmt: '2009-10-06 05:38:43 +0200'
  content: "Na Slidu 18 je v Mapperu toto:\r\n\r\n\r\n\r\nNepodařilo se mi nikde najít
    zmíňku o tom, že je toto podporováno (ani ve verzi 3 beta), dokonce ani v doctypu
    parameters není. I když bylo by to krásně a je to to poslední, co mi v iBatisu
    chybí, abych ho mohl začít používat.\r\n\r\nNa podobné téma jsem se ptal v konferenci:\r\nhttp://www.mail-archive.com/user-java@ibatis.apache.org/msg14807.html"
- id: 12969
  author: Tomáš Procházka
  author_email: atom@atomsoft.cz
  author_url: ''
  date: '2009-10-06 06:56:54 +0200'
  date_gmt: '2009-10-06 05:56:54 +0200'
  content: "Napsal jsem na to Issue:\r\nhttp://issues.apache.org/jira/browse/IBATIS-669\r\n\r\nDále
    není pravda, že anotace jsou plnohodnotné XML, rozhodně nejsou."
- id: 12971
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-10-06 12:48:49 +0200'
  date_gmt: '2009-10-06 11:48:49 +0200'
  content: "Ahoj Tomáši, tahle přednáška vznikla ještě v době, kdy o iBatisu 3 toho
    ještě moc známo nebylo. Vycházel jsem především z Whitepaperu, který byl na téma
    iBatis 3 zpracován. Na blogu mám teď dva daleko aktuálnější články o třetí verzi
    iBatisu:\r\n\r\nhttp://blog.novoj.net/2009/08/16/ibatis-30-preview-cast-prvni/\r\nhttp://blog.novoj.net/2009/08/23/ibatis-30-preview-cast-druha/\r\n\r\nV
    XML konfiguraci pak zcela běžně používají pojmenovaných parametrů víc. Pročítal
    jsem mail thread a vidím problémy s anotacemi. V Javě se v reflexi bohužel nedají
    číst názvy parametrů metody - tj. iBatis nemá z čeho zjistit názvy parametrů,
    které jsou následně v anotaci používány. Proto zatím umožňují pouze jeden parametr.
    Jediné dvě možné řešení je tvorba extra anotace, nebo používání indexů - a to
    ani jedno není moc komfortní. Dalším možností by bylo použít knihovnu Paranamer
    (http://paranamer.codehaus.org/) od Codehausu, ale ani ta není 100% - má například
    problémy s interfacy. Uvidíme, jak si s issue poradí Clinton Begin.\r\n\r\nCo
    se týká toho, že anotace plnohodnotně pokrývají možnosti XML - vycházím z toho,
    co o tom tvrdí autoři. Pokud to není plnohodnotné, mělo by se to tomu blížit.\r\n\r\nNicméně
    máš pravdu, co se týká 3tí verze, mám zatím limitované vědomosti."
---
<p>Tento týden proběhla na Univerzitě v Hradci Králové přednáška na téma iBatis SqlMaps. V přednášce jsem se snažil projít všemi základními funkcionalitami iBatisu a porovnat jej krátce s několika dalšími přístupy k implementaci datové vrstvy (plain JDBC, JPA / Hibernate) a podívat se co nového nás čeká v nové verzi iBatis číslo 3.</p>
<p>Kvůli omezenému rozsahu (1,5 hodiny) nemohlo dojít na trošku sofistikovanější záležitosti jako je použití diskrimintárů a resultObjectFactory, integrace se Springem, dávkovému zpracování dotazů do databáze a použití iBatoru. Pokud byste měl kdokoliv nějaké otázky týkající se těchto oblastí, neváhejte je napsat do komentářů k tomuto postu, a já se je pokusím zodpovědět a popřípadě publikovat i další příklady.</p>
<p><a id="more"></a><a id="more-408"></a></p>
<p>Pozn.: po poslechu se mi zdá, že kvalita záznamu je výborná ... jen se mi ke konci už trochu pletl jazyk, takže při jedné odpovědi na dotaz v závěru přednášky jsem odpověď uvedl tím, že Hibernate umí využít jak stránkování databáze, tak JDBC způsob pro skip záznamů ... samozřejmě jsem mluvil o iBatisu. Doufám, že se Vám bude přednáška líbit.</p>
<p><strong>Použitá hudba:</strong>  <a href="http://magnatune.com/artists/albums/spirit-woods/">Minstrel Spirit - Enter The Woods</a>, Gabriella (<a href="http://magnatune.com/" target="_blank">http://magnatune.com</a>) publikováno pod Creative Commons License</p>
<p><a href="http://files.novoj.net/iBatis/iBatis.mp3" title="MP3 Podcast"><img src="http://files.novoj.net/button_mp3.png" title="MP3 Podcast" alt="MP3 Podcast" style="margin-right: 10px" align="left" /></a> <a href="http://files.novoj.net/iBatis/iBatis.mp3" title="MP3 Podcast"><strong> Podcast</strong></a> [84:39] 22,4 MB</p>
<p><img src="http://he3.magnatune.com/img/somerights2.gif" title="Creative Commons - Some Rights Reserved" alt="Creative Commons - Some Rights Reserved" align="right" /></p>
<p><a href="http://files.novoj.net/iBatis/iBatis.pps" title="Presentation slides"><img src="http://files.novoj.net/button_ppt.png" title="Slidy prezentace" alt="Slidy prezentace" style="margin-right: 10px" align="left" /></a> <a href="http://files.novoj.net/iBatis/iBatis.pps" title="Slidy prezentace"><strong> Slidy prezentace ve formátu MS PowerPoint</strong></a></p>
<p><strong>Licence: </strong><a href="http://creativecommons.org/licenses/by-nc-sa/1.0/" target="_blank"> Creative Commons</a></p>
