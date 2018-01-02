---
status: publish
published: true
title: Jednoduché logování ve Springu
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Tušil jsem, že to je jednoduché, ale že to je AŽ tak jednoduché, to jsem
  nevěděl. Dokončujeme projekt pro jednu velkou českou banku a potřebovali jsme mít
  podrobným logováním pokrytou co největší část aplikace pro případ, že by se vyskytly
  problémy na prostředí, do kterého, z bezpečnostních důvodů, nemáme a nikdy nebudeme
  mít přístup.\r\n\r\nJako principiální odpůrce manuální práce jsem ihned zavrhnul
  myšlenku na manuální procházení kódu a rutinní vkládání debug logování pro strýčka
  příhodu (krom složitějších metod, kde je to nezbytně nutné). \r\n\r\nDalší má myšlenka
  samozřejmě směřovala k AOP. Už jsem si napsal kostru vlastní advice a chystal se
  psát aspekt, když ...\r\n\r\n"
wordpress_id: 471
wordpress_url: http://blog.novoj.net/?p=471
date: '2009-05-06 06:49:47 +0200'
date_gmt: '2009-05-06 05:49:47 +0200'
categories:
- Programování
- Spring Framework
tags: []
comments:
- id: 8369
  author: Tomáš Homola
  author_email: tomas.homola@uhk.cz
  author_url: ''
  date: '2009-05-07 10:30:14 +0200'
  date_gmt: '2009-05-07 09:30:14 +0200'
  content: To si musím někam uložit velmi zajímavá informace :) A o třídě org.springframework.aop.framework.autoproxy.BeanNameAutoProxyCreator
    jsem taky nevěděl, ale vypadá to velmi užiečně když chcu všechny bean obalit stejném
    Interceptor.
- id: 8372
  author: Tomáš Piňos
  author_email: tomas.pinos@aspectworks.com
  author_url: ''
  date: '2009-05-07 12:26:25 +0200'
  date_gmt: '2009-05-07 11:26:25 +0200'
  content: "Zajímavé. Dosud jsme pro stejný účel používali námi napsaný aspect. \r\nZajímalo
    by mě, jestli v produkčním prostředí logujete opravu všechny public metody *Manager
    a *Storage tříd, nebo jestli rozlišujete nějakou sadu metod / argumentů, které
    logovat nechcete (např. citlivá data jako hesla nebo rodná čísla klientů). A pokud
    ano, jak se toho docílí (na úrovni definice dynamické proxy nebo nějak jinak?)."
- id: 8373
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-05-07 12:35:31 +0200'
  date_gmt: '2009-05-07 11:35:31 +0200'
  content: "Vycházeli jsme z této úvahy - na produkčním prostředí je logování typicky
    nastavené na level WARN nebo ERROR. Tato advice loguje volání metod na úrovni
    TRACE. Tzn. na produkčním prostředí se do logu typicky nic nedostane.\r\n\r\nV
    případě, že narazíme na chybu, kterou nedokážeme odhalit podle chybového stacktrace,
    požádáme administrátory zákazníka, aby nám upravili odpovídajícím způsobem log4j
    konfiguraci (respektive jim pošleme celý konfigurační soubor) a na patřičných
    místech si zvýšíme loglevel na hodnotu TRACE.\r\n\r\nV tu dobu je tedy možné že
    by se mohly zalogovat i citlivá data. Nicméně počítáme s tím, že po odstranění
    chyby se vrátí zpět původní nastavení hladin logu a vyrobené logy s TRACE levelem
    se odstraní.\r\n\r\nNavíc máme tedy ještě tu výhodu, že nás systém nepracuje s
    výrazně citlivými daty, takže je tato politika akceptovatelná. Nicméně ano - v
    případě požadavku na zabezpečení citlivých dat je určitě legitimní mít vlastní
    custom advice.\r\n\r\nO tomto řešení jsem psal hlavně z toho důvodu, že většinou
    tak super zabezpečení není třeba a pro tyto účely máme již připravené řešení ve
    Springu out of the box."
- id: 8375
  author: Lubor Gajda
  author_email: lubor.gajda@gmail.com
  author_url: ''
  date: '2009-05-07 12:53:44 +0200'
  date_gmt: '2009-05-07 11:53:44 +0200'
  content: Malou nevyhodou tohto riesenia je ze "proxy based AOP" nieje mozne aplikovat
    na vnutorne volania metod vramci danej spring beany, ale iba v pripade ak je metoda
    volana zvonka inou beanou (teda ak volanie prechadza cez AOP proxy). Takze prakticka
    pouzitelnost je do znacnej miery zavisla na strukture vasho kodu (v akej miere
    pouziva vnutorne volania metod).
- id: 8376
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-05-07 13:18:12 +0200'
  date_gmt: '2009-05-07 12:18:12 +0200'
  content: Ad Lubor) ano, to je obecně známá vlastnost "proxy based AOP" - nicméně
    myslím, že už na základě mezivrstvového volání metod mezi objekty se dá lecos
    o problematické situaci odvodit
- id: 8380
  author: Michal Franc
  author_email: michal.franc@gmail.com
  author_url: ''
  date: '2009-05-07 15:01:58 +0200'
  date_gmt: '2009-05-07 14:01:58 +0200'
  content: Myslim ze na produkci by melo by standardne vse na info, nejen chyby te
    zajimaji, ale i co se delo pred, protoze ne vzdy je monze pouzit postup co jsi
    popsal, tj. po chybe zmenime logovani a pak zjistime vic.
- id: 16896
  author: niko
  author_email: niko@srnet.cz
  author_url: ''
  date: '2010-01-22 18:00:51 +0100'
  date_gmt: '2010-01-22 17:00:51 +0100'
  content: Začínám si s tím hrát a narazil jsem na problém s CGLIB proxy "Could not
    generate CGLIB subclass of class". Po pravdě jsem nepřišel na přesný důvod, ale
    vzhledem k tomu, že mám všechno striktně řešené přes interfaces, zdálo se mi nakonec
    i jako vhodnější použít JDK dynamic proxy a funguje to bez problémů. Zde to znamená
    změnit v ukázkovém konfiguračním souboru proxyTargetClass na false. Tak to jen
    kdyby měl třeba někdo podobný problém.
- id: 16948
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-01-25 06:17:08 +0100'
  date_gmt: '2010-01-25 05:17:08 +0100'
  content: "Zajimavý článek o Cglib2AopProxy: http://insufficientinformation.blogspot.com/2007/12/spring-dynamic-proxies-vs-cglib-proxies.html\r\n\r\nTahle
    vyjímka nastává, pokud se člověk snaží vybudovat proxy nad finální třídou, nebo
    třídou bez bezparametrického konstruktoru. Možná také maskuje vyjímky, které se
    vyhodí při volání konstruktoru třídy.\r\n\r\nKaždopádně já Cglib proxy používám
    poměrně rutinně a taky fungují bez problémů."
- id: 16957
  author: niko
  author_email: niko@srnet.cz
  author_url: ''
  date: '2010-01-25 16:25:59 +0100'
  date_gmt: '2010-01-25 15:25:59 +0100'
  content: "Jo tenhle článek jsem četl a nic podezřelého jsem nenašel (final třída
    apod.). Po kratším zamyšlení ale myslím, že problém je v tom, že už samotné beany
    vyzvedávané z kontejneru (bez AOP logování) jsou instance proxy tříd, protože
    jejich metody jsou anotované jako @Transactional a vzniká tak potřeba proxy přístupu.
    Pokud jsem správně pochopil dokumentaci, Spring upřednostňuje JDK dynamic proxy
    pokud je to možné (zde je to díky použití interfaces možné), výsledná proxy třída
    je pak final a CGLIB proxy pro potřeby logování k ní už vytvořit nejde. Pravděpodobně
    by se dalo nakonfigurovat vytváření CGLIB proxy i pro transaction management a
    pak by to fungovalo s CGLIB pro logování a s JDK dynamic proxy už zase ne... \r\nKaždopádně
    JDK dynamic proxy je mi tak nějak bližší, protože podobným způsobem (přes interface)
    bych to dělal, kdybych měl podobné logování dodělat \"ručně\" - rozhodně bych
    nepoužil dědění. Samozřejmě předpokladem je, že ty potřebné interfaces existují."
- id: 16963
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-01-25 21:06:57 +0100'
  date_gmt: '2010-01-25 20:06:57 +0100'
  content: Ano, myslím, že tohle bude to správné vysvětlení. Osobně se Cglib proxy
    nestraním - v případě, že nemá interface opodstatnění (vždy bude jen jediná implementace),
    bych jej kvůli potřebě použití JDK proxy nezakládal.
---
<p>Tušil jsem, že to je jednoduché, ale že to je AŽ tak jednoduché, to jsem nevěděl. Dokončujeme projekt pro jednu velkou českou banku a potřebovali jsme mít podrobným logováním pokrytou co největší část aplikace pro případ, že by se vyskytly problémy na prostředí, do kterého, z bezpečnostních důvodů, nemáme a nikdy nebudeme mít přístup.</p>
<p>Jako principiální odpůrce manuální práce jsem ihned zavrhnul myšlenku na manuální procházení kódu a rutinní vkládání debug logování pro strýčka příhodu (krom složitějších metod, kde je to nezbytně nutné). </p>
<p>Další má myšlenka samozřejmě směřovala k AOP. Už jsem si napsal kostru vlastní advice a chystal se psát aspekt, když ...</p>
<p><a id="more"></a><a id="more-471"></a></p>
<p>... jsem objevil, že vše je již skvěle připraveno v core balíku Spring Frameworku. Pro ty, kdo tedy o tomto pokladu ještě nevíte připojuji ukázku konfigurace. Vše bylo hotovo za 5 minut:</p>
<p>[source lang="xml"]<br />
<bean class="org.springframework.aop.framework.autoproxy.BeanNameAutoProxyCreator"></p>
<property name="proxyTargetClass" value="true"/>
<property name="beanNames" value="*Manager,*Storage"/>
<property name="interceptorNames" value="loggingAdvice"/>
</bean></p>
<p><bean id="loggingAdvice" class="org.springframework.aop.interceptor.CustomizableTraceInterceptor"></p>
<property name="useDynamicLogger" value="true"/>
<property name="hideProxyClassNames" value="true"/>
<property name="enterMessage" value="Entering method '$[methodName]' of class [$[targetClassShortName]], args: $[arguments]"/>
<property name="exitMessage" value="Exiting method '$[methodName]' of class [$[targetClassShortName]], returned: $[returnValue], execution time: $[invocationTime]"/>
<property name="exceptionMessage" value="Exception $[exception] thrown in method '$[methodName]' of class [$[targetClassShortName]]"/>
</bean><br />
[/source]</p>
<p>Výše uvedený snippet zajistí to, že všechny beany, které jsou ve stejném aplikačním kontextu jako tato deklarace a jejichž názvy končí řetězci "Manager" a nebo "Storage" budou automaticky owrapovány dynamickou proxy, která bude aplikovat CustomizableTraceInterceptor. Tento interceptor zajistí, že:</p>
<ul>
<li>bude zalogováno volání jakékoliv public metody beany včetně vstupních argumentů</li>
<li>bude zalogována výstupní hodnota včetně času, které vykonání metody trvalo</li>
<li>v případě ukončení volání vyjímkou, bude tato vyjímka také zalogována</li>
<li>logování bude na TRACE levelu a pokud je nastaveno logování pouze na vyšší úrovni, nebude volání metod v podstatě nijak výrazně zpomaleno</li>
<li>zalogované záznamy budou aplikovat původní název třídy jako název použitého loggeru (tzn. ignorují se názvy proxy class i interceptoru)</li>
</ul>
<p>Zajímavých interceptorů připravených rovnou k  použití poskytuje Spring více:</p>
<ul>
<li><b>ConcurrencyThrottleInterceptor</b> - omezuje paralelní volání metod dané instance</li>
<li><b>PerformanceMonitorInterceptor</b> - umožňuje jednoduché logování výkonnostních otisků (tzn. jak dlouho trval běh konkrétního volání metody instance)</li>
<li><b>DebugInterceptor</b> - jednoduché (fixní) logování metod dané instance</li>
<li><b>CustomizableTraceInterceptor</b> - umožňuje customizovatelné transparentní logování volání metod dané instance</li>
</ul>
<p>Nuže pokud, jste pouze tušili a nebyli si jistí, že je to se Springem jednoduché - teď už víte ...</p>
