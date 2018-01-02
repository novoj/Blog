---
status: publish
published: true
title: Maven2, release plugin a přístup do CVS přes SSH s privátním klíčem
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Před tím, než jsem mohl ozkoušet maven-release-plugin, na který jsem si
  stěžoval v článku <a href=\"http://blog.novoj.net/2007/08/22/co-bych-rad-slysel-v-zari-na-czjug/\"
  target=\"_new\">Co bych rád slyšel v září na CZJUG</a>, musel jsem rozchodit přístup
  do našeho CVS skrze SSH s přihlašováním pomocí privátního klíče. Po zkušenostech
  můžu říct, že to byla práce nelehká a musím potvrdit negativní ohlasy ostatních,
  že v některých případech dokumentace k Mavenu (respektive k jeho konkrétním pluginům)
  je opravdu nedostatečná. Oříšek jsem nakonec rozlousknul díky zdrojákům a oddebugování.\r\n\r\nKrom
  tohoto problému se v článku dotknu ještě site:deploy opět na server přes SSH s použitím
  privátního klíče. Jeden by si myslel, že zprovoznění prvního problému vyřeší všechny
  problémy tohoto charakteru, ale ouvej. Řada věcí je v maven pluginech řešena znovu
  a jinak. A toto je přesně ten případ. Řešení tu najdete také.\r\n\r\n"
wordpress_id: 41
wordpress_url: http://blog.novoj.net/2007/11/02/maven2-release-plugin-a-pristup-do-cvs-pres-ssh-s-privatnim-klicem/
date: '2007-11-02 22:23:41 +0100'
date_gmt: '2007-11-02 21:23:41 +0100'
categories:
- Maven
tags: []
comments:
- id: 962
  author: Zerem
  author_email: zerem@nekazen.eu
  author_url: ''
  date: '2007-11-05 12:45:37 +0100'
  date_gmt: '2007-11-05 11:45:37 +0100'
  content: "pouzivame svn a konfigurace maven-scm pres privatni klice byla o hodne
    jednodussi...\r\nco se tyce releasu slozitych projektu, tam to opravdu  umi pozlobit...vzdy
    jsem byl uspesnejsi pouzitim pravidla: pri releasu stromu modulu pouzivat vsude
    stejne groupId"
- id: 977
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-11-07 12:19:23 +0100'
  date_gmt: '2007-11-07 11:19:23 +0100'
  content: "Propojení se SVN jsem rozcházel asi před rokem v jiné firmě, tam jsem
    řešil zase jiné problémy a to s tím, jak správně nastavit adresářovou strukturu
    v SVN aby se jednoduše dělaly TAGY a BRANCHE s oddělenou TRUNK větví. Vím, že
    se mi to nějak taky podařilo rozchodit - jenže tam jsme jeli na Ubuntu a tam jsem
    s SSH neměl vůbec žádné problémy.\r\n\r\nKaždopádně rozchození release procesu
    není vůbec žádná trivka (napoprvé)."
---
<p>Před tím, než jsem mohl ozkoušet maven-release-plugin, na který jsem si stěžoval v článku <a href="http://blog.novoj.net/2007/08/22/co-bych-rad-slysel-v-zari-na-czjug/" target="_new">Co bych rád slyšel v září na CZJUG</a>, musel jsem rozchodit přístup do našeho CVS skrze SSH s přihlašováním pomocí privátního klíče. Po zkušenostech můžu říct, že to byla práce nelehká a musím potvrdit negativní ohlasy ostatních, že v některých případech dokumentace k Mavenu (respektive k jeho konkrétním pluginům) je opravdu nedostatečná. Oříšek jsem nakonec rozlousknul díky zdrojákům a oddebugování.</p>
<p>Krom tohoto problému se v článku dotknu ještě site:deploy opět na server přes SSH s použitím privátního klíče. Jeden by si myslel, že zprovoznění prvního problému vyřeší všechny problémy tohoto charakteru, ale ouvej. Řada věcí je v maven pluginech řešena znovu a jinak. A toto je přesně ten případ. Řešení tu najdete také.</p>
<p><a id="more"></a><a id="more-41"></a></p>
<p>Především je třeba mít správně nakonfigurované připojení na SCM. Základem je tedy následující definice v pom.xml:</p>
<p>[source lang="xml"]<br />
<scm><br />
	<connection>scm:cvs:${protocol}:${username}@${servername}:${CVSROOT}:${MODULE}</connection><br />
	<developerConnection>scm:cvs:${protocol}:${username}@${servername}:${CVSROOT}:${MODULE}</developerConnection><br />
	<url>http://${servername}</url><br />
</scm><br />
[/source]</p>
<p>Kde:</p>
<ul>
<li><b>protocol</b> specifikuje typ připojení k CVS serveru - <b>ext</b> v takovém případě se plugin bude snažit použít externí SSH aplikaci pro připojení na CVS server, <b>ssh</b> interní implementace SSH klienta, <a href="http://maven.apache.org/scm/cvs.html" target="_new">a další, které se mne netýkaly</a></li>
<li><b>servername</b> je název serveru, kde se nachází CVS repository (např. apache.org)</li>
<li><b>username</b> v našem případě se jedná o uživatele, který bude použit pro SSH autentikaci</li>
<li><b>CVSROOT</b> cesta k CVS rootu na uvedeném serveru</li>
<li><b>MODULE</b> název modulu v CVS - po dalších peripetiích jsem přišel na to, že maven-release-plugin vám nebude správně fungovat, pokud přímo v rootu vycheckoutovaného modulu nebude pom.xml, pokud máte strukturu v CVS košatější (jako my) a nemůžete mít pom.xml v rootu modulu, můžete normálně za název modulu přidat za lomítkem cestu k podadresáři, kde se nachází váš projektový pom.xml (tohle mi trvalo taky nějakou hodinku :-) )</li>
</ul>
<p>Nuže nejdříve jsem zkoušel jít cestou konfigurace maven-scm-pluginu (interní implementací SSH), který je maven-release-pluginem používán a vyzkoušet funkčnost jednoduchým zadáním "mvn scm:status". Otázka zněla, jak nakonfigurovat cestu k privátnímu klíči a passphrase?! V dokumentaci najdete leccos, ale tohle ne.</p>
<p>Šel jsem tedy do zdrojových kódů a zjistil jsem, že uvedené informace se zadávají přes property. Co mě ovšem překvapilo, že v celém pluginu se k propertám přistupuje přes System.getProperty("myProperty"). Samozřejmě, že jsem chtěl tyto property mít spíš někde v settings.xml a nechtěl jsem je předávat jako argument na příkazové řádce. Než jsem zjistil, že v konfiguraci pluginů je možné uvést i následující deklaraci, která nastaví i "systémové" property mi zase chvíli dalo (kupodivu o tomto se v dokumentaci moc nepíše).</p>
<p>[source lang="xml"]<br />
<systemProperties><br />
    <myproperty>myvalue</myproperty><br />
</systemProperties><br />
[/source]</p>
<p><i>Pozn.: možná je moje neznalost způsobená i tím, že jsem pro Maven zatím nenapsal ještě ani jeden plugin, s odstupem je mi možná jasné, proč se používá System.getProperty, jelikož takto se plugin dostane jak k argumentům z příkazové řádky, tak i k parametrům z pom.xml - jen nechápu, proč tvůrci Mavenu vše nesloučili pod jedněmi PROPERTY a proč tedy se tedy "uživatel" musí zajímat o to co musí konfigurovat přes systemProperties a co přes plugin configuration</i></p>
<p>Takže vybaven touto znalostí jsem již mohl konfiguraci závislou na lokálním prostředí externalizovat. Stačilo v deklaraci systemProperties uvést následující property:</p>
<ul>
<li>maven.scm.cvs.java.cvs_rsh (cesta k externímu SSH programu - na Windowsech třebas Plink z rodiny Putty)</li>
<li>maven.scm.cvs.java.ssh.privateKey (cesta k privátnímu klíči - není nutné specifikovat, pokud se klíč nachází ve výchozím umístění jako ${user.home}/.ssh/id_dsa nebo ${user.home}/.ssh/id_rsa podle typu použité šifry)</li>
<li>maven.scm.cvs.java.ssh.passphrase (heslo k rozkódování privátního klíče)</li>
</ul>
<p><b>Upozornění:</b> id_rsa klíč musí být privátní klíč ve formátu OpenSSH, do tohoto formátu se dá klíč uložit v programu PuttyGen.exe (menu -> Conversion -> OpenSSH)</p>
<p>Nicméně pod daným nastavením fungoval pouze maven-scm-plugin, maven-release-plugin nechodil (zdálo se mi, že se někde po cestě ztratila informace o passphrase k privátnímu klíči).</p>
<h3>Funkční řešení pro maven-release-plugin</h3>
<p>Jediný způsob, který se mi podařilo úspěšně rozchodit připojení k CVS pod oběma pluginy bylo použití protokolu <b>ext</b> v definici scm.developerConnection a nadefinování proměnné prostředí s názvem <b>CVS_RSH</b>, která obsahovala cestu k externí SSH aplikaci (Plink). Před vlastním spuštěním maven goalů spouštím aplikaci PageAnt, která je dodávaná společně s aplikací Putty (Plink) a umožňuje nahrát sadu privátních klíčů do paměti s tím, že se heslo k nim zadává pouze jednou - při každém dalším požadavku na klíč PageAnt již poskytne rozšifrovanou podobu klíče. Plink a PageAnt jsou ze stejné rodiny a proto bezchybně spolupracují.</p>
<p><b>Upozornění:</b> Plink.exe musí být uložen na cestě bez mezer, nebo musí v CVS_RSH cesta v uvozovkách.</p>
<p>Při tomto nastavení se spolupráce s CVS již rozběhla. Škoda, že jsem o tomhle zcela prostém řešení nevěděl už na začátku.</p>
<h3>Problémy pokračují - jsme u site:deploy</h3>
<p>Site deploy se provádí v rámci release procesu a typicky uploaduje vytvořenou dokumentaci na jiný server. Opět k tomu používáme SSH a kupodivu opět i privátní klíč. Jenže ouha, původní způsob, který funguje s maven-scm a maven-release pluginy zde nefunguje a celé se to konfiguruje JINAK!!! (toto je naštěstí už docela dobře zdokumentované)</p>
<p>Cesta k cílovému umístění v pom.xml vypadá takto:</p>
<p>[source lang="xml"]<br />
<distributionManagement><br />
	<site><br />
		<id>website</id><br />
		<url>scp://${servername}/${path}</url><br />
	</site><br />
</distributionManagement><br />
[/source]</p>
<p>Abych se dokázal výše uvedeným způsobem připojit na server, musím mít v <b>setting.xml</b> nadefinováno toto:</p>
<p>[source lang="xml"]<br />
<servers><br />
    <server><br />
      <id>website</id><br />
      <username>${username}</username></p>
<passphrase>${passphrase}</passphrase>
    </server><br />
  </servers><br />
[/source]</p>
<p>Než jsem prošel zmíněným postupem trvalo mi to asi dva týdny (samozřejmě, že jsem se tomu nemohl plně věnovat, takže jsem to řešil jen po chvilkách). Touto dobou jsem už byl mírně nazlobený.</p>
<h3>Ne příliš efektivní proces releasu</h3>
<p>Release plugin funguje tak, že v rámci svého běhu vytváří instance shellu a v nich na příkazové řádce spouští mvn s dalšími parametry. Tím pádem běží vlastně maven v mavenu, ovšem jedná se o dvě relativně nezávislé instance. Což například znamená, že při spuštění příkazu:</p>
<p>[source:css]<br />
mvn release:prepare release:perform -Dmaven.test.skip=true<br />
[/source]</p>
<p>se vám použije argument pro ignorování testů jen v té "hlavní" instanci mavenu, ale do vnitřních instancích se tato property už nezpropaguje. Tzn.  testy se vám stejně spustí a během celého procesu dokonce několikrát (pokud např. nemáte reporty v externím profilu, který se při releasu vynechává a ty reporty vyžadují spuštění testů).</p>
<p>Mě osobně se osvědčilo v pom.xml nadefinovat property u maven-surefire-pluginu, která vynutí vypnutí testů. Property na tomto místě se už použije kompletně v celém release procesu (což bych jako laik čekal už v prvním případě, nu ale což). Nastavení pro inspiraci uvedu (proměnné mám samozřejmě uvedeny v settings.xml):</p>
<p>[source lang="xml"]</p>
<plugin>
	<groupId>org.apache.maven.plugins</groupId><br />
	<artifactId>maven-surefire-plugin</artifactId><br />
	<configuration><br />
		<jvm>${JAVA_1_4_HOME}${JAVA_EXECUTABLE}</jvm><br />
		<skip>${SKIP_TESTS}</skip><br />
		<excludes><br />
			<exclude>**/Abstract*Test.java</exclude><br />
			<exclude>**/Abstract*TestCase.java</exclude><br />
			<exclude>**/Test*.java</exclude><br />
		</excludes><br />
	</configuration>
</plugin>
[/source]</p>
<p>Můžete namítnout, že není rozumné při releasu vynechat testy. Jenže testy mě běží na integračním serveru - tudíž mám jistotu, že release bude ok. Release ovšem obvykle dělám ručně na lokále a tam je spuštění testů s kompletním vygenerováním dokumentace prostě overkill.</p>
<h3>Závěrem</h3>
<p>Po výše popsaném martyriu jsem již schopen releasovat jednoduché moduly. U složených projektu s parent pomem a podmoduly se mi ještě vyskytuje další chyba, kdy při release:perform maven skončí s chybou, že nemůže resolvovat dependency na právě vytvářené moduly v remote repository (zcela logicky tam nejsou, protože ještě neproběhl deploy). Na tento problém mám zatím workaround, že ve vycheckoutované složce spustím ručně "mvn deploy", pak již perform fáze projde v pořádku.</p>
<p>Práce s Mavenem není vždy úplně snadná, přesto si myslím, že stojí za to jej používat. Naše firma se po půlročním zkušebním provozu rozhodla opustit Ant a nadále buildovat projekty jen Mavenem. Pomohlo nám to standardizovat hodně věcí a řekl bych, že přínosy převažují negativa. Ale někdy je to teda boj.</p>
<p><strong>Dodatek k poslednímu problému:</strong></p>
<p>S posledním uvedeným problémem jsem na tom nebyl sám. Po aplikování rad z diskusí:</p>
<ul>
<li><a href="http://www.mail-archive.com/users@maven.apache.org/msg72344.html" target="_new">Maven user mail list</a></li>
<li><a href="http://mail-archives.apache.org/mod_mbox/maven-users/200612.mbox/%3C7758847.post@talk.nabble.com%3E" target="_new">Ještě jednou maven user list</a></li>
</ul>
<p>se problém vyřešil. Škoda jen, že maven-release-plugin nefunguje správně bez dodatečné konfigurace.</p>
