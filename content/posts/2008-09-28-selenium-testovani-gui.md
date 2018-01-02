---
status: publish
published: true
title: Selenium testování GUI
author:
  display_name: Jety
  login: jetik
  email: mail@jetensky.net
  url: http://jetensky.net
author_login: jetik
author_email: mail@jetensky.net
author_url: http://jetensky.net
excerpt: "<div style=\"border: 1px solid white; background-color: #333333; font-size:
  90%; margin-top: 20px;\">\r\n\r\n<a title=\"Pavel Jetensky\" href=\"http://blog.novoj.net/binary/2008/09/pavel.jpg\"><img
  style=\"margin-left: 10px; margin-right: 10px;\" src=\"http://blog.novoj.net/binary/2008/09/pavel.jpg\"
  alt=\"Pavel Jetensky\" width=\"49\" height=\"62\" align=\"left\" /></a>\r\n\r\n<strong>O
  autorovi: </strong><a href=\"http://jetensky.net/blog\">Jetyho blog</a> | <a href=\"http://www.linkedin.com/in/paveljetensky\">LinkedIn</a>\r\n<p
  style=\"margin: 10px;\">Pavel Jetenský se věnuje Java/J2EE vývoji již od roku 2003,
  z toho několik let v Irsku. Zajímají ho techniky automatického testování. V současné
  době pracuje jako metodický vedoucí Java/J2EE v Deltax Systems a.s.</p>\r\n\r\n</div>\r\nNa
  Java Open Space jsem měl na téma Selenium lightning talk. Honza ho nahrál <a href=\"http://jopenspace.cz/audio/04_Selenium_IDE.mp3\">jako
  podcast</a> a zveřejnil v předchozím článku, ale bohužel je v nahrávce hodně šumu.\r\n\r\nNaštěstí
  ale ještě existuje screencast z původní verze školení <em>Selenium testování GUI</em>,
  které jsem prezentoval letos na jaře pro kolegy z mojí firmy. Tento záznam právě
  najdete v zde v nezkrácené a vyčištěné podobě.\r\n\r\n"
wordpress_id: 111
wordpress_url: http://blog.novoj.net/2008/09/28/selenium-testovani-gui/
date: '2008-09-28 10:29:49 +0200'
date_gmt: '2008-09-28 09:29:49 +0200'
categories:
- Testování
- Podcast
- Selenium
tags:
- selenium
- Testování
- Školení
- reuse
- Běžné problémy
comments:
- id: 4269
  author: Jirka
  author_email: jirci@centrum.cz
  author_url: ''
  date: '2008-10-30 09:04:48 +0100'
  date_gmt: '2008-10-30 08:04:48 +0100'
  content: "Pekny den vsem, mel jsem otazku na p. Jetenskeho zdali lze v tomto prg.
    (Selenium IDE) nechat testovat web aplikaci a nechat nektere vstupy, ktere se
    meni, aby vyskocily popup oknem na usera nebo to ne ?\r\n\r\nOdpoved byla tato
    (snad to nekomu take pomuze):\r\n\r\nstore\r\nmyValue\r\njavascript{prompt(\"Zadej
    svoje jmeno\", \"\")}\r\n\r\npak muzete hodnotu pouzit jako ${myValue}"
- id: 4306
  author: Jety
  author_email: mail@jetensky.net
  author_url: http://jetensky.net/blog
  date: '2008-10-31 13:39:20 +0100'
  date_gmt: '2008-10-31 12:39:20 +0100'
  content: "Jen doplním (není to z předchozího komentáře úplně jasné těm, kdo neznají
    pozadí naší komunikace s Jirkou), že v předchozím příkladě s použitím promptu
    jde o to, aby mohl v průběhu testu tester vložit nějakou dynamickou hodnotu, která
    bude pak použitá pro nějaký selenium command.\r\nNapř. zadá jméno zakládaného
    uživatele při běhu testu. Je jasné, že kvůli začleněním inputu od fyzicky existujícího
    testera není možné takový test pouštět automaticky v rámci continuous integration
    (nočních buildů)."
- id: 104025
  author: Milan
  author_email: error@seznam.cz
  author_url: ''
  date: '2012-11-05 14:22:26 +0100'
  date_gmt: '2012-11-05 13:22:26 +0100'
  content: "Dobrý den,\r\n\r\nměl bych také otázku, jakým způsobem zajistit, aby se
    některé hodnoty naplnily z externího zdroje z pole?? Bohužel jsem to nedohledal
    a potřebuji vyplnit 3 pary dat.\r\n\r\nPříklad:\r\n\r\nmám zdroj dat: \r\nJméno1,
    Prijmeni1, ID1\r\nJmeno2, Prijmeni 2, ID2\r\n...\r\n\r\nJak zajistit, aby se tato
    pole naplnila vždy relevantnimi hodnotami? \r\n\r\nDiky"
- id: 107489
  author: Jety
  author_email: pavel.jetensky@seznam.cz
  author_url: http://jetensky.net/blog
  date: '2012-11-17 15:40:08 +0100'
  date_gmt: '2012-11-17 14:40:08 +0100'
  content: "Dobrý den, \r\n\r\nSeleniu se teď již pár let nevěnuju, ale zkusím odpovědět.
    Nepíšete sice, jaký je váš externí zdroj dat, ale předpokládám, že např. databáze.\r\n\r\nZpůsob
    by mohl být podobný, jako v předchozím dotazu, vytvořil byste si nějakou javascriptovou
    funkci, která by ten zdroj dat načítala (např. z restového JSon API, funkce např.
    readAnotherUser). To lze např. pomocí user extensions (i když sám jsem to ještě
    nezkoušel) - viz. http://seleniumhq.org/docs/08_user_extensions.html\r\n\r\nPak
    byste si tu hodnotu mohl uložit třeba do proměnné user, což by bylo třeba pole\r\nstore\r\nanotherUser\r\njavascript{readAnotherUser()}\r\n\r\nPak
    muzete hodnotu pouzit jako ${anotherUser[0]} ${anotherUser[1]} ${anotherUser[2]}\r\nBude
    mě zajímat, jestli to takhle šlo."
---
<div style="border: 1px solid white; background-color: #333333; font-size: 90%; margin-top: 20px;">
<p><a title="Pavel Jetensky" href="http://blog.novoj.net/binary/2008/09/pavel.jpg"><img style="margin-left: 10px; margin-right: 10px;" src="http://blog.novoj.net/binary/2008/09/pavel.jpg" alt="Pavel Jetensky" width="49" height="62" align="left" /></a></p>
<p><strong>O autorovi: </strong><a href="http://jetensky.net/blog">Jetyho blog</a> | <a href="http://www.linkedin.com/in/paveljetensky">LinkedIn</a></p>
<p style="margin: 10px;">Pavel Jetenský se věnuje Java/J2EE vývoji již od roku 2003, z toho několik let v Irsku. Zajímají ho techniky automatického testování. V současné době pracuje jako metodický vedoucí Java/J2EE v Deltax Systems a.s.</p>
</div>
<p>Na Java Open Space jsem měl na téma Selenium lightning talk. Honza ho nahrál <a href="http://jopenspace.cz/audio/04_Selenium_IDE.mp3">jako podcast</a> a zveřejnil v předchozím článku, ale bohužel je v nahrávce hodně šumu.</p>
<p>Naštěstí ale ještě existuje screencast z původní verze školení <em>Selenium testování GUI</em>, které jsem prezentoval letos na jaře pro kolegy z mojí firmy. Tento záznam právě najdete v zde v nezkrácené a vyčištěné podobě.</p>
<p><a id="more"></a><a id="more-111"></a></p>
<h3>Stáhněte si</h3>
<p>Odkazy vedou na původní nezkrácené školení Selenium testování GUI.</p>
<p><a title="Screencast" href="http://jetensky.net/download/files/Selenium%20testovani%20gui.swf"><img style="margin-right: 10px" title="Screencast" src="http://files.novoj.net/button_swf.png" alt="Screencast" align="left" /></a> <a title="MP3 Podcast" href="http://jetensky.net/download/files/Selenium%20testovani%20gui.swf"><strong> Podcast</strong></a> [55:15] 46,5 MB</p>
<p><a title="MP3 Podcast" href="http://jetensky.net/download/files/Selenium%20testovani%20gui.mp3"><img style="margin-right: 10px" title="MP3 Podcast" src="http://files.novoj.net/button_mp3.png" alt="MP3 Podcast" align="left" /></a> <a title="MP3 Podcast" href="http://jetensky.net/download/files/Selenium%20testovani%20gui.mp3"><strong> Pouze zvuk</strong></a> [55:15] 26,5 MB</p>
<p><a title="Prezentace ke školení" href="http://jetensky.net/download/files/Selenium%20testovani%20GUI.ppt"><img style="margin-right: 10px" title="Slůi" src="http://files.novoj.net/button_ppt.png" alt="Prezentace ke školení" align="left" /></a> <a title="Slidy prezentace" href="http://jetensky.net/download/files/Selenium%20testovani%20GUI.ppt"><strong> Prezentace ke školení - MS Power Point</strong></a></p>
<h3>Obsah školení</h3>
<ul>
<li>představuje na praktických ukázkách nástroj Selenium IDE pro testování webových aplikací</li>
<li>radí, jak na reuse v Selenum testech pomocí JSP a jUnit</li>
<li>obsahuje "Best practices" pro psaní Selenium testů</li>
<li>vysvětluje běžné problémy se Selenium a jejich řešení
<ul>
<li>recorder nenahrává odeslání formuláře po stisku klávesy Enter</li>
<li>recorder nenahraje přepnutí kontextu při akci ve vnořeném iframe</li>
<li>akce ClickAndWait spadne na vypršení timeout</li>
<li>testrunner okno zmizí po spuštění testů</li>
<li>další úskalí (testování https, problém s otevření popup okna _new, nenahrání příkazu type při použití hodnoty z form history)</li>
</ul>
</li>
</ul>
<p><strong>Pozn.: </strong>Tato prezentace je majetkem firmy Deltax Systems, které patří vřelé díky autora za svolení o zveřejnění na Internetu. Budu rád, když vám tak ušetřím trochu času s průzkumem tohoto hodnotného testovacího frameworku.</p>
