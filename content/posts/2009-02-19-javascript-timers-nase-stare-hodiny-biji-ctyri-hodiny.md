---
status: publish
published: true
title: JavaScript timers - naše staré hodiny, bijí čtyři hodiny
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Absolutním Cimrmanovým rýmem začínám další ze série článků o Javascriptu.
  V něm bych chtěl rozebrat pár postřehů při práci s časovači (timery) v JavaScriptu.
  Ty se používají k lecčemu - při jQuery animacích, zobrazování aktuálního času, periodickém
  dotazováním serveru atp. Intuitivně jsme vždycky tušili, že jejich časování nemusí
  být úplně přesné, ale přesto jsme hrubě podcenili význam pro aplikaci, pro kterou
  je aktuální čas zásadní.\r\n\r\nStáli jsme před relativně jednoduchým problémem.
  Odpočítávat čas do okamžiku T a vypočítávat slevu v ceně na základě času, který
  do okamžiku T zbývá. Samozřejmě všechny údaje (ať čas nebo cena) musely být u všech
  klientů naprosto stejné a musely se měnit každou vteřinu. Tento jednoduchý problém
  nás ale docela potrápil a proto vznikl tento článek, který by měl zachytit problémy
  a jejich řešení.\r\n\r\n"
wordpress_id: 291
wordpress_url: http://blog.novoj.net/?p=291
date: '2009-02-19 12:09:35 +0100'
date_gmt: '2009-02-19 11:09:35 +0100'
categories:
- Programování
- Web
- JavaScript
tags: []
comments:
- id: 6570
  author: NkD
  author_email: michal.nikodim@gmail.com
  author_url: ''
  date: '2009-02-20 14:48:25 +0100'
  date_gmt: '2009-02-20 13:48:25 +0100'
  content: "Ten zaver do kamene tesat. Takhle naivni jsem i pres svuj seniorsky vek
    docela casto. Sam pred sebou se omlouvam slovy \"Po bitve je kazdej general\".\r\n\r\nDiky
    za clanek."
- id: 6600
  author: Martin Jansa
  author_email: Martin.Jansa@gmail.com
  author_url: ''
  date: '2009-02-23 09:04:10 +0100'
  date_gmt: '2009-02-23 08:04:10 +0100'
  content: Nezouseli jste zmerit, jestli doba "mezi vložením času do HTTP response
    a zpracování HTTP response" odpovida zhruba polovine casu od odeslani requestu
    z klienta po zpracovani response? Pak by se to mozna mohlo ješte upravovat o tuto
    konstantu.
- id: 6601
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-02-23 09:40:16 +0100'
  date_gmt: '2009-02-23 08:40:16 +0100'
  content: Abych pravdu řekl, nezkoušeli. Současná přesnost je pro nás dostačující
    - rozdíly mezi uživateli nejsou už rozpoznatelné. Ale je to zajímavý nápad.
- id: 6626
  author: Jakub Vrána
  author_email: jakub@vrana.cz
  author_url: http://php.vrana.cz/
  date: '2009-02-25 13:00:35 +0100'
  date_gmt: '2009-02-25 12:00:35 +0100'
  content: "O zobrazení serverového času u klienta jsem před časem také psal: http://php.vrana.cz/zobrazeni-serveroveho-casu.php\r\n\r\nDoplním
    jen, že pokud bychom chtěli vyřešit nepřesnost časovače, dalo by se místo setInterval
    zavolat vždy setTimeout s vypočteným časem (mírně nižším než 1 s)."
- id: 6627
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-02-25 13:48:42 +0100'
  date_gmt: '2009-02-25 12:48:42 +0100'
  content: Podle mého názoru setTimeout trpí úplně stejnými nešvary jako setTimeout
    - princip je úplně stejný - jen setInterval se provádí opakovaně a setTimeout
    jedinkrát. Na vině je jednovláknovost prohlížeče, se kterou voláním jiné metody
    nic nezískáme. Každopádně díky za reakci.
- id: 6631
  author: Jakub Vrána
  author_email: jakub@vrana.cz
  author_url: http://php.vrana.cz/
  date: '2009-02-25 18:35:32 +0100'
  date_gmt: '2009-02-25 17:35:32 +0100'
  content: Měl jsem na mysli http://php.vrana.cz/pravidelne-spousteni-javascript-kodu.php
- id: 6633
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-02-25 19:32:24 +0100'
  date_gmt: '2009-02-25 18:32:24 +0100'
  content: Pochopil jsem co jste měl na mysli. Spíš na to reaguji ve smyslu - přestože
    v daném okamžiku víte, že máte zpoždění 50ms a načasujete tedy další timer na
    950ms místo 1000s nikde nemáte zaručeno, že se vám timer skutečně zavolá za 950ms
    a ne třeba až za 1300ms. Podle mého názoru tím daný problém neřešíte.
- id: 6640
  author: Jakub Vrána
  author_email: jakub@vrana.cz
  author_url: http://php.vrana.cz/
  date: '2009-02-26 16:54:53 +0100'
  date_gmt: '2009-02-26 15:54:53 +0100'
  content: Řeší to problém narůstajícího zpoždění.
- id: 6642
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-02-26 19:07:13 +0100'
  date_gmt: '2009-02-26 18:07:13 +0100'
  content: "Narůstajícího zpoždění možná, nikoliv však přesné zobrazení času v konkrétním
    okamžiku. Navíc se mi zdá, že třeba Firefox podobnou logiku uplatňuje již na setInterval
    - když na testovacím skriptu sleduji zpoždění, tak pokud naroste, tak se po nějaké
    chvíli zase sníží. Ale možná je to jen klam.\r\n\r\nKoukal jsem na ten kód, co
    uvádíte, a nepovedlo se mi vyextrahovat, jak by se choval v případě, že by zpoždění
    přesáhlo celý sledovaný interval. Tzn. kdyby v okamžiku N bylo zpoždění 0ms a
    v okamžiku N+1 třebas +1300ms, přičemž námi sledovaná perioda je 1000ms. Pak byste
    se totiž dostal do situace, kdy byste potřeboval další timeout nastavit na -300ms,
    což nepůjde."
- id: 6651
  author: Jakub Vrána
  author_email: jakub@vrana.cz
  author_url: http://php.vrana.cz/
  date: '2009-02-27 12:00:44 +0100'
  date_gmt: '2009-02-27 11:00:44 +0100'
  content: Na konci článku to zmiňuji. Řeším to žertem, v praktické implementaci by
    to asi chtělo funkci zavolat ihned znovu.
---
<p>Absolutním Cimrmanovým rýmem začínám další ze série článků o Javascriptu. V něm bych chtěl rozebrat pár postřehů při práci s časovači (timery) v JavaScriptu. Ty se používají k lecčemu - při jQuery animacích, zobrazování aktuálního času, periodickém dotazováním serveru atp. Intuitivně jsme vždycky tušili, že jejich časování nemusí být úplně přesné, ale přesto jsme hrubě podcenili význam pro aplikaci, pro kterou je aktuální čas zásadní.</p>
<p>Stáli jsme před relativně jednoduchým problémem. Odpočítávat čas do okamžiku T a vypočítávat slevu v ceně na základě času, který do okamžiku T zbývá. Samozřejmě všechny údaje (ať čas nebo cena) musely být u všech klientů naprosto stejné a musely se měnit každou vteřinu. Tento jednoduchý problém nás ale docela potrápil a proto vznikl tento článek, který by měl zachytit problémy a jejich řešení.</p>
<p><a id="more"></a><a id="more-291"></a></p>
<p>Všechny problémy byly způsobeny dvěma příčinami. Ta první je, že každý počítač klienta má odlišný čas a přes všechny synchronizace, které <a href="http://technet.microsoft.com/en-us/library/cc773013.aspx" target="_new">operační systémy provádí.</a>. Nezanedbatelná část klientů má čas posunutý zásadním způsobem v řádech minut nebo i hodin (a to přesto, že se pohybujeme ve stejném časovém pásmu).</p>
<p>Druhou je nepřesnost časovačů v prohlížečích. Pro ilustraci jsem připravil <a href="http://files.novoj.net/JavaScriptTimers/timers.html" target="_blank">jednoduchou testovací stránku</a>, kterou si sami můžete spustit v různých prohlížečích. Především v těch, kde je horší implementace JavaScriptu (starší verze prohlížečů nebo Internet Explorer), můžeme během první minuty lehce nasbírat zpoždění i několika vteřin.</p>
<p><a href="http://files.novoj.net/JavaScriptTimers/timers.html" target="_blank">Timer tester</a></p>
<p>Vysvětlení důvodu, proč se tak děje se můžete dočíst v článku Johna Resiga, kde rozebírá princip toho <a href="http://css.dzone.com/news/how-javascript-timers-work" target="_new">jak časovače v prohlížečích fungují</a>. Především je to dáno tím, že veškeré zpracování probíhá v jednom vlákně, takže v případě, že v danou chvíli prohlížeč vyřizuje jiný kus kódu (např. kód ošetřující kliknutí myši), spuštění časovače musí počkat (respektive se zafrontuje).</p>
<h3>Z našich chyb jsme si vzali několik poučení</h3>
<h4>browser má vždy jiný čas než server </h4>
<p>Nikdy nepracujte přímo s new Date() při vypočítávání zbývajícího času. Jediný způsob, jak synchronizovat čas všech klientů, je dostat na klienta aktuální serverový čas (i tak nebudete úplně přesní, protože mezi vložením času do HTTP response a zpracování HTTP response na klientovi nějaký čas - byť minimální - uběhne). Na klientu pak vypočtete odchylku systémového času klienta a systémového času serveru a o tuto odchylku upravujte všechna volání new Date() v logice klienta (nebo ještě lépe toto chování extrahujte do nějaké metody).</p>
<p><strong>Příklad:</strong></p>
<p>[source:javascript]<br />
var serverTimeDifference;</p>
<p>function setServerTime(serverTime) {<br />
   serverTimeDifference = new Date().getTime() - serverTime.getTime();<br />
}</p>
<p>function getActualTime() {<br />
   var actualTime = new Date();<br />
   actualTime.setTime(actualTime.getTime() - serverTimeDifference);<br />
   return actualTime;<br />
}<br />
[/source]</p>
<h4>na periodu časovačů se při výpočtech nelze spolehnout</h4>
<p>V logice na klientu nikdy nepočítejte s intervalem, který řídí spouštění aktualizační logiky, ale s aktuálním systémovým časem upraveným o odchylku. Přestože je to lákavé, odpočítávání času by nemělo fungovat tak, že si nastavíte timer na 1 sekundový interval a při zavolání metody z proměnné obsahující počet zbývajících sekund odečtete jedničku. Takto odpočet nebude vůbec přesný.</p>
<p>Řešením je přepsat aktualizační metodu tak, že vždy nanovo vypočte počet zbývajících sekund odečtením cílového času udaného serverem od aktuálního času ošetřeného o odchylku.</p>
<h3>Závěrem</h3>
<p>Když si ten článek po sobě čtu, tak si říkám: "Otec Fura objevil Ameriku". Je zvláštní jak hodně dokáže být člověk i po těch letech naivní.</p>
<h3>Reference</h3>
<ul>
<li><a href="http://css.dzone.com/news/how-javascript-timers-work" target="_blank">Článek Johna Resiga osvětlující prinicipy fungování Timerů v JavaScriptu</a></li>
<li><a href="http://ajaxian.com/archives/timing-in-javascript-and-browsers-cant-be-trusted" target="_blank"></a></li>
<li><a href="http://www.shearersoftware.com/software/web-tools/clock/" target="_blank">Článek narážející na podobný problém a řešení odchylky klientského času od času serveru</a></li>
<li><a href="http://ejohn.org/blog/accuracy-of-javascript-time/" target="_blank">Zajímavé zjištění Johna Resiga o problémech spouštění javascriptových performance testů na platformě MS Windows</a> - trošku off-topic ale velmi zajímavé čtení</li>
</ul>
