---
status: publish
published: true
title: Reportáž z GeeCON Praha 2015
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<a style=\"float: left; margin-right: 2em; margin-bottom: 1em;\" href=\"http://www.geecon.cz\"
  target=\"_blank\"><img src=\"https://s3.eu-central-1.amazonaws.com/geecon2015prague/banner+206x136+friend.jpg\"
  alt=\"GeeCON 2015\" /></a> GeeCON je zavedená konference, u které se můžete spolehnout
  na kvalitní speakery a skvělou organizaci. Připočtěme ještě rozumnou cenu a fakt,
  že se děje u nás v České republice a vychází nám z toho rovnice, která má jasně
  daný výsledek = je to akce, na které nemůžete chybět, pokud nemáte opravdu dobrou
  výmluvu :)\r\n\r\nV tomto článku udělám krátkou rešerši přednášek na kterých jsem
  byl.\r\n\r\n"
wordpress_id: 3037
wordpress_url: http://blog.novoj.net/?p=3037
date: '2015-10-26 09:38:49 +0100'
date_gmt: '2015-10-26 08:38:49 +0100'
categories:
- Java
- Reportáže
- GeeCON
tags: []
comments:
- id: 157546
  author: Martin Večeřa
  author_email: mvecera@perfcake.org
  author_url: http://www.perfcake.org
  date: '2015-10-27 10:25:15 +0100'
  date_gmt: '2015-10-27 09:25:15 +0100'
  content: Jen pro upřesnění - PerfCake není knihovna, ale komplexní nástroj. Jeho
    implementace neomezuje testování pouze na Javu. Je již poměrně stabilní, vydaná
    je verze 5.1. Nesnaží se konkurovat Gatlingu, je zkrátka určen na jiný typ testování,
    jak bylo zmíněno na přednášce. Má samozřejmě i Java API, jak je ostatně vidět
    v dokumentaci. Rozhraní příkazové řádky je takové jaké je a podle nás poměrně
    přehledné. Co chybí jsou stabilní pluginy pro IDE. SmartMeteru konkurujeme například
    snadnou použitelností, rozsahem podporovaných protokolů (např. REST), výkonem,
    snadností rozšíření a integrací do testů. Jsme open-source a zdarma.
- id: 157547
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2015-10-27 14:57:03 +0100'
  date_gmt: '2015-10-27 13:57:03 +0100'
  content: "Díky za komentář! \r\n\r\nJava API jsem hledal zde: https://www.perfcake.org/docs/user-guide/ug.perfcake-features.html#ug.perfcake-features.scenario-definition
    ... ale nenašel jsem. Nepochodil jsem ani zde: https://www.perfcake.org/docs/user-guide/ug.general-usage.perfcake-api.html\r\n\r\nNemohl
    bys mě, prosím, navést k tomu API?"
- id: 157548
  author: Pavel Macík
  author_email: pavel.macik@gmail.com
  author_url: ''
  date: '2015-10-27 16:21:02 +0100'
  date_gmt: '2015-10-27 15:21:02 +0100'
  content: "Zdravím Otče Fura,\r\nzkoušel jsi http://javadoc.perfcake.org/org/perfcake/scenario/ScenarioLoader.html
    ?"
- id: 157549
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2015-10-27 16:46:55 +0100'
  date_gmt: '2015-10-27 15:46:55 +0100'
  content: Jo aha - tak už vím v čem si nerozumíme. Mě šlo primárně o to zapsat celý
    scénář pomocí Javy. Tj. naskriptovat ten scénář rovnou v Javě - bez XML / TXT
    DSL jazyka.
---
<p><a style="float: left; margin-right: 2em; margin-bottom: 1em;" href="http://www.geecon.cz" target="_blank"><img src="https://s3.eu-central-1.amazonaws.com/geecon2015prague/banner+206x136+friend.jpg" alt="GeeCON 2015" /></a> GeeCON je zavedená konference, u které se můžete spolehnout na kvalitní speakery a skvělou organizaci. Připočtěme ještě rozumnou cenu a fakt, že se děje u nás v České republice a vychází nám z toho rovnice, která má jasně daný výsledek = je to akce, na které nemůžete chybět, pokud nemáte opravdu dobrou výmluvu :)</p>
<p>V tomto článku udělám krátkou rešerši přednášek na kterých jsem byl.</p>
<p><a id="more"></a><a id="more-3037"></a></p>
<p>Úvodní <strong>keynote Grant Ingersolla</strong> z firmy <a href="http://lucidworks.com/" target="_blank">Lucidworks</a>, která stojí za známým <a href="https://lucene.apache.org/core/" target="_blank">Lucene</a> narážela na to, zda-li dostatečně využíváme data, které nám v aplikacích generují naši uživatelé. Přitom tata data mohou být klíčová při vytváření UX - díky odhalování podobností v chování uživatelů a segmentaci, můžeme již předem vědět, co by mohl daný uživatel chtít a nabízet mu personalizovaný obsah, nebo jinou prioritizaci položek. O tom, že to není úplně jednoduché je možné se dočíst v <a href="https://www.zdrojak.cz/clanky/jak-skrz-cz-radi-20k-nabidek-podle-real-time-analytiky/" target="_blank">nedávném článku na Zdrojáku</a>. Na druhou stranu preferovat ve výsledcích vyhledávání "trendy" položky e-shopu nemusí být zase až taková věda, a kdo to skutečně dělá, že?</p>
<p>[gallery columns="1" link="file" ids="3063"]</p>
<p><strong>Krzysztof Dębski</strong> mluvil o tom, jak v <a href="http://allegro.pl/" target="_blank">Allegro</a> (provozovatel Aukra) zpracovávají obrovský stream vstupních dat pomocí <a href="http://kafka.apache.org/" target="_blank">Kafky</a>. Především se věnoval problémům, se kterými se při implementaci setkali. Na toto téma doporučuji <a href="http://programio.havrlant.cz/tags/kafka/" target="_blank">sérii článku od Lukáše Havrlanta</a>, která je v tomto ohledu docela detailní. Kryštof zmiňoval např. to, že pokud máte jediného producenta dat a ponecháte výchozí strategii pro publishing eventů do Kafky, nijak nevyužijete její výkonnostní parametry na úrovni partition - publisher defaultně zapisuje nějakou dobu (např. 10 minut) do jedné partition a pak switchne na druhou. Tj. v jednom momentu je utilizovaná pouze jediná partition na zápis.</p>
<p>Upozorňoval také na konfigurační nastavení <em>replica.lag.max.messages</em> (<a href="http://www.confluent.io/blog/hands-free-kafka-replication-a-lesson-in-operational-simplicity/" target="_blank">blíže popsáno třebas zde</a>), které určuje o kolik záznamů může být replika pozadu (než je považována za mrtvou). To mj. také znamená, že když vypadne master na dané partition, můžete nenávratně příjít tento počet zpráv - pokud je replika, která se stane novým masterem pozadu v synchronizaci. Můžete samozřejmě při zápisech trvat na potvrzení (ACK) až poté, co je zpráva uložena i na replice, ale tím přicházíte o tolik potřebný výkon.</p>
<p>Upozorňoval i na chybu kernelu 3.2.x, která způsobuje, že flush na disk pozastaví na krátkou dobu chod systému (tato chyba je opravena až ve verzi 3.8.X) - správně by měl být flush prováděn asynchronně, ale v dané verzi kernelu tomu tak není. Poměrně dlouho také elaboroval nad tím, jaký formát dat zvolit pro ukládání dat do Kafky - začínali s JSON formátem, který je pro ukládání velmi neefektivní a jeho hlavní výhodu - čitelnost - vlastně nikdy nepoužili. Nedoporučoval používat protokoly <a href="https://cwiki.apache.org/confluence/display/KAFKA/Compression" target="_blank">Snappy</a> a <a href="https://issues.apache.org/jira/browse/KAFKA-1456" target="_blank">Lz4</a>, protože při jejich použití dochází sem tam k poškození dat. Jim se osvědčil formát <a href="https://avro.apache.org/" target="_blank">Avro</a>, který má malý footprint na síti (je binární), je Hadoop friendly a má schéma, dle kterého se dá validovat.</p>
<p>[gallery columns="1" link="file" ids="3045"]</p>
<p>V Allegro vyvíjejí systém <a href="https://github.com/allegro/hermes" target="_blank">Hermes</a>, kterým se snaží řešit některé negativní stránky Kafky. V tomto kontextu padl i onen často zmiňovaný problém záruky <a href="http://bravenewgeek.com/you-cannot-have-exactly-once-delivery/" target="_blank">doručení zprávy právě jednou</a> (viz. přiložený obrázek).</p>
<p><strong>Martin Večeřa </strong>a<strong> Pavel Macík</strong> na konferenci představili Java knihovnu pro výkonnostní testování - <a href="https://www.perfcake.org/" target="_blank">PerfCake</a>. Starší přednášku od této dvojice na stejné téma můžete shlédnout např. zde:</p>
<div style="text-align: center;"><iframe width="560" height="315" src="https://www.youtube.com/embed/bcaft6Fyg-0" frameborder="0" allowfullscreen="allowfullscreen"></iframe></div>
<p>Knihovna se snaží konkurovat zavedené knihovně <a href="http://gatling.io/#/" target="_blank">Gatling</a> napsané ve Scale. Testovací scénáře se píší buď ve vlastním "plain textovém" DSL nebo v XML (marně jsem hledal Java API ekvivalent). Testování je zaměřeno na ověření SLA nebo také nalezení "sweet spot", ve kterém aplikace reaguje nejlépe. Výsledky testů je možné nově uploadovat do tzv. <a href="https://github.com/PerfCake/PerfRepo" target="_blank">PerfRepo</a>, což je webová aplikace, která umí výsledky testů ukládat, tagovat, zobrazovat a porovnávat mezi sebou. Z ukazovaného dema bylo vidět, že aplikace je ještě syrová a z hlediska UI bude potřebovat ještě další dočištění. Rozhodně se však jedná o zajímavý počin, který stojí za vyzkoušení - zvlášť, pokud vám nesedí Scala :) Nástroj aktuálně neumožňuje distribuované generátory zátěže. Osobně by mě zajímalo srovnání např. s českým <a href="https://www.smartmeter.io" target="_blank">SmartMeter</a>, který mi přijde na první pohled pokročilejší, ovšem komerční.</p>
<p><strong>Lukáš Křečan</strong> z GoodData měl ve vedlejší místnosti přednášku o nebezpečí paralelních streamů v Java 8. Problém naznačil už ve svém <a href="http://blog.krecan.net/2014/03/18/how-to-specify-thread-pool-for-java-8-parallel-streams/" target="_blank">článku z roku 2014</a>. V přednášce problematiku rozvedl do větších detailů - <a href="https://drive.google.com/file/d/0BxY-qaWoIbe5S3lQNnpjbTZfNDA/view" target="_blank">posuďte sami</a> a podle mých kolegů, kteří na přednášce byly, se velmi povedla.</p>
<p><strong>Martin Škurla</strong> ve své přednášce rozebral základy fungování classloaderů v Javě - s velkým přesahem do historie. Přednáška byla určitě zajímavá pro někoho, kdo se v problematice orientuje, ale mě moc nového, bohužel, nepřinesla. Byla velmi srozumitelná a hezky podaná. Já jsem se těšil na rozebrání toho, co nás čeká v Javě 9 s projektem Jigsaw, ale toho jsem se nedočkal.</p>
<p><strong>Juergen Hoeller</strong> ve své přednášce popisoval přístup Springu k definici anotací a vypichoval věci, které on osobně považuje v celém ekosystému za zajímavé a důležité. Jednou z nich je např. možnost <a href="https://dzone.com/articles/avoid-spring-annotation-code-smell-use-spring3-custom-annotations" target="_blank">kompozice anotací</a> (je velká škoda, že podobnou věc nelze udělat i ve Spring Security - <a href="http://blog.novoj.net/2012/03/27/combining-custom-annotations-for-securing-methods-with-spring-security/" target="_blank">což sice lze obejít</a>, ale dost pracně). Zdůrazňoval respektování použitých generik v třídách autowirovaných springem a možnost využití sady odpovídajících bean např. pomocí:</p>
<p>[source lang="java"]@Autowired<br />
public MyObject(<br />
   List&lt;HttpService&gt; httpServices,<br />
   GenericDao&lt;Product&gt; productDao) {<br />
   ...<br />
}[/source]</p>
<p>Co bylo pro mě nové je možnost v rámci autowingu použít deklaraci Optional&lt;ClassBeany&gt;, což Spring vyhodnotí jako nepovinný autowiring (tj. pokud odpovídající beana existuje, bude autowirovaná, pokud ne, autowiruje se Optional.empty()). Novinkou pro mě bylo i to, že Java 8 podporuje <a href="https://docs.oracle.com/javase/tutorial/java/annotations/repeating.html" target="_blank">repeatable anotace</a>, což mi z radaru nějak uteklo. Stejně tak mi utekla i nová Spring anotace @EventListener, která <a href="https://spring.io/blog/2015/02/11/better-application-events-in-spring-framework-4-2" target="_blank">umožňuje v rámci jedné třídy</a> pořešit hned sadu souvisejících událostí. Juergen v následující přednášce také vykládal o novinkách, které chystají do následujího release Springu, ale z této přednášky mám jen pár fotek:</p>
<p>[gallery columns="2" ids="3048,3049,3050,3053"]</p>
<p>Zavítal jsem i na přednášku <strong>Toma Bujoka</strong> o distribuované memory databázi Hazelcast. Opět se mi nevyplatilo jít na přednášku na téma, kde něco málo znám - ačkoliv byla srozumitelná a hezky poslouchatelná, nedozvěděl jsem se nic jiného, než je možné dočíst v <a href="http://docs.hazelcast.org/docs/3.3/manual/html-single/hazelcast-documentation.html" target="_blank">oficiální dokumentaci</a>. Zajímavá byla zmínka o distribuovaných query v <a href="http://docs.hazelcast.org/docs/3.5/manual/html/querysql.html" target="_blank">SQL like jazyku</a> (popř. v <a href="http://docs.hazelcast.org/docs/3.5/manual/html/querycriteriaapi.html" target="_blank">predikátové formě</a>), které jsou paralelně vyhodnocovány na jednotlivých uzlech memory gridu. Část přednášky se soustředila i na strategii <a href="http://docs.hazelcast.org/docs/3.5/manual/html/performance.html#data-affinity" target="_blank">soustředění souvisejících dat na stejném uzlu gridu</a> pomocí PartitionAware rozhranní, které umožňuje efektivnější výpočty díky vyloučení nákladů na komunikaci po síti. Hazelcast může samozřejmě fungovat i jako distribuovaná cache a dokonce se dá použít i jako Memcached drop-in replacement.</p>
<p>Velmi poutavá byla přednáška <strong>Bas Knoppera</strong> o evolučních algoritmech, což je věc, se kterou se denně nesetkáváme. Popisoval v ní na příkladu cestujícího obchodníka (traveling salesman) konkrétní použití evolučního algoritmu, které si sami můžete <a href="https://github.com/bknopper/TSPEvolutionaryAlgorithmsDemo" target="_blank">vyzkoušet zde</a>.</p>
<p>[gallery columns="1" link="file" ids="3065"]</p>
<p>V přednášce byly detailně popsány základní principy každého evolučního algoritmu - od tvorby úvodní populace, stanovení fitnes funkce, výběru kandidátů pro další iteraci, kombinační a mutační funkce a mnoho dalšího. Pokud tato přednáška vyjde jako videozáznam, vřele doporučuji její shlédnutí. Evoluční algoritmy doporučuje Bas Konpper všude, kde je tak velký počet kombinací, že není možné použít přístup hrubou silou a zároveň je možné stanovit fitness funkci, funkci pro kombinaci a mutaci prvků. Podobně to <a href="https://www.youtube.com/watch?v=B7KdN4PRgj4" target="_blank">například provedla NASA</a> pro tvorbu minimalistické antény pro komunikaci s pozemní základnou.</p>
<div style="text-align: center;"><iframe width="420" height="315" src="https://www.youtube.com/embed/B7KdN4PRgj4" frameborder="0" allowfullscreen="allowfullscreen"></iframe></div>
<p><strong>Simon Brown</strong> si ve své přednášce Modular Monoliths lehce utahoval s aktuálního trendu microservis. Vyzdvihoval známou pravdu, že pokud nejste schopni vytvořit kvalitní monolickou aplikaci, přechodem na microservice architekturu si nejspíše nepomůžete - spíše naopak (o tom konec konců píše i velký <a href="http://martinfowler.com/bliki/MonolithFirst.html" target="_blank">Martin Fowler</a>). Ve své přednášce popisuje to, co ve <a href="http://www.fg.cz" target="_blank">Forrestu</a> už praktikujeme několik let (alespoň tedy na úrovni komponent), i když musím přiznat, že moje přednáška na CZJUGu nesahala této ani po paty. Holt kdo umí, ten umí :)</p>
<p>Poslední zajímavé vystoupení se týkalo testování microservice based architektury od člověka se jménem <strong>Christopher Batey</strong>, který řešil jako konzultant rozpad monolitické architektury aplikace pro poskytování streamovaného videa v Británii. V několika demech ukázal praktické použití nástrojů jako je třeba <a href="http://wiremock.org/" target="_blank">Wiremock</a>, který umožňuje simulovat problémy na síťové vrstvě a ať už v podobě prodlužování odezvy nebo zdržování jednotlivých paketů. Osobně jsem si teprve až tady uvědomil, jak složité může být v microservice architektuře (a v podstatě v každé architektuře, která má více elementů komunikujících po síti) zaručit SLA. Těch kombinací, které způsobí "zaseknutí" služby je totiž daleko více než jen connection timeout. Doporučoval např. nikdy se nevzdávat vlákna, které řeší request uživatele - veškerou komunikaci po síti provádět v separátním vlákne s pevně danými timeoutem. Klíčové sdělení jeho přednášky bylo: <em>"<strong><span style="font-weight: 400;">you don’t know a service is fault tolerant if you don’t test faults</span></strong>" </em>a položme si ruku na srdce - kdo z nás si skutečně simuloval všechny možné problémy, které mohou v distribuovaných architekturách nastat?! K přečtení doporučoval knížku <a href="https://pragprog.com/book/mnee/release-it" target="_blank">Release it!</a>, která jej k této přednášce inspirovala. Doporučoval také použití nástrojů jako jsou <a href="https://github.com/Netflix/Hystrix" target="_blank">Hystrix</a>, <a href="http://graphite.readthedocs.org/en/latest/" target="_blank">Graphite</a> nebo <a href="https://github.com/tomakehurst/saboteur" target="_blank">Saboteur</a>. I tuto přednášku doporučuji shlédnout online, pokud bude zveřejněna.</p>
<p>[gallery columns="1" link="file" ids="3066"]</p>
<p>Na konec musím poděkovat organizátorům, protože je vidět, že opravu umí - letos fungovala dokonce i Wi-Fi a to vůbec není při tomto počtu zařízení samozřejmé. <a href="https://hotcario.wordpress.com/" target="_blank">Dagimu</a> děkuji za volňásek a doufám, že jsem si ho tímto článkem zasloužil.</p>
<p><img class="aligncenter size-large wp-image-3064" src="http://blog.novoj.net/binary/2015/10/IMG_20151022_100727-1024x768.jpg" alt="IMG_20151022_100727" width="627" height="470" /></p>
