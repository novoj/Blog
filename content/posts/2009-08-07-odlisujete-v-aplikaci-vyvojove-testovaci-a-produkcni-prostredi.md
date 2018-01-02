---
status: publish
published: true
title: Odlišujete v aplikaci vývojové, testovací a produkční prostředí?
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Tento článek píšu se záměrem zjistit, zda jsme k těmto závěrům dospěli sami,
  nebo je to evoluční záležitost, ke které časem dospěje každý tvůrce produktů sloužících
  k dalšímu vývoji. Ve <a href=\"http://www.fg.cz\" target=\"_blank\">Forrestu</a>
  k realizaci webů a webových aplikací používáme <a href=\"http://www.fg.cz/cs/nabidka/system-pro-spravu-obsahu-webu-edee-cms.shtml\"
  target=\"_blank\">interní CMS systém</a>, který je nadstavbou nad vybranými Javovskými
  knihovnami a frameworky. Namátkou například Spring Framework, Freemarker, Groovy,
  Spring Security, Stripes, DWR, iBatis a řada dalších. Tím, že jsme CMS systém (ona
  už je to vlastně tak trochu programová platforma) postavili nad existujícími knihovnami
  jsme dosáhli toho, že můžeme využívat většiny jejich širokých možností a máme zdarma
  zajištěn i další vývoj, který nás v podstatě bezpracně posouvá zase dál.\r\n\r\nTím,
  že se systém sestává z takového množství dalších knihoven a frameworků, jsme začali
  narážet na problémy se složitostí konfigurace. Teď nemluvím o nastavení pro cílového
  zákazníka (zabezpečení url, nastavení rolí, definice aplikačních triggrů a maker,
  proměnné prostředí jako adresa SMTP serveru atd.), ale o vývojové záležitosti jako
  je konfigurace cache (Freemarker šablon, lokalizované zprávy, Groovy třídy), podrobnost
  chybového výstupu (pro vývoj plné stacktracy, na produkci nic neříkající HTTP 500),
  dostupnost debugovacích nástrojů (máme vlastní <a href=\"http://www.fg.cz/cs/prectete-si/clanky/30.shtml\"
  target=\"_bank\">inspektor jako Firefox plugin</a>) apod.\r\n\r\n"
wordpress_id: 577
wordpress_url: http://blog.novoj.net/?p=577
date: '2009-08-07 14:02:28 +0200'
date_gmt: '2009-08-07 13:02:28 +0200'
categories:
- Programování
- Java
tags: []
comments:
- id: 11360
  author: Josef Strzibny
  author_email: strzibny@strzibny.name
  author_url: http://letme.cz/
  date: '2009-08-08 15:59:16 +0200'
  date_gmt: '2009-08-08 14:59:16 +0200'
  content: Osobně to vnímám jako dnešní standard. Moderní frameworky to běžně oddělují.
- id: 11363
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-08-08 18:31:02 +0200'
  date_gmt: '2009-08-08 17:31:02 +0200'
  content: Můžeš být trošku konkrétnější?
- id: 11365
  author: filemon
  author_email: jiri.fabian@gmail.com
  author_url: ''
  date: '2009-08-08 21:12:05 +0200'
  date_gmt: '2009-08-08 20:12:05 +0200'
  content: Jo, ja bych rekl, ze to takhle pouzivaji skoro vsichni nasi zakaznici -
    korporatnici. DEV pro hratky a ukazky spot fixu, TST s omezenym pristupem pro
    nas coby developery pro akceptacni testy a PROD, produkce. Z tech frameworku,
    ktere to takto deli primo, uvedu napr. Rails. (a timpadem i nejspis Grails ;)
- id: 11375
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-08-09 06:53:58 +0200'
  date_gmt: '2009-08-09 05:53:58 +0200'
  content: Takže spíš evoluce než revoluce. Filemone díky za info, tohle jsem o Rails
    nevěděl.
- id: 11422
  author: uf
  author_email: ufak@seznam.cz
  author_url: ''
  date: '2009-08-11 07:01:16 +0200'
  date_gmt: '2009-08-11 06:01:16 +0200'
  content: "Vsechno genialni je pri zpetnem pohledu jednoduchy princip. Jen nekdo
    musi udelat vic kroku vyvoje a pak ten zasadni. \r\n\r\nUrcite si myslite (i se
    ctenari), ze jste to mohli zaridit drive, kdyz mate zkusenosti a vite, jak oddelit
    jednu funkcnost na jedno misto. Stejne jako po hledani chyby si clovek mysli,
    ze ji mohl predejit peclivejsi pripravou nebo hlubsim promyslenim. Stejne k nim
    dochazi. To je holt vyvoj."
- id: 11426
  author: Josef Strzibny
  author_email: strzibny@strzibny.name
  author_url: http://letme.cz/
  date: '2009-08-11 12:29:19 +0200'
  date_gmt: '2009-08-11 11:29:19 +0200'
  content: Já konkrétně měl v hlavě taky Railsy, ale tyto dobré metody přejímají dneska
    skoro všichni. Nevím jak v Javovských frameworcích, ale Grails podle mně ano.
- id: 11428
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-08-11 12:51:20 +0200'
  date_gmt: '2009-08-11 11:51:20 +0200'
  content: Naposledy jsem toto viděl zmíněné v nejnovější verzi iBatis frameworku.
    Ale obecně bych řekl, že jsem na to dosud v Javovských frameworcích moc nenarazil.
    Což bych mj. důvod, že jsme tuto strategii adoptovali teprve poměrně nedávno (cca
    1/2 roku zpět).
- id: 11431
  author: pepa
  author_email: jmarianek@atlas.cz
  author_url: http://marianek.frajerx.com
  date: '2009-08-11 15:04:49 +0200'
  date_gmt: '2009-08-11 14:04:49 +0200'
  content: Ano, pouzivame DEV-&gt;TST-&gt;PROD model. Konfiguraci udrzujeme v konf.
    property souborech, pro kazde prostredi zvlast. Zajimavy napad, vybudovat jeste
    neco nad tim...
- id: 11449
  author: jčp
  author_email: jcp@atlas.cz
  author_url: ''
  date: '2009-08-12 08:16:18 +0200'
  date_gmt: '2009-08-12 07:16:18 +0200'
  content: "Zatím jsme evolovali do jiného stavu:\r\nBěžný překlad probíhá do dev
    prostředí. \r\nant prod a ant test ve vygenerovaném waru přeplácnou specifické
    konfigurační soubory, šablony, lokalizaci...\r\nJiný slovy: konfigurace se mění
    s účelem buildu, nikoliv za běhu podle prostředí. \r\nZdrojové soubory zůstávají
    stejné. Možná máme jen příliš jednoduché aplikace. \r\n\r\nAle psát v javě konstrukce
    typu if (isDevelop()) {...} else {...}? Nevím, to se mi nezdá rozumné."
- id: 11450
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-08-12 08:43:47 +0200'
  date_gmt: '2009-08-12 07:43:47 +0200'
  content: "No spíš se jedná od dva druhy aplikací - my děláme produkt, který má jeden
    artefakt, který je výsledkem buildu. Tento artefakt se nasazuje na X instalací
    a tam se teprve customizuje pomocí konfiguračních souborů. Těch konfigurací už
    tak je poměrně hodně a proto se nám vyplatilo některá \"technická\" (nikoliv zákaznická)
    nastavení typizovat podle zmíněných třech běhových prostředí a vyjmout je ven
    (s možností přepisu). Moduly, které jsou součástí buildu si mohou potom pro tyto
    3 typizovaná prostředí použít své hardcodované defaults.\r\n\r\nTakže řekl bych,
    že spíš oba řešíme trošku něco jiného."
- id: 11544
  author: Tomáš
  author_email: atom@atomsoft.cz
  author_url: ''
  date: '2009-08-17 08:25:07 +0200'
  date_gmt: '2009-08-17 07:25:07 +0200'
  content: A neexistuje nějaká knihovna, která by výběr toho správného konfiguračního
    souboru řešila? Předpokládám, že to co parsuje ten XML soubor z   a podle toho
    rozhoduje o jaký server jde jste si psali sami?
- id: 11546
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-08-17 09:08:30 +0200'
  date_gmt: '2009-08-17 08:08:30 +0200'
  content: "Jo to parsování XML máme interní - používáme na to JDOM. Pro otestování
    těch řídících proměnných stačí analýza Java System properties, popřípadě hostname
    - což je jeden řádek:\r\n\r\nInetAddress.getLocalHost().getHostAddress()\r\n\r\nNicméně
    v tom ani není gró toho problému. To přizpůsobení chování aplikace / modulů už
    s XML nemá v podstatě nic společného. XML je jen prostředek jak to rozlišení prostředí
    definovat."
- id: 11548
  author: Tomáš
  author_email: atom@atomsoft.cz
  author_url: ''
  date: '2009-08-17 09:36:42 +0200'
  date_gmt: '2009-08-17 08:36:42 +0200'
  content: Ano, je mi to jasné. Jen stojím před podobným problémem, jen nemám vlastní
    CMS vlastní moduly, ale používám Wicket, Hibernate, logback a pár dalších knihoven
    a hledám nějaké už hotové řešení, které by pomohlo s konfigurací těchto knihoven
    dle prostředí.
- id: 11550
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-08-17 10:43:44 +0200'
  date_gmt: '2009-08-17 09:43:44 +0200'
  content: Aha, tak v tomto případě nepomůžu - my to máme prostě napsané na vlastní
    míru. Kdo ví, jestli někde něco takového existuje, podle charakteru problému bych
    si ale spíš tipnul že ne, protože je to skoro spíš úkol na nějaký integrační framework
    než nějakou utility knihovnu.
- id: 11752
  author: Tomáš
  author_email: atom@atomsoft.cz
  author_url: ''
  date: '2009-08-25 19:40:44 +0200'
  date_gmt: '2009-08-25 18:40:44 +0200'
  content: 'Jediné, co jsem našel je tohle: http://jfig.sourceforge.net/'
- id: 12674
  author: Almad
  author_email: loguser@almad.net
  author_url: ''
  date: '2009-09-21 23:07:29 +0200'
  date_gmt: '2009-09-21 22:07:29 +0200'
  content: "Tož my to nemáme takhle explicitně, prostě máme tři balíky s potřebnými
    konfiguračními soubory a k tomu jakýsi \"common\", který je společný všem třem.\r\n\r\nKonfiguraci
    ve stylu isDevel()/isDebug() z duše nenávídím, blbě se to testuje, způsobuje mrtvý
    kod a mnohdy se to na produkci chová jinak, než by člověk čekal.\r\n\r\nNicméně
    mně je java blízká asi tak jako XML pro konfiguraci, takže nevšímat :)"
- id: 14135
  author: Jarda
  author_email: Jarda.cerberos@seznam.cz
  author_url: http://zacatecnik.wu.cz
  date: '2009-11-03 08:07:18 +0100'
  date_gmt: '2009-11-03 07:07:18 +0100'
  content: "\"běží a používat konstanty ale proměnné.\"\r\nnemá tam být \"nepoužívat\"?"
- id: 14165
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-11-03 20:23:10 +0100'
  date_gmt: '2009-11-03 19:23:10 +0100'
  content: ad) Jarda, je to tak ... díky za upozornění, opraveno
- id: 18453
  author: Jety
  author_email: mail@jetensky.net
  author_url: http://jetensky.net/blog
  date: '2010-02-09 12:20:29 +0100'
  date_gmt: '2010-02-09 11:20:29 +0100'
  content: "Ahoj Honzo, díky za článek,\r\n\r\nmy ve firmě používáme nadstavbu nad
    Springem, s kterou přišel Petr Jůza. Myšlenka je taková, že pro různá prostředí
    nahrajeme různou sadu XML Spring konfiguráků.\r\n\r\nKontejner (třeba tomcat)
    se spustí s -DENV=DEVELOP nebo testy s -DENV=UNITTEST, bez parametru se to bere
    jako production. Podle toho se řídí naše extense Spring ApplicationContextu a
    naimportuje /CONF/common/*.xml a /CONF//*.xml. V /CONF/common/*.xml tedy máme
    ty Spring XML konfiguráky, které jsou společné pro všechna prostředí.\r\n\r\nV
    CONF/DEVELOP/applicationContext.xml tak třeba nemáme nakonfigurovanou autentizaci
    přes XML security a nemusíme se tak pořád na webu přihlašovat, stejně tak třeba
    v PRODUCTION máme jndiDataSource beanu ale v DEVU máme SimpleDataSource.\r\n\r\nDalší
    výhoda je, že pokud se nějaká nastavení sdílejí mezi DEVELOP a UNITTEST, lze je
    jednoduše naimportovat (v /CONF/UNITTEST/applicationContext.xml může být toto:\r\n\r\n<!--
    Tyto hodnoty se nelisi od DEVELOP profilu -->\r\n"
- id: 30551
  author: Myšlenky dne otce Fura &raquo; Blog Archive &raquo; Fail-fast nebo Fail-tolerant?
  author_email: ''
  author_url: http://blog.novoj.net/2010/12/21/fail-fast-nebo-fail-tolerant/
  date: '2010-12-21 19:30:00 +0100'
  date_gmt: '2010-12-21 18:30:00 +0100'
  content: "[...] jsem již psal v článku o rozlišování běhových prostředí, sami bychom
    měli chtít od SW odlišné chování v závislosti s jakým cílem aktuálně [...]"
- id: 90035
  author: "&raquo; Nástroje pro vývoj web aplikací ve Forrestu Myšlenky dne otce Fura"
  author_email: ''
  author_url: http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/
  date: '2012-09-04 10:00:38 +0200'
  date_gmt: '2012-09-04 09:00:38 +0200'
  content: "[...] aplikace napsaná ve stejné technologii, které umožňuje introspekci
    a je dostupná pouze ve vývojovém a testovacím prostředí. V těchto režimech jsou
    ke každé web stránce, která je renderovaná připsány dodatečné [...]"
- id: 103813
  author: "&raquo; Máte jistotu, že do session ukládáte pouze serializovatelné objekty?
    Myšlenky dne otce Fura"
  author_email: ''
  author_url: http://blog.novoj.net/2012/11/04/mate-jistotu-ze-do-session-ukladate-pouze-serializovatelne-objekty/
  date: '2012-11-04 21:15:55 +0100'
  date_gmt: '2012-11-04 20:15:55 +0100'
  content: "[...] případě, že aplikace běží ve vývojovém režimu, prochází zpracování
    requestu servletovým filtrem, který po ukončení zpracování requestu [...]"
- id: 158548
  author: "&raquo; Click through errors to IntelliJ Idea editor with Remote Call plugin
    Myšlenky dne otce Fura"
  author_email: ''
  author_url: http://blog.novoj.net/2017/02/10/click-through-errors-to-intellij-idea-editor-with-remote-call-plugin/
  date: '2017-02-10 20:16:21 +0100'
  date_gmt: '2017-02-10 19:16:21 +0100'
  content: "[&#8230;] Whenever there is error in FreeMarker template it&#8217;s get
    visualized like this (of course this version is used only in dev &amp; test environment):
    [&#8230;]"
---
<p>Tento článek píšu se záměrem zjistit, zda jsme k těmto závěrům dospěli sami, nebo je to evoluční záležitost, ke které časem dospěje každý tvůrce produktů sloužících k dalšímu vývoji. Ve <a href="http://www.fg.cz" target="_blank">Forrestu</a> k realizaci webů a webových aplikací používáme <a href="http://www.fg.cz/cs/nabidka/system-pro-spravu-obsahu-webu-edee-cms.shtml" target="_blank">interní CMS systém</a>, který je nadstavbou nad vybranými Javovskými knihovnami a frameworky. Namátkou například Spring Framework, Freemarker, Groovy, Spring Security, Stripes, DWR, iBatis a řada dalších. Tím, že jsme CMS systém (ona už je to vlastně tak trochu programová platforma) postavili nad existujícími knihovnami jsme dosáhli toho, že můžeme využívat většiny jejich širokých možností a máme zdarma zajištěn i další vývoj, který nás v podstatě bezpracně posouvá zase dál.</p>
<p>Tím, že se systém sestává z takového množství dalších knihoven a frameworků, jsme začali narážet na problémy se složitostí konfigurace. Teď nemluvím o nastavení pro cílového zákazníka (zabezpečení url, nastavení rolí, definice aplikačních triggrů a maker, proměnné prostředí jako adresa SMTP serveru atd.), ale o vývojové záležitosti jako je konfigurace cache (Freemarker šablon, lokalizované zprávy, Groovy třídy), podrobnost chybového výstupu (pro vývoj plné stacktracy, na produkci nic neříkající HTTP 500), dostupnost debugovacích nástrojů (máme vlastní <a href="http://www.fg.cz/cs/prectete-si/clanky/30.shtml" target="_bank">inspektor jako Firefox plugin</a>) apod.</p>
<p><a id="more"></a><a id="more-577"></a></p>
<p>Řada z použitých knihoven a scénářů, které jsme používali, měla sadu možností pro úpravu svého chování, které bylo velmi užitečné využít. V celkovém součtu se jednalo o tucet (a stále přibývají ;-) ) nastavení, které bylo nutné nastavit a u jejichž nastavování musel člověk přemýšlet. Také bylo nutné tato nastavení rozlišovat podle režimu v jakém aplikace běží a nepoužívat konstanty ale proměnné.</p>
<p>Vcelku brzy jsme přišli na to, že, přestože je možné všechny nastavení relativně jednoduše editovat, většinou se nastavilo pouze něco a velice často konstantně tak, že se nám na produkci dostávaly i nastavení, které tam neměly co dělat (třeba nulová cache FTL šablon omylem ponechaná z vývoje).</p>
<p>U nás rozeznáváme tři režimy běhu (a myslím, že se jedná o vcelku běžný standard):</p>
<ul>
<li><strong>development (vývoj)</strong> - v tomto prostředí potřebujeme co největší možnosti manipulace se systémem, rychlou odezvu vůči změnám, maximální přístup k debugovacím a chybovým informacím</li>
<li><strong>staging (test)</strong> - v tomto prostředí již aplikaci vidí zákazník, je tedy vhodné standardní programátorské záležitosti skrýt a neděsit ho plnou obrazovkou stacktraců - na druhou stranu potřebujeme stále výrazně upozornit pokud se někde vyskytne chyba, aby bylo možné ji odstranit před přechodem do produkce, chceme si zachovat nějakou rozumnou míru odezvy na změny v systému a přístup k debugovacím nástrojům</li>
<li><strong>production (ostrý běh)</strong> - tady chceme maximální výkon, změny v systému za běhu budou minimální (stále si chceme nechat otevřená dvířka, ale upřednostňujeme explicitní refresh konfigurace), minimalizujeme debugovací možnosti (ty mají dopad na výkon), optimalizujeme případný chybový výstup ke koncovému uživateli (stacktracy opravdu nejsou nejlepší vizitka, že Filemone?)</li>
</ul>
<p>Po nějaké době jsme se dohodli, že toto nepsané rozdělení instalací zformalizujeme a umožníme je definovat na jednom místě v konfiguraci CMS a přizpůsobíme všechny moduly, aby svá běhová nastavení odvodila od aktuálního běhového prostředí. Konfigurace je velmi jednoduchá - např.:</p>
<p>[source lang="xml"]<br />
<environment><br />
  <test hostname="nasserver.fg.cz"/><br />
  <development hostname="novoj.fg.cz"/><br />
  <development os="windows"/><br />
</environment><br />
[/source]</p>
<p>Tímto jednotně říkáme, že všechna prostředí s operačním systémem Windows a stroj se jménem "novoj.fg.cz" mají být považována za vývojová, stroj "nasserver.fg.cz" má být považován za testovací prostředí. Všechny ostatní prostředí, které neodpovídají těmto pravidlům jsou považovány za produkční.</p>
<p>Všechny moduly i standardní web aplikace si potom může ze systému vytáhnout identifikaci aktuálního běhového prostředí (voláním metody isProduction(), isStaging(), isDevelopment() na jádrové třídě) a načíst defaultní nastavení pro tento režim běhu. Pokud by kdokoliv jevil zájem tyto výchozí nastavení přepsat, může - nicméně jak praxe ukázala, nikdo to nedělá, protože toto rozlišení defaultních nastavení pro naše potřeby plně postačuje. Integrační vrstva nad knihovnami jako je Freemarker, Groovy atd. také obsahuje trojí sadu defaultních nastavení optimalizovaných pro jednotlivé režimy běhu.</p>
<p>Takto jednoduše jsme se zbavili poměrně velké bolesti, kterou jsme nějakou dobu trpěli. Jedním nastavením vcelku rozumně nyní ovládáme chování celého systému - navíc je to něco, s čím dokáže pracovat kdokoliv i bez hlubší znalosti modulů a knihoven v dané instalaci použitých.</p>
<p>Myšlenka, ke které jsme dospěli, mi s odstupem času nepřijde ani moc geniální jako spíš evoluční. Pozitivní dopady jsou ovšem pro výslednou použitelnost citelně znatelné.</p>
<p>Skončím otázkou nakonec - pokud používáte pro svou práci nějakou infrastrukturní nadstavbu, dospěli jste k podobnému závěru? Jaká je Vaše motivace, řešení a zkušenosti?</p>
