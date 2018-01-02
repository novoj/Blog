---
status: publish
published: true
title: Přednáška Juergena Höellera o Spring Framework 5
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft size-thumbnail wp-image-3308\" src=\"http://blog.novoj.net/binary/2017/04/juergen-e1491138921182-150x150.jpg\"
  alt=\"\" width=\"150\" height=\"150\" />Před týdnem jsem byl pozváni na přednášku
  <a href=\"https://spring.io/team/jhoeller\">Juergena Höellera</a> - jednoho z autorů
  Spring Frameworku, který již léta dohlíží na směrování tohoto velmi populárního
  aplikačního rámce našich Java aplikací. Akci organizovala společnost <a href=\"http://vsadnajavu.cz/2017-03/odborne/spring-framework/jake-to-bylo-s-juergenem-hoellerem/\">Morosystems</a> v
  Brně a tímto jim děkujeme za pozvání.\r\n\r\n"
wordpress_id: 3307
wordpress_url: http://blog.novoj.net/?p=3307
date: '2017-04-02 14:16:03 +0200'
date_gmt: '2017-04-02 13:16:03 +0200'
categories:
- Java
tags: []
comments:
- id: 158557
  author: František
  author_email: frantisek.rezac@calavera.info
  author_url: http://gravatar.com/calaverainfo
  date: '2017-04-02 20:36:25 +0200'
  date_gmt: '2017-04-02 19:36:25 +0200'
  content: Super, že jsi napsal výtah hlavních myšlenek textově. Vzhledem k délce
    jsem to chtěl oželet, ale že jsi zmínil tu modularitu, tak na to si holt někdy
    čas najdu, protože to je teď moje hlavní téma. Jinak jsem teď viděl poprvé micrositu
    Game of Code a palec nahoru, fakt jsem se zasmál nahlas.
- id: 158558
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2017-04-04 09:40:43 +0200'
  date_gmt: '2017-04-04 08:40:43 +0200'
  content: "Já bych to snad ani nenazval hlavními myšlenkami - spíš to jsou věci,
    které upoutaly mě. Třeba Tě zaujme něco jiného - dej tomu šanci, je to dlouhé,
    ale stojí to za to.\r\n\r\nJeště jsem zapomněl na jednu věc - Juergen říkal, že
    rozhodně stojí za zkoušku pustit stávající aplikace na JDK9 - prý bychom měli
    pozorovat výraznou úsporu paměti, díky optimalizaci práce se Stringy.\r\n\r\nA
    díky za like pro Game of Code :D"
---
<p><img class="alignleft size-thumbnail wp-image-3308" src="http://blog.novoj.net/binary/2017/04/juergen-e1491138921182-150x150.jpg" alt="" width="150" height="150" />Před týdnem jsem byl pozváni na přednášku <a href="https://spring.io/team/jhoeller">Juergena Höellera</a> - jednoho z autorů Spring Frameworku, který již léta dohlíží na směrování tohoto velmi populárního aplikačního rámce našich Java aplikací. Akci organizovala společnost <a href="http://vsadnajavu.cz/2017-03/odborne/spring-framework/jake-to-bylo-s-juergenem-hoellerem/">Morosystems</a> v Brně a tímto jim děkujeme za pozvání.</p>
<p><a id="more"></a><a id="more-3307"></a></p>
<p>Mimo specifických vlastností týkajících se páté verze Spring Frameworku se Juergen na přednášce rozhovořil také o jeho osobních vizích, kam bude směrovat další vývoj v oblasti Java aplikací a důvodech některých rozhodnutí, které ve Springu učinili.</p>
<p>Abych Vás nalákal na poslechnutí kompletní přednášky uvedu pár bodů, které mě osobně překvapily:</p>
<ul>
<li>Spring 5.X už nebude obsahovat podporu pro portlety, tato technologie je dle Juergena už několik let mrtvá a nyní už natolik, aby se její podpora úplně odstranila - jediný, kdo portlety ještě používá je Liferay, ale podle Juergena prostě jedou na dávno mrtvém koni</li>
<li>do budoucna si Juergen myslí, že slepými větvemu jsou i další server side rendering frameworky jako třeba Tapestry nebo Wicket - toto mě osobně přeci jen trochu překvapilo ... nicméně zdá se, že client side single page app jsou dlouhodobějším trendem</li>
<li>Spring začíná ve větší míře spolupracovat s autory Kotlinu - krom toho, že se jedná o zajímavý jazyk kombinující funkcionální a OO programování, také především proto, že autoři mají o spolupráci zájem a vzájemně si s týmem Springu vycházejí vstříc</li>
<li>naopak se Scala komunitou se podobná spolupráce navázat nepodařila a Juergen ji více méně hází přes palubu</li>
<li>novému modulárnímu systému Jigsaw v Java 9 nedává moc velkou šanci na úspěch mezi řadovými aplikačními vývojáři, ani Spring nebude dodávat prozatím žádné module deskriptory pro své knihovny</li>
<li>OSGI bylo pro Spring obrovské zklamání a je velmi skeptický i v souvislosti s Jigsaw - modulární návrh na úrovni jazyka přináší řadu inherentních a velmi komplexních problémů, které nelze jednoduše řešit</li>
<li>snaží se nalézt cesty, jak zrychlit Spring boot up time - ve verzi 5 přinášejí možnost funkcionálního sestavení Spring kontextu, který by vůbec neměl vyžadovat reflexní analýzu tříd a měl by být velmi rychlý (nicméně pro programátora o něco pracnější)</li>
<li>celkově se Juergenovi líbí reaktivní přístup k programování i když přiznává, že to opět není cesta pro každého a má smysl se jí vydat pouze tehdy, nestačí-li současná architektura zvládat požadavky kladené na aplikaci ... a dost možná začít s tímto přístupem experimentovat zpočátku pouze na "horkých" místech aplikace a sbírat zkušenosti nejprve tam ... pokud je součástí i data store, je nutnou podmínkou reaktivní ovladač dané technologie - nebo naopak pro ukládání dat vybírat takový typ databáze, který reaktivní přístup umožňuje</li>
</ul>
<p>Podobných myšlenek je v přednášce celá řada, a proto si ji rozhodně nenechte ujít.</p>
<h3>Video</h3>
<div style="text-align: center">
<iframe width="560" height="315" src="https://www.youtube.com/embed/0Zj_8K7UUmw" frameborder="0" allowfullscreen></iframe>
</div>
