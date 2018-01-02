---
status: publish
published: true
title: WebExpo 2010 - sobota
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Sobotní den mi zlepšil včerejší pocit z WebExpa poměrně radikálně. Dnes
  jsem měl více méně štěstí na přednášky, takže jsem většinu dne strávil podle mého
  vkusu. Organizační část se nijak výrazně nezlepšila, nicméně co se týká složení
  programu a osobnostní v něm, musím pochválit. Navíc se mi po letech \"poštěstilo\"
  ochutnat onen klasický rozblemcaný školní špenát, což je zážitek, na který budu
  zase hodně dlouho zapomínat. Ráno začalo poměrně vlažně přednáškou o <b>Continuous
  delivery</b>, ve které jsem si myslel, že se dozvím něco víc o závěrečné části -
  tedy o té \"delivery\". Bohužel Aleš Roubíček rozebral pouze základní principy CI,
  které jsou erudovanější části IT publika známé už nějaký ten pátek.\r\n\r\nHned
  druhá přednáška se však rozjela k mé spokojenosti - Jakub Nešetřil v ní rozebíral
  <b><a href=\"http://nodejs.org/\" target=\"_blank\">Node.js</a></b>. Ačkoliv by
  si člověk pod tímto názvem představil nějakou JavaScriptovou utility knihovnu běžící
  v prohlížeči, jedná se o převážně serverové řešení. Tj. Node.js je interpretované
  na serveru (je použit <a href=\"http://code.google.com/p/v8/\" target=\"_blank\">Google
  V8 JavaScript engine</a> se všemi cukrátky jako je kompilace zdrojových kódů, hotspot
  atd.) a v podstatě by se dalo nejblíže asi přirovnat k Ruby. \r\n\r\n"
wordpress_id: 1114
wordpress_url: http://blog.novoj.net/?p=1114
date: '2010-09-25 21:54:35 +0200'
date_gmt: '2010-09-25 20:54:35 +0200'
categories:
- Reportáže
- WebExpo
tags:
- webexpo
comments: []
---
<p>Sobotní den mi zlepšil včerejší pocit z WebExpa poměrně radikálně. Dnes jsem měl více méně štěstí na přednášky, takže jsem většinu dne strávil podle mého vkusu. Organizační část se nijak výrazně nezlepšila, nicméně co se týká složení programu a osobnostní v něm, musím pochválit. Navíc se mi po letech "poštěstilo" ochutnat onen klasický rozblemcaný školní špenát, což je zážitek, na který budu zase hodně dlouho zapomínat. Ráno začalo poměrně vlažně přednáškou o <b>Continuous delivery</b>, ve které jsem si myslel, že se dozvím něco víc o závěrečné části - tedy o té "delivery". Bohužel Aleš Roubíček rozebral pouze základní principy CI, které jsou erudovanější části IT publika známé už nějaký ten pátek.</p>
<p>Hned druhá přednáška se však rozjela k mé spokojenosti - Jakub Nešetřil v ní rozebíral <b><a href="http://nodejs.org/" target="_blank">Node.js</a></b>. Ačkoliv by si člověk pod tímto názvem představil nějakou JavaScriptovou utility knihovnu běžící v prohlížeči, jedná se o převážně serverové řešení. Tj. Node.js je interpretované na serveru (je použit <a href="http://code.google.com/p/v8/" target="_blank">Google V8 JavaScript engine</a> se všemi cukrátky jako je kompilace zdrojových kódů, hotspot atd.) a v podstatě by se dalo nejblíže asi přirovnat k Ruby. </p>
<p><a id="more"></a><a id="more-1114"></a></p>
<p>Node.js má vlastní implementaci pro web server a vytváří se kolem něj rodina základních knihoven a nástrojů. Jedním ze základních stavebních kamentů je asynchronicita vztažená především k non-blocking IO. Z tohoto důvodu museli autoři dokonce přepsat některé Linuxové služby jako je DNS lookup, která je v původní verzi synchronní a tedy blokující. Všechny IO operace byly přepsány jako asynchronní (tj. akceptují jako svůj parametr funkci - closure, která je zavolána ve chvíli, kdy jsou odpovídající data k dispozici). Utilizaci non-blocking IO v Javě nějaký ten pátek už známe a výkonnostní výhody jsou zřejmé. Je to především výkonnostní aspekt, kterým se Node.js chlubí - a musím uznat, že <a href="http://zgadzaj.com/benchmarking-node-js-testing-performance-against-apache-php/" target="_blank">některá měření</a> jsou skutečně ohromující. Zajímavý je i způsob debugování aplikací - na serveru se rozjede debugovací server, který posílá informace pro developer konzoli v Google Chrome - breakpointy, evaluace a další věci fungují stejně, jako byste debugovali kód běžící na klientovi. Ačkoliv je projekt ještě velmi mladý a, i podle Jakuba N., obsahuje ještě velké množství nevychytaných věcí, formuje se kolem něj velmi aktivní komunita a dynamicky se rozvíjí. Na jednu stranu nejsem fanda nových ekosystémů, které si vše budují znova od nuly, ale v tomto případě chápu důvody, které k tomu vedou. Jako zcela přirozenou se mi zdá kombinace Node.js s CouchDb, jelikož tyto dva systémy mají k sobě velmi blízko. Rozhodně stojí za to dění kolem Node.js nadále sledovat.</p>
<ul>
<li><a href="http://www.slideshare.net/jakub.nesetril/introduction-to-nodejs-5284527" target="_blank">Přednáška Jakuba Nešetřila</a></li>
<li><a href="http://www.slideshare.net/the_undefined/nodejs-a-quick-tour" target="_blank">Rychlý průvodce Node.js od jiného autora</a></li>
<li><a href="http://zdrojak.root.cz/clanky/node-js-s-javascriptem-na-server/" target="_blank">Článek na Root.cz</a></li>
</ul>
<p>Před obědem jsem navštívil session <b>Beyond Agile</b> Andrea Provaglia. Ačkoliv management a psychologie, není zrovna můj šálek kávy, v podání Andrea Provaglia jsou psychologické poučky a postřehy o sociálním chování skupin velmi zajímavé a zábavné. Z celé přednášky bych vypíchl jen několik myšlenek, které mne nejvíc oslovily (snad je budu interpretovat správně). </p>
<p>Obvykle se k řízení používá metoda cukr a bič - je to praktika lidstvu známá celá staletí. V IT průmyslu však může být tato praktika méně produktivní než prostý zápal samo-organizujících se lidí. Skupina lidí motivovaná cukrem (odměny, bonusy) může svou motivaci z uspokojení ze své práce (seberealizace) přenést na motivaci získat slibovaný cukr. Ve chvílích, kdy cukr není v dohledu, naopak daná skupina vykazuje výrazně horší výkony, než skupina "nemotivovaná". Další poměrně zásadní myšlenka přednášky je respekt vůči individualitám ve skupině a přirozeným vztahům, které v ní panují. Historicky je vlivnost členů skupiny ovlivňována 3-mi faktory:</p>
<ol>
<li>stáří (seniorita) - starší členové skupiny jsou váženější (mají vliv) než ti mladší - porovnejte třeba se stařešinami v kmenovém uspořádání</li>
<li>odpovědnost - členové skupiny, kteří na sebou berou větší odpovědnost mají opět i větší vliv ve skupině jako takové - v kmenovém uspořádání bych danou roli přirovnal např. k matkám pečující o provozní chod kmene</li>
<li>schopnost - členové s většími znalostmi / silou / průrazností opět přirozeně dosahují většího vlivu - v kmenovém uspořádání tuto roli zastupují nejlepší válečníci a lovci</li>
</ol>
<p>Tyto faktory hrají roli v zařazení členů ve skupině a přirozeně působí v samo-organizačním procesu skupiny. Z hlediska managementu je třeba na toto přirozené uspořádání brát ohled a, spíše než se jej pokoušet měnit, jej ke své potřebě využívat. V případech, kdy musíme zásadně do tohoto uspořádání zasáhnout (např. převést schopného leadera skupiny někam jinam), je třeba to dělat velmi citlivě a vyhnout se rychlých změn. Je třeba nechat skupině čas se adaptovat na nový stav.</p>
<p>Po obědě jsem zavítal na prezentaci Víta Vrby z <a href="http://www.webnode.cz" target="_blank">WebNode.com</a> <b>Jak vybudovat úspěšný Internetový startup?</b> v business tracku a chybu jsem neudělal. Vít Vrba je především skvělý prezentátor, který dokáže zaujmout publikum nejen tématem, ale i vystupováním a chytlavými "claimy". V přednášce defakto zboural všechna pravidla, které jsem v souvislosti se startupy dosud slyšel:</p>
<ul>
<li>kašlete na konkurenci - uspět se dá i na sebeobsazenějším trhu</li>
<li>kašlete na investory - uspět můžete i s minimem financi, to že rejete čumákem v hlíně má nakonec pozitivní efekt na to, co děláte (vývoj WebNode financovali z ostatních příjmů na "standardních" projektech)</li>
<li>globální business se dá rozjet s nulovými náklady na primární marketing (když vše založíte na chytrém virálním marketingu)</li>
<li>pro získání potřebné popularity nepotřebujete peníze na reklamu, ale ten správný příběh, který prodáte novinářům</li>
<li>unikátní řešení je výhodou, ale bez kopírování se neobejdete - a když kopírujete, kopírujte dobře (snažte se okopírovat myšlenky, ne chování)</li>
<li>dělejte jen základní business plán - stejně ho ve chvíli, kdy ho doděláte, budete chtít změnit</li>
</ul>
<p>Naopak potvrdil několik pravidel, které se mezi těmy obecně známými vyskytují:</p>
<ul>
<li>dělej co tě baví, peníze přijdou - a když ne, alespoň jsi se dobře bavil :-D LOL</li>
<li>začni hned a nečekej do chvíle, než to bude dokonalé (to nebude nikdy)</li>
<li>stav na kvalitním týmu lidí, kteří sdílejí stejnou vizi</li>
<li>projekty s velkou návštevností jdou monetizovat -  i když z celkového množství uživatelů platí třeba jen 0.5 - 7.5% uživatelů</li>
<li>v globálním světe nezapomeňte respektovat lokální odlišnosti - tím byste si mohli uzavřít jednotlivé potenciální trhy</li>
<li>neustále inovujte na základě kontaktu s uživateli a sledováním konkurence</li>
<li>buďte originální a odvážní</li>
</ul>
<p>Hmm, moc hezky se to poslouchá z úst někoho, komu to vyšlo. Faktem ovšem zůstává, že těch, kterým to nevyjde je pořád kolem 80%.</p>
<p>Celý můj odpolední blok se pak už věnoval "businessu". Vlasta Pokladníková ve stejné místnosti přednášela o <b>Roli venture kapitálu v úspěšných rozvíjejících se startupech pohledem ze Silicon Valley</b>, což bylo zajímavé především pohledem z druhé strany. Rozebrala, které faktory z hlediska investora hrají důležitou roli, kdy se startupu vyplatí a kdy nevyplatí hledat svého investora. Kdyby nebylo špatného ozvučení v sále, byla by pravděpodobně přednáška nabitá - bohužel v tomto ohledu organizace opět zakulhala.</p>
<p>Den jsem uzavřel účastí na Startup show, ve které o přízeň "investorů" po vzoru pořadu Den D soutěžily 4 startup projekty: </p>
<ul>
<li><a href="http://nicereply.com/" target="_blank">Nice-reply</a> - velmi jednoduchá a sympatická služba pro hodnocení Support oddělení</li>
<li><a href="http://www.superscout.com/" target="_blank">SuperScout</a> - portál pro hledání / nabízení pracovních příležitostí v IT, podobný jobs.cz obohacený o sociální aspekty</li>
<li><a href="http://www.hotgloo.com/" target="_blank">HotGloo</a> - on-line služba pro tvorbu wire-framů</li>
<li><a href="http://www.bijk.com/" target="_blank">Bijk.com</a> - on-line monitoring serverů a služeb na nich běžících</li>
</ul>
<p>Setkání startupy s investory bylo pro mě osobně velmi zajímavé. Musím uznat, že každá z uvedených služeb vypadala na první pohled vizuálně dobře a, krom českého zastoupení (Bijk), které mělo trošku potíže s angličtinou, bylo vystoupení všech zúčastněných na velmi profesionální úrovni. Služby HotGloo a Bijk.com si ve firmě určitě ještě trošku proťukneme. Klání nakonec dle očekávání (možná díky předpojatosti českého publika) vyhrál Bijk.com.</p>
<h3>Shrnutí</h3>
<p>Moje pocity jste asi z obou dvou článků již vycítili. Nejslabší článek na letošním WebExpu byla dle všeho (čerpám i z pocitů ostatních na Twitteru) organizace. Pravda je, že zvládnout 1000 návštěvníků není zase tak jednoduché, ale některé věci by měly být na 3. ročníku již vychytané. Z hlediska informačního odcházím velmi spokojen, přínos versus náklady je v mém případě rozhodně v plusu. Na to, že se jedná o lokální českou konferenci, bylo možné setkat se s některými velmi zajímavými lidmi a technologiemi. WebExpo, myslím, stojí rozhodně za návštěvu i další rok a věřím, že si organizátoři sáhnou trošku do svědomí (tedy projdou Twitter ;-) ) a příští rok už vše proběhne hladce.</p>
