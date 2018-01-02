---
status: publish
published: true
title: Elegantní způsob ukládání verzi v Java archívech
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Existují situace, kdy aplikaci neinstalujete sami, ale instaluje ji třetí
  strana - ať už je třetí stranou myšlen technik zákazníka nebo kolega z jiného oddělení
  firmy. Vy posléze přijdete už k nainstalované aplikaci, u které si nikdy tak úplně
  stoprocentně nemůžete být jisti verzí neřkuli verzemi knihoven, které daná aplikace
  používá. Přesto tato znalost může být pro řešení některých problémů zásadní (např.
  proto, že oprava může spočívat v pouhé instalaci nové verze knihovny / modulu).
  Můžete se s tím setkat i v daleko prostším případě - pokud vyvíjíte nějaký produkt
  s velkým množstvím instalací - chvíli vám může trvat než zjistíte jakou verzi má
  daný zákazník, u kterého řešíte nahlášené problémy.\r\n\r\nPřímočarým řešením je
  vytvoření nějaké info stránky se seznamem knihoven / modulů a jejich verzí, které
  jsou použity v aplikaci, která by vám umožnila všechny potřebné informace zjistit
  během vteřiny. V tu chvíli už se ale dostáváte k druhému problému -  jak zajistit
  (nelépe automatické) verzování knihoven, aby bylo zajistěno, že se knihovny budou
  pravidelně verzovat, a že u všech knihoven bude tato informace jednoduše přístupná
  (a opět nejlépe jednotným způsobem, aby info stránka neměla s vyhledáváním této
  informace problém).\r\n\r\nProblém se zdá možná jednoduchý, ale můžete narazit na
  celou řadu nepříjemností jako se to stalo třeba nám. Řešení může být ale opravdu
  velmi prosté ...\r\n\r\n"
wordpress_id: 83
wordpress_url: http://blog.novoj.net/2008/08/17/elegantni-zpusob-ukladani-verzi-v-java-archivech/
date: '2008-08-17 18:20:54 +0200'
date_gmt: '2008-08-17 17:20:54 +0200'
categories:
- Programování
- Java
- Maven
tags: []
comments:
- id: 2845
  author: JČP
  author_email: jcp@atlas.cz
  author_url: ''
  date: '2008-08-29 10:12:31 +0200'
  date_gmt: '2008-08-29 09:12:31 +0200'
  content: "Přidávám verzování pro ant\r\n\r\n\t\r\n\t\r\n\t\t\r\n\t\t\t\r\n\t\t\r\n\t\r\n\r\n\t\r\n\t\r\n\t\t\r\n\t\t\r\n\t\t\t\r\n\t\t\t\t\r\n
    \               \r\n\t\t\t\r\n\t\t   \r\n\t\t      \r\n\t\t      \r\n\t\t      \r\n\t\t
    \   \r\n\t\t\r\n\t"
- id: 2846
  author: JČP
  author_email: jcp@atlas.cz
  author_url: ''
  date: '2008-08-29 10:16:07 +0200'
  date_gmt: '2008-08-29 09:16:07 +0200'
  content: "[EDITOVÁNO NOVOJEM] příklad jsem přesunul do textu příspěvku [/EDITOVÁNO
    NOVOJEM] "
- id: 2848
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2008-08-29 12:14:38 +0200'
  date_gmt: '2008-08-29 11:14:38 +0200'
  content: Skvělý, díky za rozšíření článku. Přidám to rovnou do textu.
- id: 2939
  author: Rasto
  author_email: rastolatta@yahoo.com
  author_url: ''
  date: '2008-09-02 15:13:19 +0200'
  date_gmt: '2008-09-02 14:13:19 +0200'
  content: "My sme podobny problem vyriesili tym, ze \r\n1. programator musi zdrojak
    najprv commitnut do CVS, cim sa zapise jeho verzia aj do suboru Entries v rovnakom
    adresari\r\n2. pri baleni jarka sa pribali aj tento subor a vlastne popisuje vsetky
    subory v jarku (verziu aj cas vlozenia)\r\n\r\nNam to zatial staci a ta zmena
    aj s otestovanim trvala asi tak do 2h"
- id: 2943
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2008-09-02 19:20:47 +0200'
  date_gmt: '2008-09-02 18:20:47 +0200'
  content: Čímž verzujete konkrétní zdrojové soubory a ne vybuildovaný balík ... pochopil
    jsem to správně?
---
<p>Existují situace, kdy aplikaci neinstalujete sami, ale instaluje ji třetí strana - ať už je třetí stranou myšlen technik zákazníka nebo kolega z jiného oddělení firmy. Vy posléze přijdete už k nainstalované aplikaci, u které si nikdy tak úplně stoprocentně nemůžete být jisti verzí neřkuli verzemi knihoven, které daná aplikace používá. Přesto tato znalost může být pro řešení některých problémů zásadní (např. proto, že oprava může spočívat v pouhé instalaci nové verze knihovny / modulu). Můžete se s tím setkat i v daleko prostším případě - pokud vyvíjíte nějaký produkt s velkým množstvím instalací - chvíli vám může trvat než zjistíte jakou verzi má daný zákazník, u kterého řešíte nahlášené problémy.</p>
<p>Přímočarým řešením je vytvoření nějaké info stránky se seznamem knihoven / modulů a jejich verzí, které jsou použity v aplikaci, která by vám umožnila všechny potřebné informace zjistit během vteřiny. V tu chvíli už se ale dostáváte k druhému problému -  jak zajistit (nelépe automatické) verzování knihoven, aby bylo zajistěno, že se knihovny budou pravidelně verzovat, a že u všech knihoven bude tato informace jednoduše přístupná (a opět nejlépe jednotným způsobem, aby info stránka neměla s vyhledáváním této informace problém).</p>
<p>Problém se zdá možná jednoduchý, ale můžete narazit na celou řadu nepříjemností jako se to stalo třeba nám. Řešení může být ale opravdu velmi prosté ...</p>
<p><a id="more"></a><a id="more-83"></a></p>
<h3>Naše původní řešení nebylo nijak elegantní</h3>
<p>Pro pravidelné verzování jsme používali standardní releasovací proces Mavenu. Vkládání a čtení verzí knihoven jsme si už ale museli zajistit sami. Donedávna jsme toto nechávali v kompetenci programátorů jednotlivých modulů, což mělo několik negativních efektů:</p>
<ul>
<li>každý si to řešil tak nějak po svém - i když ve většině případů se jednalo o nějaký property file na classpath, kde Maven nahrazoval proměnné ${pom.artifactId} a ${pom.version}</li>
<li>s každou novou knihovnou / modulem to bylo nutné řešit znovu</li>
<li>díky výše uvedeným dvou bodům v několika knihovnách prostě přístup k verzím chyběl úplně</li>
</ul>
<h3>A pak přišla inspirace ...</h3>
<p>... jak jinak než ze zdrojových kódů Springu (konkrétně z <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/core/SpringVersion.html" target="_new">SpringVersion</a>). Při brouzdání jejich kódem na lovu naprosto jiné informace jsem narazil na velmi zajímavou deklaraci sestávající se z těchto dvou řádků:</p>
<p>[source lang="java"]<br />
Package pkg = someClass.getPackage();<br />
String version = (pkg != null ? pkg.getImplementationVersion() : "");<br />
[/source]</p>
<p>Na úrovni Java <a href="http://java.sun.com/j2se/1.5.0/docs/api/java/lang/Package.html" target="_new">Package</a> objektu jsou totiž dostupné některé informace, které se zapisují do souboru MANIFEST.MF ve složce META-INF každého JARu. Konkrétně se jedná o atributy:</p>
<p>[source:html]<br />
Specification-Title: Forms module<br />
Specification-Version: 2.0-SNAPSHOT<br />
Specification-Vendor: FG Forrest, a.s.<br />
Implementation-Title: Forms module<br />
Implementation-Version: 2.0-SNAPSHOT<br />
Implementation-Vendor: FG Forrest, a.s.<br />
[/source]</p>
<p>O vložení těchto atributů se samozřejmě musíte postarat. Ani Maven build ve svém standardním nastavení vám tyto atributy nepřidá. Nicméně po chvilce pátrání objevíte, že dostat je tam je velice prosté. V následujícím XML snippetu uvádím nastavení pro všechny standardní Java archívy (jar, war, ear):</p>
<p>[source lang="xml"]</p>
<plugin>
   <groupId>org.apache.maven.plugins</groupId><br />
   <artifactId>maven-jar-plugin</artifactId><br />
   <configuration><br />
      <archive><br />
         <manifest><br />
            <addDefaultImplementationEntries>true</addDefaultImplementationEntries><br />
            <addDefaultSpecificationEntries>true</addDefaultSpecificationEntries><br />
         </manifest><br />
      </archive><br />
   </configuration>
 </plugin>
<plugin>
   <groupId>org.apache.maven.plugins</groupId><br />
   <artifactId>maven-war-plugin</artifactId><br />
   <configuration><br />
      <archive><br />
         <manifest><br />
            <addDefaultImplementationEntries>true</addDefaultImplementationEntries><br />
            <addDefaultSpecificationEntries>true</addDefaultSpecificationEntries><br />
         </manifest><br />
      </archive><br />
   </configuration>
 </plugin>
<plugin>
   <groupId>org.apache.maven.plugins</groupId><br />
   <artifactId>maven-ear-plugin</artifactId><br />
   <configuration><br />
      <archive><br />
         <manifest><br />
            <addDefaultImplementationEntries>true</addDefaultImplementationEntries><br />
            <addDefaultSpecificationEntries>true</addDefaultSpecificationEntries><br />
         </manifest><br />
      </archive><br />
   </configuration>
</plugin>
[/source]</p>
<p>Pokud toto nastavení pluginu umístíte do firemních parent POM deklarací, nebude muset žádný z vašich kolegů tento problém řešit. Knihovny nebo moduly pak v sobě mohou obsahovat třídu podobnou té Springové, ale i pokud ji obsahovat nebudou, můžete kdykoliv danou verzi zjistit i zvenčí. Stačí vám k tomu znát třídu zevnitř dané knihovny (JARu) a přes reflexi se dostat na objekt Package a odtud verzi bez problémů zjistit.</p>
<p>Výše uvedený odstavec platí pouze pro MANIFEST.MF umístěný v JAR souborech. Přestože s pomocí správného nastavení war a ear pluginu se vám tyto informace promítnou i do manifestů umístěných v těchto archívech, přístup k informacím v těchto archívech již není tak přímočarý. Nicméně myslím, že v těchto případech lze problém vždycky obejít extrakcí těchto dat do vybraného JARu umístěného ve WARu či EARu.</p>
<p>Jiří Pressfreund v komentářích přidal i alternativní konfiguraci pro buildování Antem (díky ;-) ):</p>
<p>[source lang="xml"]<br />
<!–-<br />
**********************************************************************<br />
* Increase build number<br />
**********************************************************************<br />
--><br />
<target name="usage"></p>
<propertyfile file="${config.dir}/version.properties">
      <entry key="build.number" type="int" operation="+" value="1” pattern="00”/>
   </propertyfile>
</target></p>
<p><!–-<br />
**********************************************************************<br />
* Build JAR library<br />
**********************************************************************<br />
-–><br />
<target name="build" depends="compile, usage" description="Build library"><br />
   <tstamp/><br />
   <jar destfile="${dist.dir}/${ant.project.name}.jar"><br />
      <fileset dir="${build.classes.dir}"><br />
         <include name="**/*.*"/><br />
         <exclude name="**/*Test*.class"/><br />
      </fileset><br />
      <manifest><br />
         <attribute name="Built-By" value="${user.name}"/><br />
         <attribute name="Date" value="${TODAY}"/><br />
         <attribute name="Implementation-Version" value="Build ${major.number}.${minor.number}.${build.number}"/><br />
      </manifest><br />
   </jar><br />
</target><br />
[/source]</p>
<h3>Nestačí vám pouze informace o verzi?</h3>
<p>Pokud by vás zajímala informace o číslu buildu a ne pouze verzi knihovny (například pokud byste potřebovali rozeznat jeden SNAPSHOTový build od druhého), musíte jít ještě dál. Kdysi jsme zkoušeli <a href="http://mojo.codehaus.org/buildnumber-maven-plugin/" target="_new">Maven BuildNumber Plugin od Codehausu</a>, ale protože prozatím pořád používáme CVS mohli jsme využít pouze "offline" způsob generování build numberů, což při více vývojářích působilo víc problémů než užitku. Proto jsme si napsali vlastní plugin, který žádá o nové číslo buildu centrální server, kde je jednoduchý servlet přidělující nová čísla. Tím jsme schopni jednoduše zajistit unikátní čísla buildu i mezi více vývojáři.</p>
<p>Konfigurace našeho pluginu vypadá v pom.xml takto:</p>
<p>[source lang="xml"]</p>
<plugin>
	<groupId>com.fg.maven</groupId><br />
	<artifactId>maven-buildservice-plugin</artifactId><br />
	<version>1.0</version><br />
	<configuration><br />
	   <buildNumberServiceUrl>http://naseUrl</buildNumberServiceUrl><br />
	   <buildNumberMinimalValue>1</buildNumberMinimalValue><br />
	</configuration><br />
	<executions><br />
	   <execution></p>
<phase>validate</phase>
		  <goals><br />
			 <goal>create</goal><br />
		  </goals><br />
	   </execution><br />
	</executions>
 </plugin>
[/source]</p>
<p>Číslo buildu je potom možné také propagovat do manifestu. Stačí konfiguraci maven-jar-pluginu rozšířit takto:</p>
<p>[source lang="xml"]</p>
<plugin>
   <groupId>org.apache.maven.plugins</groupId><br />
   <artifactId>maven-jar-plugin</artifactId><br />
   <configuration><br />
      <archive><br />
         <manifest><br />
            <addDefaultImplementationEntries>true</addDefaultImplementationEntries><br />
            <addDefaultSpecificationEntries>true</addDefaultSpecificationEntries><br />
         </manifest><br />
         <manifestEntries><br />
            <Build-Number>${buildNumber}</Build-Number><br />
         </manifestEntries><br />
      </archive><br />
   </configuration>
</plugin>
[/source]</p>
<p>Čtení takovýchto custom dat už není tak jednoduché jako v případě verzí. K tomuto účelu už budeme muset najít a přečíst MANIFEST.MF sami. Abyste nemuseli dávat kód dohromady, uvádím ten náš:</p>
<p>[source lang="java"]<br />
/**<br />
 * Returns build number if it could be found - otherwise returns ? character.<br />
 * @param moduleClass<br />
 * @return<br />
 */<br />
public static String getBuildNumber(Class moduleClass) {<br />
   String buildNumber = "?";<br />
   try {<br />
      ClassLoader classLoader = Thread.currentThread().getContextClassLoader();<br />
      String className = moduleClass.getName().replaceAll("\\.", "/") + ".class";<br />
      if(log.isDebugEnabled()) {<br />
         log.debug("ClassName: " + className);<br />
      }<br />
      URL resource = classLoader.getResource(className);<br />
      if (resource != null) {<br />
         String path = resource.getPath();<br />
         if(log.isDebugEnabled()) {<br />
            log.debug("Path to class: " + path);<br />
         }<br />
         int index = path.indexOf("!");<br />
         if (index > -1) {<br />
            String jarPath = path.substring(0, index);<br />
            if (jarPath.startsWith("file:")) {<br />
               jarPath = jarPath.substring(5);<br />
            }<br />
            if(log.isDebugEnabled()) {<br />
               log.debug("Normalized path to jar: " + jarPath);<br />
            }<br />
            JarFile jar = new JarFile(jarPath);<br />
            Manifest manifest = jar.getManifest();<br />
            buildNumber = manifest.getMainAttributes().getValue("Build-Number");<br />
         }<br />
      }<br />
   } catch (Exception ex) {<br />
      log.error("Build number cannot be found! Due to: " + ex.getMessage(), ex);<br />
   }<br />
   return buildNumber;<br />
}<br />
[/source]</p>
<p>Nuže a to je všechno. Vyřešili jsme další rutinní nepříjemnost vývoje.</p>
<h2>Užitečné odkazy</h2>
<ul>
<li><a href="http://maven.apache.org/plugins/maven-jar-plugin/examples/manifest-customization.html" target="_new">Dokumentace Maven JAR pluginu v otázce Manifestu</a></li>
<li><a href="http://maven.apache.org/plugins/maven-war-plugin/examples/war-manifest-guide.html" target="_new">Dokumentace Maven WAR pluginu v otázce Manifestu</a></li>
<li><a href="http://java.sun.com/developer/Books/javaprogramming/JAR/basics/manifest.html" target="_new">Krátké shrnutí významu a obsahu MANIFEST.MF souboru</a></li>
<li><a href="http://java.sun.com/j2se/1.5.0/docs/guide/jar/jar.html" target="_new">Podrobný rozbor MANIFEST.MF souboru</a></li>
<li><a href="http://www.rgagnon.com/javadetails/java-0388.html" target="_new">Tipy pro přístup k datům v MANIFEST.MF z Java kódu</a></li>
<li><a href="http://www.jdocs.com/spring/2.0.6/org/springframework/core/SpringVersion.html" target="_new">Kód SpringVersion class, kde jsem se inspiroval</a></li>
<li><a href="http://mojo.codehaus.org/buildnumber-maven-plugin/" target="_new">Maven BuildNumber Plugin od Codehausu</a></li>
</ul>
