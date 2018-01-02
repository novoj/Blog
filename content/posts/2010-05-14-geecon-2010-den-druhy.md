---
status: publish
published: true
title: GeeCON 2010 - Den druhý
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Po včerejší after párty se mi dneska skutečně nechtělo příliš vstávat. Niméně
  diskuse s Hansem Dockterem (autorem Gradle) skutečně stála za to. Hans je skutečně
  mimořádný člověk se skvělými názory - přidávám další bodík pro Gradle. Styl, jakým
  se Gradle vyvíjí a filozofie, která za ním stojí, se mi skutečně zamlouvá. U dikuse
  byl také Vašek Pech z JetBrains, který má na svém kontě také samostatný OS projekt
  GPars, takže se diskuse odvíjela i na téma zkušeností s vedením OS projektu, respektive
  firmy, která je živa z konzultací a školení spojených s daným OS projektem. Tyhle
  chvilky jsou zkrátka na konferencích asi to nejlepší - dostat se do kontaktu s výjimečnými
  lidmi a mít možnost s nimi mluvit tváří v tvář. Jsem opravdu rád, že tyhle \"výlety\"
  na konference jsou ve <a href=\"http://www.fg.cz\" target=\"_blank\">Forrestu</a>
  možné, protože to zdaleka není samozřejmost.\r\n\r\nV rámci druhého dne se odehrála
  celá řada velmi zajímavých přednášek, které bych rád trošku nastínil v dnešním příspěvku.\r\n\r\n"
wordpress_id: 904
wordpress_url: http://blog.novoj.net/?p=904
date: '2010-05-14 18:48:02 +0200'
date_gmt: '2010-05-14 17:48:02 +0200'
categories:
- Reportáže
- GeeCON
tags:
- geecon
- koference
comments: []
---
<p>Po včerejší after párty se mi dneska skutečně nechtělo příliš vstávat. Niméně diskuse s Hansem Dockterem (autorem Gradle) skutečně stála za to. Hans je skutečně mimořádný člověk se skvělými názory - přidávám další bodík pro Gradle. Styl, jakým se Gradle vyvíjí a filozofie, která za ním stojí, se mi skutečně zamlouvá. U dikuse byl také Vašek Pech z JetBrains, který má na svém kontě také samostatný OS projekt GPars, takže se diskuse odvíjela i na téma zkušeností s vedením OS projektu, respektive firmy, která je živa z konzultací a školení spojených s daným OS projektem. Tyhle chvilky jsou zkrátka na konferencích asi to nejlepší - dostat se do kontaktu s výjimečnými lidmi a mít možnost s nimi mluvit tváří v tvář. Jsem opravdu rád, že tyhle "výlety" na konference jsou ve <a href="http://www.fg.cz" target="_blank">Forrestu</a> možné, protože to zdaleka není samozřejmost.</p>
<p>V rámci druhého dne se odehrála celá řada velmi zajímavých přednášek, které bych rád trošku nastínil v dnešním příspěvku.</p>
<p><a id="more"></a><a id="more-904"></a></p>
<h2>Easing JPA DAO development with Hades / Oliver Gierke</h2>
<p>Tato přednáška byla pro mne asi tím nejzajímavějším z dnešního dne. Oliver Gierke rozebíral projekt Hades, který umožňuje automatické generování DAO interfaců. Přednáška byla tím zajímavější, že podobnou věc (vlastní implementaci postavenou nad JdbcTemplate) u nás už cirka 3/4 roku používáme.</p>
<p>Hades je nadstavba JPA využívající ke svému běhu Spring Framework. Myšlenka pochází ze světa dynamických jazyků (GORM například), kdy programátor pouze volá (v případě plain Javy deklaruje signatury metod) DAO metody, jejichž implementace nikde neexistuje, ale je systémem automaticky generována na základě nějakých pravidel.</p>
<p>Cílem je samozřejmě maximalizovat produktivitu - řada metod na DAO vrstvě je prostě velmi jednoduchá a jejich implementace je repetitivní. Programátor se takto může soustředit jen na ty složitější a repetitivní práci přenechat generátoru. V našem prostředí mohu po 9 měsících směle prohlásit, že tento přístup se už osvědčil a skutečně je zvýšení produktivity jasně cítit.</p>
<p>Na tohle téma bych chtěl letos mluvit na JOpenspace konferenci, a teď mám konečně pro účastníky konference i odkaz na OS projekt, na kterém si životaschopnost tohoto přístupu mohou okamžitě vyzkoušet.</p>
<h2>JDK 7 Update / Dalibor Topic</h2>
<p>V této přednášce Dalibor topic rozebíral <a href="http://openjdk.java.net/projects/jdk7/features/" target="_blank">novinky v JDK7</a>. Bohužel se člověk, který si udržuje jen základní přehled o dění v Java světě, v přednášce moc nového nedozvěděl. Bylo to jen taková průřezová rekapitulace toho, co se do JDK7 dostane. Ani datum vydání JDK nebylo zpřesněno - pouze, že má vyjít v letošním roce.</p>
<p>Zajímavé bylo shrnutí toho, co se musí udělat při každé změně specky Javy:</p>
<ul>
<li>aktualizovat vlastní specifikaci jazyka</li>
<li>implementovat potřebná rozšíření / úpravy v kompilátoru</li>
<li>upravit existující knihovny, tak aby využívaly této novinky</li>
<li>implementovat sadu testů, prověřující danou funkcionalitu</li>
<li>upravit specifikaci VM</li>
<li>aktualizovat VM a nástroje pro práci s class soubory</li>
<li>aktualizovat Reflection API</li>
<li>implementovat podporu v Serializaci</li>
<li>aktualizovat výstup do JavaDocu</li>
</ul>
<p>To jsou všechno věci, které si vývojář, který Javu pouze používá a nevyvíjí, moc neuvědomuje.</p>
<h2>Squeezing Java Performance: When you need a little more / Thomas Enebo</h2>
<p>Thomas Enebo je jedním z lidí pracujících na vývoji JRuby. Svoji přednášku uvedl prohlášením, že JRuby je v současné době 2x až 2,5x rychlejší jak originální distribuce psaná v Céčku - to je jistě věc pozoruhodná a stojí za zamyšlení ;-) .</p>
<p>Zajímavá pro mě byla informace o tom, jak HotSpot pracuje - jednak, že optimalizaci provádí iterativně - vždy provede jen jeden optimalizační krok v čase, následně sleduje, jestli daný krok vedl k navýšení výkonu či ne. Pokud ne, vrátí tuto optimalizaci zpět a pokusí se provést něco jiného, pokud optimalizace vedla k navýšení výkonu, HotSpot zkusí na zoptimalizovaném kódu provádět další optimalizace.</p>
<p>Další zajímavá věc je ta, že HotSpot vám nezoptimalizuje rozsáhlé metody. Čím více menších metod, tím lepší práci vám HotSpot provede. Základním optimalizačním mechanismem je tzv. inlining, kdy se konkrétní kód v externí metodě přímo vloží do metody druhé na místo, kde je použito volání. HotSpot má však zabudované omezení, které zamezí inlinování metod, které mají více jak 35 bytecode instrukcí. Taktéž se při inlinování zastaví na hloubce 9 vnořených volání.</p>
<p>Non-thread safe třídy HotSpot optimalizuje lépe - tj. nezamykejte, pokud to skutečně nepotřebujete. ConcurrentHashMap nemá jeden zámek na celou mapu, ale má několik menších zámků pro konkrétní oblasti. Immutabilita může úplně odstranit práci se zámky a tudíž zvýšit výkon. Autoboxing a varargs zpomalují, zkuste zvážit overloadované metody, pokud třeba danou metodu s varargy voláte často s jedním, dvěma parametry apod.</p>
<p>Základní pravidlo, které nám Thomas Enebo kladl na srdce, je pokud možno výkonnostní optimalizaci neprovádět. A pokud přeci musíme, tak ji provádět na základě smysluplných měření. Smysluplné měření by mělo probíhat na kompletní aplikaci (ne na nějakém prototypu - malé aplikace zoptimalizuje HotSpot jinak než velké), na cílovém HW (JVM na různých platformám může běžet řádově jinak), a mělo by se z měření odečítat úvodní sekvence, ve které se program "zahřívá" (tj. při které HotSpot optimalizuje kód za běhu). Taktéž by se měly pokud možno minimalizovat IO operace, pokud se netestují právě ony.</p>
<p>Ideálně neoptimalizujte dřív, než je aplikace hotová, protože:</p>
<ul>
<li>můžete pracně optimalizovat část, která nakonec bude fungovat jinak a nebo se i odstraní</li>
<li>optimalizací obvykle kód velmi znepřehledníte a díky tomu s ním bude obtížná práce a bude problém jej udržovat</li>
</ul>
<p>První věcí na, na kterou byste se měli zaměřit nejsou jednotlivosti v dané aplikaci, ale celková architektura a evidentní nedomyšlenosti (jako příklad uváděl společnost, která si je pozvala na optimalizaci JRuby kódu, protože prý běžel pomalu, aby se po chvíli zjistilo, že při zobrazení každé stránky parsují 250kB XML pro to, aby mohli zobrazit jméno a příjmení přihlášeného uživatele). Jako jednu z prvních věcí se také zkuste podívat na vlastní nastavení Javy - např. přechodem z Javy 1.5 na 1.6 u JRuby dosáhnete cirka 20% zrychlení. Také správné nastavení GC na různých HW konfiguracích může hrát značnou roli.</p>
<p>Přednáška byla zajímavá, i když vlastní přednes byl takový univerzitní - přistihl jsem pár kolegů, kteří si u této přednášky dávali po včerejším kulečníkovém turnaji šlofíka ;-) .</p>
<h2>Game Programming with Groovy / James Williams</h2>
<p>James Williams ukazoval použití Groovy pro programování jednoduchých 2D her. Na ukázkách dokazoval, že Java je pro tyto účely dostatečně rychlá. Na přednášce provedl rychlý vhled do knihoven JavaMonkeyEngine, Lightweight java Graphics Library (LWJGL), JOGL, JOAL, JInput, <a href="http://www.mapeditor.org" target="_blank">Tilemaps</a>, Slick a zmínil DarkStar Project.</p>
<p>Snažil se ukázat <a href="http://code.google.com/p/bluecove/" target="_blank">podporu bluetooth</a>, na demu s WiiMote ovladačem <a href="http://motej.sourceforge.net" target="_blank">pomocí knihovny Motej</a>, která by měla podporovat i další zařízení jako např. Nunchuk, Balance Board a klasické ovladače. Což se nakonec bohužel nepodařilo (generálský efekt, který určitě znají všichni, kdo někdy prezentovali).</p>
<p>Pro mě se jednalo o aajímavý náhled do světa her. Čekal jsem něco ve formě existujících DSL jazyků postavené nad Groovy, nicméně přednáška v tomhle byla poměrně skoupá.</p>
<h2>Static analysis using JSR308 annotations / Adam Warski</h2>
<p>Adam Warski ukazoval jak by se v praxi měla chovat validace pomocí JSR308 anotací. Bylo velmi zajímavé vidět anotace na typech, generikách, polích a dokonce i v přetypování:</p>
<p>[source lang="java"]<br />
@NoNull String s;<br />
Map&lt;String, @NotNull String&gt; map;<br />
class MyClass extends &lt;@NotNull String&gt; {}<br />
[/source]</p>
<p>a vlastní rozšíření validačních anotací díky specifikaci Bean validation:</p>
<p>[source lang="java"]<br />
Map&lt;@Email String&gt; emails;<br />
[/source]</p>
<p>Bohužel prozatím tuto podporu nemohl ukázat v IDE, takže celá přednáška probíhala přes spouštění JavaC z příkazové řádky s ruční konfigurací anotačních processorů. Pro většinu přítomných asi zatím těžko zkousnutelná věc, ale s podporou v IDE v tom vidím zajímavou možnost, jak vylepšit statickou analýzu správného použití cizího API.</p>
<h2>HTML5 Web Sockets: All-You-Can-Eat Real Time! / Peter Lubbers</h2>
<p>WebSockets jsou novinkou ve specifikaci HTML5 a měly by se stát plnohodnotnou náhradou současných ajaxových volání serveru. Zkraje přednášky Peter rozebral všechny základní v současnosti používané principy AJAXového volání a jejich nevýhody:</p>
<ul>
<li>Polling - časté dotazy na server, často s nulovým výsledkem (žádná změna na serveru není) - velmi drahé na režii volání</li>
<li>Long polling - odpověď serveru se neuzavře do doby než je k dispozici nějaká nová informace na serveru - neefektivní, pokud na serveru často vznikají nové zprávy / stavy</li>
<li>Comet - streaming, odpověď se nikdy neukončí - problematické pokud jsou na cestě nějaké staré proxy servery nebo firewally, které vyžadují ukončení odpovědi serveru</li>
</ul>
<p>WebSockety fungují na bázi standardního HTTP protokolu (tj. přes porty 80 a 443). Pokud klient i server tuto techniku podporují, dohodnou se na tzv. "upgradu" protokolu a začnou spolu komunikovat přes WebSocket. To je kanál, který se nikdy neuzavře a komunikace po něm probíhá oboustranně. Data, která se po něm přenášejí jsou textového charakteru (ale ten lze upravit i pro přenos binárního obsahu). Na klientovi dokážeme podporu WebSocketů identifikovat pomocí jednoduchého konstruktu:</p>
<p>[source lang="java"]<br />
if (window.WebSocket) {<br />
   ...<br />
}<br />
[/source]</p>
<p>A v současnosti jej podporuje Chrome 4, Safari (v night buildech), Opera a Firefox na něm pracují a měli by ho podporovat do konce tohoto roku a náš poslední utlačovaný IE jej bude podporovat až někdy ve verzi 10. WebSocket nebude trpět crossdomain problémem - tj. jak jsem pochopil, mělo by být možné z klienta vytvořit několik WebSocketů na servery na jiných doménách.</p>
<p>Vše se neobešlo bez řádné reklamy na <a href="http://www.kaazing.com" target="_blank">Kaazing WebSocket Server</a>, který by měl již implementovat práci s WebSockety s emulací této podpory i pro starší prohlížeče typu IE6. Pravda je, že tento komerční produkt je velmi vymakaný a při reálných ukázkách toho, co se dá přes WebSockety provádět nám trošku klesala čelist. Pro Apache by se měl vyvíjet <a href="http://code.google.com/p/pywebsocket/" target="_blank">pywebsocket</a>, který by měl tuto <a href="http://www.travisglines.com/web-coding/how-to-set-up-apache-to-serve-html5-websocket-applications-with-pywebsocket">podporu zajistit snad pro širší publikum</a>.</p>
<h2>JSR-299 Context and Dependency Injection / Mark Struberg</h2>
<p>V poslední přednášce nám Mark Struberg popisoval konkrétní implementační detaily JSR-299 na téma Context and Dependency Injection. V rychlosti řečeno, většina věcí člověka, který používá Spring v kombinaci s anotacemi neměla překvapit. Valnou část této specky podle mého názoru Spring integroval již ve verzi 2.5.X.</p>
<p>Pravda je, že když Mark ukázal kombinace jednotlivých anotací, s možností (nutností) vytvářet další anotace vlastní, začal kód vypadat poměrně hodně magicky. Celá specifikace mě na první pohled připadala velmi komplikovaná (jaký je český výraz pro "overengeneered"?) a v případě, že by některé z různých kombinací anotací přestaly funguvat asi by člověk dost těžko zjišťoval, kde konkrétní vendor implementující specku udělal chybu (respektive pokud je chyba u mě, ta v čem spočívá). Celkové propojení bean na základě anotací prostě vypadalo až příliš magicky.</p>
<p>Co mi ovšem přišlo jako zásadní problém je to, že CDI funguje na základě classpath scanningu. Tj. automaticky při startu aplikace vyhledá všechny JARy obsahující v META-INF soubor beans.xml a v těch se snaži najít libovolné třídy obsahující ty správné anotace. Pro prohledání classpat nahodí jeden velký kontext se všemi beanami podle pravidel definovaných jejich anotacemi. V tomto ohledu se obávám dvou věcí: a) nikdy nebudu vědět, jestli s nějakým přilinkovaným JARem se mi do kontextu nezamíchá něco co nechci b) (a to i v souvislosti s předchozím bodem) jestli mi někde nedojde nějakému name clashingu.</p>
<p>V době kdy je modularita jedním ze žhavých témat, mělo být toto (myslím si) rozhodně vzato v úvahu.</p>
<h2>Závěrem</h2>
<p>GeeCON je rozhodně konference, na kterou se vyplatí jet. Poměr cena / výkon je u této konference skutečně velmi příjemná. Organizačně to kluci zvládli na jedničku a vůbec se mi zdálo, že v Polsku je to pro nás Čechy takové velmi přívětivé a domácké. Na několika místech, kde nefungovala angličtina, jsme to dokonce zvládli s češtinou.</p>
<p>Jsem rád, že jsem tu mohl strávit nějaký čas a vracím se plný dojmů a nových inspirací. Takže díky pánové z Polského JUGu a díky <a href="http://www.fg.cz" target="_blank">Forreste</a>.</p>
