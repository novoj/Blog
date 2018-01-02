---
status: publish
published: true
title: 'jOpenSpace 2008 – Audio #2'
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Není se třeba obávat, že by můj zájem o publikaci přednášek z jOpenSpace
  2008 zveřejněním té mé ochladl. Ba naopak - předkládám Vám druhou várku záznamů
  a ještě nás čeká jedna várka, na kterou se můžete do konce roku těšit.\r\n\r\nPro
  úplnost ještě uvádím odkaz na předchozí záznamy:\r\n<ul>\r\n\t<li><a href=\"http://blog.novoj.net/2008/08/31/jopenspace-2008-audio-1/\">Audio
  #1</a></li>\r\n</ul>\r\n"
wordpress_id: 113
wordpress_url: http://blog.novoj.net/?p=113
date: '2008-10-19 07:54:16 +0200'
date_gmt: '2008-10-19 06:54:16 +0200'
categories:
- Java
- Podcast
- Reportáže
- jOpenSpace
tags: []
comments: []
---
<p>Není se třeba obávat, že by můj zájem o publikaci přednášek z jOpenSpace 2008 zveřejněním té mé ochladl. Ba naopak - předkládám Vám druhou várku záznamů a ještě nás čeká jedna várka, na kterou se můžete do konce roku těšit.</p>
<p>Pro úplnost ještě uvádím odkaz na předchozí záznamy:</p>
<ul>
<li><a href="http://blog.novoj.net/2008/08/31/jopenspace-2008-audio-1/">Audio #1</a></li>
</ul>
<p><a id="more"></a><a id="more-113"></a></p>
<h3>Lightning Talk - Using Spring in large applications, Roman Pichlík</h3>
<p>V této přednášce Dagi popisuje zkušenost s nasazením (a používáním) Spring Frameworku na velkém projektu v Hewlett-Packard. Velkým projektem se rozumí projekt složený z cca. 150 Maven subprojektů = 150 aplikačních kontextů, na kterém pracuje cca 40 vývojářů. Od šesté minuty se probírá zajímavý problém skládání velkého množství aplikačních kontextů Springu, na toto téma navazují já ve 13 minutě s narážkou na řešení popsané v <a href="http://blog.novoj.net/2007/09/08/serial-modularni-systemy-ve-spring-frameworku/">seriálu o modulárních systémech ve Springu</a>. Od 11 minuty se diskutuje o problematice autowiringu na velkých projektech. Po 15 minutě se naráží na použitelnost OSGI v J2EE projektech a obecně o rychlosti adopce nových Java standardů u velkých zákazníků. Po 20 minutě se probírají problémy vendor descriptorů a způsob instalace takto velké aplikace u různých zákazníků.</p>
<p>Zkraje je kvalita záznamu dobrá, v prostřední části se výrazně zhoršuje, aby se ke konci opět dostala na relativně rozumnou úroveň. Diskuse je nicméně zajímavá, takže snad někteří z vás vydrží až do konce.</p>
<p><a title="MP3 Podcast" href="http://jopenspace.cz/audio/06_Spring_in_large_applications.mp3"><img style="margin-right: 10px" title="MP3 Podcast" src="http://files.novoj.net/button_mp3.png" alt="MP3 Podcast" align="left" /></a> <a title="MP3 Podcast" href="http://jopenspace.cz/audio/06_Spring_in_large_applications.mp3"><strong> Podcast</strong></a> [43:27] 10,4 MB</p>
<p><a title="Presentation slides" href="http://jopenspace.cz/data/spring_adoption_in_large_enterprise_project.pdf"><img style="margin-right: 10px" title="Slidy" src="http://files.novoj.net/button_pdf.png" alt="Slidy prezentace" align="left" /></a> <a title="Slidy prezentace" href="http://jopenspace.cz/data/spring_adoption_in_large_enterprise_project.pdf"><strong> Slidy prezentace ve formátu PDF</strong></a></p>
<h3>Open Space Talk - Java vs. dynamické jazyky, Jan Štěrba</h3>
<p>Tato session se zaměřuje na porovnání Javy a programování v dynamických jazycích - např. Ruby (JRuby), Groovy, Python (Jython) a dalších.</p>
<p>Na začátku (1:47) je shrnutí obou přístupů, statické vs. Dynamické jazyky. Účastníci hovoří o svých zkušenostech a vyjadřují vlastní názory na dynamické jazyky:</p>
<p><strong>Názory na výhody dynamických jazyků</strong></p>
<ul>
<li>Lépe se v tom programuje</li>
<li>Jedná se o rozdíl v myšlení oproti Java (3:30)</li>
<li>Pozitivem je zjednodušení kódu (Dagi, 7:20), ale existují i negativa (Dagi, 14:30)</li>
<li>Díky novějšímu datu vzniku je lepší API (JŠ)</li>
<li>Vhodné použít proto, že mohou být víc lightweight a mít nižší nároky na HW než Java (python) (6:08) O rychlosti python vs Java též kolem 21:50, včetně porovnání run-time enginů.</li>
<li>Vyšší produktivita práce (23:00)</li>
</ul>
<p><strong>Názory na nevýhody dynamických jazyků</strong></p>
<ul>
<li>Problémem je chybějící úplná code completion (4:40)</li>
<li>Horší dokumentace oproti dokonalým Javadocům Java API (JŠ)</li>
<li>chybí refaktorizace a compile-time validace (PJ, 23:30)</li>
<li>Pokud vývojář začne rovnou v dynamickém jazyku bez znalosti Javy, hrozí riziko špatného kódu (29:30 a 35:00). V té souvislosti o nesporné důležitosti automatických testů při vývoji v dynamických jazycích (31:40), o snadnější cestě k vytvoření nesrozumitelného, špatného kódu oproti statickým jazyků.</li>
<li>O nedostatku znalostí v týmu v oblasti dynamických jazyků (33:20)</li>
</ul>
<p>V střední části se diskutovalo, kdy je vhodné dynamický přístup použít (5:40 a též ještě 25:45). Zmínily se dynamické frameworky - Ruby on rails (10:10) a Groovy (29:00), též jak je to s adaptací Java programátora na Groovy (11:20).</p>
<p>Další témata byla:</p>
<ul>
<li>Jak se řeší v dyn. jazycích změna třídy za run-time (13:30)</li>
<li>Doporučení pro přístup k definování nových dynamických metod v dyn. Jazyku<br />
Je vhodné neměnit chování metod při běhu aplikace, jen při jejím startování (16:50)<br />
O JQuery a nebezpečí dynamičnosti při předefinovávání chování existujících metod za běhu (pomocí pluginů, 19:07).</li>
<li>Možnost využít dynamické jazyky pro prototypování modulů, které se později přepíšou do Javy (26:45)</li>
</ul>
<p>V poslední části se probíralo, jaké jsou rozdíly mezi objektovým a procedurálním přístupem (36:45) a jak nechat inspirovat Javu příjemnými vlastnostmi co se týče syntaxe a API mladších dynamických jazyků (37:40). Hovořilo se o technologických limitech Javy, bránících zavedení některých novinek a o templates v Cčku v porovnání s řešením v Java (40:10).</p>
<p>Zmínil se .NET (41:34) a Java 3.0 (42:10). Podrobněji se probraly některé konstrukty v Javě - Comparable, pole vs. Collections (43:00), primitivní datové typy (např. int) vs objektové alternativy (např. Integer) (46:00) a jak jsou primitivní typy optimalizovány v Smalltalku (48:00). Diskuze se ukončila zmínkou o využití Rhino pro automatické generování formulářů (51:00).</p>
<p><a title="MP3 Podcast" href="http://jopenspace.cz/audio/07_Java_vs_dynamicke_jazyky.mp3"><img style="margin-right: 10px" title="MP3 Podcast" src="http://files.novoj.net/button_mp3.png" alt="MP3 Podcast" align="left" /></a> <a title="MP3 Podcast" href="http://jopenspace.cz/audio/07_Java_vs_dynamicke_jazyky.mp3"><strong> Podcast</strong></a> [54:26] 16,3 MB</p>
<h3>Lightning Talk - Grid &amp; Cloud Computing, Lukáš Kolísko</h3>
<p>Tento záznam zachycuje přednášku na téma cloud computingu. Lukáš Kolísko v něm osvětluje základy této problematiky s vazbou na projekt EU <a href="http://www.reservoir-fp7.eu/" target="_new">Reservoir</a> (Resources and Services Virtualization without Barriers), na němž se jeho tým podílí. Přednáška rozebírá základní problémy spojené s virtualizací a cloud computingem. Od 7 minuty se Lukáš zabývá tzv. business service managementem - tedy zpoplatnění služby uvnitř cloudu s ohledem na měřitelnost spotřeby služby. Od 11 minuty se zabývá optimalizací jednotek v gridech - tato část je bez slidů, pouze z audia obtížně pochopitelná. Od 19 minuty naráží Lukáš na možnosti migrací Java aplikací mezi jednotkami gridu - což je část, kteoru se právě zabývá jeho tým. Po 32 minutě začínají Q&amp;A.</p>
<p>Nahrávka není v ideální kvalitě nicméně při dobře nastavené hlasitosti by mělo být rozumět všemu. Kvalita je v průběhu záznamu víceméně konstantní.</p>
<p><a title="MP3 Podcast" href="http://jopenspace.cz/audio/08_Grid_and_Cloud_Computing.mp3"><img style="margin-right: 10px" title="MP3 Podcast" src="http://files.novoj.net/button_mp3.png" alt="MP3 Podcast" align="left" /></a> <a title="MP3 Podcast" href="http://jopenspace.cz/audio/08_Grid_and_Cloud_Computing.mp3"><strong> Podcast</strong></a> [44:42] 10,7 MB</p>
<h3>Lightning Talk - AndroMDA / Enterprise Architect, Petr Ferschmann, Pavel Petřek</h3>
<p>Tento záznam obsahuje dvojpřednášku Petra Ferschmanna a Pavla Petřeka o zkušenostech z použití MDA přístupu při tvorbě aplikací. Oba se kupodivu shodují na závěru, že přínosy použití <a href="http://en.wikipedia.org/wiki/Model-driven_architecture" target="_new">MDA</a> v reálné praxi jsou přinejmenším diskutabilní. Přednášku začíná Petr s popisem nástroje AndroMDA. Ve 3 minutě popisuje Petr motivaci pro použití MDA. V jejich případě se jednalo především na použití MDA pro datovou vrstvu aplikace. Po 8 minutě se lehce naráží na zkušenosti s nástroji ArgoUML, Poseidon. V 10 minutě rozebírá Petr základní princip pro použití MDA při jednosměrné konverzi Model -&gt; Kód. Tedy, že z modelu jsou generováni abstraktní předci tříd, ze kterých programátor dědí třídy, do kterých teprve umisťuje aplikační logiku. Při přegenerování jsou potom přepisovány pouze abstraktní předci a implementace zůstává netknutá. V 14 minutě se poprvé naráží na výhody / nevýhody MDA přístupu. Od 20 minuty se strhává diskuse nad jednotlivými problémy.</p>
<p>V 31 minutě začíná druhá část přednášky v podání Pavla Petřeka. Ten popisuje zkušenosti s Enterprise Architectem. V 37 minutě se probírá problematika verzování datového modelu a generování ALTER skriptů mezi verzemi. Po 40 minutě se Pavel věnuje shrnutí jejich zkušeností. Vyžaduje to vyšší nároky na team, přináší to celou řadu nových problémů k řešení, což přínosy tohoto přístupu nevyváží. Po 46 minutě popisuje Pavel použití MDA na generování komunikačního protokolu s LDAPem, s čímž udělal naopak poměrně pozitivní zkušenost.</p>
<p>V závěru se oba přednášející shodují na tom, že MDA odkrývá konflikt mezi světem vývojáře a analytika a ve výsledku jde jen o to, zda-li chceme vyhovět více analytikovi (MDA analytikovi pomáhá) nebo vývojářovi (MDA vývojářovi zesložiťuje práci).</p>
<p>Kvalita tohoto záznamu je na rozumné úrovni - je rozumět relativně všemu. Rozhodně doporučuji k poslechnutí všem, kteří koketují s MDA.</p>
<p><a title="MP3 Podcast" href="http://jopenspace.cz/audio/10_MDA_AndroMDA_a_EnterpriseArchitect.mp3"><img style="margin-right: 10px" title="MP3 Podcast" src="http://files.novoj.net/button_mp3.png" alt="MP3 Podcast" align="left" /></a> <a title="MP3 Podcast" href="http://jopenspace.cz/audio/10_MDA_AndroMDA_a_EnterpriseArchitect.mp3"><strong> Podcast</strong></a> [59:07] 14,2 MB</p>
<p><a title="Presentation slides" href="http://jopenspace.cz/data/andromda.zip"><img style="margin-right: 10px" title="Slidy" src="http://files.novoj.net/button_zip_slides.gif" alt="Slidy prezentace" align="left" /></a> <a title="Slidy prezentace" href="http://jopenspace.cz/data/andromda.zip"><strong> Slidy prezentace ve formátu HTML</strong></a></p>
<h3>Lightning Talk - Repetitive Strain Injury, Pavel Jetenský</h3>
<p>Tento záznam je z předposlední session sobotního večera. Přednáškou se prolínal již úvod do další, kterou byla ochutnávka moravských vín v podání Petra Adámka! Proto je nálada a poznámky v průběhu této přednášky daleko veselejší. RSI je problém, které se týká všech programátorů - jedná se o nemoc z opakovaného, monotónního pohybu (např. strnulé sezení s psatní na klávesnici). RSI je spojená s CPS, což je zánět karpálního tunelu. Oba tyto pojmy jsou vysvětleny hned zkraje přednášky. Ve 3 minutě jsou popsány syndromy. Po 8 minutě Pavel popisuje způsob prevence. Po 23 minutě se strhává živá diskuse, která dále volně přechází v degustaci vín.</p>
<p>Záznam je poměrně často prokládán hlasitým smíchem a proto doporučuji nastavit hlasitost na rozumnou úroveň. Z textu je rozumět takřka všemu.</p>
<p>Pro tuto přednášku Pavel připravil i <a href="http://jetensky.net/blog/2008/10/17/jak-predejit-a-resit-bolest-v-zapesti-zkusenosti-programatora/" target="_new">speciální post</a>, který je dostupný na jeho blogu. Zde jsou také další články, materiály a odkazy, které se této problematiky dotýkají.</p>
<p><a title="MP3 Podcast" href="http://jopenspace.cz/audio/11_Repetitive_Strain_Injury.mp3"><img style="margin-right: 10px" title="MP3 Podcast" src="http://files.novoj.net/button_mp3.png" alt="MP3 Podcast" align="left" /></a> <a title="MP3 Podcast" href="http://jopenspace.cz/audio/11_Repetitive_Strain_Injury.mp3"><strong> Podcast</strong></a> [38:00] 9,1 MB</p>
<p><a title="Presentation slides" href="http://jopenspace.cz/data/problemy_se_zapestim_pri_praci_s_PC.ppt"><img style="margin-right: 10px" title="Slidy" src="http://files.novoj.net/button_ppt.png" alt="Slidy prezentace" align="left" /></a> <a title="Slidy prezentace" href="http://jopenspace.cz/data/problemy_se_zapestim_pri_praci_s_PC.ppt"><strong> Slidy prezentace ve formátu MS Power Point</strong></a></p>
<p><a title="Videocast" href="http://jetensky.net/download/files/Problemy%20se%20zapestim%20pri%20praci%20s%20PC.swf"><img style="margin-right: 10px" title="Slidy" src="http://files.novoj.net/button_swf.png" alt="Videocast" align="left" /></a> <a title="Videocast" href="http://jetensky.net/download/files/Problemy%20se%20zapestim%20pri%20praci%20s%20PC.swf"><strong> Videocast</strong></a></p>
<div align="center">###</p>
<p>Kompletní itinerář konference, rozcestník a materiály jsou k dispozici na<br />
<a href="http://jopenspace.cz/" target="_new&quot;">http://jopenspace.cz/</a></p>
<p>###</p></div>
<p><strong>V podcastech byla použita hudba:</strong><br />
<a href="http://magnatune.com/artists/albums/magnacomp-sampler/">Burning Babylon</a>, Roots Fi Cool (<a href="http://magnatune.com/" target="_blank">http://magnatune.com</a>) publikováno pod Creative Commons License</p>
<div style="margin-bottom: 30px">
<img title="Creative Commons - Some Rights Reserved" src="http://he3.magnatune.com/img/somerights2.gif" alt="Creative Commons - Some Rights Reserved" align="right" /></p>
<p><strong>Podcast Licence: </strong><a href="http://creativecommons.org/licenses/by-nc-sa/1.0/" target="_blank"> Creative Commons</a>
</div>
<p><i><strong>Poděkování: </strong>Za pomoc při zpracování tohoto postu děkuji Pavlu Jetenskému, který se postaral o část tranksriptů.</i></p>
