---
status: publish
published: true
title: jQuery effects - quick start
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "V <a href=\"http://blog.novoj.net/2008/11/07/javascript-closures-prekvapeni-java-programatora/\">minulém
  článku</a>, ve kterém jsem se zabýval JavaScript Closures, jsem se zmiňoval o tom,
  že mě k jejich studiu donutilo používání efektů z knihovny jQuery. Také jsem sliboval,
  že o svých zkušenostech něco málo napíšu v dalším článku. Nuže směle do toho.\r\n\r\njQuery
  je obecná knihovna obalující odlišné implementace (více než odlišnosti jazyka, míním
  odlišnosti práce s DOM reprezentací) JavaScriptu v běžně používaných prohlížečích.
  Efekty jsou pouze její minoritní částí, kterou možná většina vývojářů pracujících
  s jQuery ani nevyužívá. Jelikož jsem hračička, koketoval jsem s efekty už od první
  chvíle, kdy jsem s jQuery začal. Z globálního pohledu musím říct, že mě překvapuje,
  že tyto efekty fungují velmi dobře skrze všechny podporované prohlížeče a kupodivu
  jsou poměrně svižné i na pomalejších počítačích (pomalejšími mám na mysli, průměrný
  počítač koupený před 3-4 lety). Základní použití je velmi jednoduché a zvládne ho
  i člověk, který s JavaScriptem a jQuery teprve začíná. Kromě  <a href=\"http://docs.jquery.com/Effects\"
  target=\"_blank\">základních efektů</a> dodávaných přímo jako součást jQuery Core
  (show, hide, toggle, fadeIn, fadeOut, animate), je k dispozici ještě oficiální dodatečná
  knihovna s widgety a dalšími effekty známá jako <a href=\"http://docs.jquery.com/UI#Effects\"
  target=\"_blank\">jQuery UI</a> (zde najdete řadu dalších pěkných efektů, které
  byly kdysi součástí js knihovny interface.js).\r\n\r\nPokud máte zájem o to shlédnout
  některé z animací, které jsme pro naše zákazníky vytvořili, zde nabízím pár odkazů:\r\n\r\n<ul>\r\n
  \  <li>\r\n\t\t<a href=\"http://www.moje-firma.cz/srv/www/consultation/newQuery.x\"
  target=\"_blank\">Moje Firma</a> - web Komerční Banky zaměřený na podnikatelskou
  sféru\r\n\t\t<ul>\r\n\t\t   <li>v části podnikatelská poradna jsme využili efekty
  k odeslání formuláře s daty na server bez reloadu celé stránky, efekt si můžete
  bez následků vyzkoušet pokud se pokusíte odeslat prázdný formulář - výsledkem bude
  animace, která vám zobrazí chyby, které ve skutečnosti generuje server v odpovědi
  na odeslání formuláře (žádné JS kontroly ;-) )<br> <b>Update 29.10.2010</b> Odkaz
  již není funkční</li>\r\n\t\t</ul>\r\n   </li>\r\n   <li>\r\n\t\t<a href=\"http://www.trotina.cz\"
  target=\"_blank\">TROTINA AUTO, s.r.o.</a> - stránky prodejce ojetých vozidel ve
  Východních Čechách\r\n\t\t<ul>\r\n\t\t   <li>vyzkoušejte si třeba vložit pár vozidel
  na parkoviště, vybrat ve vyhledávání terénní vozidla, v detailu vozidla odeslat
  doporučení příteli apod.</li>\r\n\t\t   <li>kapitolou samou o sobě je potom <a href=\"https://www.trotina.cz/srv/www/auction/homepage.do\"
  target=\"_blank\">Dražba na ruby</a>, kterou si můžete vyzkoušet je v případě, že
  je nějaká aktuálně vypsaná - zde se veškerá logika aplikace odehrává v podstatě
  jen na dvou obrazovkách a zbytek je řešen AJAXem s využitím jQuery efektů</li>\r\n\t\t</ul>\r\n
  \  </li>\r\n</ul>\r\n\r\n"
wordpress_id: 236
wordpress_url: http://blog.novoj.net/?p=236
date: '2009-01-04 14:00:31 +0100'
date_gmt: '2009-01-04 13:00:31 +0100'
categories:
- Programování
- Web
- JavaScript
tags:
- jQuery
comments:
- id: 5744
  author: benzin
  author_email: bendal@quick.cz
  author_url: http://live.jabbim.cz/benzin
  date: '2009-01-05 09:10:45 +0100'
  date_gmt: '2009-01-05 08:10:45 +0100'
  content: Super diky. To mne presvedcilo ze to zacnu pouzivat. Dotedka sem si podobne
    veci sem si skriptil sam, ale tohle je fakt super.
- id: 5760
  author: kubino
  author_email: kubino@gmail.com
  author_url: ''
  date: '2009-01-05 21:19:33 +0100'
  date_gmt: '2009-01-05 20:19:33 +0100'
  content: Super clanek diky, zrovna delam s JQuery a kvalitnich prikladu neni nikdy
    dost.
- id: 5766
  author: srakyi
  author_email: srakyi@gmail.com
  author_url: http://srakyi.modry.cz/blog
  date: '2009-01-06 12:33:15 +0100'
  date_gmt: '2009-01-06 11:33:15 +0100'
  content: Ja jsem na podobne efekty pouzival Scriptaculous (http://script.aculo.us),
    ale tohle rozhodne vyzkousim. Diky za tip!
- id: 5778
  author: Radka
  author_email: radovana_straube@yahoo.com
  author_url: ''
  date: '2009-01-08 17:35:42 +0100'
  date_gmt: '2009-01-08 16:35:42 +0100'
  content: Dakujem za zaujimavy clanok. Na domovskej stranke jQuery sa pise, ze progressbar
    by mal fungovat od verzie jQuery UI 1.6, ale priklad na stranke (http://docs.jquery.com/UI/Progressbar)
    mi nefunguje. Nevenovali ste nahodou aj tomuto widgetu?
- id: 5787
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-01-08 20:03:04 +0100'
  date_gmt: '2009-01-08 19:03:04 +0100'
  content: "Díky za všechny reakce.\r\n\r\nRadko, bohužel vám nepomůžu - Progressbar
    jsem zatím nepotřeboval použít, takže žádnou zkušenost nemám."
---
<p>V <a href="http://blog.novoj.net/2008/11/07/javascript-closures-prekvapeni-java-programatora/">minulém článku</a>, ve kterém jsem se zabýval JavaScript Closures, jsem se zmiňoval o tom, že mě k jejich studiu donutilo používání efektů z knihovny jQuery. Také jsem sliboval, že o svých zkušenostech něco málo napíšu v dalším článku. Nuže směle do toho.</p>
<p>jQuery je obecná knihovna obalující odlišné implementace (více než odlišnosti jazyka, míním odlišnosti práce s DOM reprezentací) JavaScriptu v běžně používaných prohlížečích. Efekty jsou pouze její minoritní částí, kterou možná většina vývojářů pracujících s jQuery ani nevyužívá. Jelikož jsem hračička, koketoval jsem s efekty už od první chvíle, kdy jsem s jQuery začal. Z globálního pohledu musím říct, že mě překvapuje, že tyto efekty fungují velmi dobře skrze všechny podporované prohlížeče a kupodivu jsou poměrně svižné i na pomalejších počítačích (pomalejšími mám na mysli, průměrný počítač koupený před 3-4 lety). Základní použití je velmi jednoduché a zvládne ho i člověk, který s JavaScriptem a jQuery teprve začíná. Kromě  <a href="http://docs.jquery.com/Effects" target="_blank">základních efektů</a> dodávaných přímo jako součást jQuery Core (show, hide, toggle, fadeIn, fadeOut, animate), je k dispozici ještě oficiální dodatečná knihovna s widgety a dalšími effekty známá jako <a href="http://docs.jquery.com/UI#Effects" target="_blank">jQuery UI</a> (zde najdete řadu dalších pěkných efektů, které byly kdysi součástí js knihovny interface.js).</p>
<p>Pokud máte zájem o to shlédnout některé z animací, které jsme pro naše zákazníky vytvořili, zde nabízím pár odkazů:</p>
<ul>
<li>
		<a href="http://www.moje-firma.cz/srv/www/consultation/newQuery.x" target="_blank">Moje Firma</a> - web Komerční Banky zaměřený na podnikatelskou sféru</p>
<ul>
<li>v části podnikatelská poradna jsme využili efekty k odeslání formuláře s daty na server bez reloadu celé stránky, efekt si můžete bez následků vyzkoušet pokud se pokusíte odeslat prázdný formulář - výsledkem bude animace, která vám zobrazí chyby, které ve skutečnosti generuje server v odpovědi na odeslání formuláře (žádné JS kontroly ;-) )<br> <b>Update 29.10.2010</b> Odkaz již není funkční</li>
</ul>
</li>
<li>
		<a href="http://www.trotina.cz" target="_blank">TROTINA AUTO, s.r.o.</a> - stránky prodejce ojetých vozidel ve Východních Čechách</p>
<ul>
<li>vyzkoušejte si třeba vložit pár vozidel na parkoviště, vybrat ve vyhledávání terénní vozidla, v detailu vozidla odeslat doporučení příteli apod.</li>
<li>kapitolou samou o sobě je potom <a href="https://www.trotina.cz/srv/www/auction/homepage.do" target="_blank">Dražba na ruby</a>, kterou si můžete vyzkoušet je v případě, že je nějaká aktuálně vypsaná - zde se veškerá logika aplikace odehrává v podstatě jen na dvou obrazovkách a zbytek je řešen AJAXem s využitím jQuery efektů</li>
</ul>
</li>
</ul>
<p><a id="more"></a><a id="more-236"></a></p>
<p><script language="JavaScript" src="http://files.novoj.net/jQueryEffects/jquery.js"></script><script language="JavaScript" src="http://files.novoj.net/jQueryEffects/demo.js"></script><br />
<h2>Základní použití</h2>
<p>Jak už jsem avizoval základní použití efektů je velmi jednoduché. Pokud si vezmeme jako příklad jednoduché skrytí / zobrazení konkrétní části stránky (div, span, p atp.), stačí nám toto:</p>
<div id="example1do">
[source lang="java"]<br />
function example1() {<br />
	$("#example1do").hide();<br />
	$("#example1undo").show("fast");<br />
}<br />
[/source]</p>
<p><input  type="button" onclick="example1()" value="Spustit příklad 1">
</div>
<p><input id="example1undo" type="button" onclick="example1undo()" value="Reset zobrazení" style="display: none"></p>
<p>Spuštění příkladu vyvolá pozvolné skrytí prvního tlačítka s příkladem a pomalé zobrazení tlačítka druhého. První část (dolar zastupuje volání jQuery knihovny, výraz v prvních závorkách CSS selektor) vrátí list DOM objektů (obalených v jQuery reprezentaci, takže je možné dál volat metody jQuery), na kterých se zavolá metoda v druhé části výrazu (např. hide()). Většina animací umožňuje definovat rychlost buď jako přesný časový interval v milisekundách (např. hide(10000) bude znamenat úplné skrytí prvku v 10 vteřinách) nebo ve třech stupních "slow", "normal", "fast".</p>
<p>Trošku specifickým efektem je funkce toggle(), která interně provede zavolání show nebo hide funkce v závislosti na aktuálním stavu daného prvku (tzn. pokud je prvek skrytý zavolá se show, pokud je prvek zobrazený, zavolá se hide). Na první pohled prkotina, která ve výsledku docela dost urychluje práci. Základní toggle pracuje s metodami show a hide, nicméně i některé další efekty nabízejí "toggle" alternativu, která vám šetří práci s analýzou aktuálního stavu zobrazení daných prvků. Krátký příklad:</p>
<div class="example2">
[source lang="java"]<br />
function example2() {<br />
	$(".example2").toggle(10000);<br />
}<br />
[/source]
</div>
<p><input class="example2" type="button" onclick="example2()" value="Spustit příklad 2"><br />
<input class="example2" type="button" onclick="example2()" value="A znovu spustit" style="display: none"></p>
<p>Jak je z příkladu hezky vidět, jedním příkazem zvládneme část stránky skrýt a jinou část zobrazit - stačí nám k tomu shodná třída "example2", kterou můžeme použít v selektoru.</p>
<h2>Řetězení efektů / paralelní, sériové spouštění</h2>
<h3>Vynucené sériové spouštění operací</h3>
<p>Pokud chceme začít dělat s efekty divočejší kousky, měli bychom být schopni pracovat s načasováním. Příklady, které jsem doposud uváděl provádějí tzv. paralelní vykonání efektů - efekty se spustí současně a v závislosti s nastavenou délkou trvání odpovídajícím způsobem skončí (pokud všem nastavíme stejné časování např. 1 vteřinu, měly by také v jeden moment skončit, viz. předchozí příklad). Často ale potřebujeme nastavit nějaký animační scénář, který by měl jednotlivé efekty zřetězit. Ukažme si to na příkladu - mějme nějaký blok textu, který chceme v konkrétní chvíli vyměnit. Můžeme to hulvátsky provést tak, že rovnou vyměníme text daného paragrafu, nicméně to není zrovna způsob atraktivní pro uživatele (může to vypadat ošklivě nebo si toho uživatel nemusí všimnout). Proto vše obalíme do jednoduché animace - pozvolna paragraf skryjeme, ve skrytém stavu vyměníme texty a opětovně paragraf pozvolna zobrazíme. K tomu budeme ale muset umět použít sériové spuštění efektů - viz. příklad:</p>
<p>[source lang="java"]<br />
function example3() {<br />
	$("#example3paragraph").hide("slow", function() {<br />
		$(this).load("/text.txt", function(data) {<br />
			$(this).show("slow");<br />
		});<br />
	});<br />
}<br />
[/source]</p>
<p id="example3paragraph" style="border: 1px solid white; background-color: lightgray; color: black;">Tento text bude nahrazen textem nahraným ze serveru.</p>
<p><input type="button" onclick="example3()" value="Spustit příklad 3"> <input type="button" onclick="example3_reset()" value="Reset"></p>
<p>V příkladu navíc pracujeme i s Ajaxovou funkcí "load", kterou poskytuje jQuery, abychom si načetli nějaký text ze serveru. Jak vidíte, relativně složité chování lze napsat na 4 řádky kódu.</p>
<p>Co je na příkladu důležité je to, že většina (ne-li všechny) jQuery animací umožňuje jako poslední parametr předat Closure, která bude spuštěna <b>po</b> dokončení dané animace. Tzn. v našem případě bude výměna textu pomocí metody "load" zavolána až ve chvíli, kdy skončí animace skrytí prvku a animace jeho opětovného zobrazení nezačne dřív, než se podaří načíst a vyměnit text paragrafu. Řetězení animací není nijak omezeno, stejně tak jako není omezeno hnízdění (nestování) Closures.</p>
<p>Z tohoto důvodu je nutné znát alespoň základy pro práci s JavaScript Closures. Pokud chcete navíc extenzivněji pracovat pomocí AJAXu se serverem (ne tak jednoduchým způsobem, jak jsme si ukázali na příkladě, ale např. pomocí knihovny <a href="http://directwebremoting.org/" target="_blank">DWR</a> volat metody na serveru), budete pravděpodobně potřebovat předávat si ve volání i řadu dat, což už vyžaduje trošku větší jistotu v otázce Closures. To jsem se však pokusil alespoň trochu nastínit v <a href="http://blog.novoj.net/2008/11/07/javascript-closures-prekvapeni-java-programatora/">minulém článku</a>.</p>
<h3>Sériové spouštění animací</h3>
<p>Autoři jQuery chtěli definici sériového spouštění animací zjednodušit a proto zavedli tzv. fronty (queue) animací. Nevím přesně jak jsou fronty implementované, ale představuji si, že uvnitř je asociativní mapa, kde klíčem je konkrétní DOM element a hodnotou právě fronta animací.</p>
<p>Paradoxně se zavedením front řada věcí o trochu zkomplikovala. Člověk, který si hned neuvědomí, jak to uvnitř jQuery funguje, se může velmi jednoduše zamotat. Celá záležitost je o to problematičtější tím, že pracujeme s paralelními operacemi v reálném čase. Jedinou možností, kterou máme abychom zjistili, co se kdy děje, je, nastavit dlouhé periody animací a zírat na zpomalenou sekvenci nebo použít nějaký mechanismus logování s časovými známkami.</p>
<p>V prvním příkladě jsem ukazoval paralelní spuštění animací, pokud se však skript bude týkat stejného DOM elementu nebudou animace spuštěny paralelně, ale sériově - jedna po druhé. O to se právě stará animační fronta. Zkuste porovnat jednotlivé zápisy v následující funkci:</p>
<p>[source lang="java"]<br />
function testAnimations() {<br />
	//ukázka z prvního příkladu<br />
	//bude spuštěno paralelně - jedná se o odlišné DOM elementy<br />
	$("#example1do").hide();<br />
	$("#example1undo").show("fast");</p>
<p>	//pokud se ale to samé bude týkat stejného DOM elementu<br />
	//jako je na tomto příkladě, bude spuštění sériové<br />
	$("#example1do").show();<br />
	$("#example1do").hide();</p>
<p>	//celé to jde zapsat díky tomuto chování ještě jednodušeji<br />
	$("#example1do").show().hide();<br />
}<br />
[/source]</p>
<p>Díky tomuto chování můžeme v kondenzované formě (viz. poslední řádek) zapsat animační sekvence týkající se <b>stejných DOM elementů</b> na stránce. Pokud chceme dělat složitější animační scénáře, kde potřebujeme pracovat s více DOM elementy na stránce, nezbyde nám jiná varianta než použití callback metod (Closures).</p>
<p>S animačními frontami si můžeme taky ošklivě naběhnout, pokud definujeme hromadné animační scénáře (tzn. kdy nám selektor vybere více než jeden DOM element). Fronta platí totiž jen pro konkrétní element a nikoliv pro použitý selektor. Situaci si můžeme znázornit na následujícím příkladě:</p>
<table style="width: 500px;" cellpadding="0" cellspacing="0">
<tr>
<td style="padding: 10px;">
<div style="width: 80px; height: 200px; border: 1px solid darkgray; background-color: white; color: black;">
<div id="d1" class="blok">První div</div>
<div id="d2" class="blok">Druhý div</div>
<div id="d3" class="blok">Třetí div</div>
<div id="d4" class="blok">Čtvrtý div</div>
</div>
</td>
<td style="padding: 10px;">
[source lang="java"]<br />
function example4_good() {<br />
	$(".blok").css("position", "absolute");<br />
	$("#d1").animate({ top: "+=80px"}, 2000);<br />
	$("#d2").animate({ top: "+=110px"}, 2000);<br />
	$("#d3").animate({ top: "+=140px"}, 2000);<br />
	$("#d4").animate({ top: "+=170px"}, 2000);</p>
<p>	$("#d1").animate({ fontSize: "150%"}, 2000);<br />
	$("#d3").animate({ fontSize: "150%"}, 2000);</p>
<p>	$(".blok").animate({ top: "-=50px"}, 2000);<br />
}<br />
[/source]
</td>
</tr>
</table>
<p><input id="example4" type="button" onclick="example4_good()" value="Spustit test 4"></p>
<p>Jak je vidět, na začátku metody instruujeme DIVy 1 - 4, aby se posunuly vertikálně dolů o různý počet pixelů. Jelikož se tyto instrukce týkají pokaždé jiného elementu, budou probíhat paralelně. V další části instruujeme již jen DIVy 1 a 3, aby se jejich font postupně o polovinu zvětšil (zvětšování fontů se opět bude provádět paralelně, ovšem díky frontě až po dokončení vertikálního posunu DIVů 1 a 3 dolů). V poslední části pak hromadným selektorem instruujeme najednou všechny DIVy 1 - 4 (všechny mají totiž class="blok"), aby se posunuly vertikálně nahoru o 50px. V poslední instrukci ale tkví ten problém - díky použití animačních front se totiž načasování animace rozloží takto:</p>
<style>
#timing {<br />
   width: 500px;<br />
   border: 1px solid white;<br />
}<br />
#timing tr th {<br />
   text-align: center;<br />
   background-color: #333333;<br />
}<br />
#timing tr td {<br />
   text-align: center;<br />
}<br />
</style>
<table id="timing" cellspacing="0" cellpadding="0">
<tr>
<th>Vteřina</th>
<th>1.</th>
<th>3.</th>
<th>5.</th>
</tr>
<tr>
<td>DIV #d1</td>
<td>posun dolů</td>
<td>zvětšení fontu</td>
<td>posun nahoru</td>
</tr>
<tr>
<td>DIV #d2</td>
<td>posun dolů</td>
<td>posun nahoru</td>
<td>nic</td>
</tr>
<tr>
<td>DIV #d3</td>
<td>posun dolů</td>
<td>zvětšení fontu</td>
<td>posun nahoru</td>
</tr>
<tr>
<td>DIV #d4</td>
<td>posun dolů</td>
<td>posun nahoru</td>
<td>nic</td>
</tr>
</table>
<p>Aby nebyl celé legrace konec, animační fronty se týkají pouze animací. Tzn. když mezi jednotlivé animace vložíte nějakou neanimační operaci - jako třeba v následujícím příkladě AJAXové volání serveru, tato operace se vám do fronty nevloží a provede se paralelně se začátkem animace:</p>
<p>[source lang="java"]<br />
function example4_bad() {<br />
	$("#example4paragraph").hide(10000).load("/text.txt").show(10000);<br />
}<br />
[/source]</p>
<p id="example4paragraph" style="border: 1px solid white; background-color: lightgray; color: black;">Tento text bude nahrazen textem nahraným ze serveru.</p>
<p><input type="button" onclick="example4_bad()" value="Spustit příklad 4 - chyták"></p>
<p>Záměrně jsem prodloužil délku trvání animace na 10 vteřin, abyste mohli postřehnout, že již při skrývání paragrafu se v něm provede náhrada textu. Tedy nikoliv, až ve chvíli kdy je paragraf skrytý, jak bychom původně mohli čekat. Samozřejmě díky tomu, že se jedná o AJAXové volání, záleží na rychlosti odezvy serveru - někdy by se mohlo zdát, že se animace chová tak jak zamýšlíme, ale opak je pravdou - může se chovat jen o náhodnou synchronizaci díky pomalé odpovědi ze strany serveru (tím že prodloužíme dobu animace to můžeme jednoduše odhalit).</p>
<h3>Síla funkce animate</h3>
<p>Většina (pokud ne všechny) jQuery efekty používají na pozadí generickou funkci s názvem Animate. Ta umožňuje rozfázovat přechod od jednoho nastavení CSS atributů k jinému. Vezměme si jednoduchý příklad - při implementaci dražby vozidel pro TROTINA AUTO jsme chtěli při sledování seznamu dražených vozidel průběžně aktualizovat stavy vozidel a aktuálně vydražená vozidla odlišovat jiným barevným podkladem řádku. Vše se děje ajaxovým způsobem, tzn. bez reloadu stránky se mají postupně jednotlivá vozidla podbarvovat tak jak jsou aktuálně prodávána. Pokud uživatel sleduje danou stránku nevypadalo by hezky pokud bychom provedli změnu barevného podkladu skokově - pro tento případ jsme použili právě funkci Animate.</p>
<p>Efekt animate vypočte číselnou řadu mezi dvěma hodnotami tak, aby vlastní změna proběhla plynule v čase určeném animaci. Možnosti animate jsou omezené - nelze použít vždy a na vše. Všimněte si především této části dokumentace:</p>
<style>
.quote {<br />
   font-size: 120%;<br />
   font-family: Serif;<br />
   background-color: #dddddd;<br />
   color: black;<br />
   padding: 10px<br />
}<br />
</style>
<div class="quote">"Only properties that take numeric values are supported (e.g. backgroundColor is not supported). As of jQuery 1.2 you can now animate properties by em and % (where applicable). Additionally, in jQuery 1.2, you can now do relative animations - specifying a "+=" or "-=" in front of the property value moves the element positively or negatively, relative to its current position."</div>
<p>[source lang="java"]<br />
function example5() {<br />
	if ($("body").css("opacity") != 1) {<br />
		$("body").animate({ opacity: 1}, 2000, function() {$("#example5").attr("value", "Spustit příklad 5");});<br />
	} else {<br />
		$("body").animate({ opacity: 0.1}, 2000, function() {$("#example5").attr("value", "Vzít příklad 5 zpět");});<br />
	}<br />
}<br />
[/source]</p>
<p><input id="example5" type="button" onclick="example5()" value="Spustit příklad 5"></p>
<p>Samozřejmě barvy jsou jedna z věcí, které bychom právě animovat chtěli. Pro tento účel ovšem musíme použít <a href="http://plugins.jquery.com/project/color" target="_blank">dodatečný plugin</a>, který nám to umožní.</p>
<p>Funkce animate má kromě standardních parametrů určujících změnu cílové vlastnosti nebo použití transformační funkce (ano kromě změny CSS vlastností je možné přidávat pro animate <a href="http://docs.jquery.com/Release:jQuery_1.2/Effects#Extensible_Animations" target="_blank">vlastní složitější funkce</a>) také sadu Options. V nich je možné dále zasahovat do chování této animace:</p>
<ul>
<li><b>duration</b><br>délka trvání v milisekundách</li>
<li><b>easing</b><br>linear/swing - aproximační funkce pro výpočet změny vlastností v čase</li>
<li><b>complete</b><br>closure, která se má vykonat po ukončení animace</li>
<li><b>step</b><br>closure, která se má vykonat v každém kroku animace; má dva parametry: now - aktuální hodnotu měněné vlastnosti, fx - objekt reprezentující efekt</li>
<li><b>queue</b><br>true/false - definuje zda má být animace zařazena do animační fronty elementu či nikoliv</li>
</ul>
<p>Konkrétní efekty (show, hide, fadeIn, fadeOut ...) již tyto options nevystavují, takže pokud budete chtít dělat složitější věci budete muset používat tuto nízkoúrovňovou funkci.</p>
<h2>Závěrem</h2>
<p>Efekty jQuery jsou skvělý nástroj jak zatraktivnit statické HTML a také elegantní způsob jak vyřešit změnu obsahu částí stránky při použití AJAXu. Jejich použití je natolik triviální, že jsou přístupné takřka všem. Velmi brzy se však člověk osmělí a pustí se do složitějších scénářů, kde si bez hlubší znalosti principů uvnitř jQuery a JavaScript closures, může jednoduše naběhnout. Mluvím z vlastní zkušenosti, protože já jsem na tom pěkných pár hodin nechal.</p>
<h2>Reference</h2>
<ul>
<li><a href="http://docs.jquery.com/Release:jQuery_1.2/Effects" target="_blank">Velmi šikovná dokumentace k refaktoringu efektů v jQuery v. 1.2.X</a></li>
<li><a href="http://plugins.jquery.com/project/color" target="_blank">Plugin umožňující změnu barev jako součást animační funkce</a></li>
<li><a href="http://acko.net/blog/abusing-jquery-animate-for-fun-and-profit-and-bacon" target="_blank">Velmi atraktivní využití extensibility funkce animate</a></li>
<li><a href="http://www.learningjquery.com/" target="_blank">Portál orientovaný čistě na jQuery</a></li>
<li><a href="http://www.detacheddesigns.com/blog/blogSpecific.aspx?BlogId=78" target="_blank">Alternativní článek v angličtině věnující se stejnému tématu</a></li>
</ul>
