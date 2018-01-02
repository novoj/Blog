---
status: publish
published: true
title: Spring One - den druhý
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Dnešní den přenesl (alespoň v mém případě) řadu roztrpčení. K tomu se ale
  dostanu až o pár odstavců později. Dnešní keynote se nesla v duchu <a herf=\"http://en.wikipedia.org/wiki/Lean_software_development\"
  target=\"_blank\">Lean software development</a> - a to především ve smyslu, jak
  se co nejrychleji dostat z fáze vývoje do fáze produkčního běhu. Přednáška byla
  poměrně zajímavá - Adrian Colyer ukazoval prostřednictvím STS živý deployment Spring
  / Grails aplikací (byť) triviálních přímo na Google App Engine nebo na Amazon EC2.
  Ačkoliv pro to zatím nemám usecase, praktická ukázka byla skutečně impresivní. Adrian
  je především skvělý přednášející, který je schopný živě reagovat na odezvu publika
  a vkládat skutečně zajímavé oživující prvky, které udrží dobrou náladu a pozornost
  posluchačů (jako třeba bílý tučnák, kterého v průběhu přednášky trestal za jakoukoliv
  chybu, která se mu ukázkách povedla). Kéž bych uměl své přednášky udělat tak zajímavé
  jako on ;-) . To co jsem si z přednášky odnesl je to, že nasadit Spring aplikaci
  na GAE nebo EC2 nemusí být zase tak těžké, jak by se na první pohled mohlo zdát.\r\n\r\n"
wordpress_id: 464
wordpress_url: http://blog.novoj.net/?p=464
date: '2009-04-28 23:02:28 +0200'
date_gmt: '2009-04-28 22:02:28 +0200'
categories:
- Java
- Spring Framework
- Reportáže
tags:
- SpringOne
comments:
- id: 8126
  author: lzap
  author_email: lzap@seznam.cz
  author_url: ''
  date: '2009-04-30 14:27:42 +0200'
  date_gmt: '2009-04-30 13:27:42 +0200'
  content: "Ono je to hodně jednoduché říct \"nepoužívejte XA\". Chápu, že mnohem
    hezčí je použití jiných paternů jako je Exactly-Once Processing, ale někdy se
    XAčku prostě nevyhneme. U jednoho zákazníka je vidět, že při nestabilním systému
    (jednom z mnoha) začíná být error recovery problémem, což je u aplikací/integrací
    s XA snadnější.\r\n\r\nJe to celé dvousečné. Na jednu věc nepoužití XA může zjednodušit
    návrh i udělat vyšší výkon, když se ale něco \"hodně sere\", pak jsou zase XA
    vhodnější volbou...\r\n\r\nPěkný články. Fotky by nebyly? :-)"
- id: 8131
  author: Michal Franc
  author_email: michal.franc@gmail.com
  author_url: http://www.michalfranc.com
  date: '2009-04-30 19:47:56 +0200'
  date_gmt: '2009-04-30 18:47:56 +0200'
  content: "Fotky muzu nabidnout jakozto Hoznuv doprovod\r\nhttp://picasaweb.google.com/michal.franc/AmsterdamSpringOne"
- id: 8181
  author: Ariel
  author_email: ariel@gmail.com
  author_url: ''
  date: '2009-05-02 13:09:49 +0200'
  date_gmt: '2009-05-02 12:09:49 +0200'
  content: "Mám stejný názor na tu roztříštěnost Spring MVC vs. Spring WebFlow. Jsou
    to dva úplně odlišné produkty a popravdě web se dá udělat v jednom nebo druhém,
    ale kombinovat bych to určitě nechtěla.\r\n\r\nSpring MVC je v podstatě náhrada
    Struts - geniální framework, ale chybí tam snadné tvoření wizardů (conversation
    scope).\r\nWebFlow je nepoměrně složitější webový framework, kde se deklarativně
    určují přechody mezi stránkami a deklarativně se volají Controllery (eventuelně
    přímo Servicy). Trochu to připomíná přechodové XML z JSF.\r\n\r\nKaždopádně spolu
    nemají nic společného a kvůli jednomu až dvěma trojstránkovým průvodcům bych si
    určitě 10MB knihoven WebFlow do aplikace nepřidávala, pokud bych měla zbytek ve
    Spring MVC."
- id: 8232
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-05-03 20:42:58 +0200'
  date_gmt: '2009-05-03 19:42:58 +0200'
  content: "Ad Izap) naprosto souhlasím - někdy to bez XA nejde a někdy si tím jen
    šetříme práci - nicméně to přesně odpovídá větě: \"při použití XA transakcí si
    musíte být vědomi toho, že vyměňujete programátorské pohodlí za výkonnostní penalizaci
    (a ne zrovna malou)\"\r\n\r\ndíky za reakci"
- id: 8233
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-05-03 20:53:06 +0200'
  date_gmt: '2009-05-03 19:53:06 +0200'
  content: Ad Ariel) 10 MB ve SpringFlow? ta velikost mě teda trošku překvapila -
    nicméně pohledem do Maven repository by se mělo jednat jen asi o 600kB v hlavním
    JARu - to jsou tam nějaké zvláštní dependence?
- id: 8259
  author: Petr Juza
  author_email: pjuza@seznam.cz
  author_url: http://javicka.blogspot.com/
  date: '2009-05-04 07:47:53 +0200'
  date_gmt: '2009-05-04 06:47:53 +0200'
  content: "Tak trochu (v dobrém) ti závidím tvoji účast na SpringOne :) - na této
    konferenci jsem již také byl a pro mě osobně to bylo opravdu hodně přínosné, ze
    všech konferencí nejvíce.\r\n\r\nNaposledy jsem byl před dvěma roky, kdy si pamatuji,
    že Ben Alex měl přednášku o ROO, ale bylo to hodně v plenkách. Přednáška byla
    spíše o myšlenkách než o tom, co je hotové. A vida, výsledek je na světě."
---
<p>Dnešní den přenesl (alespoň v mém případě) řadu roztrpčení. K tomu se ale dostanu až o pár odstavců později. Dnešní keynote se nesla v duchu <a herf="http://en.wikipedia.org/wiki/Lean_software_development" target="_blank">Lean software development</a> - a to především ve smyslu, jak se co nejrychleji dostat z fáze vývoje do fáze produkčního běhu. Přednáška byla poměrně zajímavá - Adrian Colyer ukazoval prostřednictvím STS živý deployment Spring / Grails aplikací (byť) triviálních přímo na Google App Engine nebo na Amazon EC2. Ačkoliv pro to zatím nemám usecase, praktická ukázka byla skutečně impresivní. Adrian je především skvělý přednášející, který je schopný živě reagovat na odezvu publika a vkládat skutečně zajímavé oživující prvky, které udrží dobrou náladu a pozornost posluchačů (jako třeba bílý tučnák, kterého v průběhu přednášky trestal za jakoukoliv chybu, která se mu ukázkách povedla). Kéž bych uměl své přednášky udělat tak zajímavé jako on ;-) . To co jsem si z přednášky odnesl je to, že nasadit Spring aplikaci na GAE nebo EC2 nemusí být zase tak těžké, jak by se na první pohled mohlo zdát.</p>
<p><a id="more"></a><a id="more-464"></a></p>
<p>Druhou mojí přednáškou dnešního dne byla přednáška Jurgena Hoellera na téma nativních transakcí. Jurgen je prostě mistr v oboru, takže poměrně detailně popisoval dopady použití XA transakcí v porovnání s nativními. Z jeho přednášky se v podstatě daly získat následující závěry:</p>
<ul>
<li>nepoužívejte remotní XA transakce tam, kde to není nutné (a to ve valné většině případů skutečně nutné není) a držte se lokálních transakcí</li>
<li>nepoužívejte XA transakce pokud pro to nemáte skutečně dobrý důvod, při použití XA transakcí si musíte být vědomi toho, že vyměňujete programátorské pohodlí za výkonnostní penalizaci (a ne zrovna malou)</li>
</ul>
<p>Obecně Jurgen spíše nabádal držet se co nejjednoduššího způsobu, který stále ještě řeší váš problém. Spíše implementovat kompenzační logiku na úrovni aplikace, než aplikovat obecnou XA logiku, která je díky své obecnosti výkonnostně daleko dražší. To mi v podstatě připomíná závěry, které jsem slyšel ve spojitosti s architekturou tak velkých systémů jako je eBay nebo The Guardian. A zároveň to potvrzuje závěry, které jsme si udělali ve Forrestu sami.</p>
<p>Krom těchto věcí také přednášel o významu read-only flagu na úrovni deklarativních transakcí ve Springu. Ten má význam částečně pro JDBC drivery, které jej podporují, ale také především pro O/R mappery (jako je třeba Hibernate), které v daném případě nemusí analyzovat objektové stromy pro zjištění modifikovaných property ve vašich POJO.</p>
<p>Jurgen je naprosto skvělý odborník na záležitosti okolo Javy, takže jsem hltal i jeho další přednášku v pozdním odpoledni, která se týkala novinek v J2EE 6.  Z řady věcí, které v přednášce zmiňoval jsem neměl vůbec dobrý pocit. Jednou z nich byla samozřejmě specka Servlet 3.0, o které vím z mnoha zdrojů (krom jiných i od Dagiho), že má poměrně značné množství kontroverzních změn - od možnosti atomatické inicializace servletů ze strany knihoven na classpath (security issue), až po nešťastné řešení anotací přímo na úrovni Servletu aj. Další specky, které třeba vypadají nadějně se ve vývoji úplně zastavily (např. concurrency API). Na druhou stranu vznikly knihovny, které jsou vůči Springu duplicitní a interoperabilita je přinejmenším problematická. Konkrétně JAX-RS (referenční implementace Jersey), která je sice velmi povedenou implementaci REST rozhraní jako Spring 3.0, ale na druhou stranu žije jako takový samostatný ostrov uprostřed ostatních web frameworků, na které není jednoduché na ni navázat.</p>
<p>Dále se Jurgen docela opřel do specifikace EJB 3.1, která má řadu podobných rysů jako samotný Spring, ale i řadu nelogičností jako např. @Locked anotace na statefull singleton beanách, jejíž nesmyslnost Jurgen probíral poměrně dlouho. Spring se snaží monitorovat dění okolo JCP a adaptovat se změnám v tomto směru, ale rozhodně zůstává poměrně kritický k tomu, co se v této oblasti děje. Docela mě překvapil i postoj Jurgena Hoellera k profilům v J2EE 6, když na férovku řekl, že pochybuje, že by někdo měl zájem implementovat samostatně Web Profile. Podle jeho názoru je stále Web Profile na lehké servery jako je Tomcat / Jetty těžký a naopak plnotučné servery ala WebSphere / WebLogic / Glassfish budou mít motivaci vždy implementovat plný profil. Překvapuje mne to především proto, že jsem si dosud myslel, že za rozdělením J2EE 6 do profilů stojí především SpringSource v čele s Rodem Johnsonem.</p>
<p>Poměrně velkým zklamáním pro mne byl dnes Spring dc Server postavený na OSGi. Přiznávám, že je to zcela jistě subjektivní pocit, katalyzovaný tím, že se dnes klukům ze SpringSource za přednášecím pultem moc nedařilo. Nicméně tak či tak, pocit, který jsem si ze třech hodin přednášek o dc Serveru odnesl je ten, že OSGi platforma je pro většinu normálních projektů prostě příliš složitá. Pravda je, že dostáváte k dispozici obrovskou sílu v možnosti mít na "classpath" stejné knihovny v různých verzích, detailně řízené viditelnosti tříd na úrovni package, explicitně exportovaných servisy modulů atd. atd. Jenže to všechno za předpokladu, že jste jako developer schopný si nad celým tím soukolím udržet kontrolu. </p>
<p>To je podle mě právě ten hlavní kámen úrazu. Řekl bych, že dnes jsme měli před sebou odborníky na slovo vzaté - v podstatě autory samotného dc Serveru, ale pokud jsme v průběhu přednášky věnovali desítky minut hledáním problémů v dependencích a nastaveních, které ústily v to, že nadeployovaná aplikace buď vůbec neodpovídala, nebo neměla správně nawirované beany, tak něco není určitě v pořádku. Já osobně jsem se ve vazbách mezi pár moduly Hello World aplikace ztratil už během chvíle, takže pro mne většina přednášky byla pak už jen pocitovou záležitostí. Sám mám nějaké zkušenosti s provozem modulárních systémů (ovšem pouze na úrovni skládání Spring aplikačních kontextů a nikoliv na úrovni skládání classloaderů), ale to co je potřeba provádět při programování bundlů pro OSGi je prostě o třídu jinde. Výsledný pocit, který jsem z toho měl je ten, že se tato architektura vyplatí možná pro obrovské modulární aplikace typu Eclipse, ale pro malé a střední projekty, které hlavně potřebujete jednoduše složit a rychle dodat zákazníkovi se opravdu nehodí. Tam vám opravdu nikdo hodiny strávené nad hledáním problémů v dependencích, exportech a importech rozhraní nikdo nezaplatí. Možná jsem si od dc Serveru sliboval příliš mnoho ...</p>
<p>S kolegou jsme dneska taky diskutovali drobné nekonzistence v portfoliu SpringSource. Kupříkladu jsme se shodli na tom, že Spring Webflow a Spring MVC jsou v podstadě dva poměrně velmi odlišné přístupy k návrhu a především "konfiguraci" web aplikací. Podle slov SpringSource jsou to dvě řešení, které jedno je určené pro stateless části aplikace (MVC) a to druhé pro statefull (WebFlow = konverace = wizardy) a tedy se vzájemně doplňují. Z mého pohledu se ale jedná o dvě řešení, které mají společné akorát slovo Spring ve svém názvu a napojení na Spring Framework v pozadí. Už jen způsob jakým probíhá navigace ze stránku na stránku (MVC = uvnitř kódu controlleru, WebFlow = dekarativní v XML), nebo data binding se mi zdá mezi oběma frameworky dost odlišný. Možná o tom vím (jako uživatel Stripes) ale přeci jen moc málo.</p>
<p>Druhá nekonzistence, která nás spolu s Michalem Francem uhodila do očí je podobný přístup nového produktu Spring ROO a Grails command-line pro generování programových komponent (doménové objekty, controllery, instalace / odinstalace pluginů atd. atd.). Jsou to defakto dva oddělené nástroje, které principielně dělají to samé. Prozatím nikdo neřekl nic o tom, že by se tyto dva nástroje měly do budoucna sloučit, ale z mého pohledu mi nepřipadá logické, aby se udržovaly odděleně, když v podstatě dělají to samé.</p>
<p>Rozhodně si vážím práce SpringSource týmu, ale po dnešním dni nemůžu o všem jen psát s nadšením, když na první pohled vidím pár nedostatečně dotažených věcí. Doufejme, že budoucnost na přinese větší integraci a sjednocení produktů v portfoliu Springu.</p>
<p>Btw. pro ty co si chtějí hrát - <a href="http://stsmedia.net/introducing-spring-roo/" target="_blank">první verze Roo je k dispozici ke stažení a vyzkoušení</a>.</p>
