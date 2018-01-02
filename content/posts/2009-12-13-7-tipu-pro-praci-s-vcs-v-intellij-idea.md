---
status: publish
published: true
title: 7 tipů pro práci s VCS v IntelliJ Idea
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Znát velmi dobře IDE, se kterým pracujete deno denně, je pro vaši produktivitu
  zcela zásadní. Poslední rok mne utvrdil v tom, že přesto že IntelliJ Ideu používám
  už několik let, přesto je plno věcí, které nevím a které mi nakonec ušetří plno
  práce. Příkladem budiž pár klávesových zkratek o kterých jsem absolutně nevěděl
  a které jsem se dozvěděl teprve z <a href=\"http://refcardz.dzone.com/announcements/upgrading-intellij-idea-81-get\"
  target=\"_blank\">DZone IntelliJ Cheatsheetu od Hamleta D'Arcyho</a> - kupříkladu:\r\n\r\n<ul>\r\n
  \  <li><strong>Ctrl+Shift+Insert</strong> - vertikální výběr oblasti (skvělé pro
  hromadné úpravy CSV souborů, SQL apod.)</li>\r\n   <li><strong>Ctrl+Shift+U</strong>
  - změna case vybraného textu (tzn. na upper-case nebo lower-case)</li>\r\n   <li><strong>Ctrl+Alt+Left,
  Ctrl+Alt+Right</strong> - posun na předchozí / následující lokaci kurzoru (používal
  jsem ikony) - skvělé pokud si prohlížíte jinou část třídy, včetně přesunutí kurzoru
  a pak se chcete vrátit rychle zpět</li>\r\n   <li><strong>F11</strong> - vložení
  rychlého bookmarku do kódu, který se vám ukazuje po pravé straně a je možné se na
  něj rychle vrátit</li>\r\n</ul>\r\n\r\nMožná, že teda i já vím pár věcí, které tak
  úplně známé nejsou, a třeba někomu z vás pomůžou.\r\n\r\n"
wordpress_id: 682
wordpress_url: http://blog.novoj.net/?p=682
date: '2009-12-13 22:40:46 +0100'
date_gmt: '2009-12-13 21:40:46 +0100'
categories:
- Programování
- Java
- IntelliJ Idea
tags: []
comments:
- id: 15837
  author: blaf
  author_email: tom.vojtech@seznam.cz
  author_url: ''
  date: '2009-12-13 23:09:15 +0100'
  date_gmt: '2009-12-13 22:09:15 +0100'
  content: "Docela uzitecny mi prijde shortcut Ctrl+Alt+Shift+N - slouzi k vyhledavani
    symbolu v kodu (jmena promennych, spring bean a kdovi ceho vseho)\r\n\r\nmisto
    pouzivani svn bar jsem si nadefinoval quick list a asocioval ho s klavesovou zkratkou,
    ktera mi zobrazi seznam s VCS akcemi, potom uz jenom napisu cast nazvu akce, kterou
    chci udelat, takze dam Ctrl+Alt+Shift+P, potom napisu \"late\" a v tom seznamu
    se mi vyfiltruje Compare with latest version, ... stejny zpusob pouzivam napr.
    refactor akci, prijde mi to pohodlnejsi nez klikat mysi"
- id: 15886
  author: Ladislav Thon
  author_email: ladicek@gmail.com
  author_url: ''
  date: '2009-12-14 23:49:34 +0100'
  date_gmt: '2009-12-14 22:49:34 +0100'
  content: "Ad 4: change listy jsou užitečné, ale už jsem se párkrát nechal nachytat,
    když jsem v souvislosti s aktuálním úkolem změnil soubor, který už byl z dřívějška
    kvůli jiné změně v jiném change listu. Odhaduju, že při použití Gitu by to mohlo
    být inteligentnější, ale CSV a SVN holt verzují celé soubory a ne jednotlivé změny.
    Shelf se v tomhle kontextu tuším česky říká přihrádka :-)\r\n\r\nAd 5: historie
    je naprosto _klíčová_, ale pro první pohled používám Annotate (klik pravým na
    gutter -- ten panel vlevo zmiňovaný v bodu 1), občas postačí.\r\n\r\nAd 7: tak
    Compare Two Files jsem znal, ale Compare with Clipboard nikoliv, díky!!!"
- id: 15900
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-12-15 07:48:10 +0100'
  date_gmt: '2009-12-15 06:48:10 +0100'
  content: "@Ladislav Thon:\r\n\r\nS changelisty máš pravdu - taky jsem přišel na
    to, že je to v podstatě jen per file. Na dost usecasů mě to zatím stačilo. Pokud
    by se to chovalo jako shelve, bylo by to zajímavé, ale trošku bych se obával toho,
    aby si člověk ještě udržel nad změnami přehled. V takovém případě se člověk nevyhnutelně
    musí dostat ke konfliktům."
- id: 15977
  author: antaran
  author_email: martin.vician@gmail.com
  author_url: http://www.zont.eu
  date: '2009-12-16 16:37:39 +0100'
  date_gmt: '2009-12-16 15:37:39 +0100'
  content: ":) to porovnavanie dvoch suborov a porovnavanie so schrankou som este
    nevidel :)\r\n\r\n-&gt; k tym changelistom, ja si vacsinou na kazde issue vytvaram
    zvlast changelist, existuje take nastavenie tu:\r\n\r\nSettings/VersionControl/IssueNavigation\r\n\r\n-&gt;
    kde sa da nastavit pattern web stranky issue trackeru (pre jiru je na to button)\r\n-&gt;
    potom ked do mena changelistu napisem kod issue, tak sa mi z neho automaticky
    vyrobi link do trackeru\r\n\r\nje to sikovne odporucam vyskusat... :)"
- id: 15992
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-12-16 20:32:10 +0100'
  date_gmt: '2009-12-16 19:32:10 +0100'
  content: "@antaran - aha, tak to jsem pro změnu zase nevěděl já ... vyzkouším, díky"
- id: 16006
  author: podlesh
  author_email: podlesh@podlesh.cz
  author_url: ''
  date: '2009-12-17 09:01:01 +0100'
  date_gmt: '2009-12-17 08:01:01 +0100'
  content: "To s tou lokální historií omezenou na jednotlivé soubory není tak docela
    pravda - lze pracovat i na úrovni adresářů.\r\n\r\nMezi další užitečné věci v
    idee bych uvedl:\r\n\r\n- Ctrl+Shift+V = paste s výběrem několika posledních obsahů
    schránky\r\n\r\n- Alt+Q = ukáže hlavičku aktuální metody nebo třídy, v jejímž
    těle se právě nacházím (a která je typicky oscrollována někam pryč)"
- id: 16007
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-12-17 10:13:56 +0100'
  date_gmt: '2009-12-17 09:13:56 +0100'
  content: "@podlesh\r\n\r\nS tou lokální historií máš pravdu - na úrovni adresářů
    jsem si myslel, že to funguje pouze pro to jak získat již odstraněné soubory,
    ale ono to správně zobrazuje i stav souborů v čase, což je super.\r\n\r\nDíky
    za další tipy - Ctrl+Shift+V je základ, ten snad zná každý :) - tuhle věc jsem
    si tak oblíbil, že jsem ji potřeboval i ve Windows samotných tak jsem si doinstaloval
    CLCL ( http://www.nakka.com/soft/clcl/index_eng.html ).\r\n\r\nAlt-Q je zajímavé
    - zkusím začít používat."
- id: 16064
  author: Jety
  author_email: mail@jetensky.net
  author_url: http://jetensky.net/blog
  date: '2009-12-18 14:45:36 +0100'
  date_gmt: '2009-12-18 13:45:36 +0100'
  content: Ahoj Honzo, díky. Líbí se mi ten shelving, dost často už jsem ho potřeboval
    a nevěděl jsem, co mi vlastně chybí :). Taky často používám ten Annotate. Ctrl+Shift+V
    nepoužívám, místo toho používám ClipDiary (obdoba CLCL) jak pro windows, tak pro
    Ideu, takže mám jistotu, že když něco zkopíruju odjinud, bude to tam taky.
- id: 16067
  author: Jety
  author_email: mail@jetensky.net
  author_url: http://jetensky.net/blog
  date: '2009-12-18 16:18:05 +0100'
  date_gmt: '2009-12-18 15:18:05 +0100'
  content: "@antaran\r\nDíky, to issue navigation funguje pěkně a hodí se mi. Jen
    jsem musel trochu upravit JIRA pattern z [A-Z]+\\-\\d+ na [A-Z0-9]+\\-\\d+, protože
    klíče máme např. O2DU-1234."
- id: 16091
  author: Petr
  author_email: petr.charvat@gmail.com
  author_url: http://pcharvat.blogspot.com/2008/07/vychytvky-v-intellij-idea-o-kterch-jsem.html
  date: '2009-12-18 23:29:58 +0100'
  date_gmt: '2009-12-18 22:29:58 +0100'
  content: "Praktická je taky zkratka CTRL+SHIFT+I - udělá náhled metody, nad kterou
    zrovna jste. Nemusíte tedy skočit dovnitř přes CTRL+B a pak zase zpátky.\r\n\r\nDalší
    vychytávka je Ctrl+Shift+A - vyhledává akci v menu - doporučuji vyzkoušet.\r\n\r\nHrátky
    z shelf jsem ještě nezkoušel, ale vypadá to jako super feature."
- id: 16118
  author: antaran
  author_email: martin.vician@gmail.com
  author_url: http://www.zont.eu
  date: '2009-12-19 15:59:26 +0100'
  date_gmt: '2009-12-19 14:59:26 +0100'
  content: "@Jety\r\nano, to sa pomerne casto stava, ale da sa to tam zmenit lahko
    aj vyskusat...\r\n\r\ninak, niekedy strasne davno asi viac nez rok, dva  dozadu,
    bola v IDEI taka moznost pozriet si statistiky pouzitych klavesovych skratiek...teraz
    to nemozem nikde najst :( poznate to niekto?\r\n\r\nak ste nejaku instalaciu IDEI
    pouzivali dlhsi cas, len ju stale updatovali, tak tam boli take zaujimave informacie,
    napr. stlacenie Ctrl + Space 100 000 krat a tak... :)"
- id: 16172
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-12-21 10:42:49 +0100'
  date_gmt: '2009-12-21 09:42:49 +0100'
  content: "@antaran jeto tam stále: statistiky vyvoláš klávesovou zkratkou Alt +
    H + P nebo přes Menu -> Help -> Productivity Guide\r\n\r\nJá mám třeba:\r\nBasic
    code completion 162 369 krát\r\nSyntax aware selection 86 471 krát\r\n\r\nZajímavé
    počteníčko :-)\r\n\r\nTímto děkuji Václavovi Pechovi za zodpovězení, sám jsem
    nevěděl."
- id: 16201
  author: antaran
  author_email: martin.vician@gmail.com
  author_url: http://www.zont.eu
  date: '2009-12-22 16:34:46 +0100'
  date_gmt: '2009-12-22 15:34:46 +0100'
  content: "@Otec Fura\r\n\r\nvdaka :), v poslednej dobe som sa rozhodol zacat viac
    pouzivat live templates tak si chcem odsledovat ako mi to ide...\r\n\r\nja som
    bohuzial nechal svoje skoro 3 rocne statistiky v minulej praci...ale tiez som
    tam mal vysoke cisla...mno jo keby som dostal jedno euro za kazdy \"Basic code
    completion\" mohol by som ist do dochodku :)"
---
<p>Znát velmi dobře IDE, se kterým pracujete deno denně, je pro vaši produktivitu zcela zásadní. Poslední rok mne utvrdil v tom, že přesto že IntelliJ Ideu používám už několik let, přesto je plno věcí, které nevím a které mi nakonec ušetří plno práce. Příkladem budiž pár klávesových zkratek o kterých jsem absolutně nevěděl a které jsem se dozvěděl teprve z <a href="http://refcardz.dzone.com/announcements/upgrading-intellij-idea-81-get" target="_blank">DZone IntelliJ Cheatsheetu od Hamleta D'Arcyho</a> - kupříkladu:</p>
<ul>
<li><strong>Ctrl+Shift+Insert</strong> - vertikální výběr oblasti (skvělé pro hromadné úpravy CSV souborů, SQL apod.)</li>
<li><strong>Ctrl+Shift+U</strong> - změna case vybraného textu (tzn. na upper-case nebo lower-case)</li>
<li><strong>Ctrl+Alt+Left, Ctrl+Alt+Right</strong> - posun na předchozí / následující lokaci kurzoru (používal jsem ikony) - skvělé pokud si prohlížíte jinou část třídy, včetně přesunutí kurzoru a pak se chcete vrátit rychle zpět</li>
<li><strong>F11</strong> - vložení rychlého bookmarku do kódu, který se vám ukazuje po pravé straně a je možné se na něj rychle vrátit</li>
</ul>
<p>Možná, že teda i já vím pár věcí, které tak úplně známé nejsou, a třeba někomu z vás pomůžou.</p>
<p><a id="more"></a><a id="more-682"></a></p>
<p>Začněme třeba s prací s VCS a revizemi - u nás používáme CVS, ale řekl bych, že tyto věci budou přenositelné i na SVN a další VCS systémy:</p>
<h3>1. Revize přístupné z kódu</h3>
<p><a href="http://blog.novoj.net/binary//2009/12/CVS-gutter.png"><img src="http://blog.novoj.net/binary//2009/12/CVS-gutter.png" alt="CVS-gutter" title="CVS-gutter" width="480" height="162" class="aligncenter size-full wp-image-684" /></a> </p>
<p>V editoru kódu máte hned po levé straně informaci o tom, jaké změny jsou v aktuálním kódu oproti poslední revizi ve VCS. Jedním klikem můžete pak můžete vrátit změny dané části na původní verzi uloženou v CVS, rychle porovnat změny nebo si původní verzi vložit do schránky.</p>
<h3>2. CVS / SVN Bar</h3>
<p><a href="http://blog.novoj.net/binary//2009/12/CVS-bar.png"><img src="http://blog.novoj.net/binary//2009/12/CVS-bar.png" alt="CVS-bar" title="CVS-bar" width="331" height="26" class="alignleft size-full wp-image-685" /></a> Plno šikovných operací s CVS je skryto až na druhé úrovni popup menu apodobně. Pro rychlý přístup k těmto operacím je možné si nainstalovat plugin CVS / SVN bar, který vám nejčastější operace (přidat soubor do CVS, commit / update / rollback, show history, diff) zpřístupní v nástrojovém menu.</p>
<h3>3. Vybavení naposledy vložených komentářů při commitu</h3>
<p>Je zajímavé, že o téhle fíčurce jsem nevěděl strašně dlouho a při diskusi s dalšími vývojáři jsem zjistil, že ani oni ji moc neznali. V commit dialogu se vám nabízí vždy jen poslední vložený komentář, jak ale vyvolat starší historii komentářů (často potřeba, když se pracuje na více tascích najednou)? Magické tlačítko jsem označil červeným kroužkem:</p>
<p><a href="http://blog.novoj.net/binary//2009/12/CVS-message-history.png"><img src="http://blog.novoj.net/binary//2009/12/CVS-message-history.png" alt="CVS-message-history" title="CVS-message-history" width="418" height="349" class="aligncenter size-full wp-image-686" /></a></p>
<h3>4. Change listy / Shelf</h3>
<p>Change listy jsou skvělým nástrojem, pokud pracujete na více věcech najednou, nebo máte právě rozpracovánu novou funkcionalitu a potřebujete pro kolegy udělat rychlý hotfix. Hodí se taky pro změny, které děláte v souborech, které jsou součástí VCS, ale u kterých nechcete abyste je omylem commitnuli (např. rychlé nastavení nějakých property pro vaše lokální vývojové prostředí apod). </p>
<p>Práci se shelvem (poličkou?! :-) ) <a href="http://www.jetbrains.com/idea/training/demos/changesShelf.html" target="_blank">ukazuje skvěle Václav Pech v 5ti minutovém demíčku</a>.</p>
<p>Co se týká change-listů, tak ty používám v případě, že potřebuju oddálit commit některých souborů. Jednoduše je přesunu do odděleného changelistu a při průběžných commitech už nemusím řešit odškrtávání těchto souborů v commit listu. Jde především o to, že při běžné práce by se mi určitě brzy stalo, že bych je omylem commitnul. Často mám totiž rychlejší ruce než mozek.</p>
<h3>5. Historie revizí</h3>
<p>Můj oblíbený nástroj, při kterém obvykle vyslovuji větu "ze mě nikdo blbce dělat nebude". Pokud člověk potřebuje zjistit, kdo ve zdrojovém souboru provedl tu změnu, která dle všech zůčastněných vznikla sama od sebe je historie skvělý nástroj, jak tomu přijít na kloub:</p>
<p><a href="http://blog.novoj.net/binary//2009/12/CVS-message-history1.png"><img src="http://blog.novoj.net<a href="http://blog.novoj.net/binary//2009/12/CVS-history.png"><img src="http://blog.novoj.net/binary//2009/12/CVS-history.png" alt="CVS-history" title="CVS-history" width="600" height="153" class="aligncenter size-full wp-image-692" /></a></p>
<p>Stejně často tento přístup používám, pokud se sám potřebuji vrátit k nějaké předchozí revizi, nebo když potřebuji zjistit, jakého člověka se mám zeptat na důvody a detaily konkrétní implementace v kódu. Bez této funkce se podle mého názoru prostě nedá obejít.</p>
<h3>6. Lokální historie</h3>
<p>V každém případě pro vás Idea udržuje lokální historii, takže přestože commity do CVS děláte jen čas od času, máte k dispozici daleko jemnější pohled na změny v kódu mezi revizemi. </p>
<p><a href="http://blog.novoj.net/binary//2009/12/Local-history-menu.png"><img src="http://blog.novoj.net/binary//2009/12/Local-history-menu.png" alt="Local-history-menu" title="Local-history-menu" width="488" height="75" class="aligncenter size-full wp-image-696" /></a></p>
<p><a href="http://blog.novoj.net/binary//2009/12/Local-history.png"><img src="http://blog.novoj.net/binary//2009/12/Local-history.png" alt="Local-history" title="Local-history" width="715" height="201" class="aligncenter size-full wp-image-695" /></a></p>
<p>Ani nemusím říkat, kolikrát mi tahle funkce zachránila plno času v případě souborů, které jsem do VCS ještě necommitnul. Obvykle ji používám spíše jako poslední záchrannou brzu - je tu sice ještě možnost pojmenovat si stav lokálních změn (Put label) - tedy něco jako lokální tag, ale tu používám málokdy, protože obvykle radši straním plnohodnotným tagům v CVS.</p>
<p>Jedinou nevýhodou (ale logickou) je to, že v lokální historii pracujete vždy jen s aktuálním souborem - tj. pokud se potřebujete dostat zpět do určitého stavu u více souborů, musíte po jednom. Nicméně v takových situacích, ve kterých tuto funkci používám já, jsem stejně rád, že jsem rád a klidně tuto práci podstoupím, jen když mi to zachrání napsaný kód.</p>
<h3>7. Porovnání kódu proti schránce</h3>
<p>Tahle fíčurka už nesouvisí s VCS jako takovým, ale souvisí s prací se změnami v kódě, tak jsem ji taky zařadil. IntelliJ Idea má naprosto skvělý DIFF editor, který se samozřejmě používá při práci s VCS, ale můžete ho použít velmi efektivně i samostatně. Zkuste třeba označit dva soubory v Project browseru a v popup menu vybrat položku:</p>
<p><a href="http://blog.novoj.net/binary//2009/12/Compare-two-files.png"><img src="http://blog.novoj.net/binary//2009/12/Compare-two-files.png" alt="Compare-two-files" title="Compare-two-files" width="356" height="496" class="aligncenter size-full wp-image-699" /></a></p>
<p>Nebo si text hoďte do schránky, vyberte kus textu v jiném souboru a vyberte:</p>
<p><a href="http://blog.novoj.net/binary//2009/12/Compare-clipboard1.png"><img src="http://blog.novoj.net/binary//2009/12/Compare-clipboard1.png" alt="Compare-clipboard" title="Compare-clipboard" width="399" height="505" class="aligncenter size-full wp-image-698" /></a></p>
<p>Tohle je věc, kterou jsem také objevil teprve nedávno a strašně rád ji používám.</p>
<div align="center">...</div>
<p>Jak jsem už v úvodu řekl, je plno věcí, které neznám a jsem strašně překvapený, když se je po letech dozvím. Zkuste mě překvapit třeba v komentářích :-)</p>
