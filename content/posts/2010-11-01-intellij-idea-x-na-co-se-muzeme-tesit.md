---
status: publish
published: true
title: IntelliJ Idea X - na co se můžeme těšit?
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img src=\"http://blog.novoj.net/binary/2010/10/IdeaX.png\" alt=\"\" title=\"IdeaX\"
  width=\"200\" height=\"170\" class=\"alignleft size-full wp-image-1167\" />Ode dneška
  (1. listopadu 2010) bude pro zakoupené <a href=\"http://www.jetbrains.com/idea/buy/buy.jsp\"
  target=\"_blank\">licence IntelliJ Idey 9</a> k dispozici <a href=\"http://blogs.jetbrains.com/idea/2010/11/free-upgrade-two-versions-of-intellij-idea-for-the-price-of-one/\"
  target=\"_blank\">upgrade na verzi 10 zdarma</a>. Stejně tak pokud nyní upgradujete
  své starší verze Idey (6, 7, 8) na devítku, dostanete upgrade na 10 také zadarmo.
  To značí jedinou věc - vývoj IntelliJ Idea X  se blíží ke svému konci a během měsíce
  nebo dvou bychom se mohli dočkat finální verze. A v této verzi nás čekají skutečně
  zajímavé libůstky.\r\n\r\nV tomto příspěvku jsem se pokusil shrnout pár nejvýznamnějších
  změn, které můžeme v nové verzi očekávat. Jedná se o můj subjektivní výběr, každopádně
  si myslím, že je to jedna z verzí, na kterou se vyplatí upgradovat. JetBrains zase
  o kousek posunují hranice produktivity.\r\n\r\n"
wordpress_id: 1160
wordpress_url: http://blog.novoj.net/?p=1160
date: '2010-11-01 16:48:51 +0100'
date_gmt: '2010-11-01 15:48:51 +0100'
categories:
- Java
- Softwarové nástroje
- IntelliJ Idea
tags: []
comments:
- id: 27617
  author: Stan Svec
  author_email: substral@seznam.cz
  author_url: ''
  date: '2010-11-02 08:08:55 +0100'
  date_gmt: '2010-11-02 07:08:55 +0100'
  content: Já IDEU nepoužívám, ale i tak mi udělala radost podpora AspectJ. Doufám,
    že to pomůže většímu rozšíření tohoto skvělého nástroje a AOP konceptu.
- id: 27742
  author: Albi
  author_email: dev@seznam.cz
  author_url: ''
  date: '2010-11-04 16:11:17 +0100'
  date_gmt: '2010-11-04 15:11:17 +0100'
  content: Podpora Androidu v komunity edition urcite potesi .... treti do partie
    po eclipse a  netbeans
---
<p><img src="http://blog.novoj.net/binary/2010/10/IdeaX.png" alt="" title="IdeaX" width="200" height="170" class="alignleft size-full wp-image-1167" />Ode dneška (1. listopadu 2010) bude pro zakoupené <a href="http://www.jetbrains.com/idea/buy/buy.jsp" target="_blank">licence IntelliJ Idey 9</a> k dispozici <a href="http://blogs.jetbrains.com/idea/2010/11/free-upgrade-two-versions-of-intellij-idea-for-the-price-of-one/" target="_blank">upgrade na verzi 10 zdarma</a>. Stejně tak pokud nyní upgradujete své starší verze Idey (6, 7, 8) na devítku, dostanete upgrade na 10 také zadarmo. To značí jedinou věc - vývoj IntelliJ Idea X  se blíží ke svému konci a během měsíce nebo dvou bychom se mohli dočkat finální verze. A v této verzi nás čekají skutečně zajímavé libůstky.</p>
<p>V tomto příspěvku jsem se pokusil shrnout pár nejvýznamnějších změn, které můžeme v nové verzi očekávat. Jedná se o můj subjektivní výběr, každopádně si myslím, že je to jedna z verzí, na kterou se vyplatí upgradovat. JetBrains zase o kousek posunují hranice produktivity.</p>
<p><a id="more"></a><a id="more-1160"></a></p>
<h3>Autocomplete on the fly</h3>
<p>Tohle je asi ta nejzásadnější změna, která jde průřezově celým IDE. Po několika dnech používání musím říct, že je to bomba. Jedná se o to, že Idea vám napovídá možné varianty kódu již ve chvíli, kdy píšete. Tedy není nutné mačkat klávesovou kombinaci pro autocomplete (Ctrl+Space), ale pokud se ocitne správná položka jako první, stačí jen uhodit na Enter/Tab (popř. šipkami vybrat jinou nabídku a odentrovat). Jedno video za tisíc slov:</p>
<p><object width="500" height="375" id="_player" name="_player" data="http://tv.jetbrains.net/sites/default/files/flowplayer3/flowplayer-3.2.2.swf" type="application/x-shockwave-flash"><param name="movie" value="http://tv.jetbrains.net/sites/default/files/flowplayer3/flowplayer-3.2.2.swf" /><param name="allowfullscreen" value="true" /><param name="allowscriptaccess" value="always" /><param name="flashvars" value='config={"clip":{"baseUrl":"http://tv.jetbrains.net","scaling":"orig","autoPlay":false,"autoBuffering":true,"url":"sites/default/files/videos/converted/autocompletion2.flv"},"playlist":[{"baseUrl":"http://tv.jetbrains.net","scaling":"orig","autoPlay":false,"autoBuffering":true,"url":"http://tv.jetbrains.net/sites/default/files/videos/converted/autocompletion2.flv"}]}' /></object></p>
<p>Nejdřív jsem se obával, že by mohlo toto napovídání působit rušivě a odpoutávat moji pozornost. Jenže to tak vůbec není - jediným efektem je to, že píšete skoro minimálně. Zní to hodně divně, ale jsou chvíle, kdy mačkám víc Enter než ostatní klávesy a kód tak přibývá raketovou rychlostí. Navíc Idea je opravdu dobrá v tom, jak seřadit nabídku v autocomplete menu - s vysokou pravděpodobností vám jako první nabídne skutečně to, co potřebujete.</p>
<p>Instant autocomplete je samozřejmě i v jiných jazycích než je Java (XML, HTML, JavaScript ...).</p>
<p>Však si to vyzkoušejte sami na vlastní kůži - funkce je <a href="http://confluence.jetbrains.net/display/IDEADEV/IDEA+X+EAP" target="_blank">dostupná již v aktuálním EAP</a>.</p>
<h3>AspectJ compiler (Spring Roo) support</h3>
<p>Po nativní podpoře AspectJ kompilátoru <a href="http://youtrack.jetbrains.net/issue/IDEA-26959" target="_blank">byla velká poptávka</a>. Aktuálně je dostupný <a href="http://plugins.intellij.net/plugin/?idea&id=4679" target="_blank">AspectJ Support plugin (tj. již pro verzi 9)</a>, který umožňuje na pozadí spouštět AspectJ kompilátor a využívat autocomplete i pro kód, který vzniká až teprve po aplikaci aspektů na originální kód. Podrobnější informace o jeho fungování jsou k dispozici na <a href="http://confluence.jetbrains.net/display/~roman.shevchenko/AspectJ+Support+Plugin" target="_blank">homepage pluginu</a>. Tento plugin by měl být ve verzi 10 snad již standardní součástí.</p>
<p>S fungováním pluginu nemám osobní zkušenosti, takže pokud někdo takové má, podělte se o ně s ostatními v komentářích k článku.</p>
<h3>Editor fragmentů v jiném jazyce</h3>
<p>Již ve verzi 9 byla k dispozici funkcionalita pro označování fragmentů kódu, který je v jiném jazyce než je jazyk aktuálně editovaného souboru (SQL query v Java souboru, HQL query, HTML, CSS v Javě, Groovy ...). Idea vám pak hezky napovídala pomocí autocomplete to, co v daném jazyce očekáváte (ve SQL názvy tabulek, v HTML názvy tagů atd.). I přes tuto podporu bylo trošku nešikovné to, že pokud byly dané řetězce příliš dlouhé nebo byly naopak rozděleny rozděleny na několik řádků, nebyla editace příjemná. V nové Idee můžete pomocí intention (Alt+Enter) otevřít extra editor, ve kterém se vám přehledně zobrazí jen daný fragment v koncovém formátu, kde svoji editaci provedete a která se vám promítne do původního kódu. Detaily (obrázky) <a href="http://blogs.jetbrains.com/idea/2010/08/full-featured-intellij-idea-editor-for-injected-language-fragments/" target="_blank">v článku na blogu JetBrains</a>.</p>
<h3>Android development support (součástí Community edition)</h3>
<p>Pro vývojáře Androidích aplikací (což já bohužel dosud nejsem ;-) ), je tu poměrně zajímavá zpráva. IntelliJ Idea má od verze 10 podporu pro vývoj aplikací pro tuto "mobilní" platformu. Konkrétní detaily v článcích:</p>
<ul>
<li><a href="http://blogs.jetbrains.com/idea/2010/09/android-library-projects-support/" target="_blank">Podpora Android platformy</a></li>
<li><a href="http://blogs.jetbrains.com/idea/2010/09/android-unit-testing-support/" target="_blank">Podpora unit testování</a></li>
</ul>
<p>Nejzajímavější zpráva pro mě je <a href="http://blogs.jetbrains.com/idea/2010/10/intellij-idea-10-free-ide-for-android-development/" target="_blank">oznámení o zpřístupnění Android podpory v Community edition</a> IntelliJ Idey - tedy ve verzi zadarmo.</p>
<p>Z celého usuzuji, že se jedná o útok JetBrains na pozici Eclipse, který je teď uváděn jako primární podporovaná vývojová platforma ze strany Google. Uvidíme, jestli tento krok přinese nějaký obrat.</p>
<h3>Další vylepšení pro Maven</h3>
<p>Velmi hezky udělané je nově generování dependencí do stávajícího pom.xml - přes Alt-Insert se vám objeví dialog, kde si můžete ve svém repository najít artifact, který potřebujete a jednoduše ho do POMu doplnit. Kromě lokálních repository je možné nastavit i indexování remote repository (například vaší firemní proxy). Artefakty, které vám lokálně chybí Idea sama do repository stáhne a zaindexuje.</p>
<p>Vylepšený je i dependency diagram, jehož výstup by měl být nyní pro člověka daleko přehlednější. Názorně je to ukázáno <a href="http://blogs.jetbrains.com/idea/2010/05/maven-dependencies-diagram/" target="_blank">v tomto postu na JetBrains blogu</a>.</p>
<p><object width="500" height="375" id="_player" name="_player" data="http://tv.jetbrains.net/sites/default/files/flowplayer3/flowplayer-3.2.2.swf" type="application/x-shockwave-flash"><param name="movie" value="http://tv.jetbrains.net/sites/default/files/flowplayer3/flowplayer-3.2.2.swf" /><param name="allowfullscreen" value="true" /><param name="allowscriptaccess" value="always" /><param name="flashvars" value='config={"clip":{"baseUrl":"http://tv.jetbrains.net","scaling":"orig","autoPlay":false,"autoBuffering":true,"url":"sites/default/files/videos/converted/maven.flv"},"playlist":[{"baseUrl":"http://tv.jetbrains.net","scaling":"orig","autoPlay":false,"autoBuffering":true,"url":"http://tv.jetbrains.net/sites/default/files/videos/converted/maven.flv"}]}' /></object></p>
<h3>Version control</h3>
<p>Nově v desítce uvidíme podporu distribuovaného VCS Mercurial a také vylepšení podpory GITu. V souvislosti s GITem je zajímavá především rozšířená <a href="http://blogs.jetbrains.com/idea/2010/10/github-integration-in-intellij-idea-base-features/" target="_blank">podpora pro nejznámější GIT hosting GitHub</a>. Mezi <a href="http://confluence.jetbrains.net/display/IDEADEV/GitHub+Integration+Stories" target="_blank">standardní use-case</a> patří samozřejmě checkout z vaší stávající repository na GitHubu, vytvoření nové repository a push zdrojáků z aktuálního projektu.</p>
<h3>Drobnosti, které mě potěšily</h3>
<p>Subjektivně se mi zdá, že <b>Idea o něco zrychlila</b> - prozatím ale není žádná oficiální zpráva, že skutečně nějaká rychlostní optimalizace proběhla. Jen se zkraje vývoje mluvilo o tom, že 10ka bude především o optimalizaci a tuningu rychlosti spíš než o velkém množství nově podporovaných technologií. Prozatím těžko soudit, uvidíme jaká bude finální verze. Bohužel toto je vnímáno asi jako největší problém Idey jako takové (třeba se ale vyřeší sám s nástupem SSD disků ;-) ).</p>
<p>V editoru se nově <b>obarvují záložky</b> a názvy tříd ve vyhledávacím dialogu. Seznam se tak zpřehledňuje - na první pohled víte, v kterých záložkách máte testy a v kterých produkční kód. Barvy je možné si customizovat, je možné vytvářet nové "scope" a přiřazovat jim vlastní barvy. Můžete si tak definovat barvy např. podle příslušnosti do odlišných vrstev aplikace podle packagí atd.. Ve velkých projektech jistě zajímavá možnost.</p>
<p>V editoru se také <b>změnšily scrollbary</b>. Chvilku mi trvalo než jsem si zvyknul, trefit se na uzší scrollbar, ale po chvíli mi přišlo nové řešení lepší - nezabírají tolik prostoru v zobrazovací části (člověk chce vidět hlavně kód). Navíc po chvíli zblednou, takže nepůsobí tak výrazně v editačním prostředí. Možná je to drobnost, ale člověk ji používá každý den, takže svoji roli rozhodně hraje.</p>
<p>Opět <b>přibylo pár inspekcí</b>. Příjemně mě například překvapilo nové upozornění na redundantní IF statementy, které se dají dále zjednodušit. Jsou prostě věci, které ve své kódu nevidíte :-).</p>
<p>Zajímavé urychlení také představuje <b>bezdialogový refactoring inline variable</b>. Typicky jste totiž ve starších verzích Idey jen odklepli dialog s názvem proměnné, což zbytečně zdržovalo. Teď se vše odehraje poměrně rychle v rámci editoru. Jméno proměnné můžete samozřejmě ihned v rámci vysvícené oblasti upravit, ale ve většině případů stačí jen Enter.</p>
<p>Moje drobnost, která mě ale dlouho neuvěřitelně točila - <b>serialUID se konečně generuje na vrchu fieldů dané classy</b>. Konec neustálého přemisťování tohoto fieldu. Generované fieldy se tedy konečně začaly řadit podle logické posloupnosti.</p>
<p>V <b>SQL editoru</b> půjde nyní přímo <a href="http://blogs.jetbrains.com/idea/2010/08/graphical-database-table-editor-in-intellij-idea-10/" target="_blank">upravovat hodnoty ve sloupcích tabulky</a>, přidávat a odstraňovat sloupce.</p>
<p>Jak vidíte, je na co se těšit. Bohužel nikde není dosud zveřejněna kompletní roadmap - její část je k dispozici na <a href="http://java.dzone.com/news/intellij-idea-x-early-release?utm_source=am6_feedtweet&utm_medium=twitter&utm_campaign=toya256ForRSS" target="_blank">DZone</a>. Takže vesele upgradujte - nákupy se vám budou vztahovat už na desítkovou verzi Idey.</p>
<p><b>Update 2. 11. 2010:</b> Na stránkách Jetbrains vyšel <a href="http://www.jetbrains.com/idea/nextversion/index.html" target="_blank">oficiální feature sheet pro novou verzi Idey</a>.</p>
