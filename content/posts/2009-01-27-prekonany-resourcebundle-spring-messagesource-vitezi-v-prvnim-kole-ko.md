---
status: publish
published: true
title: Překonaný ResourceBundle, Spring MessageSource vítězí v prvním kole KO
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Tento článek mám ve WordPressu rozepsaný snad už rok. Jeho původní název
  zněl \"ResourceBundle - stačí Javě beze změny?\". Plno věcí, které jsme původně
  jako Java vývojáři dělali my, postupně uzpůsobujeme tak, aby je mohli dělat web
  designeři. Na prezentační vrstvu zcela jistě patří lokalizované texty a zprávy,
  pro které standardně používáme ResourceBundly Javy, které se načítají z property
  souborů. Ideální model pro web developery je iterace: navrhnu stránku, vložím text
  do property bundlu, uložím, reloadnu stránku a kouknu jak to vypadá. V tomhle jednoduchém
  scénáři jsme však narazili hned na několik problémů.\r\n\r\nStandardní PropertyResourceBundle
  se obvykle získává takto (to je mmch. cesta zmíněná v dokumentaci ResourceBundle):
  \r\n\r\n[source lang=\"java\"]\r\nResourceBundle myResources = \r\n   ResourceBundle.getBundle(\"MyResources\",
  currentLocale);\r\n[/source]\r\n\r\nTakto načítaný property soubor (\"MyResources.properties\")
  musíme mít na classpath (kde samozřejmě není editovatelný) a musíme jej mít ve Ascii
  formátu zkonvertovaný utilitou Native2Ascii. Dalším problémem je sekvence, ve které
  se hledají konkrétní lokalizované varianty bundlu. Díky tomu, že Java původně vznikla
  hlavně pro desktopové aplikace se do posloupnost hledání bundlů dostává i bundle
  pro systémové locale stroje, na kterém aplikaci spouštíme. V případě volání metody
  getBundle s Locale(\"cs\",\"CZ\") se na anglickém Ubuntu hledá property bundle v
  této posloupnosti:\r\n\r\n<ol>\r\n   <li>messages_cs_CZ.properties</li>\r\n   <li>messages_cs.properties</li>\r\n
  \  <li>messages_en_US.properties</li>\r\n   <li>messages_en.properties</li>\r\n
  \  <li>messages.properties</li>\r\n</ol>\r\n\r\nTuto věc jsem ještě před rokem nevěděl,
  a to možná také proto, že není nijak zmíněná v dokumentaci Javy.\r\n\r\nTak se nám
  těch problémů nakonec sešlo docela dost - na to, že řešíme takovou hloupost jako
  je lokalizace - že?\r\n\r\n"
wordpress_id: 75
wordpress_url: http://blog.novoj.net/?p=75
date: '2009-01-27 05:17:27 +0100'
date_gmt: '2009-01-27 04:17:27 +0100'
categories:
- Programování
- Java
- Spring Framework
- Web
tags: []
comments:
- id: 6015
  author: Pavel
  author_email: pave@ponec.net
  author_url: ''
  date: '2009-01-27 12:07:44 +0100'
  date_gmt: '2009-01-27 11:07:44 +0100'
  content: "Konverzi kódové stránky by mělo řešit IDE. NetBeans obsahuje výborný nástroj
    ve stylu tabulkového editoru, každý řádek obsahuje klíč property + jazykové mutace
    a sloupce se dají řadit. \r\n\r\nPro překlad se občas hodí i samostatný SW:\r\nhttps://prbeditor.dev.java.net/manual/manual_0.9.5_8.html\r\n\r\nJinak
    díky za zajímavý článek."
- id: 6016
  author: Makub
  author_email: makub@ics.muni.cz
  author_url: ''
  date: '2009-01-27 13:13:49 +0100'
  date_gmt: '2009-01-27 12:13:49 +0100'
  content: Nějak jsem z toho nepochopil, jak se dostanu k textům z JSP stránek. Ideálně
    pomocí JSTL tagů.
- id: 6017
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-01-27 14:43:29 +0100'
  date_gmt: '2009-01-27 13:43:29 +0100'
  content: "Pavel: vím, že konverzi by mělo řešit IDE, nicméně jsou situace, kdy člověk
    potřebuje udělat třeba rychlý zásah někde kde IDE k dispozici není. Nebo pokud
    třeba ne zrovna zásah, tak minimálně kouknout rovnou do property bundlu, co je
    tam vlastně uložené a encodované znaky čitelnost výrazně snižují (BTW - řada našich
    webařů dělá v Notepad++ nebo PSPadu, takže i to je argument).\r\n\r\nMakub: pravda
    .... moje chybka. Spring nabízí ve standardní TLD knihovně JSP tag. Více viz.
    http://static.springframework.org/spring/docs/1.1.5/taglib/tag/MessageTag.html\r\n\r\nTento
    tag potom bude koukat do defaultního web aplikačního kontextu, takže při nějakém
    složitějším složení stromu aplikačních kontextů na serverové straně bude třeba
    zajistit, aby byl viditelný správný MessageSource."
- id: 6020
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-01-27 18:21:31 +0100'
  date_gmt: '2009-01-27 17:21:31 +0100'
  content: Teprve teď jsem měl čas kouknout trochu na ten PRB Editor a vypadá na překlady
    většího rázu opravdu dobře. Nemáte někdo tip na nějakou kvalitní překladovou agenturu,
    která by uměla pracovat s něčím jiným než s Wordem a Excelem?
- id: 6021
  author: Ivan
  author_email: ivan.pullman@gmail.com
  author_url: ''
  date: '2009-01-27 18:41:53 +0100'
  date_gmt: '2009-01-27 17:41:53 +0100'
  content: "nema to sice vsetky vlastnosti, ale urcite je to krok vpred:\r\n\r\nhttp://java.sun.com/javase/6/docs/api/java/util/ResourceBundle.Control.html"
- id: 6022
  author: Ladislav Thon
  author_email: ladicek@gmail.com
  author_url: ''
  date: '2009-01-27 19:02:48 +0100'
  date_gmt: '2009-01-27 18:02:48 +0100'
  content: Díky za výborný článek, MessageSource jsem sice znal, ale rozhodně ne tak
    detailně. I like this. Ale pořád si myslím, že ideální by bylo mít texty (aspoň
    jejich defaulty) přimo v HTML šabloně. Máme na to nějaké udělátko, ale pro webaře
    není úplně příjemné...
- id: 6040
  author: kubino
  author_email: kubino@gmail.com
  author_url: ''
  date: '2009-01-29 11:26:55 +0100'
  date_gmt: '2009-01-29 10:26:55 +0100'
  content: cacheMillis mi nejak nefacha (spring 2.5.5), cacheSeconds ano, diky.
- id: 6041
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-01-29 11:41:09 +0100'
  date_gmt: '2009-01-29 10:41:09 +0100'
  content: Pravda ... opravím v článku cacheMillis je název fieldu. Setter metoda
    je cacheSeconds a hodnotu tam převádějí na milisekundy. Omlouvám se.
- id: 36472
  author: Vlada
  author_email: pravenec@centrum.cz
  author_url: ''
  date: '2011-03-17 16:33:57 +0100'
  date_gmt: '2011-03-17 15:33:57 +0100'
  content: "Ahoj, v clanku je napsano: \"resourceLoader – implementace rozhraní pro
    přístup k souborům reprezentujícím message bundly; díky resource loaderu můžete
    jednoduše zajistit načtení obsahu souboru třebas z databáze\"\r\n\r\nNebyl by
    nejaky priklad jak to nacitani z DB udelat? Googlil jsem neuspesne :-(\r\n\r\nMoc
    hezkej clanek!"
- id: 36633
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-03-19 20:54:39 +0100'
  date_gmt: '2011-03-19 19:54:39 +0100'
  content: "ResourceLoader ti umožní získat Resource pro libovolný binární obsah ze
    zdrojového úložiště, které je daným ResourceLoaderem podporováno. Spring podporuje
    několik základních typů zdrojových úložišť: classpath, file, url, servlet context
    a toto rozhraní je přímo implementováno ApplicationContextem.\r\n\r\nRozbor s
    examplem: \r\nhttp://www.mkyong.com/spring/spring-resource-loader-with-getresource-example/\r\n\r\nPokud
    člověk potřebuje dodat nový typ úložiště (např. DB) musí udělat dvě věci:\r\n\r\n1)
    extendovat konkrétní ApplicationContext třídu (tj. např. ClassPathXmlApplicationContext
    nebo XmlWebApplicationContext apod.) a přetížit metodu org.springframework.core.io.DefaultResourceLoader#getResourceByPath,
    ve které následně implementovat rozpoznání nového typu zdrojového úložiště (např.
    prefixem db:)\r\n\r\n2) implementovat vlastní implementaci Resource rozhraní pro
    soubor uložený v DB (tj. něco, co ve finále poskytne InputStream)\r\n\r\nA to
    je vše. My jsme si podobné rozšíření provedli, ale bohužel ho nemůžu ukázat. V
    našem případě je totiž natolik specifické, že bych to musel, pro účely porozumitelného
    příkladu, naimplementovat znovu."
- id: 36837
  author: Vlada
  author_email: pravenec@centrum.cz
  author_url: ''
  date: '2011-03-23 07:22:52 +0100'
  date_gmt: '2011-03-23 06:22:52 +0100'
  content: "Díky. Bylo by možné alespoň naznačit implementaci Resource rozhraní v
    případě, že data jsou v DB uložena jako jednotlivé řádky, nikoliv soubor (clob).
    Je možné i v tomto případě do DB přistupovat pomocí EntityManageru (tedy s využitím
    existujícího připojení do DB)?\r\n\r\nPS: Moje otázky asi zní hloupě, ale dostal
    jsem se k J2EE aplikacím teprve nedávno, tak studuju a studuju, ale postrádám
    některé zásadní praktické zkušenosti :("
- id: 90024
  author: "&raquo; Nástroje pro vývoj web aplikací ve Forrestu Myšlenky dne otce Fura"
  author_email: ''
  author_url: http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/
  date: '2012-09-04 07:11:32 +0200'
  date_gmt: '2012-09-04 06:11:32 +0200'
  content: "[...] směru využíváme skvělé podpory Springu ve formě ReloadableResourceBundle,
    jak jsem jej popsal v tomto článku. Díky pár úpravám jsme schopni monitorovat,
    jaká oblast stránky používá které [...]"
---
<p>Tento článek mám ve WordPressu rozepsaný snad už rok. Jeho původní název zněl "ResourceBundle - stačí Javě beze změny?". Plno věcí, které jsme původně jako Java vývojáři dělali my, postupně uzpůsobujeme tak, aby je mohli dělat web designeři. Na prezentační vrstvu zcela jistě patří lokalizované texty a zprávy, pro které standardně používáme ResourceBundly Javy, které se načítají z property souborů. Ideální model pro web developery je iterace: navrhnu stránku, vložím text do property bundlu, uložím, reloadnu stránku a kouknu jak to vypadá. V tomhle jednoduchém scénáři jsme však narazili hned na několik problémů.</p>
<p>Standardní PropertyResourceBundle se obvykle získává takto (to je mmch. cesta zmíněná v dokumentaci ResourceBundle): </p>
<p>[source lang="java"]<br />
ResourceBundle myResources =<br />
   ResourceBundle.getBundle("MyResources", currentLocale);<br />
[/source]</p>
<p>Takto načítaný property soubor ("MyResources.properties") musíme mít na classpath (kde samozřejmě není editovatelný) a musíme jej mít ve Ascii formátu zkonvertovaný utilitou Native2Ascii. Dalším problémem je sekvence, ve které se hledají konkrétní lokalizované varianty bundlu. Díky tomu, že Java původně vznikla hlavně pro desktopové aplikace se do posloupnost hledání bundlů dostává i bundle pro systémové locale stroje, na kterém aplikaci spouštíme. V případě volání metody getBundle s Locale("cs","CZ") se na anglickém Ubuntu hledá property bundle v této posloupnosti:</p>
<ol>
<li>messages_cs_CZ.properties</li>
<li>messages_cs.properties</li>
<li>messages_en_US.properties</li>
<li>messages_en.properties</li>
<li>messages.properties</li>
</ol>
<p>Tuto věc jsem ještě před rokem nevěděl, a to možná také proto, že není nijak zmíněná v dokumentaci Javy.</p>
<p>Tak se nám těch problémů nakonec sešlo docela dost - na to, že řešíme takovou hloupost jako je lokalizace - že?</p>
<p><a id="more"></a><a id="more-75"></a></p>
<h2>ReloadableResourceBundleMessageSource</h2>
<p>Naštěstí je tu Spring - jak jinak. Je to prozatím jediné místo, kde jsem našel zmíněný problém pořešený natolik dobře, že likvidace všech zmíněných problémů nám nakonec zabere jen pár minut.</p>
<p>To řešení se jmenuje <a href="http://static.springframework.org/spring/docs/2.5.x/api/org/springframework/context/support/ReloadableResourceBundleMessageSource.html" target="_blank">ReloadableResourceBundleMessageSource</a>. Jeho použití má řadu předností:</p>
<ul>
<li><strong>basenames</strong> - property akceptující array stringů reprezentující základ cesty k properties souborům (v základu je podporován i XML formát); property ze všech těchto souborů se sloučí a vy můžete žádat o texty z libovolného z nich</li>
<li><strong>defaultEncoding, respektive fileEncodings</strong> - výchozí kódování property souborů - buď hromadně pro všechny uvedené (defaultEncoding), nebo jednotlivě pro každý zvlášť (fileEncodings); od této chvíle už nepotřebujete Native2Ascii</li>
<li><strong>fallbackToSystemLocale</strong> - property, která určuje jestli se při výpočtu variant souborů má počítat i se systémovým locale nebo ne; nastavením na false se zbavíte problému s nelogickou posloupností v prostředí web aplikací</li>
<li><strong>cacheSeconds</strong> - definuje čas v sekundách po který jsou obsahy property bundlů cachovány; na produkci se hodí hodnota -1 (napořád), při vývoji naopak 0 (nikdy)</li>
<li><strong>propertiesPersister</strong> - interface pro načítání / ukládání messagí do / z cílového formátu (v základu properties a XML, ale díky rozhraní si můžete dopsat cokoliv - třeba i načítání z MS Excelu)</li>
<li><strong>resourceLoader</strong> - implementace rozhraní pro přístup k souborům reprezentujícím message bundly; díky resource loaderu můžete jednoduše zajistit načtení obsahu souboru třebas z databáze</li>
</ul>
<p>Jediná Spring třída nám v podstatě řeší všechny problémy naráz. Pokud budu mít ve svém aplikačním kontext následující definici:</p>
<p>[source lang="xml"]<br />
<bean id="messageSource" class="org.springframework.context.support.ReloadableResourceBundleMessageSource"></p>
<property name="basenames">
<list>
			<value>file:/projekt/neco/messages</value><br />
			<value>file:/projekt/neco/exceptions</value><br />
			<value>file:/projekt/neco/disclaimer</value>
		</list>
	</property>
<property name="defaultEncoding" value="UTF-8"/>
<property name="fallbackToSystemLocale" value="false"/>
<property name="cacheSeconds" value="0"/>
</bean><br />
[/source]</p>
<p>... získám přesně tu funkcionalitu, kterou pro hladký vývoj potřebuji. Property soubory jsou uložené v textových souborech ve formátování UTF-8 na filesystému, při změně libovolného z nich se mi změna okamžitě projeví i v obsahu web stránky. Navíc se mi konečně hledání správného property bundlu chová tak jak očekávám, tzn. můžu bez obav vytvořit "default" property bundle s pojmenováním "neco.properties" a vím, že pokud bude chtít lokalizované zdroje, které zatím nemám k dispozici (třeba thajštinu), tak se použije obsah právě tohoto "default" bundlu a nikoliv (záhadně) odlišná lokalizace dle nativního locale Javy na serveru.</p>
<h2>Jak se ke zprávám dostanu z kódu</h2>
<p>Dostáváme se k základům Springu, ale pokud by někdo přeci jen nevěděl ... </p>
<p>Pokud dodržíme jmennou konvenci a beanu nazvu "messageSource" není třeba již nic moc složitého provádět. Stačí když ve svých beanách implementuji rozhraní <a href="http://static.springframework.org/spring/docs/2.5.x/api/org/springframework/context/MessageSourceAware.html" target="_blank">MessageSourceAware</a>, Spring sám mi do nich injektuje referenci na připravený MessageSource se zprávami.</p>
<p>MessageSource sice již obsahuje potřebné metody k získání zpráv, ale často se hodí i použití helper wrapperu <a href="http://static.springframework.org/spring/docs/2.5.x/api/org/springframework/context/support/MessageSourceAccessor.html" target="_blank">MessageSourceAccessor</a>, který sadu metod rozšiřuje. Ten navíc obsahuje i integraci s třídou <a href="http://static.springframework.org/spring/docs/2.5.x/api/org/springframework/context/i18n/LocaleContextHolder.html" target="_blank">LocaleContextHolder</a>, která nám zase zajišťuje přístup ke správnému locale pro aktuální request (v kombinaci s <a href="http://static.springframework.org/spring/docs/2.5.x/api/org/springframework/web/servlet/DispatcherServlet.html" target="_blank">DispatcherServlet</a> nebo libovolným filtrem / servletem, který si sami napíšete).</p>
<h2>MessageSourceResolvable - když je jeden klíč pro zprávu málo</h2>
<p>Další skvělou vlastností MessageSource Springu je možnost hledat lokalizovanou zprávu pod několika klíči naráz v předem definované posloupnosti. Na podobnou funkcionalitu narazíte i ve web frameworku Stripes. Na první pohled by se mohlo zdát jako zbytečnost - vždyť pokud přeci potřebuju lokalizovaný text, tak přeci vždy vím jaký. A to právě není tak úplně pravda ...</p>
<p>Pokud píšete nějakou obecnější věc, může se hodit seskupovat lokalizované zprávy do konkrétních skupin obecnosti. V případě aplikační chyby třeba definovat nejen konkrétní klíč pro danou chybu "exception.myBusinessClass.errorCode", ale i obecnější kód "exception.general" - popř. i více kódů pro jemnější členění. Uživatel vaší knihovny se pak může rozhodnout které kódy využije (přeloží) a které nikoliv. Pokud nepotřebuje detailní rozlišení pro chybová hlášení, může se rozhodnout přeložit pouze hlášení "exception.general" a má lokalizaci vyřešenou.</p>
<p>Osobně považuji tento mechanismus za geniální -  v našem prostředí ho využíváme například pro validační hlášení. Každé validační chybové hlášení hledáme pomocí <a href="http://static.springframework.org/spring/docs/2.5.x/api/org/springframework/context/MessageSourceResolvable.html" target="_blank">MessageSourceResolvable</a> pod těmito klíči:</p>
<ul>
<li>validation.lokaceStranky.lokaceKomponenty.typValidace (validation.blogs.createBlog.title.required)</li>
<li>validation.lokaceStranky.typValidace (validation.blogs.createBlog.required)</li>
<li>validation.typValidace (validation.required)</li>
</ul>
<p>Takto je potom možné mít obecnější validační hlášení pro celý web, ale pokud je potřeba pro konkrétní stránku toto hlášení uzpůsobit, stále je tu ta možnost.</p>
<h2>Ještě nekončíme - co se znovupoužitelnými knihovnami?</h2>
<p>Je tu ještě jeden problém, který jsem dosud nezmínil. Co když chceme mít obecnou knihovnu, která potřebuje produkovat hlášení prezentované uživateli? Rádi bychom, abychom ji mohli dát na classpath a bez jakékoliv dodatečné práce ji mohli hned používat (tzn. knihovna měla sama v sobě zabudovaná použitelná lokalizovaná hlášení). Na druhou stranu bychom ale zase chtěli, aby nám zůstala možnost výběrově některé z hlášení při specifickém nasazení změnit.</p>
<p>Pro tyto účely můžeme využít hierarchického členění MessageSourců (<a href="http://static.springframework.org/spring/docs/2.5.x/api/org/springframework/context/HierarchicalMessageSource.html" target="_blank">HierarchicalMessageSource</a>), které se principem podobá mechanismu který platí i pro samotné aplikační kontexty. Pokud zajistíme, aby "systémová" lokalizace knihovny byla nastavena jako parentMessageSource pro námi používaný MessageSource docílíme požadovaného chování. V našem MessageSource potom můžeme předefinovat jen pár lokalizovaných hlášení, o která nám jde a zbytek bude delegován na nadřízený MessageSource, kde vždy nalezneme původní systémová hlášení knihovny.</p>
<p>Podpora pro hnízdění MessageSourců je již implementována v aplikačním kontextu Springu - konkrétně v AbstractApplicationContext. Pokud ve svém podřízeném aplikačním kontextu nadefinujete beanu "messageSource", která bude implementovat HierarchicalMessageSource a nebude mít nastavený parentMessageSource, Spring sám mu nastaví tento parentMessageSource na MessageSource nadřízeného aplikačního kontextu. Tahle věta je možná trošku oříšek, ale jednodušeji jsem to zapsat nedokázal - v případě nejasností se stačí kouknout do třídy <a href="http://static.springframework.org/spring/docs/2.5.x/api/org/springframework/context/support/AbstractApplicationContext.html" target="_blank">AbstractApplicationContext</a>, metody <a href="http://static.springframework.org/spring/docs/2.5.x/api/org/springframework/context/support/AbstractApplicationContext.html#initMessageSource()" target="_blank">initMessageSource()</a>.</p>
<h2>Závěrem</h2>
<p>Škoda, že podobná podpora, jakou nalezneme ve Springu není součástí standardní Javy. V ní se po víc jak deseti letech vývoje (JDK 1.6) <a href="http://java.sun.com/javase/6/docs/api/java/util/PropertyResourceBundle.html#PropertyResourceBundle(java.io.Reader)" target="_blank">objevil pouze nový konstruktor</a>, který umožní načíst obsah property souboru pomocí dodaného Readeru. Alespoň už nemusíme nutně používat Native2Ascii. Není to ale přeci jenom trochu málo?</p>
