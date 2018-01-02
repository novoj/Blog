---
status: publish
published: true
title: Hackathon - RefactoringNG
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img src=\"http://blog.novoj.net/binary/2010/11/logo-minified.png\" alt=\"\"
  title=\"logo-minified\" width=\"150\" height=\"51\" class=\"alignleft size-full
  wp-image-1223\" /> Dnes proběhl další hackathon, který se zaměřil na RefactorNG
  plugin do NetBeans. <a href=\"http://kenai.com/projects/refactoringng\" target=\"_blank\">RefactoringNG</a>
  je modul pro NetBeans, který slouží k automatizované refaktorizaci kódu. Pro bližší
  seznámení doporučuji projít existující články na Java.cz: \n\n<ul style=\"margin-left:
  15em;\">\n   <li><a href=\"http://java.cz/article/refactoringng\">Úvod do RefactorNG</a></li>\n
  \  <li><a href=\"http://java.cz/article/refactoringngtovarna\">Refaktorizace - továrna</a></li>\n
  \  <li><a href=\"http://java.cz/article/refactoringngzamenametody\">Refaktorizace
  - záměna metody</a></li>\n   <li><a href=\"http://java.cz/article/refactoringngevolucerozhrani\">Refaktorizace
  - evoluce rozhraní</a></li>\n</ul>\n\nPlugin funguje tak, že v prostředí Netbeans
  můžete označit konkrétní Java zdrojáky (popř. balíky zdrojáků) a aplikovat na ně
  pravidla uložená v RNG souboru. Pravidla se skládají ze dvou částí - první obsahuje
  pattern, kterým se porovnává zkoumaný zdrojový Java soubor a pokud dojde ke shodě
  části AST stromu, je na tuto část aplikován pattern v druhé části pravidla, který
  provede požadované modifikace.\n\n"
wordpress_id: 1347
wordpress_url: http://blog.novoj.net/?p=1347
date: '2011-02-12 02:05:09 +0100'
date_gmt: '2011-02-12 01:05:09 +0100'
categories:
- Programování
- Reportáže
- Hackathon
tags: []
comments:
- id: 33676
  author: Zdeněk Troníček
  author_email: tronicek@fit.cvut.cz
  author_url: http://java.cz/blog/tronicek
  date: '2011-02-12 15:16:24 +0100'
  date_gmt: '2011-02-12 14:16:24 +0100'
  content: |-
    Honzo, byl tam ještě Denis Stepanov. Pokud o řádkové volání, tak já jsem samozřejmě pro. Zbývá to jen vykuchat z NetBeans refaktorizační framework a upravit RefactoringNG a je to!
    Jinak moje dojmy z včerejší akce jsem shrnul na http://java.cz/article/hackathon.
- id: 33680
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-02-12 16:09:20 +0100'
  date_gmt: '2011-02-12 15:09:20 +0100'
  content: Ahoj Zdeňku, vidíš, taková důležitá osoba pro náš včerejší večer a já na
    něj zapomenu. Díky - opraveno. Jdu si přečíst tvůj článek.
- id: 33692
  author: Tweets that mention Myšlenky dne otce Fura » Blog Archive » Hackathon –
    RefactoringNG -- Topsy.com
  author_email: ''
  author_url: http://topsy.com/blog.novoj.net/2011/02/12/hackathon-refactoringng/?utm_source=pingback&amp;utm_campaign=L2
  date: '2011-02-12 22:16:37 +0100'
  date_gmt: '2011-02-12 21:16:37 +0100'
  content: "[...] This post was mentioned on Twitter by Jan Novotný, Michal Bernhard.
    Michal Bernhard said: hezky report z #hackathon od @novoj : http://bit.ly/hCSQt1
    [...]"
---
<p><img src="http://blog.novoj.net/binary/2010/11/logo-minified.png" alt="" title="logo-minified" width="150" height="51" class="alignleft size-full wp-image-1223" /> Dnes proběhl další hackathon, který se zaměřil na RefactorNG plugin do NetBeans. <a href="http://kenai.com/projects/refactoringng" target="_blank">RefactoringNG</a> je modul pro NetBeans, který slouží k automatizované refaktorizaci kódu. Pro bližší seznámení doporučuji projít existující články na Java.cz: </p>
<ul style="margin-left: 15em;">
<li><a href="http://java.cz/article/refactoringng">Úvod do RefactorNG</a></li>
<li><a href="http://java.cz/article/refactoringngtovarna">Refaktorizace - továrna</a></li>
<li><a href="http://java.cz/article/refactoringngzamenametody">Refaktorizace - záměna metody</a></li>
<li><a href="http://java.cz/article/refactoringngevolucerozhrani">Refaktorizace - evoluce rozhraní</a></li>
</ul>
<p>Plugin funguje tak, že v prostředí Netbeans můžete označit konkrétní Java zdrojáky (popř. balíky zdrojáků) a aplikovat na ně pravidla uložená v RNG souboru. Pravidla se skládají ze dvou částí - první obsahuje pattern, kterým se porovnává zkoumaný zdrojový Java soubor a pokud dojde ke shodě části AST stromu, je na tuto část aplikován pattern v druhé části pravidla, který provede požadované modifikace.</p>
<p><a id="more"></a><a id="more-1347"></a></p>
<p>RefactorNG pracuje na úrovni AST připraveného Javac parserem a tudíž je s ním pevně svázaný (používají se třídy z com.sun). Aby mohl člověk psát kvalitní pravidla je znalost AST v zásadě nutná. Běžně může docházet k takovým věcem, že pravidlo zapsané pro náhradu volání date.toString() za date.toGMTString() v následujícím snippetu směle nahradí výskyt #1, zato v #2 jej vynechá (protože na tomto místě vypadá AST jinak):</p>
<p>[source lang="java"]<br />
Date date = new Date();<br />
//#1<br />
String time = date.toString();<br />
//#2<br />
new Date().toString();<br />
[/source]</p>
<p>Aktuálně není možné pravidla spouštět mimo IDE NetBeans, i když jsem Zdeňka lámal, aby zvážil headless variantu pro volání RNG skriptů z řádkových build nástrojů. Nu, uvidíme.</p>
<p>Na hackathonu se nás tentokrát sešlo 7 s jedním člověkem připojeným přes Skype. V úvodní hodině jsme se seznámili s principy modulu a během večera padly za vlast 4 issue z BugTrackeru a před jedním požadavkem na rozšíření jsme museli kapitulovat:</p>
<ul>
<li><a href="http://kenai.com/bugzilla/show_bug.cgi?id=3701" target="_blank">Better names for refactoring rules</a></li>
<li><a href="http://kenai.com/bugzilla/show_bug.cgi?id=3691" target="_blank">Insert the closing brace automatically</a></li>
<li><a href="http://kenai.com/bugzilla/show_bug.cgi?id=3692" target="_blank">Indentation of closing brace</a></li>
<li><a href="http://kenai.com/bugzilla/show_bug.cgi?id=4016" target="_blank">NullPointerException when typing ref</a></li>
</ul>
<p>Musím smeknout před Zdeňkem Troníčkem, který postavil API nad málo nebo vůbec dokumentovanými třídami NetBeans a ne jednoduchou dokumentací Java parseru. Osobně jsem v průběhu večera pochytil jen nějaké základní principy, ale že bych byl v obraze to se opravdu říct nedá. Reflexní API je proti API kompilátoru hračka - rovnat tomu se snad může jen vyhodnocování generik, se kterým jsem si užil také pár perných chvilek.</p>
<p>Tímto bych chtěl za Zdeňka poděkovat všem zúčastněným: Michalovi Bernhardovi, Pavlu Jetenskému, Michalovi Škrdlovi, Vlastimilu Dolejšovi, Denisovi Štěpanovi a především Váškovi Pechovi, který poskytl útočiště v sídle JetBrains a zajistil pití a pizzu.</p>
<p>Pokud byste se chtěli účastnit dalšího hackathonu, nebo měli nějaké nápady na OS projekty, které by potřebovali ofixovat pár issues v trackeru, zapojte se do <a href="https://groups.google.com/group/czech-hackathon-group" target="_blank">naší google grupy</a>. Vítán je každý.</p>
<p>[gallery columns="2"]</p>
