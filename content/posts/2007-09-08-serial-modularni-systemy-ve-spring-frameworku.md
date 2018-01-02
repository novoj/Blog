---
status: publish
published: true
title: 'Seriál: Modulární systémy ve Spring Frameworku'
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Ve chvíli, kdy začnete používat při vývoji masivněji Spring Framework a
  začnete vytvářet znovupoužitelné knihovny postavené nad tímto frameworkem, začnete
  řešit jak z těchto knihoven co nejlépe složit výslednou aplikaci. První myšlenky
  povedou pravděpodobně těmito cestami:\r\n\r\n<ol>\r\n   <li>konfigurační soubory
  jednotlivých knihoven sloučit v jednom velkém aplikačním kontextu</li>\r\n   <li>držet
  jednotlivé knihovny odděleně - nechat jim jejich vlastní aplikační kontexty a k
  těmto kontextům se dostávat programovým způsobem</li>\r\n</ol>\r\n\r\nObě cesty
  však mají svá úskalí.\r\n\r\n"
wordpress_id: 33
wordpress_url: http://blog.novoj.net/2007/09/08/serial-modularni-systemy-ve-spring-frameworku/
date: '2007-09-08 18:59:42 +0200'
date_gmt: '2007-09-08 17:59:42 +0200'
categories:
- Java
- Spring Framework
tags: []
comments:
- id: 645
  author: Roman Dagi Pichlik
  author_email: pichlik@seznam.cz
  author_url: http://www.sweb.cz/pichlik/
  date: '2007-09-10 08:13:09 +0200'
  date_gmt: '2007-09-10 07:13:09 +0200'
  content: Resime neco podobneho a ja se prave klonim k pouziti OSGi. OSGi podle me
    nestoji na principu vsechno nebo nic, takze pokud ty "enterprise" featury nepotrebujes,
    tak te je nikdo nenuti pouzivat. Ja mam z OSGi jediny problem, a to ze vidim pesimisticky
    jeho funkcnost v ruznych aplikacnich serverech a navic ve spolupraci s EJB. Kazdopadne
    jsi rad prectu o vasem reseni.
- id: 646
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-09-10 09:44:24 +0200'
  date_gmt: '2007-09-10 08:44:24 +0200'
  content: "V podstatě jde jenom o jednoduché aplikování vlastností Springu. Nečekej
    od toho nic světoborného, ale zatím se nám to docela osvědčilo. Řeší to ty naše
    problémy a není to žádné velké hackování, a to je hlavní.\r\n\r\nCo ale v textu
    nebude je nasazení toho systému v prostředí EJB. To je pro mě trošku horká půda
    - nejsem moc velký odborník na EJB a už jsem si několikrát naběhl, to klidně přiznám.
    Při vývoji navíc EJB nepoužíváme, takže fakt ani praktické zkušenosti nemám. Nerad
    uváděl někoho v omyl nějakými mými neověřenými informacemi a proto se tomuhle
    tématu úplně vyhnu.\r\n\r\nBTW - ty už jsi nasadil OSGi ve Springu? Nějaké zkušenosti?
    Já se čísla verze 0.7 docela obávám pro nějaké vážnější nasazení na projektu."
- id: 647
  author: Lukas
  author_email: lukas@cnawr.cz
  author_url: http://www.archaebacteria.net
  date: '2007-09-10 10:03:29 +0200'
  date_gmt: '2007-09-10 09:03:29 +0200'
  content: Me by zajimalo, jestli umite vyresit i to, aby kazdy modul mel vlastni
    class path (napr. stare nebo patchovane verze knihoven)?
- id: 649
  author: jk
  author_email: nemam@nedam.cz
  author_url: ''
  date: '2007-09-10 10:42:31 +0200'
  date_gmt: '2007-09-10 09:42:31 +0200'
  content: Resim neco podobneho nad modularnim systemem v Netbeans. Podle dokumentace
    by to nemel  byt problem, napred se vytvori jedna bean factory per classloader
    (modul) a ty se slozi do contextu.
- id: 650
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-09-10 10:45:13 +0200'
  date_gmt: '2007-09-10 09:45:13 +0200'
  content: Skoro bych si tipnul, že tohle by mohlo umět to OSGi (usuzuji z fíčury
    "mít možnost provozovat různé verze modulů současně"). My nejdeme za hranice Spring
    frameworku a classloadery necháváme na pokoji ve stavu, v jakém nám je připraví
    cílový server. Ono vůbec, hraní si s classloadery je někdy spíše ke škodě - při
    deployi do J2EE serveru máte problém - classloading by tam měl být plně v režii
    serveru - podobně třeba jako správa threadů. Takže v tomhle ohledu bych byl stejně
    opatrný.
- id: 651
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-09-10 10:46:55 +0200'
  date_gmt: '2007-09-10 09:46:55 +0200'
  content: 'Ad jk: client side to je jiné kafe, tam si člověk může dovolit lecos ;).
    Ale my jedeme skoro výhradně server side ...'
- id: 652
  author: Lukas
  author_email: lukas@cnawr.cz
  author_url: http://www.archaebacteria.net
  date: '2007-09-10 11:03:02 +0200'
  date_gmt: '2007-09-10 10:03:02 +0200'
  content: 'Novoj: co umi OSGi docela dobre vim, rok jsem delal Eclipse RCP aplikaci
    a tam se tomu clovek nevyhne.'
- id: 653
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-09-10 11:46:55 +0200'
  date_gmt: '2007-09-10 10:46:55 +0200'
  content: Jasně - v OSGi jsem lamka, čerpám zatím jen z toho zdroje implementace
    OSGi do Springu.
- id: 654
  author: Roman Dagi Pichlik
  author_email: pichlik@seznam.cz
  author_url: http://www.sweb.cz/pichlik/
  date: '2007-09-10 11:52:47 +0200'
  date_gmt: '2007-09-10 10:52:47 +0200'
  content: "Classloadery aplikacniho serveru je prave onen problem, pokud me pamet
    neklame, tak v nejake specce je dokonce zakazano vytvaret si vlastni classloadery.
    Navic v kazdem aplikacnim serveru se chovani classloaderu lisi, takze se to musi
    specialne nastavit proprietarnimi deployment descriptory. Nam by OSGi poskytlo
    nekolik vlastnosti: moznost explicitne exportovat pouze urcitou cast API (slo
    by castecne dosahnout pomoci fasady), runtime reload/deploy modulu, oddeleni classpath
    jednotlivych modulu (rozdilne verze stejnych knihoven - potencialne). Neco z tech
    vlastnosti by slo zrejme naimplementovat svepomoci, ale proc to delat, kdy je
    tu OSGi. Spring OSGi nam do toho pasuje naramne, protoze vetsina aplikacnich modulu
    je managovana springovskym IoC kontejnerem.\r\n\r\nMy jsme ve stadiu kdy vime,
    co bychom asi tak potrebovali a co by nam OSGi prineslo. Tedka analyzujeme jake
    by to melo dopady na deployment a strukturu aplikace a co by to vlastne znamenalo.
    Mozna budeme delat i nejaky prototyp pro overeni funkcnosti. Pokud budou nejake
    zajimave informace, tak se o ne rad podelim ;-)."
- id: 655
  author: Roman Dagi Pichlik
  author_email: pichlik@seznam.cz
  author_url: http://www.sweb.cz/pichlik/
  date: '2007-09-10 11:58:19 +0200'
  date_gmt: '2007-09-10 10:58:19 +0200'
  content: Pro NetBeans je to hracka stejne jako pro Eclipse a ve sve podstate pro
    jakykoliv kontejner, ktery s modularnosti aplikace pocita. Bohuzel to je problem
    v J2EE kontejnerech, kde se s necim podobnym nepocitalo. Tam je v podstate jedina
    moznost a to napsat si vlastni reseni a nebo pouzit nejake open source proprietarni
    jako OSGi.
- id: 53690
  author: Myšlenky dne otce Fura &raquo; Blog Archive &raquo; Hledáme parťáka do Forresta
  author_email: ''
  author_url: http://blog.novoj.net/2011/10/31/hledame-partaka-do-forresta/
  date: '2011-10-31 08:04:52 +0100'
  date_gmt: '2011-10-31 07:04:52 +0100'
  content: "[...] je Spring Framework (nedávno jsme přešli na 3.X verzi), na kterém
    je také postaven náš modulární systém. Na pkomponentový web framework RamJrojektech
    se také setkáte se Spring Security,MyBatis, [...]"
---
<p>Ve chvíli, kdy začnete používat při vývoji masivněji Spring Framework a začnete vytvářet znovupoužitelné knihovny postavené nad tímto frameworkem, začnete řešit jak z těchto knihoven co nejlépe složit výslednou aplikaci. První myšlenky povedou pravděpodobně těmito cestami:</p>
<ol>
<li>konfigurační soubory jednotlivých knihoven sloučit v jednom velkém aplikačním kontextu</li>
<li>držet jednotlivé knihovny odděleně - nechat jim jejich vlastní aplikační kontexty a k těmto kontextům se dostávat programovým způsobem</li>
</ol>
<p>Obě cesty však mají svá úskalí.</p>
<p><a id="more"></a><a id="more-33"></a></p>
<p><b>ad 1)</b></p>
<p>Ta první s sebou nese řadu problémů týkající se porušením zapouzdření konkrétních knihoven. Např. budete řešit problémy s konflikty názvů bean (stanovení jmenných konvencí je možná cesta, ale velmi trnitá). Bude se vám špatně definovat rozhraní jednotlivých knihoven. Ve společném kontextu budou mít všechny beany přístup ke všem ostatním beanám v něm. Aplikační události budou všem knihovnám společné - takže může docházet k interferencím. Prostě se vám bude špatně odhadovat co se stane, když zkombinujete konfiguraci knihovny A s konfigurací knihovny B. A to ani nemluvě o některých vlastnostech Springu, které by vám spojení některých knihoven mohly ošklivě zkomplikovat (např. pokud by každá knihovna potřebovala svůj vlastní speciální Multicaster, jste v koncích).</p>
<p><b>ad 2)</b></p>
<p>Druhá cesta má také své problémy. Každou knihovnu musíte konfigurovat zvlášť a to i v případě bean, které by se vám hodily sdílet - typicky beany DataSource a TransactionManager, které zajišťují spojení s databází. Často máte jen jedinou databázi a při deploymenu je opravdovou výhodou, pokud máte konfiguraci jen jednou. Nemluvím jen konfiguraci url, username a pwd, ale třeba i nastavení connection poolu apod. - vždy je lepší mít pouze jediný connection pool pro aplikaci, než aby si každá knihovna řešila to samé znovu (ano na aplikačním serveru, toto není tak velký problém, protože toto můžete řešit mimo vaší aplikaci a dostate se přes JNDI k hotovému, ale ne vždy to můžete chtít nebo mít tu možnost). Dalším problémem jsou transakce - nad oddělenými aplikačními kontexty budete problematicky definovat sdílenou transakci.</p>
<p>Dost se nadřete - nemůžete využít vlastností Springu pro sestavení celé aplikace. Spring vám sestaví pouze jednotlivé moduly, ale propojení mezi nimi si už musíte řešit sami. Pravděpodobně bude mít každá knihovna nějakou speciální fasádu, přes kterou budete volat metody rozhraní této knihovny (fasáda si pak uvnitř získá inicializované beany ze aplikačního kontextu pomocí metody getBean(String beanName)). A to nemluvím o tom, že si to každá knihovna může řešit tak trochu po svém.</p>
<p>Kudy z toho ven?</p>
<h4>Modulární systémy</h4>
<p>Spring Framework připravuje podporu pro technologi OSGi, která právě řeší způsob jak vyvíjet a integrovat znovupoužitelné moduly. OSGi jako takové má za sebou poměrně dlouhou historii a v současné době se jedná o sofistikovaný a propracovaný způsob práce s moduly. OSGi ve Springu bude nabízet například následující vlastnosti:</p>
<ul>
<li>oddělení aplikační logiky do modulů</li>
<li>schopnost současně provozovat modul v různých verzích</li>
<li>možnosti dynamicky vyhledávat a používat služby nabízené ostatními moduly systému</li>
<li>možnost instalovat, aktualizovat a odinstalovávat moduly za běhu</li>
<li>nechat Spring Framework instanciovat, konfigurovat, skládat a dekorovat komponenty v a i nad jednotlivými moduly</li>
<li>jednoduchý a známý programovací model pro enterprise developry využívat vlastnosti OSGi platformy</li>
</ul>
<p>Mezi dalšími vlastnostmi, které vývojáři slibují je i podpora pro JMX, vlastní životní cykl jednotlivých modulů apod. Podrobněji se o OSGI rozepsal <a href="http://www.sweb.cz/pichlik/archive/2007_08_26_archive.html#4612983720007901953" target="_new">Dagi na svém blogu</a>.</p>
<p><b>ALE</b></p>
<p>Jenže <a href="http://www.springframework.org/osgi/specification" target="_new">podpora OSGi ve Springu</a> je stále ve stádiu přípravy (o tom mluví i číslo současné verze - 0.7) a tudíž se může rozhraní a způsob použití ještě měnit a řada věcí může být poměrně nevyladěných. Celý systém na první pohled nevypadá tak jednoduše, jak je deklarováno a řadu věcí pro menší aplikace možná ani nevyžadujeme.</p>
<p>V současné chvíli ve většině projektů, kterých se účastním, potřebuji jen následující vlastnosti:</p>
<ul>
<li>mít možnost vyvíjet knihovny samostatně bez ohledu na to jak budou ve výsledku do systému zapojeny</li>
<li>v aplikačních knihovnách mít možnost bez obavy využít veškerých možností Springu, bez obavy, že tím ovlivním ostatní součásti systému</li>
<li>sdílet společné části výsledné aplikace skrze moduly - typicky beany zapouzdřující připojení k databázi, mail serveru, ldap atp. - tzn. mít fyzicky v celé aplikaci pouze jedinou intanci beany daného druhu</li>
<li>jasně definovat rozhraní modulu - tedy aby se okolní moduly aplikace dostaly jen k těm beanám mého modulu, která já určím jako veřejné (těch bude v modulu typicky jen pár)</li>
<li>zajistit funkčnost Observer patternu (aplikační eventy / listenery) nad všemi moduly - ovšem pouze selektivně, tedy mít veřejné události jednotlivých modulů, na které mohou reagovat moduly ostatní</li>
<li>mít možnost refreshnout aplikaci za běhu (bez nutnosti restartu web kontextu v kontejneru)</li>
<li>mít možnost jednoduše nadefinovat sdílenou transakci nad voláním různých modulů standardním Spring (tím myslím AOP) způsobem</li>
</ul>
<p>Jsou vlastnosti, které nabízí zmíněné OSGi a které typicky k životu nepotřebuji:</p>
<ul>
<li>schopnost současně provozovat modul v různých verzích (tohle je ovšem potřeba jen opravdu ve velkých systémech, kde řadu věcí nemáte tak úplně pod kontrolou - zatím jsem podobnou věc nikdy nepotřeboval)</li>
<li>dynamicky vyhledávat služby ostatních modulů (když tvořím aplikaci určuji, které moduly budu potřebovat a které ne)</li>
<li>instalovat, aktualizovat a odinstalovávat moduly za běhu (mě stačí jednou za čas provést redeploy aplikace u zákazníka - nevadí mi, když se kvůli tomu systém na pár minut odstaví)</li>
<li>řešit lifecycle modulů zvlášť (mě stačí lifecycle, který definuje samotný Spring)</li>
</ul>
<p>Jednoduše řečeno pro mé potřeby se mi zdá OSGi technologie jako kanón na vrabce. Vždyť já toho k životu zase až tak moc nepotřebuji, chci jen rozumně vyvíjet aplikace, složené ze znovupoužitelných modulů založených na Springu. OSGi má řadu enterprise fíčur, které nikdy nevyužiji. </p>
<p>Pokud sdílíte můj názor, máte podobné problémy a hledáte nějaké jednoduché řešení, je tento můj seriál určen právě pro vás. Nečekejte žádné enterprise řešení plné buzzwordů a super reklamních fíčur. Jen jednoduchý kód, který vám pořeší problémy, které jsem zmínil. Budeme k tomu potřebovat jen pár dobře umístěných tříd a využití vlastností Springu, které v něm už léta jsou.</p>
<p>Pokud hledáte robustnější řešení bude samozřejmě lepší sáhnout po OSGi (až bude jeho implementace ve Springu dokončena) - tímto seriálem rozhodně nechci hodnotu OSGi shazovat (aby nedošlo k nějaké mýlce ;-) ).</p>
<h4>Dodatek</h4>
<p>Můj původní záměr byl pouze jediný článek. Materiálu je však na jeden příspěvek hodně a proto jsem se rozhodl text rozdělit do několika po sobě jdoucích příspěvků, které vám budu dávkovat zhruba v týdenních intervalech.</p>
<p><a href="http://blog.novoj.net/2007/09/14/cast-1-modularni-systemy-ve-spring-frameworku/">Díl #1: Aplikační kontexty</a></p>
