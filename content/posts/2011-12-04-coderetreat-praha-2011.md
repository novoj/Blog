---
status: publish
published: true
title: CodeRetreat Praha 2011
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img src=\"http://blog.novoj.net/binary/2011/12/codeRetreat.jpg\" alt=\"Organizátoři
  byli večer skutečně znavení\" title=\"Organizátoři byli večer skutečně znavení\"
  width=\"100\" height=\"102\" class=\"alignleft size-full wp-image-1726\" />Nikdy,
  nikdy nepodlehněte své lenosti. Všichni známe předvánoční čas plný akcí a večírků
  a uznávám, že včera jsem velmi zvažoval, jestli chci na <a href=\"http://coderetreat.cz/\"
  target=\"_blank\">CodeRetreat</a> vlastně jet a zmizet o desíti z jiné akce s přáteli
  úplně střízlivý. Přiznávám svou slabost a stydím se, že jsem vůbec kdy zapochyboval.
  CodeRetreat byl jednou z mých letošních nejlepších akcí a musím říct, že naboural
  žebříček nejhodnotnějších akcí vůbec. Přičemž i příčka jOpenSpace se zachvěla ve
  svých základech.\r\n\r\n<strong>Vstupy:</strong>\r\n\r\n1. lidi, co chtějí o víkendu
  kódovat (zázrak sám o sobě a předvýběr jako sviňa)\r\n2. na první pohled jednoduchý
  problém k vyřešení v nereálném čase\r\n3. podmínka TDD, párové programování, změny
  párů v 45 minutových intervalech\r\n\r\n<strong>Důsledky:</strong>\r\n\r\n1. střídání
  programovacích jazyků, IDE, klávesnic i programátorských přístupů\r\n2. přistoupení
  na hru, že cesta je cíl\r\n3. destilovaný programátorský zážitek\r\n\r\n"
wordpress_id: 1723
wordpress_url: http://blog.novoj.net/?p=1723
date: '2011-12-04 01:30:51 +0100'
date_gmt: '2011-12-04 00:30:51 +0100'
categories:
- Programování
- Reportáže
tags: []
comments:
- id: 56004
  author: Robert Dresler
  author_email: dresler.robert@gmail.com
  author_url: http://www.robertdresler.cz/
  date: '2011-12-04 13:39:41 +0100'
  date_gmt: '2011-12-04 12:39:41 +0100'
  content: "Bezva reportáž! O to víc mě mrzí, že jsem se nezúčastnil :(\r\nDotaz na
    účastníky: Dá se podobná akce udělat např. v rámci firmy, je organizace složitá?"
- id: 56024
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-12-04 23:08:24 +0100'
  date_gmt: '2011-12-04 22:08:24 +0100'
  content: 'Není a návody a rady jsou přímo na: http://coderetreat.org/hosting'
- id: 56060
  author: Martin
  author_email: martin@netsafe.cz
  author_url: ''
  date: '2011-12-05 09:59:38 +0100'
  date_gmt: '2011-12-05 08:59:38 +0100'
  content: V ramci firmy mame v netsafe vyzkouseny Coding Dojos. Funguje to moc dobre.
    Marian nebo ja se  kdyztak muzem podelit o zkusenosti.
- id: 57941
  author: Jety
  author_email: pavel.jetensky@seznam.cz
  author_url: http://jetensky.net/blog
  date: '2011-12-27 20:18:36 +0100'
  date_gmt: '2011-12-27 19:18:36 +0100'
  content: Díky za článek, Honzo, zajímavě jsem si početl.
---
<p><img src="http://blog.novoj.net/binary/2011/12/codeRetreat.jpg" alt="Organizátoři byli večer skutečně znavení" title="Organizátoři byli večer skutečně znavení" width="100" height="102" class="alignleft size-full wp-image-1726" />Nikdy, nikdy nepodlehněte své lenosti. Všichni známe předvánoční čas plný akcí a večírků a uznávám, že včera jsem velmi zvažoval, jestli chci na <a href="http://coderetreat.cz/" target="_blank">CodeRetreat</a> vlastně jet a zmizet o desíti z jiné akce s přáteli úplně střízlivý. Přiznávám svou slabost a stydím se, že jsem vůbec kdy zapochyboval. CodeRetreat byl jednou z mých letošních nejlepších akcí a musím říct, že naboural žebříček nejhodnotnějších akcí vůbec. Přičemž i příčka jOpenSpace se zachvěla ve svých základech.</p>
<p><strong>Vstupy:</strong></p>
<p>1. lidi, co chtějí o víkendu kódovat (zázrak sám o sobě a předvýběr jako sviňa)<br />
2. na první pohled jednoduchý problém k vyřešení v nereálném čase<br />
3. podmínka TDD, párové programování, změny párů v 45 minutových intervalech</p>
<p><strong>Důsledky:</strong></p>
<p>1. střídání programovacích jazyků, IDE, klávesnic i programátorských přístupů<br />
2. přistoupení na hru, že cesta je cíl<br />
3. destilovaný programátorský zážitek</p>
<p><a id="more"></a><a id="more-1723"></a></p>
<p>Podstatou problému byla tzv. <a href="http://en.wikipedia.org/wiki/Conway's_Game_of_Life" target="_blank">Game of life</a> reprezentovaná čtyřmi pravidly, která nečiní problém komukoliv v jakémkoliv jazyce nakódovat, přičemž jsou tak jednouchá, že je musí v naivní variantě spráskat i student s prvním ročníkem programování. Na druhou stranu je to problém s otevřeným koncem - tedy cesta po které se dá jít ještě dál, než jste si napoprvé mysleli, že je možné dojít (trošku mi to připomíná náš přijímací pohovor do Forresta). Záleží jen na tom, jaké všechny okolnosti vezmete při svém přemýšlení v úvahu. Začnete ve svém dvourozměrným polem a skončíte u nekonečného vesmíru, vezmete v potaz dvoudimenzionalní prostor a zkusíte si jak by vypadal propočet ve vícedimenzionálním, zkusíte si algoritmus v Javě, C# v DARTu nebo Groovy (nekecám, tím jsem si dneska opravdu prošel).</p>
<p>Po první iteraci zcela ztratíte chuť dělat to vážně a začnete to brát jako hru. Hra má pevná pravidla, do které vstupujete s vámi akceptovanými zjednodušeníni a unikátním přístupem, po dohodě s vaším parťákem. To vše (kromě 4 pevných pravidel) se po 45 minutách a změně vašeho kolegy mění. Nikdo se nechce nudit a proto pokaždé berete stejný problém z jiného úhlu a přicházíte na lepší řešení. Máte jeden notebook a kolega vás bije přes prsty, když sklouznete dříve k implementaci logiky před implementací testu (mimochodem prsty mám dnes úplně omlácené :D).</p>
<p>Dnešní den byl vyjímečný i tím, že CodeRetreat se odehrál po celém světě, snad ve všech časových pásmech. Už ráno po páté ve vlaku do Prahy jsem četl tweety z Melbourne, Tokia a HongKongu, že CodeRetreat u nich právě začal. Když jsem si postesknul, že ve vývojářských luzích a hájích je to samý chlap (v Čechách kodérky asi nejsou :( ), dostal jsem odpověď z Berlína, že alespoň dvě členky něžného pohlavi se v našich řadách přeci jen nacházejí. Poslední uzavírací tweet, přišel po pár hodinách z Honolulu, kde se CodeRetreat letošního roku uzavřel. Člověk si hned nepřipadá blbě, když se po celém světě najdou lidi ochotní jít do podobné záležitosti s ním.</p>
<p>Paradoxem je, že díky triviálnímu problému si člověk dokáže vyzkoušet během pár hodin plno věcí - stačí se soustředit a nemít cíl. Velkým překvapením je pro mě dnes DART - spolu s <a href="https://twitter.com/#!/kolman" target="_blank">@kolman</a> jsme si chvíli hráli s problémem v DARTu (mimochodem díky za energii věnovanou zprovznění vývojového prostředí) a došli jsme k závěru, že DART je v podstatě mixem C# a Javy. Vzhledem k velmi obtížně dohledatelné dokumentaci jsme skutečně jeli stylem test -> implementace a když se nám DART nechtěl zkompilovat, tak jsme syntaxi C# a Javy vyměnili (@kolman je .NETista a já Javista) nebo naopak a kompilátor na jednu z variant zabral. Jen tak trochu nevím, na které publikum Google s DARTem míří - že by na obě?</p>
<p>Krásně bylo vidět, jak enterprise jazyky jako je C# nebo Java v produktivitě zaostávají za jazyky jako je Groovy (alespoň na problému tohoto typu). Pravda je, že v neproduktivních jazycích jsme si byli, na druhou stranu, daleko víc jistí v kramflecích. Velmi zábavná mi připadla TDD hra - napiš test a já implementaci, která tvému testu vyhoví (samozřejmě tě zkusím obelhat), kterou jsem v poslední iterací hrál s <a href="https://twitter.com/#!/philipp_riemer" target="_blank">@philipp_riemer</a> (němec z Norimberka tč. studující v Praze na VŠE).</p>
<p>Ještě jednou díky všem českým organizátorům, sponzorům (<a href="http://gmchk.cz/" target="_blank">GMC</a>) a firmě <a href="http://www.jetbrains.com/" target="_blank">JetBrains</a> za licence IDE pro šťastného výherce a trička pro všechny (co jsem dokázal na zádech z Pardubic unést). Mimochodem - doteď nechápu, jaktože M$ ještě nenavázal s JetBrains úzkou spolupráci - dnes jsem neviděl Visual Studio bez Resharperu (kdo ví, jestli byli všechny legální? :D ).</p>
<p><strong>WTF: M$ can't you make proper IDE for your developers on your own?</strong></p>
