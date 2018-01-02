---
status: publish
published: true
title: Pozvánka na přednášku na UHK <br> iBatis SqlMaps
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Po relativně krátké době se chystá nová přednáška na Univerzitě Hradec Králové
  - tentokrát o knihovně iBatis, která řeší objektově relační mapování tak trochu
  jiným způsobem než jde JPA a Hibernate. <a href=\"http://blog.novoj.net/binary/2009/02/pozvanka_uhk_ibatis.png\"><img
  src=\"http://blog.novoj.net/binary//2009/02/pozvanka_uhk_ibatis-214x300.png\" alt=\"Pozvánka
  UHK - iBatis SqlMaps\" title=\"Pozvánka UHK - iBatis SqlMaps\" width=\"91\" height=\"128\"
  style=\"float: right; margin: 5px 0px 5px 5px;\" /></a> A to způsobem, který vyhovuje
  nejen nám, ale i tisícům vývojářů po celém světě. iBatis je řešením, které leží
  někde mezi JDBC a JPA - na jednu stranu už se nemusíte zabývat detaily spojenými
  s používáním JDBC (uvolňování zdrojů, konverze dat z ResultSetu do Pojo, cachování
  atd.), na druhou stranu zůstává vše stále na jednoduché úrovni bez použití magie
  (nad kterou hloubá každý, kdo se pokouší začít třebas s Hibernatem). \r\n\r\nOhlasy
  na iBatis lze nalézt i na naší české scéně - <a href=\"http://blog.novoj.net/2007/05/08/ibatis-sqlmaps-tak-trochu-opomijeny-orm/\"
  target=\"_blank\">třeba u mě :-) </a>, <a href=\"http://sweb.cz/pichlik/ibatis/presentation.pdf\"
  target=\"_blank\">u Dagiho</a>, u <a href=\"http://jirablog.blogspot.com/2009/01/orm-mych-snu-ibatis-3.html\"
  target=\"_blank\">Jiry</a> nebo na <a href=\"http://blog.vyvojar.cz/minority/archive/2007/12/02/seznameni-s-ibatis-net.aspx\"
  target=\"_blank\">Minority blogu v portaci .NET</a>.  Pokud máte tedy zájem nakouknout
  pod pokličku práce s iBatis, jste vítáni.\r\n\r\n"
wordpress_id: 381
wordpress_url: http://blog.novoj.net/?p=381
date: '2009-02-08 19:07:30 +0100'
date_gmt: '2009-02-08 18:07:30 +0100'
categories:
- Java
- iBatis
tags: []
comments:
- id: 6701
  author: milos
  author_email: silhanek.m@seznam.cz
  author_url: ''
  date: '2009-03-03 14:15:18 +0100'
  date_gmt: '2009-03-03 13:15:18 +0100'
  content: Bylo to prima. Nemůžete mi poslat prezentaci? Díky
- id: 6702
  author: milos
  author_email: silhanek.m@seznam.cz
  author_url: ''
  date: '2009-03-03 14:21:46 +0100'
  date_gmt: '2009-03-03 13:21:46 +0100'
  content: Vyhledáním iBatis na java.cz jsem našel odkaz na článek iBatis SqlMaps
    - tak trochu opomíjený ORM, kde je odkaz na prezentaci.
- id: 6703
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-03-03 14:47:23 +0100'
  date_gmt: '2009-03-03 13:47:23 +0100'
  content: "@milos Prezentaci zkusím ještě tento týden zpracovat a publikovat jak
    audio, tak i ten PowerPoint, který jsem dnes na přednášce používal. V tom článku
    iBatis SqlMaps je pokud vím odkaz na přednášku od Dagiho, který něco podobného
    dělal jako interní školení v HP."
---
<p>Po relativně krátké době se chystá nová přednáška na Univerzitě Hradec Králové - tentokrát o knihovně iBatis, která řeší objektově relační mapování tak trochu jiným způsobem než jde JPA a Hibernate. <a href="http://blog.novoj.net/binary/2009/02/pozvanka_uhk_ibatis.png"><img src="http://blog.novoj.net/binary//2009/02/pozvanka_uhk_ibatis-214x300.png" alt="Pozvánka UHK - iBatis SqlMaps" title="Pozvánka UHK - iBatis SqlMaps" width="91" height="128" style="float: right; margin: 5px 0px 5px 5px;" /></a> A to způsobem, který vyhovuje nejen nám, ale i tisícům vývojářů po celém světě. iBatis je řešením, které leží někde mezi JDBC a JPA - na jednu stranu už se nemusíte zabývat detaily spojenými s používáním JDBC (uvolňování zdrojů, konverze dat z ResultSetu do Pojo, cachování atd.), na druhou stranu zůstává vše stále na jednoduché úrovni bez použití magie (nad kterou hloubá každý, kdo se pokouší začít třebas s Hibernatem). </p>
<p>Ohlasy na iBatis lze nalézt i na naší české scéně - <a href="http://blog.novoj.net/2007/05/08/ibatis-sqlmaps-tak-trochu-opomijeny-orm/" target="_blank">třeba u mě :-) </a>, <a href="http://sweb.cz/pichlik/ibatis/presentation.pdf" target="_blank">u Dagiho</a>, u <a href="http://jirablog.blogspot.com/2009/01/orm-mych-snu-ibatis-3.html" target="_blank">Jiry</a> nebo na <a href="http://blog.vyvojar.cz/minority/archive/2007/12/02/seznameni-s-ibatis-net.aspx" target="_blank">Minority blogu v portaci .NET</a>.  Pokud máte tedy zájem nakouknout pod pokličku práce s iBatis, jste vítáni.</p>
<p><a id="more"></a><a id="more-381"></a></p>
<p>Zjednodušený program přednášky:</p>
<ul align='left'>
<li>popis a použití frameworku v praxi</li>
<li>řešení základních problémů</li>
<ul>
<li>automaticky generované klíče</li>
<li>řešení problému N+1 selectů</li>
<li>dynamické selecty</li>
<li>cachování</li>
</ul>
<li>srovnání přístupu iBatis s Hibernate</li>
</ul>
<p><strong>Kde:</strong> Univerzita Hradec Králové - Fakulta informatiky a managementu<br><br />
<strong>Místnost:</strong> učebna J12<br />
<strong>Kdy:</strong> 3. března 2008, od 8:15 do 9:45<br><br />
<strong>Přednášející:</strong> Jan Novotný (FG Forrest)</p>
<p>Vzhledem k tomu, že přednáška je především určena studentům UHK a tudíž bude již část místnosti obsazená studenty, rád bych vás požádal, abyste mi, pokud plánujete na přednášku přijít, napsali jen krátce počet osob na můj email 'novotnaci[zavináč]gmail.com'. Přednášku bych opět rád zaznamenal a zveřejnil na blogu jako podcast - rozhodně však budu rád, když si ji přijdete poslechnout osobně.</p>
