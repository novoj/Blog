---
status: publish
published: true
title: Groovy namísto shell skriptů
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img src=\"http://blog.novoj.net/binary/2011/05/groovy-logo-big-300x148.png\"
  alt=\"\" title=\"Groovy\" width=\"150\" height=\"74\" class=\"alignleft size-medium
  wp-image-1476\" /> Pár shell skritpů jsem už napsal - jak pro Windows tak pro Linux,
  ale v tomto směru se považuji za naprostou lamu a to se ještě nějakou dobu nezmění.
  Proto jsem fascinovaně naslouchal <a href=\"http://twitter.com/#!/mittie\" target=\"_blank\">Dierk
  Königovi</a>, který na přednášce pražského CZJUGu zmiňoval <a href=\"http://www.java.cz/dwn/1003/43677_Groovy_Usage_Patterns.pdf\"
  target=\"_blank\">použití Groovy pro psaní shell skriptů</a>. Vyměnit jazyk proprietárního
  shellu, ve kterém toho moc neumím, za multiplatformní Groovy, kde jsem na výrazně
  pevnější půdě, se zdá jako perfektní nápad. Vše šlo tak hladce, že neváhám podobnou
  věc doporučit všem, co denně kódují na JVM.\r\n\r\n"
wordpress_id: 1407
wordpress_url: http://blog.novoj.net/?p=1407
date: '2011-06-15 00:00:39 +0200'
date_gmt: '2011-06-14 23:00:39 +0200'
categories:
- Programování
- Java
- Groovy
tags:
- GroovyServ
comments:
- id: 43572
  author: Pavel
  author_email: pavsyk@seznam.cz
  author_url: ''
  date: '2011-06-16 10:57:00 +0200'
  date_gmt: '2011-06-16 09:57:00 +0200'
  content: "Dík za článek. Ten GroovyServ vypadá zajímavě.\r\n\r\nJá používám již
    nějakou dobu obdobným způsobem skripty v jazyce Scala, což běží taktéž pod JVM.
    Má to výhodu, že celá \"instalace\" Scaly jsou oproti Javě jen 2 JARy. Obvykle
    mám jen kostru v shellu, ze které se volají jednotlivé skripty ve Scale.  Narazil
    jsem ale na zajímavý problém, který se asi netýká jen Scaly. JVM běží ještě nějakou
    dobu po skončení skriptu a drží si soubor, do kterého skript zapisuje logy. Takže
    další skript v pořadí logovací soubor nemůže otevřít. Dosud jsem nepřišel na nic
    jiného než okliku - pro každé nové volání skriptu vytvořit nový logovací soubor
    s náhodným jménem."
- id: 43579
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-06-16 13:08:29 +0200'
  date_gmt: '2011-06-16 12:08:29 +0200'
  content: Hmm v tomhle řešení to JVM na pozadí běží pořád - tj. zrovna s tímto by
    problém být neměl. Navíc je to fakt rychlé ... jak dlouho ty čekáš na start JVM
    s tou Scalou?
- id: 43590
  author: Pavel
  author_email: pavsyk@seznam.cz
  author_url: ''
  date: '2011-06-16 15:56:17 +0200'
  date_gmt: '2011-06-16 14:56:17 +0200'
  content: "No, jenže u mne si další skript spustí svou novou JVM a na starou kašle.
    \r\n\r\nAni nevím, jak dlouho trvá spuštění, ale pro mne to zatím nebylo nic zaásadního.
    Své skripty pouštím ručně jen zřídka (většinou jsou naplánované přes noc) a protože
    jsou to různé operace s poměrně dlouhými XML soubory, tak ty skripty běží řádově
    minuty. V tom případě mne moc nezajímá, zda to startuje vteřinu nebo pět. Krátké
    věci, které by se měly pouštět třeba s vyšší frekvencí, jsem v tom ještě nepsal."
- id: 43713
  author: v6ak
  author_email: reknu@nic.cz
  author_url: http://twitter.com/v6ak
  date: '2011-06-18 10:14:14 +0200'
  date_gmt: '2011-06-18 09:14:14 +0200'
  content: "Taky jsem zkoušel Scalu na takovéto lightweight skripty. Jazyk vypadá
    celkem \"light\". Jenže:\r\n* Doba startu je kvůli kompilaci nepříjemná (vypadá
    to tak na min. jednu sekundu, i když studený start je delší). Kéž by se tu cacheoval
    bytecode... To se teda dá řešit pmocí fsc a nějakého jednoduchého bash skriptu,
    ale už to prostě není ono. Ale, ono by se asi na to dalo něco vymyslet... Možná
    časem něco vyplodím.\r\n* Některé věci by to asi chtělo zjednodušit. Jazyk jako
    takový je sice light, ale pokud jsem chtěl knihovnu pro práci s MySQL, potřeboval
    jsem upravovat classpath a moc \"light\" to nevypadalo.\r\n\r\nNa druhou stranu,
    pro jednoduché dávkové operace (třeba převod cca 4 GiB dat z H2 do MySQL) je to
    pěkné, účinné a hlavně rychlé."
- id: 43715
  author: v6ak
  author_email: reknu@nic.cz
  author_url: http://twitter.com/v6ak
  date: '2011-06-18 10:37:29 +0200'
  date_gmt: '2011-06-18 09:37:29 +0200'
  content: |-
    Ještě dvě poznámky:
    * Scala IMHO toho daemona používá jen pro kompilaci, ale pro běh založí vlastní JVMku.
    * Koukám, že integrace shellu vypadá pěkně: http://dcsobral.blogspot.com/2011/03/on-scala-29s-road.html
- id: 43866
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-06-20 11:46:55 +0200'
  date_gmt: '2011-06-20 10:46:55 +0200'
  content: 'To v6ak & Pavel: Díky za reakce ... já jsem ještě ke Scale nedospěl -
    zatím jen teoreticky sbírám informace okolo. Tak snad jednou budu schopen v této
    věci trochu sekundovat, dnes ale ne :('
- id: 44011
  author: msk
  author_email: msk.conf@gmail.com
  author_url: ''
  date: '2011-06-22 11:05:28 +0200'
  date_gmt: '2011-06-22 10:05:28 +0200'
  content: "Ja som dostal za ulohu napisat script na \"mavenizaciu\" haldy proprietarnych
    jarov, rozhadzanych v projekte na milion miestach. Zacal som najprv cygwinom (
    bohuzial v praci musim pracovat na videohernom operacnom pasysteme ), kvoli zlozitosti
    a nachylnosti k chybam ( backslashe, medzery v nazvoch suborov, podivnosti ako
    \"disky\" C,D,E,F,G atd ) som to prepisal do Javy ( a .bat scriptom som z toho
    spravil \"spustitelny\" kod, mvn assemble a mvn exec ) a nakoniec som to zahodil
    a napisal to na par riadkov v groovy. Az nasledne som si uvedomil, ze som vlastne
    napisal script v jave ( hehe, vlastne JavaScript :-] ), ktory nie len ze bol takmer
    hned hotovy, mohol som si dovolit relativne zlozite veci, ktore v bashi tak lahko
    nespravim, ale zaroven je lahko udrzovatelny, pretoze to nie je splet tradicneho
    javovskeho chaosu vo forme haldy packagi a jarov, ale proste jeden jediny textovy
    subor.\r\n\r\nTakze za mna jednoznacne success story, predstava, ze to pisem v
    nejakom BAT interpreteri ma desi."
- id: 58270
  author: "&raquo; Pátý rok Myšlenek Otce Fura Myšlenky dne otce Fura"
  author_email: ''
  author_url: http://blog.novoj.net/2012/01/01/paty-rok-myslenek-otce-fura/
  date: '2012-01-01 14:43:34 +0100'
  date_gmt: '2012-01-01 13:43:34 +0100'
  content: "[...] Groovy namísto shell skriptů [...]"
---
<p><img src="http://blog.novoj.net/binary/2011/05/groovy-logo-big-300x148.png" alt="" title="Groovy" width="150" height="74" class="alignleft size-medium wp-image-1476" /> Pár shell skritpů jsem už napsal - jak pro Windows tak pro Linux, ale v tomto směru se považuji za naprostou lamu a to se ještě nějakou dobu nezmění. Proto jsem fascinovaně naslouchal <a href="http://twitter.com/#!/mittie" target="_blank">Dierk Königovi</a>, který na přednášce pražského CZJUGu zmiňoval <a href="http://www.java.cz/dwn/1003/43677_Groovy_Usage_Patterns.pdf" target="_blank">použití Groovy pro psaní shell skriptů</a>. Vyměnit jazyk proprietárního shellu, ve kterém toho moc neumím, za multiplatformní Groovy, kde jsem na výrazně pevnější půdě, se zdá jako perfektní nápad. Vše šlo tak hladce, že neváhám podobnou věc doporučit všem, co denně kódují na JVM.</p>
<p><a id="more"></a><a id="more-1407"></a></p>
<p>Groovy jsme už na několika projektech použili, ale nějak mi nedocvaklo, že je možné napsat libovolný Groovy skript, pustit jej z příkazové řádky a použít jej pro skriptování na vlastním systému. Jakmile nainstalujete <a href="http://groovy.codehaus.org" target="_blank">Groovy</a> na svůj disk a zařadíte jej do PATH proměnné, můžete odkudkoliv zavolat:</p>
<pre>
groovy cesta/ke/groovy/třídě.groovy
</pre>
<p>Groovy zařídí interpretaci skriptu a vy dostáváte k dispozici jazyk s rozsáhlými možnostmi, které znáte daleko lépe než shell. V základu tedy oproti Javě jako takové dostáváte jednu zásadní výhodu - skripty není nutné kompilovat. Stačí udělat změnu ve zdrojovém kódu a změněný soubor je možné ihned spustit. Ve svých Groovy skriptech můžete ovšem linkovat další externí knihovny a celkově disponujete mnohem větším arzenálem, než s kterým byste mohli počítat v shellu.</p>
<p>Na Linuxu (a MacOS?!) je možné dokonce z vlastního Groovy skriptu vytvořit přímo spustitelný soubor. Stačí na začátek Groovy skriptu přidat cestu k interpreteru zbytku souboru. V mém případě tedy stačí do Groovy skriptu přidat cestu k souboru, který spouští / interpretuje Groovy. Ukázka jednoduchého skriptu, který se po nastavení oprávnění (chmod 0744), stane samostatně spustitelným souborem:</p>
<pre>
#!/opt/Groovy/bin/groovy
println "Hello world!"
</pre>
<p>Brzy však narazíte na jednu nevýhodu, se kterou se těžko žije a tou je čas pro spuštění vlastní JVM a Groovy interpreteru. Standardně se horko těžko dostanete pod sekundu. Dierk König však v rámci přednášky ukazoval skripty, které se vykonávaly ve zlomku vteřiny. To bylo možné jen díky ...</p>
<h2>GroovyServ</h2>
<p><a href="http://kobo.github.com/groovyserv" target="_blank">GroovyServ</a> je Cčková implementace client-server řešení, ve kterém na pozadí žije proces s běžícím Groovy enginem, ke kterému se připojuje přes TCP/IP protokol klient, který serveru předá Groovy skript k interpretaci. Tím, že Groovy je již spuštěné, dojde k úspoře valné většiny času potřebné k interpretaci Groovy skriptu. Statistiky zrychlení jsou k dispozici na originálním GroovyServ webu - zde uvádím vlastní měření na <a href="http://reviews.cnet.com/laptops/lenovo-thinkpad-t61/4507-3121_7-32442903.ht" target="_blank">Lenovo Thinkpad T61</a> (rozparsování server.xml souboru v instalaci Tomcatu):</p>
<pre>
#spuštění přes standardní GROOVY
novoj@jnonb:~/Prototypes/groovyScripts/src$ time groovy cz/novoj/infrastructure/groovy/InfrastructureScriptInvoker.groovy PWD
Current project set to: [/www/p_prj/p_fg/bm2010/]

real	0m1.370s
user	0m1.684s
sys	0m0.168s

#spuštění přes GroovyServ
novoj@jnonb:~/Prototypes/groovyScripts/src$ time groovyclient cz/novoj/infrastructure/groovy/InfrastructureScriptInvoker.groovy PWD
Current project set to: [/www/p_prj/p_fg/bm2010/]

real	0m0.148s
user	0m0.000s
sys	0m0.004s
</pre>
<p>Instalace GroovyServ je velmi jednoduchá a tudíž zde nebudu přepisovat instalační postup. Po prvním spuštění serveru je jakékoliv další spuštění groovy skriptů přes groovyclient velmi rychlé.</p>
<h2>Debugging skriptů</h2>
<p>Skripty v Groovy je možné snadno debugovat ve standardním Java IDE (což je věc, po které se budete v shellu těžko shánět). V případě použití GroovyServ stačí v souboru <strong>/bin/groovyserver</strong> nastavit JAVA_OPTS proměnnou. Pro inspiraci uvádím výsek z mé verze souboru:</p>
<pre>
#-------------------------------------------
# Setup other variables
#-------------------------------------------

# -server option for JVM (for performance) (experimental)
export JAVA_OPTS="$JAVA_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=9080 -server"
</pre>
<p>Pak už stačí ve vašem IDE nakonfigurovat remote debugging standardním způsobem. Opět pro inspiraci přikládám screen z IntelliJ Idey:</p>
<p><a href="http://blog.novoj.net/binary/2011/06/debug.png" class="lightbox"><img src="http://blog.novoj.net/binary/2011/06/debug-300x270.png" alt="" title="debug" width="300" height="270" class="aligncenter size-medium wp-image-1529" /></a></p>
<h2>Prototypové skripty - ukládání a načítání server.xml konfigurací Tomcatu</h2>
<p>Pro vlastní potřeby jsem vytvořil pár skriptů pro ukládání a načítání <strong>server.xml</strong> konfigurací Tomcat serveru. Vzhledem k tomu, že ve <a href="http://www.fg.cz" target="_blank">Forrestu</a> pracujeme souběžně na řadě projektech a často musím přepínat z jednoho do druhého, zvykl jsem si překopírovávat zazálohované server.xml konfigurace pro cílovou doménou přes ostrou konfiguraci. Tj. mám například soubor <strong>server-trotina</strong>, který obsahuje konfiguraci webu <a href="http://www.trotina.cz" target="_blank">www.trotina.cz</a> (samozřejmě nastavenou na localhost) a který v případě potřeby překopíruju přes aktuální server.xml soubor. Po restartu Tomcata už pracuji na jiném projektu. Tato akce však vyžaduje spuštění nějakého správce souborů nebo shellu, nanavigování do složky Tomcatu, vybrání souboru a překopírování přes aktuální server.xml. Pomocí Groovy skriptů jsem si vytvořil jednoduché shell příkazy, které totéž provedou během vteřinky v rámci jediné operace:</p>
<pre>
#příkaz vytiskne aktuální doménu daného Tomcatu
novoj@jnonb:~$ gscript pwd
Using Tomcat: /opt/Apache/Tomcat_6.0
Current project set to: [/www/p_java/cps/]

#příkaz zazálohuje konfigurační soubor aktuální domény
novoj@jnonb:~$ gscript swd
Using Tomcat: /opt/Apache/Tomcat_6.0
Saved file: /opt/Apache/Tomcat_6.0/conf/backup/server-cps.xml

#příkaz obnoví konkrétní soubor ze zálohy, 
#skript inteligentně vyhledává konfiguraci podle shody názvu s argumentem volání
novoj@jnonb:~$ gscript rd cps
Using Tomcat: /opt/Apache/Tomcat_6.0
Found these matching files:
---------------------------------------------------
1 pts. : server-vodafoneic.xml, server-agcom.xml, server-hodnoceni-olivka.xml
2 pts. : server-kb_sec.xml, server-praguewelcome.xml, server-vodafoneic-public.xml
3 pts. : server-specialsettings.xml, server-jakchutnauspech.xml
9 pts. : server-cpsprototype.xml
1000 pts. : server-cps.xml
---------------------------------------------------
Restored file: /opt/Apache/Tomcat_6.0/conf/backup/server-cps.xml
</pre>
<p>Zdrojové kódy včetně shellového skriptu <strong>gscript</strong> jsou <a href="https://github.com/novoj/Groovy-Dev-Scripts" target="_blank">uloženy na GitHubu</a>, takže pokud byste měl někdo podobný use-case jako já, můžete využít mé hotové práce. Zajímavý je minimálně <a href="https://github.com/novoj/Groovy-Dev-Scripts/blob/master/script/gscript" target="_blank">zmíněný shell skript</a>, protože díky <a href="http://jira.codehaus.org/browse/GROOVY-2037" target="_blank">chybě Groovy</a>, není možné jednoduše použít wildcard znaků v linkování připojených JARů ze složky.</p>
<p><strong>Pozn.:</strong> na Groovy jsem převedl i další skripty pro hromadnou konverzi kódování textových souborů a odstranění BOM z UTF-8 popsaných v článku <a href="http://blog.novoj.net/2009/08/01/az-budete-chtit-nekdy-davkove-konvertovat-kodovani-souboru/" target="_blank">Až budete chtít někdy dávkově konvertovat kódování souborů …</a></p>
<p><strong>Zdrojové soubory:</strong> <a href="https://github.com/novoj/Groovy-Dev-Scripts" target="_blank">GitHub</a></p>
<h2>Souhrnně</h2>
<p>Každý z nás sem tam potřebuje napsat shell skript a Groovy má pro nás Java vývojáře řadu nesporných výhod:</p>
<ul>
<li>multiplatformní vývoj - skript, který napíšu pro Linux může běžet bez problémů i na Win platformě</li>
<li>řada pokročilých funkcí k dispozici "out of the box" (XML processing, Ant funkce, databáze)</li>
<li>použitelnost stávající znalostí z Java vývoje</li>
<li>objektový přístup k shell skriptům</li>
<li>možnost využití existujících Java knihoven (Apache Commons atp.)</li>
<li>použití Groovy goodies - closures, řada funkcí ulehčující práci s Java objekty</li>
<li>programovat v Groovy je zábava a toto je jedna z bezpečných možností, jak přičichnout ke Groovy i v případě, že jej nemůžeme používat pro produkční kód :)</li>
</ul>
<h2>Poznámky na okraj</h2>
<p>Dierk König také na své přednášce zmiňoval optimalizovaný vyhledávač (respektive customizovaný vyhledávací formulář Google) pro Groovy výrazy <a href="http://groovysearch.org/" target="_blank">http://groovysearch.org/</a>. Což by mohlo taktéž řadu z nás poměrně zajímat.</p>
