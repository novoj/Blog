---
status: publish
published: true
title: Tak Forresti taky přešli na Git, paní Millerová
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft  wp-image-2644\" title=\"git\" src=\"http://blog.novoj.net/binary/2013/07/git-300x125.png\"
  alt=\"\" width=\"210\" height=\"88\" />Ve Forrestu jsme jako verzovací systém používali
  po velmi dlouhou dobu prastaré CVS. Respektive v době, kdy se s tím ve firmě začínalo
  (pamětníků už je jen hrstka) to zase až taky zastaralý systém nebyl (mluvíme o roku
  2000). Dlouhou dobu jsme zvažovali náhradu za nějaké modernější VCS, ale nikdo se
  toho nechtěl osobně ujmout a byla tady celá řada překážek, se kterými bychom se
  museli kvůli přechodu vypořádat. Kromě infrastruktury (háčky do issue trackeru,
  build a install skripty, zálohování atd.) jsme měli obavu i o to, jak by přechod
  zvládly ty desítky vývojářů, kteří CVS používají - kritické místo se nám zdál tým
  webmasterů starající se o drobné úpravy na existujících projektech (v řádu desítek
  úprav denně). Prostě jsme <a href=\"http://www.mitvsehotovo.cz/2013/07/proc-to-vzdavam-prave-ja/\"
  target=\"_blank\">hledali výmluvy</a>, protože se nám do migrace nechtělo - zvlášť,
  když jsme neměli uvnitř firmy nikoho, kdo by nějaké nové VCS evangelizoval.\r\n\r\nSamozřejmě
  existovaly i poměrně důležité motivy, proč se do migrace pustit - kromě nešvarů,
  které CVS mělo od svých prvopočátků (nemožnost odstraňovat složky, nemožnost přesunovat
  soubory - tj. při refaktoringu docházelo ke ztrátě historie, obtížné slučování nezávislých
  vývojových větví atp.) jsme věděli, že i vývojářské nástroje dříve nebo později
  začnou od podpory CVS ustupovat a i kdyby ne, investice do tohoto VCS bude nulová.
  Svět už prostě CVS nezajímá poměrně dlouho a jiné už to nebude. Řada z nás tak měla
  pocit, že nám tady ujíždí (pokud už dávno neujel) vlak. Někteří z nás, sice přišli
  do styku s Gitem na nějakých OS projektech, ale to rozhodně nestačilo na to, abychom
  se ho dokázali pořádně naučit.\r\n\r\nZkrátka jsme přešlapovali na skokánku a ostýchali
  se skočit.\r\n\r\n"
wordpress_id: 2637
wordpress_url: http://blog.novoj.net/?p=2637
date: '2013-07-07 21:04:02 +0200'
date_gmt: '2013-07-07 20:04:02 +0200'
categories:
- Programování
tags: []
comments:
- id: 152032
  author: banter
  author_email: lubos.racansky@gmail.com
  author_url: http://blog.zvestov.cz
  date: '2013-07-07 21:26:35 +0200'
  date_gmt: '2013-07-07 20:26:35 +0200'
  content: "Opět připomínám video již z roku 2007, kdy Linus Torvalds představuje
    koncept Gitu (zcela netechnicky, \"jen\" principy) v Google. http://www.zdrojak.cz/zpravicky/video-na-vikend-linus-torvalds-o-gitu/\r\n\r\nDocela
    závidím, že se vám to podařilo nasadit. Sice CVS už pár let nepoužívám, ale SVN
    neumožňuje invazivně nasadit code review (jako třeba pomocí gerrit)"
- id: 152033
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-07-07 21:40:46 +0200'
  date_gmt: '2013-07-07 20:40:46 +0200'
  content: "To video jsem viděl a Linus je místy dost hustej :)\r\nNastavení formálnějšího
    code review je další krok - aktuální ad-hoc způsob, který děláme nepřináší takové
    benefity, které bych si představoval :/ Byl jsem na přednášce kluků ze Suse Linuxu
    a jejich způsob code review bych chtěl dostat i k nám. Minimálně na vývoj produktů.
    Snad to půjde ..."
- id: 152034
  author: banter
  author_email: lubos.racansky@gmail.com
  author_url: http://blog.zvestov.cz
  date: '2013-07-08 04:38:39 +0200'
  date_gmt: '2013-07-08 03:38:39 +0200'
  content: Přesně, ad-hoc review není ono. Chystám se na blog sepsat poznámky z knihy
    <a href="http://smartbear.com/SmartBear/media/pdfs/best-kept-secrets-of-peer-code-review.pdf"
    rel="nofollow">Best Kept Secrets of Peer Code Review</a>
- id: 152036
  author: michalfranc
  author_email: michal.franc@gmail.com
  author_url: ''
  date: '2013-07-08 08:48:43 +0200'
  date_gmt: '2013-07-08 07:48:43 +0200'
  content: "K těm poděkováním se sluší doplnit: \r\nDíky Honzo, za zorganizování školeníčka
    :o)\r\n\r\nJinak jasně se ukazuje, jak je důležité měnit vše s čím člověk není
    úplně spokojený a hlavně, že změnu u nás může prosadit každý, jen do toho jít."
- id: 152038
  author: KarelI
  author_email: artur@seznam.cz
  author_url: ''
  date: '2013-07-09 12:19:51 +0200'
  date_gmt: '2013-07-09 11:19:51 +0200'
  content: Docela me prekvapilo ze jste dokazali tak dlouho vyrzet s necim takovym,
    pripada mi ze vam ve firme schazeji nadsenci co by zkoumali nove veci a chteli
    zlepsit postupy. U nas ve firme uz by si hodne lidi neunosne stezovalo ze musi
    pouzivat CVS. Na druhou stranu je dobre ze jste si to sami uvedomili, tak jen
    pripominam, ze zlepsovani je nekonecny proces :-)
- id: 152039
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-07-09 13:42:05 +0200'
  date_gmt: '2013-07-09 12:42:05 +0200'
  content: "Co na to říct :) ... není nás pět v jednom kanclu abychom mohli měnit
    věci raketovou rychlostí ze dne na den. Neřekl bych, že nám chybí nadšenci - spíš
    je tolik oblastí, kde je možné zlepšovat, že se nedá všechno řešit najednou.\r\n\r\nV
    oblasti VCS jsme určitě měli být rychlejší - to nezastírám. A pořád nám tu zbývá
    ještě dost kostlivců, se kterými se musíme vypořádat. Neříkej, že vy žádné ve
    skříni nemáte ;)"
- id: 152040
  author: KarelI
  author_email: artur@seznam.cz
  author_url: ''
  date: '2013-07-09 14:43:58 +0200'
  date_gmt: '2013-07-09 13:43:58 +0200'
  content: "Opravdu jsem se ted uprimne zamyslel ( :-) ) a nevim o zadnem kostlivci
    v tom smyslu ze by byl ve skrini a nenasel by se nikdo kdo by ji chtel otevrit
    a kostlivce vyhnat. Mame par lidi kteri resi jen procesy a prehledy. Admin je
    akcni a kdyz mu reknem ze chcem vyzkouset nejaky tool, tak ho ochotne instaluje.
    Kdyz se vyskytne cokoli co nas brzdi v praci a nevyresi se to samo behem par tydnu,
    tak se tim nekdo cilene zabyva. Dokonce i prubezne prepisujeme nejhorsi a zabugovany
    kusy kodu, je to sice na dlouhy lokte, ale resi se to.\r\n\r\nJasny, nebylo to
    tak vzdy, byly doby kdy se nechavalo vsechno jen vyhnit, ale prisla tezka doba
    a museli jsme s tim zacit neco delat, takze zhruba poslednich 8 let prubezne a
    cilene zlepsujeme. Treba takovy Joel Test je pro nas zaklad ktereho jsme dosahli
    uz davno."
- id: 152041
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-07-09 15:13:57 +0200'
  date_gmt: '2013-07-09 14:13:57 +0200'
  content: A kde děláš? Takovýhle přístup si zaslouží reklamu! :)
- id: 152042
  author: KarelI
  author_email: artur@seznam.cz
  author_url: ''
  date: '2013-07-10 08:20:07 +0200'
  date_gmt: '2013-07-10 07:20:07 +0200'
  content: "Nejak nevidim tlacitko odpovedet u posledniho prispevku...\r\n\r\nNo my
    delame docela specialni desktop app pro modelovani a vypocty a mame docela vysoky
    naroky, takze jentak nekdo k nam nemuze a taky by to jen tak nekoho nebavilo,
    takze verim ze se vzajemne najdeme i bez reklamy :-) . Ne, vazne to nechci rikat.\r\n\r\nJeste
    k codereview ktere tu bylo zmineno - pouzivame CodeCollaborator, vse co ma jit
    do hlavni vetve musi byt prohlednuto interne v ramci tymu a pak nekolika lidma
    z jinych tymu a najde se tim docela dost chyb..."
- id: 152043
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-07-10 08:49:32 +0200'
  date_gmt: '2013-07-10 07:49:32 +0200'
  content: "No ona je ta diskuse max. 3-úrovňová - proto to chybějící tlačítko :)\r\n\r\nCode
    Collaborator = http://smartbear.com/products/software-development/code-review
    ?\r\nJá jsem taky přesvědčený o tom, že by formální code review dost věcí vyřešilo,
    ale teprve se k tomu propracováváme ... zatím jen ad-hoc, takže to někteří dělají,
    ale ne na všechno a někdo to nedělá vůbec  :( . \r\n\r\nOno tím, jak děláme desítky
    projektů a leckteré z nich jsou prostě jen chytřejší weby, tak ne všude to má
    smysl dělat - tj. hledáme i rozumný kompromis ve smyslu cena/přínos."
- id: 152045
  author: banter
  author_email: lubos.racansky@gmail.com
  author_url: http://blog.zvestov.cz
  date: '2013-07-11 08:06:42 +0200'
  date_gmt: '2013-07-11 07:06:42 +0200'
  content: "@Karell Nedělej fóry a řekni, kde děláš. Taky by mě to zajímalo. Takových
    firem moc není a ještě se schovávají. Nevidím v tom smysl."
- id: 152050
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-07-13 13:25:36 +0200'
  date_gmt: '2013-07-13 12:25:36 +0200'
  content: Koukal jsem na ten Code Collaborator a sice na jednu stranu vypadá pěkně,
    ale na druhou  dost enterprise. Skoro se mi to zdá jako zbytečný overhead pro
    malý tým. Nestačily by prostě jen neformální žádosti formou pull requestů?
- id: 152051
  author: Guido
  author_email: vit.kotacka@gmail.com
  author_url: http://www.sw-samuraj.cz/
  date: '2013-07-14 21:49:41 +0200'
  date_gmt: '2013-07-14 20:49:41 +0200'
  content: Docela by mě zajímalo, jestli to rozhodování Git/Mercurial nebylo jen formální.
    Šli jste u toho do hloubky, nebo to bylo spíš ve stylu Git je cool, používají
    ho všichni - Linus i Franta Vomáčka...?
- id: 152052
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-07-15 06:15:20 +0200'
  date_gmt: '2013-07-15 05:15:20 +0200'
  content: "Žádný sofistikovaný rozhodovací proces to nebyl. Předcházelo tomu pár
    diskusí a shodli jsme se na tom, že abychom si dokázali objektivně vybrat, museli
    bychom oba dva zkusit reálně nasadit. S tím Gitem byla teď zrovna příležitost
    na projektu RunCzech, protože spolupracující firma Git používá a usnadnilo nám
    to spolupráci. Takže jsme se rozhodli vyzkoušet jako první Git. Navíc pro Git
    hrály do noty i další faktory, jako je právě penetrace na trhu (používá ho Linus
    i Franta Vomáčka) a díky tomu je na netu k dispozici dost informací a řešení problémů.\r\n\r\nKdyž
    si přečteš třeba porovnání Git a Mercurial od Attlassianu:\r\n\r\nhttp://blogs.atlassian.com/2012/03/git-vs-mercurial-why-git/\r\nhttp://blogs.atlassian.com/2012/02/mercurial-vs-git-why-mercurial/\r\n\r\nTak
    ti to do ruky taky nedá žádné rozhodující argumenty. Rozhodně ne do doby, než
    si to s nějakým DVCS na vážno zkusíš. Takže spíš než kvalifikovaným výběrem bych
    to nazval intuitivní shodou více lidí jít tudy a zjistit, jaké problémy a pozitiva
    to přináší."
- id: 152053
  author: banter
  author_email: lubos.racansky@gmail.com
  author_url: http://blog.zvestov.cz
  date: '2013-07-15 08:35:46 +0200'
  date_gmt: '2013-07-15 07:35:46 +0200'
  content: 'Jen jsem ty články prolétl, ale líbilo se mi tam, že "git doesn’t actually
    track renames". Často používám svn blame, jdu si pro radu, ale slyším jen: "Já
    to nepsal, my jen přesouvali moduly".'
- id: 152371
  author: Jakub Ječmínek (@JecminekJakub)
  author_email: JecminekJakub@twitter.example.com
  author_url: http://twitter.com/JecminekJakub
  date: '2014-04-13 20:43:07 +0200'
  date_gmt: '2014-04-13 19:43:07 +0200'
  content: "Jen pro zajimavost, co pouzivate pro managovani gitovych repozitaru?\r\nGitosis?
    Gitolite nebo neco jineho?"
- id: 152375
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2014-04-18 11:52:31 +0200'
  date_gmt: '2014-04-18 10:52:31 +0200'
  content: Gitolite ... na zobrazování přes web http://www.gitalist.com/ ale reálně
    to nikdo z developerů moc nepoužívá a pracujeme s Gitem z IDE nebo přes příkazovou
    řádku ... máme interně issue na vyzkoušení https://github.com/takezoe/gitbucket
    ... ale ta teď aktuálně spí. Zkrátka zatím nás to moc netlačí.
- id: 152376
  author: Jakub Ječmínek (@JecminekJakub)
  author_email: JecminekJakub@twitter.example.com
  author_url: http://twitter.com/JecminekJakub
  date: '2014-04-18 18:58:11 +0200'
  date_gmt: '2014-04-18 17:58:11 +0200'
  content: My ve firme uspesne pouzivame gitosis, ale poohlizime se po necem co by
    odpovidalo githubu. Zatim se jako nejlepsi kandidat zda byt gitlab https://www.gitlab.com/
    Je zcela zdarma(open source) a jen vyzaduje debian/ubuntu server. Ja bych jeste
    doporucil gerrit https://code.google.com/p/gerrit/ je to sice nastroj primarne
    urceny na code review ale ma i zabudovanou spravu gitovych repozitaru.
- id: 152807
  author: Zdenek Henek
  author_email: vrablik@gmail.com
  author_url: http://gravatar.com/vrablik
  date: '2014-07-24 16:55:21 +0200'
  date_gmt: '2014-07-24 15:55:21 +0200'
  content: "Pouzivame celkem uspesne GitBlit http://www.gitblit.com/\r\n\r\numi post
    commit hooky, takze spojeni s CI serverem (jenkins) je celkem jednoduche\r\n\r\nGitblit
    ma indexovany commit zpravy, takze se f tom da hledat, napriklad podle ID z jiry
    ..."
---
<p><img class="alignleft  wp-image-2644" title="git" src="http://blog.novoj.net/binary/2013/07/git-300x125.png" alt="" width="210" height="88" />Ve Forrestu jsme jako verzovací systém používali po velmi dlouhou dobu prastaré CVS. Respektive v době, kdy se s tím ve firmě začínalo (pamětníků už je jen hrstka) to zase až taky zastaralý systém nebyl (mluvíme o roku 2000). Dlouhou dobu jsme zvažovali náhradu za nějaké modernější VCS, ale nikdo se toho nechtěl osobně ujmout a byla tady celá řada překážek, se kterými bychom se museli kvůli přechodu vypořádat. Kromě infrastruktury (háčky do issue trackeru, build a install skripty, zálohování atd.) jsme měli obavu i o to, jak by přechod zvládly ty desítky vývojářů, kteří CVS používají - kritické místo se nám zdál tým webmasterů starající se o drobné úpravy na existujících projektech (v řádu desítek úprav denně). Prostě jsme <a href="http://www.mitvsehotovo.cz/2013/07/proc-to-vzdavam-prave-ja/" target="_blank">hledali výmluvy</a>, protože se nám do migrace nechtělo - zvlášť, když jsme neměli uvnitř firmy nikoho, kdo by nějaké nové VCS evangelizoval.</p>
<p>Samozřejmě existovaly i poměrně důležité motivy, proč se do migrace pustit - kromě nešvarů, které CVS mělo od svých prvopočátků (nemožnost odstraňovat složky, nemožnost přesunovat soubory - tj. při refaktoringu docházelo ke ztrátě historie, obtížné slučování nezávislých vývojových větví atp.) jsme věděli, že i vývojářské nástroje dříve nebo později začnou od podpory CVS ustupovat a i kdyby ne, investice do tohoto VCS bude nulová. Svět už prostě CVS nezajímá poměrně dlouho a jiné už to nebude. Řada z nás tak měla pocit, že nám tady ujíždí (pokud už dávno neujel) vlak. Někteří z nás, sice přišli do styku s Gitem na nějakých OS projektech, ale to rozhodně nestačilo na to, abychom se ho dokázali pořádně naučit.</p>
<p>Zkrátka jsme přešlapovali na skokánku a ostýchali se skočit.</p>
<p><a id="more"></a><a id="more-2637"></a></p>
<p>Důležitým impulsem pro nás byla spolupráce s <a href="http://www.inmite.eu/" target="_blank">Inmite </a>na projektu <a href="http://www.runczech.com/" target="_blank">RunCzech.cz</a> - sdílení zdrojových kódu v CVS s externí firmou totiž znamenalo řadu komplikací, které nás donutily k zamyšlení. Když přišel náš hlavní vývojář projektu RunCzech (díky <a href="https://twitter.com/MichalKolesnac" target="_blank">Michale</a>) s návrhem realizovat projekt nad Gitem, chopili jsme se toho jako příležitosti prototypového nasazení. Jak už jsem <a href="http://blog.novoj.net/2012/04/19/partyzanskou-stezkou/" target="_blank">tady kdysi psal</a>, za většinou zásadních rozhodnutí ve firmě, stojí osobní odvaha jednotlivých lidí a v tomto případě to nebylo jinak.</p>
<p>Když jsme uvažovali o migraci VCS, měli jsme v hledáčku jen dvě možnosti - <a href="http://git-scm.com/" target="_blank">Git </a>nebo <a href="http://mercurial.selenic.com/" target="_blank">Mercurial </a>(věděli jsme, že chceme jít směrem <a href="http://en.wikipedia.org/wiki/Distributed_version_control_system" target="_blank">DVCS</a>). Pro Git hovořila větší penetrace na trhu, lepší podpora v nástrojích a také to, že někteří z nás už s Gitem jakés takés zkušenosti měli. V lednu tohoto roku jsme byli tedy rozhodnuti prototypově nasadit Git a teprve, kdybychom narazili na nějaké zásadnější problémy, vyzkoušet na jiném projektu Mercurial.</p>
<p>Po několika měsících se však ukázalo, že cesta je průchozí a přináší víc pozitiv než problémů (i když na pár zapeklitostí jsme po cestě také narazili). Tým, který realizoval projekt pro RunCzech se použitím Gitu prokousal sám, ale pro zbytek vývojářů jsme už zorganizovali <a href="http://webexpo.cz/academy/kurzy/git-distribuovany-verzovaci-system-pro-kazdeho" target="_blank">školení od WebExpo Academy</a> pod taktovkou <a href="http://blog.prskavec.net/" target="_blank">Ladislava Prskavce</a>. Školení bylo výborné a musím říct, že mi v některých ohledech otevřelo oči (a to jsem už Git sem tam používal) - rozhodně jsme všichni odcházeli s pocitem, že základním pochodům a principům Gitu rozumíme (a se zbytkem nám už pomůže pan Google).</p>
<p>Po necelém půl roce máme základní infrastrukturu pro Git připravenou, základní projekty zmigrované a všechny nové projekty už zakládáme pod Gitem. Nakonec nebyl přechod ani z poloviny tak problematický, jak jsme si mysleli že bude.</p>
<h3>Ponaučení</h3>
<p>Z dnešního pohledu vidím naše váhání jako velkou chybu a to především chybu nás seniorů, kteří jsme za tyto věci primárně zodpovědní. Už dlouhou dobu bylo zcela evidentní, že CVS budoucnost nemá a spíše dřív nebo později pro nás začne být limitující. Ačkoliv jsme toto dobře věděli, zdálo se nám, že cena za přechod bude příliš veliká kvůli "objektivním" překážkám a "specifickému" způsobu fungování uvnitř firmy. Byl to ale pouze přelud, za který se maskovala naše lenost a nedostatek odvahy udělat změnu.</p>
<p>Na druhou stranu se mi zdá, že ve chvíli, kdy jsme se rozhoupali, už byla posloupnost kroků poměrně optimální. Prototypové období trvalo cca 3 měsíce a ukázalo nám, že neexistují zásadní překážky, proč by Git neměl být nasazen všude. Navíc jsme díky tomu získali první "odborníky" uvnitř firmy, kteří byli schopni poskytnout alespoň základní podporu a rady ostatním v začátcích. Na prototypovém nasazení jsme si navíc ověřili, že Git je akceptovatelný jak Java, tak i Web developery, což je pro nás klíčové.</p>
<p>Před dalším rozšířením jsme přes školení dostali základní představu o fungování Gitu mezi další lidi a ujasnili řadu věcí i našim prvním "odborníkům". Od té chvíle jsme začali nasazovat Git všude a začali migrovat naše hlavní knihovny pomocí <a href="http://cvs2svn.tigris.org/cvs2git.html" target="_blank">Cvs2Git</a> (díky <a href="https://twitter.com/michalfranc" target="_blank">Frci</a>) a snažíme se, aby většina lidí, co byli na školení měla příležitost se s Gitem setkat co nejdříve na vlastní kůži a začít ho dennodenně používat a postupy si zažít.</p>
<p>Že to ale trvalo ... :)</p>
