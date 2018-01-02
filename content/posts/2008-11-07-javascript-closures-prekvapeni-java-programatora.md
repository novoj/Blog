---
status: publish
published: true
title: JavaScript Closures - překvapení Java programátora
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Javascript používám několik let, snad už od doby kdy jsem na univerzitě
  začal koketovat s webem. Celou dobu ho používám jen na jednoduché skriptování bez
  ambic na jakýkoliv propracovanější programovací model. S nástupem kvalitních frameworků
  jako je třeba <a href=\"http://jquery.com/\" target=\"_new\">jQuery</a>, <a href=\"http://www.prototypejs.org/\"
  target=\"_new\">PrototypeJS</a>, <a href=\"http://mootools.net/\" target=\"_new\">MooTools</a>,
  <a href=\"http://script.aculo.us/\" target=\"_new\">Script.aculo.us</a> a další,
  je člověk přinucen ponořit se do tajů JavaScriptu hlouběji a narazí na věci o kterých
  se mu před tím ani nesnilo. V tomto článku bych se s vámi rád podělil o pár zkušeností
  a především odkazů na kvalitní články o tzv. Closures v JavaScriptu. Dopředu upozorňuji,
  že nejsem žádný JavaScript guru a že čerpám především z odkazovaných článků a z
  několika projektů, kde jsem díky jQuery a DWR s closures přišel do styku.\r\n\r\n"
wordpress_id: 167
wordpress_url: http://blog.novoj.net/?p=167
date: '2008-11-07 17:46:13 +0100'
date_gmt: '2008-11-07 16:46:13 +0100'
categories:
- Web
- JavaScript
tags: []
comments:
- id: 4572
  author: Vaclav Pech
  author_email: vaclav.pech@seznam.cz
  author_url: http://www.jroller.com/vaclav
  date: '2008-11-08 13:29:10 +0100'
  date_gmt: '2008-11-08 12:29:10 +0100'
  content: Tak o tehle vlastnostech JavaScriptu jsem taky nevedel. Diky za prehledne
    shrnuti.
- id: 4618
  author: NkD
  author_email: michal.nikodim@gmail.com
  author_url: ''
  date: '2008-11-10 08:43:54 +0100'
  date_gmt: '2008-11-10 07:43:54 +0100'
  content: Parada. Proste parada. Super clanek. Hned jsu poslat link kolegum.
- id: 4621
  author: Filip Jirsák
  author_email: filip@jirsak.org
  author_url: ''
  date: '2008-11-10 11:13:28 +0100'
  date_gmt: '2008-11-10 10:13:28 +0100'
  content: "Na closures v JS je podle mne největší pastička v tom, že mohou být volány
    i jako funkce i jako metody, takže dopředu nikdy není jasné, na co bude odkazovat
    uvnitř closure \"this\".\r\n\r\nNo a ta hlavní výhoda closures – že si s sebou
    vezou lokální kontext – mi osobně připadá jenom jako trošku zakamuflované globální
    proměnné, aby se programátorům, kteří někdy slyšeli, že globální proměnné jsou
    fuj, neježily hrůzou vlasy na hlavě. Jinak je to v podstatě to samé, umožňuje
    to pracovat s nějakou proměnnou mimo její kontext, aniž bych tu proměnnou musel
    explicitně předávat jako parametr."
- id: 4626
  author: Ladislav Thon
  author_email: ladicek@gmail.com
  author_url: ''
  date: '2008-11-10 13:28:31 +0100'
  date_gmt: '2008-11-10 12:28:31 +0100'
  content: "Chápu, že programátoři v Javě apod. jsou zvyklí operovat se zásobníkem
    jako místem, kam se ukládají lokální proměnné, ale vzhledem k tomu, že tady \"lokální\"
    proměnné mohou svůj lexikální obor platnosti \"přežít\", ve skutečnosti nejsou
    na zásobníku, ale normálně na heapu. Trochu jsem o tom psal, ve spojitosti s Javou,
    tady: http://www.abclinuxu.cz/blog/variace/2006/10/prvotridni-java\r\n\r\n&gt;
    ta hlavní výhoda closures – že si s sebou vezou lokální kontext – mi osobně připadá
    jenom jako trošku zakamuflované globální proměnné\r\n\r\nJo jo jo jo jo, to jsou
    úúúúúplně normální globální proměnné, akorát že nejsou globální :-) \"Doba života\"
    se sice liší od lexikálního oboru platnosti, ale ten je pořád zachován, žádná
    \"práce s proměnnou mimo její kontext\" neexistuje."
- id: 4634
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2008-11-10 22:03:42 +0100'
  date_gmt: '2008-11-10 21:03:42 +0100'
  content: Díky za komentáře. Z nich si pro sebe vyvozuji to, že přestože jsem si
    už tak trochu zažil chování closures, ještě stále dost plavu na povrchu v detailech
    konkrétní implementace v JavaScript enginu. No snad nikoho tímhle článkem nepřivedi
    příliš na scestí.
- id: 4635
  author: David
  author_email: wolczyk.david@gmail.com
  author_url: ''
  date: '2008-11-10 22:10:27 +0100'
  date_gmt: '2008-11-10 21:10:27 +0100'
  content: Super clanek, snad prvni vec o javascriptu, co jsem docetl az do konce.
    Skoda, ze porad nezmenil muj nazor na javascript :D
- id: 4678
  author: Luboš
  author_email: lubos.svoboda@codedynamics.cz
  author_url: http://www.codedynamics.cz
  date: '2008-11-12 22:55:36 +0100'
  date_gmt: '2008-11-12 21:55:36 +0100'
  content: Díky za pěkný článek!
- id: 4915
  author: mirci
  author_email: mkoskar@gmail.com
  author_url: ''
  date: '2008-11-21 14:59:41 +0100'
  date_gmt: '2008-11-21 13:59:41 +0100'
  content: "Pekne zhrnutie, \r\nrovnako som v nedavnej dobe pracoval s DWR a JQuery.
    Javascriptovy kod sa nam zacal hromadit skoro na kazdej stranke a tak bola nutnost
    napisat nejaku abstrakciu na volanie DWR a veci okolo toho, tam sa closury na
    par miestach vyuzili.\r\n\r\nVrelo odporucam knihu, Pro Javascript Techniques
    od autora JQuery. Priznam sa, ze to bola moja prva JS kniha, ktoru som cital (pred
    tym som cital vacsinou zdroje na webe, ktorych je v celku dost). Je prelozena
    aj do cestiny ale v anglictine je to viac ono. Hned od uvodu sa venuje objektovemu
    javascriptu, closuram a podobne, proste veci, ktore su velmi podstatne ale nejak
    som sa o nich vo webovych tutorialoch nikdy nedocital. Priznam sa, ze predtym
    som Javascript nemal rad, ale po prestudovani ako veci funguju som prisiel tomuto
    jazyku na chut. \r\n\r\nPS: momentalne sa hram s groovy a s jeho closurami, a
    po mojom testiku mozem potvrdit, ze fungovanie je velmi podobne javascriptu aspon
    co sa tyka tych kontextov:\r\n\r\ndef getFunction1(param1) {\r\n  return [\r\n
    \         {it -&gt;\r\n            param1++;\r\n            println \"$it $param1\"\r\n
    \         },\r\n          {it -&gt;\r\n            param1++;\r\n            println
    \"$it $param1\"\r\n          }\r\n  ]\r\n}\r\n\r\ngetFunction1(1).each {it(\"param\")}\r\n\r\nVysledok:\r\n&gt;&gt;
    param 2\r\n&gt;&gt; param 3\r\n\r\n// fix\r\ndef getFunction2(param1) {\r\n  return
    [\r\n          {it -&gt;\r\n            def _param1 = {param1}();\r\n            _param1++;\r\n
    \           println \"$it $_param1\"\r\n          },\r\n          {it -&gt;\r\n
    \           def _param1 = {param1}();\r\n            _param1++;\r\n            println
    \"$it $_param1\"\r\n          }\r\n  ]\r\n}\r\n\r\ngetFunction2(1).each {it(\"param\")}\r\n\r\nVysledok:\r\n&gt;&gt;
    param 2\r\n&gt;&gt; param 2"
- id: 4976
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2008-11-24 11:05:53 +0100'
  date_gmt: '2008-11-24 10:05:53 +0100'
  content: Na Groovy se chystám už od jara. Odkládám to už moc dlouho - o Vánocích
    se do toho pustím a čím dál víc se na to těším. Díky za info.
- id: 5883
  author: Matus Mala
  author_email: homer68@gmail.com
  author_url: ''
  date: '2009-01-16 08:19:54 +0100'
  date_gmt: '2009-01-16 07:19:54 +0100'
  content: Tak tento clanok je fakt super. Makam momentalne na vacsiom projekte (projektoch),
    kde vyuzivame aj dost Javascriptu a komunikaciu s Ajaxom a toto vyzera velmi dobre.
    Asi to aj pouzijem, len to musim este poriadne kuknut.
---
<p>Javascript používám několik let, snad už od doby kdy jsem na univerzitě začal koketovat s webem. Celou dobu ho používám jen na jednoduché skriptování bez ambic na jakýkoliv propracovanější programovací model. S nástupem kvalitních frameworků jako je třeba <a href="http://jquery.com/" target="_new">jQuery</a>, <a href="http://www.prototypejs.org/" target="_new">PrototypeJS</a>, <a href="http://mootools.net/" target="_new">MooTools</a>, <a href="http://script.aculo.us/" target="_new">Script.aculo.us</a> a další, je člověk přinucen ponořit se do tajů JavaScriptu hlouběji a narazí na věci o kterých se mu před tím ani nesnilo. V tomto článku bych se s vámi rád podělil o pár zkušeností a především odkazů na kvalitní články o tzv. Closures v JavaScriptu. Dopředu upozorňuji, že nejsem žádný JavaScript guru a že čerpám především z odkazovaných článků a z několika projektů, kde jsem díky jQuery a DWR s closures přišel do styku.</p>
<p><a id="more"></a><a id="more-167"></a></p>
<h2>Closures jsou i  pro lamky</h2>
<p>Kapitolku začnu stejným názvem jako článek, který mě do problematiky closures zasvětil asi nejvíc. Co je tedy vlastně ta "Closure"?<br />
<script language="JavaScript" src="http://files.novoj.net/JavaScriptClosures/examples.js"></script><br />
<script language="JavaScript" src="http://files.novoj.net/JavaScriptClosures/caveats.js"></script><br />
Closure je v základu ukazatel na funkci, který je možné přiřadit jako hodnotu proměnné, vrátit ji jako návratovou hodnotu jiné funkce nebo použít jako parametr volání funkce. Následující příklad obsahuje validní JavaScript kód:</p>
<p>[source lang="java"]<br />
function example1() {<br />
   //this shows no allert<br />
   var myFnct = function() { alert("Hello World!") };<br />
   //this shows function as string - no execution will happen<br />
   alert(myFnct.toString());<br />
   //there we'll execute it<br />
   myFnct();<br />
}</p>
<p>function example2() {<br />
   //we'll fetch a function and execute it on next line<br />
   var myFnct = getSomeFunction();<br />
   myFnct("Father Fourah");<br />
   //we can do it even in shorter way - looks quite ridiculous - doesn't it?<br />
   getSomeFunction()("Reader");<br />
}</p>
<p>function getSomeFunction() {<br />
   return function(name) {alert("Hello " + name)};<br />
}</p>
<p>function example3() {<br />
   var names = ["Jan", "Petr", "Milan"];<br />
   var myFnct = function(name) {alert(name)};<br />
   forEachExecute(names, myFnct);<br />
   //or the same in more compressed way<br />
   forEachExecute([1,2,3], function(nmb) {alert(nmb)});<br />
}</p>
<p>function forEachExecute(data, callback) {<br />
   for(i = 0; i < data.length; i++) {<br />
      callback(data[i]);<br />
   }<br />
}<br />
[/source]<br />
<input type="button" onclick="example1()" value="Spuštění příkladu 1"/><br />
<input type="button" onclick="example2()" value="Spuštění příkladu 2"/><br />
<input type="button" onclick="example3()" value="Spuštění příkladu 3"/></p>
<p>Pokud se vám zdá zápis s použitím function() {} - tzn. anonymní funkce nepřehledný a složitý je možné i toto použití (nicméně pozor tímto nevytváříme closures v pravém slova smyslu - v následujícím příkladě pracujeme pouze s ukazateli na metodu, jak se dozvíte o pár odstavců níže):</p>
<p>[source lang="java"]<br />
function example4() {<br />
	//this is equivalent to anonymous function declaration<br />
	var myFnct = someFunction;<br />
	//this proves that function isn't executed until next line<br />
	alert("Before function execution");<br />
	myFnct();<br />
	//the same is valid for method with parameters<br />
	//we can deliver parameters only when we call method not before<br />
	var myFnct2 = someFunctionWithParam;<br />
	alert("Before second function execution");<br />
	myFnct2("Jan");<br />
	//this won't work as it executes function immediately<br />
	//and assigns null value to our variable<br />
	var myFnct3 = someFunctionWithParam("Petr");<br />
	alert("As you can see this is displayed after execution of third function, value "<br />
			+ myFnct3 + " is assigned to variable, not a function itself.");<br />
}</p>
<p>function someFunction() {<br />
	alert("Hello world!");<br />
}</p>
<p>function someFunctionWithParam(name) {<br />
	alert("Hello " + name + "!");<br />
}<br />
[/source]</p>
<p><input type="button" onclick="example4()" value="Spuštění příkladu 4"/></p>
<p>Prozatím jsme si na příkladech ukázali pouze první vlastnost closures a to je možnost používat "ukazatel" na metodu jako proměnnou (zjednodušeně řečeno). Druhá důležitá vlastnost closures je však zachování lokálního stacku proměnných metody, kde je closures vytvořena. Na první pohled to zní složitě, nicméně princip je relativně jednoduchý.</p>
<p>Podobně jako v Javě jsou i v JavaScriptu lokální proměnné metody uvolňovány po skončení této metody (respektive uvolněny v některém z následujících cyklů GC) - samozřejmě jen tehdy, pokud je nespojíme s objektem s delší životností (tzn. globální proměnné, DOM stromu prohlížeče apod.). Pokud v naší metodě vytvoříme closure a ta se dostane mimo vlastní metodu (třeba je použita jako návratová hodnota), není stack lokálních proměnných metody uvolněn, ale zůstává v paměti pro použití z dané closure (closure má delší životnost jak metoda ve které byla vytvořena - žije tak dlouhod dokud je odkaz na closure uchován v nějaké žijící proměnné). Chování by odpovídalo situaci, jako kdyby closure v sobě obsahovala reference na všechny lokální proměnné metody, ve které byla vytvořena.</p>
<p>Celý princip si můžeme ukázat na následujícím příkladě</p>
<p>[source lang="java"]<br />
function example5() {<br />
	var myFnct = getFunctionExample5("Just kidding.");<br />
	//can you see? getFunctionExample5 method scope is closed now<br />
	//but we can still access local variable name of that scope via closure<br />
	//in example we are mixing even method parameters<br />
	myFnct("No, no - I am serious.");<br />
}</p>
<p>function getFunctionExample5(suffix) {<br />
	var name = "Father Fourah";<br />
	return function(postSuffix) {alert(name + " rulez!\n" + suffix + "\n" + postSuffix)};<br />
}</p>
<p>function example6() {<br />
	var myFnct = getFunctionExample6();<br />
	//this doesn't work no closure was created<br />
	//we have acquired only method pointer<br />
	myFnct();<br />
}</p>
<p>function getFunctionExample6() {<br />
	var name = "Father Fourah";<br />
	return example6function;<br />
}</p>
<p>function example6function() {<br />
	alert(name + " See? Name is not know in this case - this doesn't create closure!");<br />
}</p>
<p>function example7() {<br />
	var myFnct = getFunctionExample7();<br />
	//but in case of inner methods closures are created<br />
	myFnct();<br />
}</p>
<p>function getFunctionExample7() {<br />
	var name = "Father Fourah";</p>
<p>	function example7function() {<br />
		alert(name + " can use even inner functions - these are closures!")<br />
	}</p>
<p>	return example7function;<br />
}<br />
[/source]</p>
<p><input type="button" onclick="example5()" value="Spuštění příkladu 5"/><br />
<input type="button" onclick="example6()" value="Spuštění příkladu 6"/><br />
<input type="button" onclick="example7()" value="Spuštění příkladu 7"/></p>
<p>Closure si nedrží referenci pouze na proměnné metody, která closure vytvořila, ale na celý strom volání metod až k metodě, která closure vytvořila. Opět lze předvést na následujícím příkladě.</p>
<p>[source lang="java"]<br />
function example8() {<br />
	var myFnct = getFunctionExample8();<br />
	//but closures keep reference to whole stack tree<br />
	//not only to stack of method closure is created in<br />
	myFnct()();<br />
}</p>
<p>function getFunctionExample8() {<br />
	var name = "Father Fourah";<br />
	return function() {<br />
		var suffix = "goes insane!"<br />
		return function() {<br />
			alert(name + " " + suffix);<br />
		}<br />
	}<br />
}<br />
[/source]</p>
<p><input type="button" onclick="example8()" value="Spuštění příkladu 8"/></p>
<h2>Pasti, pasti, pastičky</h2>
<p>Closures jsou velmi silným nástrojem JavaScriptu, ale už na předchozích příkladech jste asi postřehli, bez znalosti principů v pozadí, to může být poměrně velká magie. A to jsme teprve na začátku. V dalších odstavcích chci probrat několik pastiček, na které můžeme narazit a na kterých si velmi jednoduše můžeme vylámat zuby (mě za tento týden zbyly už jenom dvě stoličky :-) ).</p>
<h3>Všechny closures vytvořené ve stejné metodě sdílejí stack</h3>
<p>Jak již bylo výše řečeno - closures si nedrží kopie proměnných metody, která je vytvořila ale referenci na stack. To znamená, že pokud v metodě vytvoříme více closures budou všechny přistupovat ke stejným proměnným. To si lze deklarovat na dalším příkladě:</p>
<p>[source lang="java"]<br />
function caveat1() {<br />
	//this will create array with three closures in it<br />
	var myFncts1 = getFunctionSet(1);<br />
	var myFncts2 = getFunctionSet(10);<br />
	//we'll examine array twice<br />
	for(i = 0; i < 2; i++) {<br />
		//and we'll call each closure in that array<br />
		for(j = 0; j < myFncts1.length; j++) {<br />
			//we could expect displaying 1, 2, 4, 4, 5, 10<br />
			myFncts1[j]();<br />
		}<br />
	}<br />
	//now again for the second array<br />
	for(i = 0; i < 2; i++) {<br />
		for(j = 0; j < myFncts2.length; j++) {<br />
			//we could expect displaying 10, 11, 22, 22, 23, 46<br />
			myFncts2[j]();<br />
		}<br />
	}<br />
	//as you can see, both arrays keeps their own stack<br />
	alert(<br />
		"Final value of first set is " + myFncts1[3]() + "\n" +<br />
		"Final value of second set is " + myFncts2[3]()<br />
	);<br />
}</p>
<p>function getFunctionSet(startingValue) {<br />
	var number = startingValue;<br />
	return [<br />
		function() {alert(number)},<br />
		function() {number++; alert(number)},<br />
		function() {number=number*2; alert(number)},<br />
		function() {return number},<br />
	];<br />
}<br />
[/source]</p>
<p><input type="button" onclick="caveat1()" value="Spuštění pasti 1"/></p>
<p>Jak je vidno z kódu, změna hodnoty proměnné způsobená jednou closure vytvořenou ve stejném volání metody se promítá při práci se stejnou proměnnou v jiné closure vytvořené ve stejném volání metody. Na první pohled možná těžko srozumitelná věta, ale kdy ji spojíte s průzkumem kódu bude vám brzy jasno.</p>
<p>Druhou důležitou věcí je to, že druhé volání metody getFunctionSet vytváří samostatný stack pro lokální proměnné, takže druhá vytvořená sada closures pracuje s odlišnou proměnnou number než první sada closures. Proměnná je sdílena pouze v rámci jednoho lokálního kontextu (v našem případě jedné sady closures).</p>
<h3>Closure přistupuje vždy k aktuální hodnotě proměnné ve chvíli volání</h3>
<p>Z minulého příkladu by tento fakt mohl být patrný, ale pro jistotu ho ještě zdůrazním. Tím že si closure drží referenci a nikoliv kopii proměnných, přistupuje ve chvíli svojí exekuce k aktuálním hodnotám daných proměnných. Velmi jednoduchý příklad demonstruje tuto záludnost:</p>
<p>[source lang="java"]<br />
function caveat2() {<br />
	var myFnct = getCaveat2function();<br />
	//if you think value 1 will be displayed,<br />
	//you're terribly wrong - neither 1 or error will occur<br />
	myFnct();<br />
	//when we need to fix variable values we need to use objects<br />
	getCaveat2functionKeepingItsOriginalValue().showNumber();<br />
}</p>
<p>function getCaveat2function() {<br />
	var number = 1;<br />
	var myFnct = function() {alert(number + anotherNumber)};<br />
	number ++;<br />
	var anotherNumber = 50;<br />
	return myFnct;<br />
}</p>
<p>function getCaveat2functionKeepingItsOriginalValue() {<br />
	var number = 1;<br />
	//for fixing values we need to create objects<br />
	var MyFnct = function(number) {<br />
		//this will copy number value at the time<br />
		//instance of this object is created<br />
		var myNumber = number;<br />
		//by this declaration we'll create new method<br />
		//of this object that simply displays inner value<br />
		this.showNumber = function() {<br />
			alert(myNumber)<br />
		}<br />
	};<br />
	//in this moment variables are copied<br />
	var result = new MyFnct(number);<br />
	//this won't affect result inner value<br />
	number++;<br />
	return result;<br />
}<br />
[/source]</p>
<p><input type="button" onclick="caveat2()" value="Spuštění pasti 2"/></p>
<p>Z této pasti se dostaneme s pomocí deklarace objektu, v jehož konstruktoru vytvoříme vnitřní proměnnou objektu, do které uložíme hodnotu lokální proměnné v době, kdy se vytváří instance objektu. Pomocí metod tohoto objektu pak můžeme přistupovat k vnitřním proměnným, které jsou již kopií a změny hodnot původních lokálních proměnných metody, kde byl objekt vytvořen již tyto proměnné neovlivní.</p>
<p>Tohle byla pro mě už tak trochu vyšší dívčí do doby než jsem si příklad napsal.</p>
<h3>Loop proměnné vám zamotají pěkně hlavu</h3>
<p>Tohle je přesně ta pastička, kvůli které jsem začal princip fungování closures zkoumat. Chování opět vychází ze stále opakované věty, že closure přistupuje vždy k aktuální hodnotě proměnné ve chvíli volání. Nejlépe si problémek rozebrat na příkladě:</p>
<p>[source lang="java"]<br />
function caveat3() {<br />
	var data = ["Janek","Pepa","Luca"];<br />
	var myFncts1 = getLoopFunctionSet(data);<br />
	for(var i = 0; i < myFncts1.length; i++) {<br />
		//do you think we'll see Closure #Janek, Closure #Pepa, Closure #Luca ?<br />
		//nope! we'll see Closure #undefined, Closure #undefined, Closure #undefined !<br />
		//why? because variable i value at the end of method getLoopFunctionSet is 3<br />
		myFncts1[i]();<br />
	}<br />
	//but we can solve it with objects pattern<br />
	var myFncts2 = getLoopFunctionSetSolution(data);<br />
	for(var j = 0; j < myFncts2.length; j++) {<br />
		myFncts2[j].showIt();<br />
	}<br />
	//but we can solve it with extended function pattern<br />
	var myFncts3 = getLoopFunctionSetSolution(data);<br />
	for(var k = 0; k < myFncts3.length; k++) {<br />
		myFncts3[k].showIt();<br />
	}<br />
}</p>
<p>//naive method<br />
function getLoopFunctionSet(sourceList) {<br />
	var result = new Array(sourceList.length);<br />
	for(var i = 0; i < sourceList.length; i++) {<br />
		result[i] = function() {alert("Closure #" + sourceList[i])};<br />
	}<br />
	return result;<br />
}</p>
<p>//data transfer object pattern<br />
function getLoopFunctionSetSolution(sourceList) {<br />
	var result = new Array(sourceList.length);<br />
	for(var i = 0; i < sourceList.length; i++) {<br />
		var Dto = function() {<br />
			var innerValue = sourceList[i];<br />
			this.showIt = function() {alert("Closure #" + innerValue)};<br />
		};<br />
		result[i] = new Dto();<br />
	}<br />
	return result;<br />
}</p>
<p>//function transfer pattern<br />
function getLoopFunctionSetAnotherSolution(sourceList) {<br />
	var result = new Array(sourceList.length);<br />
	for(var i = 0; i < sourceList.length; i++) {<br />
		//calling extendedFunction will enforce javascript to copy value of variable<br />
		//on curent position in array<br />
		result[i] = extendedFunction(sourceList[i]);<br />
	}<br />
	return result;<br />
}</p>
<p>function extendedFunction(name) {<br />
	return function() {alert("Closure #" + name)};<br />
}<br />
[/source]</p>
<p><input type="button" onclick="caveat3()" value="Spuštění pasti 3"/></p>
<p>Pokud neznáte pozadí fungování closures, zcela jistě začnete s naivní implementací jak je uvedena v příkladě (respektive já takhle začal) a pak jen kroutíte hlavou. Vysvětlení je prosté - v closure přistupujete k proměnným ve stavu v jakém jsou v momentu, kdy se closure vykonává. Ve chvíli, kdy se spouští ta v našem příkladě, je již loop ukončen a proměnná i=3 (oproti Javě, kde by proměnná mimo scope loopu neexistovala). Na čtvrté pozici pole však již žádná hodnota není a proto se dostaneme jen k "undefined".</p>
<p>V tomto případě musíme zajistit zafixování hodnoty proměnné ve chvíli, kdy jsme uvnitř toho loopu a máme k dispozici očekávanou hodnotu iterační proměnné. To vyžaduje vykopírování hodnoty někam mimo lokální stack metody, která vytváří closure. Možná jsem to nepopisuji úplně přesně, ale doufám, že moje kostrbaté vysvětlení bude v kombinaci s příkladem pro výsledné pochopení stačit. Vykopírování aktuální hodnoty můžeme docílit minimálně dvěma způsoby. Vytvořením DTO v jehož konstruktoru zafixujeme hodnotu aktuální v daný moment (toto řešení jsme již použili v minulém příkladě), nebo vytvořením funkce "přes koleno", která také obnáší vytvoření kopie hodnoty.</p>
<h2>Závěr</h2>
<p>Zažití použití closures v JS vyžaduje nějaký čas a experimentování. Mně osobně k tomu donutilo používání Ajaxu (konkrétně DWR spolu s Prototype.js nebo jQuery) a vůbec toho nelituji. Přestože Closures, tak jak je o nich diskutováno v Javě by byly ve výsledku v řadě ohledů odlišné, základní princip bude plus mínus zachován (pokud closures v Javě vůbec kdy budou) a já jsem minimálně nakouknul pod pokličku toho mechanismu někde, kde již řadu let funguje. Rozhodně to nebyl marný výlet a já jsem rád, že jsem se mohl zase něco dalšího naučit.</p>
<p>V příštím článku bych se s vámi chtěl podělit o nějaké zkušenosti s efekty v jQuery, které byly prapůvodní příčinou mého zájmu o JavaScript a motorem pro napsání tohoto článku ...</p>
<h2>Reference</h2>
<p>Pokud vám budou některé příklady nejasné, nebo moje vysvětlení nepřesné, určitě koukněte na následující odkazy, z nichž jsem informace čerpal:</p>
<ul>
<li><a href="http://blog.morrisjohns.com/javascript_closures_for_dummies" ratget="_new">JavaScript Closures for Dummies</a> - výborný blogpost, který byl pro mě tím světlem na konci tunelu</li>
<li><a href="http://www.permadi.com/tutorial/jsFunc/index.html" target="_new">Inroduction to JavaScript functions</a> - úvod do práce s funkcemi v JS</li>
<li> <a href="http://www.crockford.com/javascript/private.html" target="_new">Private Members in JavaScript</a> - skvělý článek popisující rozdíly mezi veřejnými a priváními metodamy / atributy javascriptového objektu</li>
<li><a href="http://www.mennovanslooten.nl/blog/post/62" target="_new">JavaScript closures in for-loops</a> - rozbor pasti s loop proměnnými</li>
<li><a href="http://programujte.com/index.php?akce=clanek&cl=2008073100-funkce-v-javascriptu" target="_new">Funkce v JavaScriptu</a> - článek v češtině obecně o funkcích v JS</li>
</ul>
<p>Příklady zobrazené v tomto článku je možné si stáhnout zde:</p>
<ul>
<li><a href="http://files.novoj.net/JavaScriptClosures/examples.js">Příklady</a></li>
<li><a href="http://files.novoj.net/JavaScriptClosures/caveats.js">Pastičky</a></li>
</ul>
