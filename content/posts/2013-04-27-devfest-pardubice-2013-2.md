---
status: publish
published: true
title: DevFest Pardubice 2013
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft  wp-image-2540\" title=\"devfest-logo-pardubice\"
  src=\"http://blog.novoj.net/binary/2013/04/devfest-logo-pardubice1.png\" alt=\"\"
  width=\"180\" height=\"180\" />\r\n\r\nTento víkend se v Pardubicích konal historicky
  první \"pardubický\" <a href=\"http://pardubice.devfest.cz/\" target=\"_blank\">Google
  DevFest</a> a bylo by hříchem nevydat se na tak zajímavou akci zvlášť, když probíhá
  jen pár stovek metrů od mého domu. Na <a href=\"http://pardubice.devfest.cz/program/\"
  target=\"_blank\">programu </a>byli přitom samí zajímaví řečníci - Michal Špaček,
  Daniel Steigerwald, Pavel Lahoda, googleři Danut Echanoiu a Margarita Manterola
  a další.\r\n\r\nPokud vás zajímá, jak vše vypadalo okem diváka, připravil jsem pro
  vás tuto reportáž.\r\n\r\n"
wordpress_id: 2530
wordpress_url: http://blog.novoj.net/?p=2530
date: '2013-04-27 09:29:30 +0200'
date_gmt: '2013-04-27 08:29:30 +0200'
categories:
- Java
- Reportáže
- Android
- DevFest
tags: []
comments:
- id: 151841
  author: radeksimko
  author_email: radek.simko@gmail.com
  author_url: ''
  date: '2013-05-02 21:21:07 +0200'
  date_gmt: '2013-05-02 20:21:07 +0200'
  content: "Historicky první Google DevFest?\r\n1) To nepořádal Google, ale komunita,
    jak je ostatně zmíněno na konci článku.\r\n2) To byl druhý DevFest (http://prague.devfest.cz/)\r\n\r\n;-)"
- id: 151842
  author: QuoniamG
  author_email: vit.kotacka@gmail.com
  author_url: http://gravatar.com/Quoniam
  date: '2013-05-04 19:50:59 +0200'
  date_gmt: '2013-05-04 18:50:59 +0200'
  content: Díky za reportáž. Na přednášky asi nebude čas, ale beru to aspoň jako upozornění
    na zajímavé projekty.
- id: 151847
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-05-06 12:14:36 +0200'
  date_gmt: '2013-05-06 11:14:36 +0200'
  content: Díky za upozornění - ta věta byla špatně formulovaná (již jsem napravil).
    Chtěl jsem říci, první PARDUBICKÝ DevFest (vím, že první byl na podzim v Praze).
- id: 151854
  author: peter
  author_email: peter1000@inmail.sk
  author_url: ''
  date: '2013-05-07 16:25:35 +0200'
  date_gmt: '2013-05-07 15:25:35 +0200'
  content: "existuju k jednotlivym prednaskam video podcasty? ze by som si ich aspon
    doma takto popozeral\r\nak ano kde ich mozem najst?"
- id: 151859
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-05-11 08:18:01 +0200'
  date_gmt: '2013-05-11 07:18:01 +0200'
  content: 'Zjišťuju u organizátorů. Jakmile se něco dozvím, napíšu to sem. #stayTuned'
- id: 151880
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-05-16 20:40:40 +0200'
  date_gmt: '2013-05-16 19:40:40 +0200'
  content: Podle organizátorů by měly být přednášky online nejpozději do prázdnin
    a toto oznámí skrz standardní kanály – tj. Twitter, Facebook či web.
---
<p><img class="alignleft  wp-image-2540" title="devfest-logo-pardubice" src="http://blog.novoj.net/binary/2013/04/devfest-logo-pardubice1.png" alt="" width="180" height="180" /></p>
<p>Tento víkend se v Pardubicích konal historicky první "pardubický" <a href="http://pardubice.devfest.cz/" target="_blank">Google DevFest</a> a bylo by hříchem nevydat se na tak zajímavou akci zvlášť, když probíhá jen pár stovek metrů od mého domu. Na <a href="http://pardubice.devfest.cz/program/" target="_blank">programu </a>byli přitom samí zajímaví řečníci - Michal Špaček, Daniel Steigerwald, Pavel Lahoda, googleři Danut Echanoiu a Margarita Manterola a další.</p>
<p>Pokud vás zajímá, jak vše vypadalo okem diváka, připravil jsem pro vás tuto reportáž.</p>
<p><a id="more"></a><a id="more-2530"></a></p>
<h2>OAuth 2 (Danut Echanoiu)</h2>
<p>První přednáška Danuta Echanoiu byla na již trošku ohrané téma <a href="http://cs.wikipedia.org/wiki/Oauth" target="_blank">OAuth </a>autentizačního a autorizačního protokolu. Ačkoliv jsem již byl asi na dvou přednáškách o OAuth - tato mi přišla mimořádně dobrá a to především kvůli tomu, že veškeré technikálie byly vysvětleny velmi jednoduše a lidsky.</p>
<p>Základem bylo přirovnání mechanismu OAuth k situaci, kdy nám kamarád svěří nějaká svá soukromá data jako třeba bankovní výpisy, osobní deník, závěť atp. Následně zavolá jeho účetní s žádostí o poskytnutí jeho bankovních výpisů. Přirozeně, že neznámému člověku bychom data svého kamaráda jen tak nedali a proto mu zavoláme, jestli účetního zná a jestli je to v pořádku, že mu ta data předáme. Kamarád nám svolení dá a tak, účetnímu předáme požadovaná data.</p>
<p>Situace se opakuje i následující den, ale tentokrát účetní požaduje kamarádovu závěť. To nám nicméně připadá divné a proto se opět obrátíme na kamaráda, jestli je poskytnutí závěti v pořádku. Ten ale účetního pošle k šípku a poprosí nás, abychom mu už napříště už žádné údaje neposkytovali.</p>
<p>No a to je zjednodušeně celá podstata OAuth. Danut skutečně dokázal vystihnout podstatu věci tak, že od této doby nikdo z přítomných určitě už nezaváhá. Následovala i praktická ukázka autentizačního mechanismu a vysvětlení základních pojmů. Zajímavá mi přišla zmínka o <a href="https://developers.google.com/oauthplayground/" target="_blank">OAuth Playground</a>, díky kterému si můžeme jednoduše vyzkoušet protokol v praxi s vysvětlivkami a zobrazením jednotlivých požadavků a odpovědí.</p>
<p>Danut samozřejmě doporučoval nepsat si celý autentizační mechanismus znovu, ale použít již vyladěné <a href="https://developers.google.com/accounts/docs/OAuth2#libraries" target="_blank">Google knihovny</a>, které jsou dostupné pro řadu programovacích jazyků včetně JavaScriptu.</p>
<p>Zajímavá byla také zmínka o tom, že aplikace běžící na AppEnginu mají od Google implementovanou i serverovou část OAuth protokolu, takže stačí jen pár řádek a OAuth server s možností přidělovat přístupy k datům aplikace na AppEnginu začne dýchat.</p>
<h2>Improving Android XP (Pavel Lahoda)</h2>
<p>V druhé přednášce<a href="http://www.perpetumdesign.com/" target="_blank"> Pavel Lahoda</a> rozebíral bolavá místa při vývoji Android aplikací a místy propíral Google tak, až jsem si říkal, jestli bude na DevFestech ještě někdy vítaným hostem :)</p>
<p>Kromě kritiky ale také nabízel řešení - třeba místo sady layoutů pro různé formáty obrazovek a orientace doporučuje skládat view programově. Tento přístup kromě lepší správy obrazovek pro řadu rozlišení i zrychluje odezvy aplikace při změně orientace (díky tomu, že se neprovádí aplikace nového layout z XML s bindingem na komponenty).</p>
<p>V krátkosti také představil knihovnu pro rychlé prototypování (nejen) formulářově oritentovaných aplikací <a href="http://www.objectforms.com/" target="_blank">Object Forms</a>, která (pokud jsem správně pochopil) prozatím ještě není oficiálně dostupná, ale která by měla být v dohledné době k dispozici ke stažení. Knihovná má <a href="http://objectforms.com/license.html" target="_blank">duální licencování</a> - pro komerční použití stojí pár dolarů a v GPL licenci je zdarma.</p>
<p>V přednášce zazněla celá řada dalších doporučení, ale vzhledem k tomu, že sám nejsem Android vývojář, nejsem schopen je dostatečně srozumitelně reprodukovat a proto na tomto místě radši skončím. Pro ty z vás, kteří pro Android vyvíjíte bych ale přednášku určitě doporučil a pokud jsem správně zaslechl, její záznam by se měl objevit na stránce DevFestu brzy ke shlédnutí.</p>
<h2>Webová bezpečnost (Michal Špaček)</h2>
<p>Nenajde se mnoho lidí, kteří by dělali něco s webem a neznali <a href="https://twitter.com/spazef0rze" target="_blank">Michala Špačka</a>, přesto jsem ho na této konferenci viděl naživo poprvé. Přednáška byla perfektní a přesto, že některé problémy jsou spíš doménou PHP (např. <a href="http://cs.wikipedia.org/wiki/SQL_injection" target="_blank">SQL Injection</a>), dozvěděl jsem se také spoustu nových věcí, z nichž celou řadu jsem si nestačil ani zapsat. Takže se společně s vámi budu těšit na záznam s přednášky, abych si ty věci projel znova.</p>
<p>Co mi přišlo zajímavé je třeba možnost použít cizí weby (třeba W3C validátor) pro port scanning webů. Možnost volat z JavaScriptu v omezené míře Javovský kód (WTF) nebo získat zdrojové kódy webů přes <a href="http://www.skullsecurity.org/blog/2012/using-git-clone-to-get-pwn3d" target="_blank">získání obsahu VCS adresářů</a>, které se na produkci dostali i s ostrým kódem a které se zapomněly zabezpečit.</p>
<p>Z některých věcí trochu mrazí v zádech a proto každá podobná přednáška rozhodně není ztraceným časem. Shlédnout tuto přednášku je prostě povinnost ;)</p>
<h2>Reaktivní programování (Aleš Roubíček)</h2>
<p>Následovala poměrně teoretická přednáška zaměřená na aspekty funkcionálního programování. Osobně jsem do funkcionálního programování jen nakouknul a tak jsem přestal v některých pasážích stíhat. Funkcionální programování se musí (stejně jako logické programování) zažít, to se nedá pochopit z jedné přednášky.</p>
<p>Zajímavá mi přišla zmínka o <a href="https://github.com/Reactive-Extensions/" target="_blank">Reactive Extensions</a>, které pocházejí z dílny M$ a které jsou v současné době portovány do celé řady dalších jazyků (Javy, C a JavaScriptu nevyjímaje). Jejich hlavní motivací bylo vytvořit responsivní systém, který realizuje většinu operací asynchronně a tím dochází ke zvýšení prostupnosti systému. Rx jsou postaveny nad <a href="http://en.wikipedia.org/wiki/Observer_pattern" target="_blank">Observer</a> patternem, který spojují s prvky funkcionálního programování. Výsledkem je potom krátký a čitelný kód, který se navíc ve vícevláknovém zpracování chová předvídatelně.</p>
<h2>Google protocol buffers (Pavel Jetenský)</h2>
<p>Na další přednášku jsem si odskočil do lightning-talk room, kde přednášel můj kamarád Pavel Jetenský z Inmite o komunikačním protokolu, který používají mezi mobilními přístroji a serverem a zároveň mezi mobilními přístroji navzájem. Jedná se o <a href="https://developers.google.com/protocol-buffers/" target="_blank">binární protokol</a>, který je velmi úsporný jak ve srovnání s XML, tak i JSON. Protokol minimalizuje náklady na infrastrukturní část (tj. názvy polí, hlavičky atp.) výměnnou za nečitelnost dat, které tudy protékají.</p>
<p>GPB vyžadují pro svoje fungování tzv. deskriptor dat, který popisuje v jaké verzi protokolu se přenášejí které datové pole konkrétního typu (z výše uvedeného vyplývá, že protokol řeší verzování). Další velkou výhodou GBP je, že jsou dostupné pro <a href="https://code.google.com/p/protobuf/wiki/ThirdPartyAddOns" target="_blank">celou řadu jazyků</a> a tudíž mohou sloužit jako protokol pro multiplatformní výměnu dat podobně jako je tomu v případě JSON formátu.</p>
<p>Pokud tedy potřebujete použít nějaký úsporný datový formát pro přenos dat, je GBP daleko lepší varianta, než zastaralý <a href="http://en.wikipedia.org/wiki/Hessian_(web_service_protocol)" target="_blank">Hessian</a>.</p>
<h2>Google Closure Tools (Daniel Steigerwald)</h2>
<p>Přednáška od Daniela Steigerwalda byla jedním slovem divadlo a druhým cirkus :) Destilovaná zábava od začátku až do konce :)</p>
<p>V dnešní vyhypované a turbulentní době programování v JavaScriptu není jednoduché se vyznat ve spoustě knihoven a frameworků, které vznikají. Právem se řada lidí (a především těch z M$ platformy, kteří jsou zvyklí na nalinkovanou cestu vpřed) cítí ztracena a hledá ten "správný přístup". A jestli se nebudete bránit, Daniel vás jednoduše přesvědčí o správnosti přístup <a href="https://developers.google.com/closure/" target="_blank">Google Closure Tools</a>. V naší firmě měl taky školení a ani my jsme se neubránili - náš nový <a href="http://www.edee-cms.cz/" target="_blank">Edee</a> pohání právě GCT.</p>
<p>Na přednášce padla celá spousta zajímavých jmen - <a href="http://angularjs.org/" target="_blank">AngularJs</a> počínaje, přes <a href="http://documentcloud.github.io/backbone/" target="_blank">BackBone</a> až k <a href="http://emberjs.com/" target="_blank">Ember.js</a> ovšem žádný neobstál Danově kritice. Jeho názorem je, že všechny tyto frameworky škálují jen do určité složitosti projektu a pokud potřebujete jít dál,  je zatím GCT jedinou možnou variantou. Už jen třeba z toho důvodu, že se jedná o stabilizovanou knihovnu, která je již několik let ve stavu "production ready". GCT ovšem nejsou frameworkem - jen ekosystémem, který potřebuje zasadit do nějakého rámce. Tento rámec nabízí Danův pet-project <a href="http://estejs.tumblr.com/" target="_blank">Este.js</a>, který GCT propojuje se zbytkem světa a dává dohromady lépe uchopitelný nástroj pro vývoj web aplikací.</p>
<p>Mezi další zajímavé technologie zařadil například <a href="http://bower.io/" target="_blank">Bower</a> - nástroj pro jednoduchou správu a linkování dependencí v JavaScriptu a <a href="http://gruntjs.com/" target="_blank">Grunt</a> - nástroj pro spouštění automatizovaných tasků na správu projektu.</p>
<p>Při dotazu na nový <a href="http://meteor.com/" target="_blank">Meteor.js</a> jej Dan označil na zajímavou technologii, se kterou by se ovšem neodvážil jít zatím do produkce.</p>
<h2>Závěrem</h2>
<p>Myslím, že pardubický DevFest byla výborná akce, která oživila vody Východních Čech a rozhodně byl vidět velký kus odvedené organizační práce. Skvělé bylo, že se sem podařilo dostat zajímavé řečníky a sponzory. Pokud bude následovat další ročník, určitě vám jej doporučuji navštívit - už jen kvůli té rodinné atmosféře, kterou na hektických konferencích v Praze nemáte šanci zažít. Moje speciální díky patří <a href="http://jirka.penzes.cz/" target="_blank">Jirkovi Pénzešovi</a> a <a href="http://blog.voracek.net/" target="_blank">Honzovi Voráčkovi</a>, kteří mají velký podíl na tom, že se podobné akce v Pardubicích konají.</p>
<p><strong>Update 16.5.2013:</strong> Podle organizátorů by měly být přednášky online nejpozději do prázdnin a toto oznámí skrz standardní kanály - tj. <a href="http://www.twitter.com/gdgpardubice">Twitter</a>, <a href="http://www.facebook.com/gdgpardubice">Facebook</a> či <a href="http://gdgpardubice.cz/">web</a>.</p>
