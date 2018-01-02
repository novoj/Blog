---
status: publish
published: true
title: Co bych rád slyšel v září na CZJUG
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Tento post je tak trochu věnován <a href=\"http://blog.softeu.cz/\" target=\"_new\">Petru
  Ferschmannovi ze SoftEU</a>, který bude mít <a href=\"http://blog.softeu.cz/pozvanka-maven-prakticke-nasazeni/\"
  target=\"_new\">19. září 2007 přednášku na téma praktické nasazení Mavenu na CZJUGu</a>.
  Jelikož vím, že občas na můj blog zamíří (doufám že pravidelně :-) ), věřím, že
  na článek zareaguje a kdo ví - třeba na moje otázky v září odpoví.\r\n"
wordpress_id: 31
wordpress_url: http://blog.novoj.net/2007/08/22/co-bych-rad-slysel-v-zari-na-czjug/
date: '2007-08-22 12:04:15 +0200'
date_gmt: '2007-08-22 11:04:15 +0200'
categories:
- Maven
tags: []
comments:
- id: 445
  author: Petr Ferschmann
  author_email: pferschmann@softeu.com
  author_url: http://blog.softeu.cz
  date: '2007-08-22 18:08:36 +0200'
  date_gmt: '2007-08-22 17:08:36 +0200'
  content: "Zdravím,\r\n\r\npřesně na tato témata (a i další) chci ve své přednášce
    odpovědět. Takže děkuji za hozenou rukavici :-)  Odpověď si, ale nechám až na
    svoji přednášku - přijďte jste zváni.\r\n\r\nPetr Ferschmann"
- id: 451
  author: Jirka
  author_email: jirkovi@gmail.com
  author_url: ''
  date: '2007-08-23 07:57:05 +0200'
  date_gmt: '2007-08-23 06:57:05 +0200'
  content: "Pokud by byl záznam CZJUGu i na videu bylo by to super. \r\n( Nejsu z
    Prahy - 5 hodin vlakem... :-( )\r\n\r\nJirka"
- id: 452
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-08-23 08:22:15 +0200'
  date_gmt: '2007-08-23 07:22:15 +0200'
  content: Záznamy obvykle bývají - jen mají asi měsíční zpoždění (jak kdy). Za první
    rok CZJUGu (do prázdnin) jsou myslím už všechny. Já to mám naštěstí "jen" 1,5
    hodiny z Pardubic.
- id: 456
  author: 3rojka
  author_email: 3rojka@gmail.com
  author_url: http://blog.3rojka.com
  date: '2007-08-23 11:19:01 +0200'
  date_gmt: '2007-08-23 10:19:01 +0200'
  content: Ohledně toho jednotného verzovaní, nemám to vyzkoušené protože na to stále
    jaksi nezbyl čas, ale kdy jsem si stím hrál a myslím že by to šlo udělat nějak
    tahkle. Nazveme naší devel verzi DEVEL-SNAPSHOT a všechny potomky potom odkazují
    na DEVEL-SNAPSHOT parenta, o verzovaní se potom postará release plugin, který
    nahrazí SNAPSHOT release verzí. Jako následující verzi potom zase musíme zadat
    DEVEL-SNAPSHOT, tím odbouráme nutnost přečíslovávat verze paranta i jeho potomků
    a všechno verzování se odahrává pouze na releasu. Možná že blafu ale myslím že
    by to takhle nějak šlo, ale jak říkám nikdy jsem to neodzkoušel.
- id: 457
  author: Honza Novotný
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-08-23 11:55:37 +0200'
  date_gmt: '2007-08-23 10:55:37 +0200'
  content: No problém spočívá v tom, že se mi nikdy nepodařilo rozjet (pravda, je
    to asi půl roku, co jsem to zkoušel naposledy) maven-release-plugin pro multiproject.
    Po checkoutu se rozjely nějak cesty a build failnul. Jinak si myslím, že pak by
    stačilo jen dát všem modulům i parentu v úvodu stejnou verzi a release plugin
    by se postaral o náležité zvednutí verze všech artefaktů. Ale to taky vařím z
    vody, protože jak říkám - v praxi se mi to nezadařilo.
- id: 458
  author: Petr Ferschmann
  author_email: pferschmann@softeu.com
  author_url: http://blog.softeu.cz
  date: '2007-08-23 16:20:28 +0200'
  date_gmt: '2007-08-23 15:20:28 +0200'
  content: "Zdravím,\r\n\r\ntak tedy zkusím trošku popostrčit správným směrem :-)\r\n\r\nPlatí
    základní pravidlo \"U Mavenu se multiprojekt skládá z více projektů\". To ale
    znamená, že mohu vycheckoutovat jen podadresář a přesto budu schopný projekt přeložit.
    Takže není něco jako adresář výš.\r\n\r\nMyšlenka je taková, že máte větší projekt
    a continuum vám pravidelně vše kompiluje a nahrává do vaší lokální snapshot repository.
    A vy buildíte všechno vůči ní. Když mi tohle došlo, tak mi téměř vše v Mavenu
    začalo fungovat :-)\r\n\r\nNeříkám, že toto je jediné a ideální řešení (pro mně
    to byla docela změna způsobu myšlení), ale dá se s tím celkem dobře sžít a teď
    už mi to ani nepřijde zvláštní."
- id: 459
  author: Petr Ferschmann
  author_email: pferschmann@softeu.com
  author_url: http://blog.softeu.cz
  date: '2007-08-23 16:26:13 +0200'
  date_gmt: '2007-08-23 15:26:13 +0200'
  content: "Ještě doplním, že continuum to může nahrát do repository až po tom, co
    je prošli testy. \r\n\r\nA pokud máte několik projektů s různými životními cykly
    (jak knihovny třetích stran tak ve vlastní firmě - např. \"úžasný\" framework)
    tak je toto řešení celkem příjemné a dobré.\r\n\r\nDříve jsme obvykle měli buď
    vše v jednom repository SVN/CVS a pokud něco bylo sdílené mezi více projekty byl
    to problém. Případně se prostě do projektu nahrál až výsledný JAR."
- id: 460
  author: Honza Novotný
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-08-23 17:27:25 +0200'
  date_gmt: '2007-08-23 16:27:25 +0200'
  content: "To že multiprojekt = více projektů a co z toho vyplývá, si myslím, že
    jsem pochopil. Nemám s tímhle žádný problém. Chyba je (nebo třeba už je to opraveno)
    v tom maven-release-pluginu - ten je na adresářové struktuře závislý právě díky
    tomu, že se to checkoutuje z VCS (nebo si to alespoň myslím). Nebyl jsem schopný
    vydat hromadně release, pokud jsem spustil goaly na parent projektu - první (přípravná)
    fáze proběhla, ale když jsem spustil druhou, kde se provádí checkout do target
    složky mi to celé failnulo na tom, že se maven snažil volat release:perform někde,
    kde ty moduly vycheckoutované nebyly. Když jsem to volal jednotlivě pro každý
    modul, tak to samozřejmě fungovalo - ale bylo to pracné.\r\n\r\nTo byl stav před
    půl rokem - je možné že s tím pluginem za tu dobu už pohnuli. Dám si domácí úkol
    a prověřím to, abych tady nedělal vlny zbytečně."
- id: 464
  author: Petr Ferschmann
  author_email: pferschmann@softeu.com
  author_url: http://blog.softeu.cz
  date: '2007-08-24 06:40:45 +0200'
  date_gmt: '2007-08-24 05:40:45 +0200'
  content: "Zdravím,\r\nvycházel jsem z textu \"Po vycheckoutování mu ale nesedí relativní
    cesty k pom.xml jednotlivých modulů a celé to vyhoří.\".\r\n\r\nMaven v každém
    podprojektu vycheckoutuje do podadresáře target/checkout jen a pouze ten podprojekt.
    \r\n\r\nTakže moje otázka zní: byla v to pom.xml Ještě další závislost mezi jednotlivými
    pom.xml (např. pomocí relativePath - s tím jsem se setkal) a nebo to Maven nezvládl
    sám o sobě? (a s tím už jsem se nesetkal :-)"
- id: 466
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-08-24 08:25:57 +0200'
  date_gmt: '2007-08-24 07:25:57 +0200'
  content: "No měl jsem dojem, že problém je v deklaraci toho parent pom.xml. Tam
    mám v deklaraci dejme tomu dva moduly:\r\n\r\n&lt;modules&gt;\r\n    &lt;module&gt;test1&lt;/module&gt;\r\n
    \   &lt;module&gt;test2&lt;/module&gt;\r\n&lt;/modules&gt;\r\n\r\nMaven očekává,
    že najde pom.xml pro tyto dva moduly v podložkách test1 + test2 složky, kde se
    nachází parent pom.xml. Pokud bych chtěl mít modul na stejné úrovni jako je složka
    parent pom.xml musel bych uvést:\r\n\r\n&lt;modules&gt;\r\n    &lt;module&gt;test1&lt;/module&gt;\r\n
    \   &lt;module&gt;test2&lt;/module&gt;\r\n    &lt;module&gt;../test3&lt;/module&gt;\r\n&lt;/modules&gt;\r\n\r\nProblém
    toho maven-release-pluginu byl myslím (pozor toto jsou vzpomínky půl roku staré)
    v tom, že po checkoutu do složky target, resolvoval plugin cesty vztažené k parent
    pom.xml ve \"vývojové\" složce a ne ve složce \"target\", kam si to celé vycheckoutoval.
    A na tom to myslím vyhořelo. A to i v případě, že ty moduly byly v podsložkách
    jako v prvním příkladě, co jsem uvedl (tedy žádné používání ../ v cestě a podobné
    hrůznosti)."
- id: 515
  author: 3rojka
  author_email: radek.riedel@gmail.com
  author_url: http://blog.3rojka.com
  date: '2007-08-28 19:22:41 +0200'
  date_gmt: '2007-08-28 18:22:41 +0200'
  content: Našel jsem si chvíli na vyzkoušení a něco jsem o tom naspal http://blog.3rojka.com/index.php/2007/08/28/maven-release-plugin-in-action/
- id: 516
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-08-28 20:20:31 +0200'
  date_gmt: '2007-08-28 19:20:31 +0200'
  content: "Díky - přesně stejný postup jsem zkoušel před necelým rokem a neprocházel
    mi - je možné, že v té době byl release plugin ještě v ranějším stádiu s chybkami.\r\n\r\nVěnoval
    jsem zopakování postupu asi hodinku a nějak jsem se zasekl na použití maven SCM
    pluginu - potřebuji z Windows komunikovat s CVS přes SSH s použitím privátního
    klíče. Což není zase až taková trivka, jak jsem si nejdříve myslel.\r\n\r\nNapojení
    na CVS je must-have precondition pro maven-release-plugin, takže než rozlousknu
    tohle, tak si to neozkouším. Škoda, že teď zrovna nemám moc času :(.\r\n\r\nKaždopádně
    3rojko, díky za reakci a článek."
---
<p>Tento post je tak trochu věnován <a href="http://blog.softeu.cz/" target="_new">Petru Ferschmannovi ze SoftEU</a>, který bude mít <a href="http://blog.softeu.cz/pozvanka-maven-prakticke-nasazeni/" target="_new">19. září 2007 přednášku na téma praktické nasazení Mavenu na CZJUGu</a>. Jelikož vím, že občas na můj blog zamíří (doufám že pravidelně :-) ), věřím, že na článek zareaguje a kdo ví - třeba na moje otázky v září odpoví.<br />
<a id="more"></a><a id="more-31"></a></p>
<h3>Problémy s maven-release-plugin</h3>
<p>Vycházím z praktické zkušenosti (cca 3/4 roku staré tedy), kdy jsem se snažil použít <a href="http://maven.apache.org/plugins/maven-release-plugin/" target="_new">maven-release-plugin</a> pro vydávání verzi v multiprojektu. Typicky mám parent pom.xml v nadřízené složce, a pom.xml jednotlivých modulů ve složkách o úroveň níže (obdobný problém jsem ale měl i pokud jsem parent umístil také do složky druhé úrovně, myslím). Při použití maven-release-pluginu na parent projektu bych čekal, že správně releasne jak hlavní projekt, tak všechny moduly v něm registrované. Problém je  v tom, že plugin všechny zdrojáky zataguje ve VCS a následně si je vycheckoutuje pod tímto tagem do složky "target". Po vycheckoutování mu ale nesedí relativní cesty k pom.xml jednotlivých modulů a celé to vyhoří. Jediným způsobem, jak plugin použít, pro mne bylo spouštět postupně releasy na všech modulech projektu, což bylo velmi nekomfortní. Dále mě na celém tomto způsobu vadilo, že v celém release procesu jsou spouštěny např. testy 2x - přitom by přeci stačilo je spustit jen jednou. Navíc parametry, se kterým se spustil daný release se posléze nepřenesly do buildování již té vycheckoutované verze - mám ten dojem, že plugin si interně spouští úplně novou instanci mavenu na zbuildování vycheckoutované verze.</p>
<p>Existuje nějaký lepší plugin (i když zmíněný plugin patří mezi ty "oficiální", mavenovské pluginy)? Nebo jak správně sestavit strukturu pomů a používat release plugin tak, aby pracoval dle očekávání i v multiproject použití?</p>
<h3>Stanovení jednotné verze pro modul s potomky</h3>
<p>Co řeším velmi často je opravdu jednoduchá věc a zatím jsem nenašel žádné elegantní řešení. Pokud mám multiprojekt, rád bych vedl verzi jen na úrovni parent projektu a při jeho buildu by všechny moduly tohoto projektu byly vydané pod touto verzí. Problém je v zápise a odkazování, které maven používá. Aby se informace z verze mohla zdědit, musí se všichni potomci odkázat na svého parenta - ovšem musí uvést verzi tohoto parenta. Takže jakmile změním verzi v parent projektu, tak bych musel ve všech modulech změnit i prolinkování na tu správnou "novou" verzi parenta aby se verze mohla pro build změnit - prostě deadlock jako vyšitej.</p>
<p>Řešil jsem to pomocí property souboru, který parent používal (moduly díky dědičnosti také) - takže jsem verzi mohl mít jen v něm. Bohužel s takto zapsanou verzí nedokáže pracovat Artifactory, takže jsem tuto cestu musel opustit. Ono je to také dost nestandardní - když potom kouknete do pomu, tak tam tu verzi nenajdete, což není zrovna ideální stav.</p>
<p>Prohledal jsem web i pár elektronických knih o Mavenu, ale nějak jsem řešení tohoto problému nenašel. Možná to je hloupost, ale opravdu to otravuje život ;-) .</p>
<h3>Nasazení firemní repository - proxy veřejných repository</h3>
<p>Obvykle každá firma řeší problém vlastní repository a velmi rychle i nasazení nějaké proxy, která centralizuje pro všechny vývojáře přístup ke knihovnám třetích stran. Rozhodně by byly zajímavé zkušenosti z této oblasti. Konkrétně třebas:</p>
<ul>
<li>s jakými proxy máte zkušenosti, která by se dala doporučit?</li>
<li>jak řešíte deploy knihoven třetích stran, které nejsou ve veřejných repository (třeba u Artifactory je to poměrně snadné, ale u Maven-proxy od Codehaus už to byl trochu problém)?</li>
<li>oddělujete v repository SNAPSHOT a "ostré" verze knihoven? jak potom řešíte nastavení distributionManagement pro tyto různé druhy repository - vše přes profily?</li>
</ul>
<h3>CI, Night buildy</h3>
<p>Jelikož se má přednáška týkat i CI, zajímavá informace by byla i o struktuře build konfigurací a jejich skladbě. Mám tím na mysli, jestli při každé změně ve VCS se okamžitě spouští kompilace i testy. Nebo jen kompilace a testy jen v definovaných intervalech (např. každou hodinu). Jestli a jakým způsobem řeší vytváření night buildů a jestli je cílem těchto night buildů pouze vyrobení artefaktů, nebo i instalace na nějaký testovací server (tady ale narážíme na problém PermGenSpace).</p>
<p>Zajímavé by bylo i porovnání a zkušenosti různých CI serverů - myslím tím z hlediska praxe a nikoliv z oficiálních zdrojů.</p>
<h4>Výkonnostní testy</h4>
<p>Jaké mají zkušenosti s automatickými testy výkonnosti aplikace - jak řeší např. problém spouštění testů na různě výkonných serverech nebo v různých časech (někdy může být stejný server vytížen více a někdy méně - pokud nemáme dedikovaný server jen na výkonnostní testy).</p>
<p>*) výkonnostními testy jsou myšleny testy, které např. odpovídají QOS pro danou web aplikaci a měly by garantovat, že postupným vývojem projektu se nepřekročí stanovené limity odezev</p>
<h4>Web testy</h4>
<p>Jak řešíte spouštění automatických web testů, které potřebují pro svůj běh nainstalovanou a zprovozněnou aplikaci na web serveru? Součástí buildu by potom musela být nejprve automatická instalace na server a pak teprve spuštění automatizovaných web testů. Vždy mne od tohoto záměru odradila představa potenciální "chybovosti" tohoto procesu. Řešili jste třebas toto?</p>
<h3>Praktické nasazení</h3>
<p>S jakými praktickými problémy jste se při nasazení setkali? Na co si vaši vývojáři, kteří na něco takového nebyli před tím zvyklí stěžovali a jak jste jejich výtky překonali? Byli třeba nějaké slepé větve, které jste s postupem času opustili?</p>
<h3>Výzva ostatním</h3>
<p>Možná vás tohoto článku při čtení otázek a problémů, které trápí mne, napadnou i další - z vaší vlastní vlastní praxe. Uvítám, pokud se s nimi o ně podělíte a napíšete je do komentářů k tomuto článku. Myslím, že rozhodně není od věci, zkusit apelovat na řečníka, aby ve své přednášce probral i otázky, které nás pálí.</p>
