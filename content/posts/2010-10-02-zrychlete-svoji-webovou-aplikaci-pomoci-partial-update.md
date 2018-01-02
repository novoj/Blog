---
status: publish
published: true
title: Zrychlete svoji webovou aplikaci pomocí Partial Update
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img src=\"http://blog.novoj.net/binary/2010/08/recycle_sign1-150x150.jpg\"
  alt=\"\" title=\"recycle_sign[1]\" width=\"150\" height=\"150\" class=\"alignleft
  size-thumbnail wp-image-1055\" />Partial update neboli částečná aktualizace stránky
  (pomocí AJAXu) není technika zrovna nová. Po pravdě řečeno však stále není běžná,
  přestože její správné použití může velmi pozitivní dopady na celkový výkon systému
  a také je velmi dobře přijímána uživateli. Na otázku proč, můžeme odpovědět problematickou
  podporou ve frameworcích - některé se na jedné straně snaží o maximální odstínění
  programátorů od JavaScriptu, čímž z dané techniky dělají věc více méně magickou
  - jinde naopak použití vyžaduje větší než malé znalosti \"skriptování\", což zase
  většinu Javistů, paradoxně, vyřadí ze hry.\r\n\r\nV tomto článku si vysvětlíme základní
  principy, které jsou s touto technikou spojovány a ukážeme si je na příkladech živé
  aplikace. Způsob jakým jsme tuto techniku implementovali my, by se měl přibližovat
  k vlastnímu jádru věci, takže by vám měl být princip zřejmý.\r\n\r\n"
wordpress_id: 1042
wordpress_url: http://blog.novoj.net/?p=1042
date: '2010-10-02 12:51:11 +0200'
date_gmt: '2010-10-02 11:51:11 +0200'
categories:
- Programování
- Web
- JavaScript
tags:
- ajax
comments:
- id: 26219
  author: Lukas Vlcek
  author_email: lukas.vlcek@gmail.com
  author_url: ''
  date: '2010-10-02 14:13:18 +0200'
  date_gmt: '2010-10-02 13:13:18 +0200'
  content: "Moc pěkný článek +1!\r\n\r\nNutí mě přemýšlet nad tím, jak velký problém
    je, když web nefunguje při vypnutém Javascriptu v browseru. Píšeš, že se to týká
    asi 2-3% uživatelů, to je jen odhad nebo máte nějaké měření? Zkusil jsem si vypnout
    Javascript (v Chrome) a vůbec mě nepřekvapilo, že \"New Twitter\" vůbec nenaběhne.
    Je to #fail nebo ne, když stránka v dnešní době vůbec nepočítá s tím, že Javascript
    může být vypnutý?\r\n\r\nPokud si třeba Twitter (ať už úmysleně nebo omylem) dovolí
    ignorovat část uživateů, kteří Javascript nemaji (a v jejich případě i ty 2-3%
    bude velké číslo), tak se mi zdá, že by možná bylo lepší vůbec se renderováním
    HTML na serveru nezabývat a posílat klientovi (browseru) jen JSON, ať si s ním
    udělá co chce (třeba z něj vyrobí HTML), jedna z výhod takového přístupu je, že
    data lze snadno konzumovat i jinými JSON friendly klienty. Pokdu jsem to dobře
    pochopil, tak přesně touto cestou se vývojáři, kteří pracovali na \"New Twitter\"
    vydali: http://engineering.twitter.com/2010/09/tech-behind-new-twittercom.html"
- id: 26234
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-10-02 19:44:00 +0200'
  date_gmt: '2010-10-02 18:44:00 +0200'
  content: "Statistiky browserů s vypnutým JavaScriptem se dost různí a prý nejsou
    ani moc přesné (díky proxy serverům, indexovacím robotům atd.). Různí se, ale
    většina hovoří o 2-4%. Sehnal jsem pár statistik, které jsou alespoň trochu aktuální:\r\n\r\nhttp://www.w3schools.com/browsers/browsers_stats.asp\r\nhttp://www.woopra.com/forums/topic/track-users-with-javascript-disabled\r\nhttp://statcounter.com/project/standard/system.php?account_id=397157&login_id=1&code=ba7c7043e25ecfacd62fc4d67fc2f508&guest_login=1&project_id=2368090\r\n\r\nObecně
    řečeno - tím, že stránky jsou \"JavaScript only\" komplikuješ práci:\r\n\r\n-
    indexovacím robotům (ty JS pokud vím neinterpretují)\r\n- uživatelům s nestandardními
    (starými nebo specifickými browsery)\r\n- uživatelům přistupujících pomocí specifických
    zařízení (screen readerům, některým mobilním zařízením atd.)\r\n\r\nOtázka je,
    jestli si to můžeš u svých web stránek dovolit. Na intranetu asi ano, u e-shopu
    rozhodně ne.\r\n\r\nVelmi mne oslovila reakce AdrianH v na této stránce: http://uxexchange.com/questions/3360/should-we-really-be-concerned-with-javascript-being-disabled-anymore-disregardin
    - s ní se naprosto ztotožňuji. Na internetu není žádné procento dost malé - pořád
    tím vylučujete tisíce potenciálních uživatelů / zákazníků vašich stránek."
- id: 26235
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-10-02 19:51:11 +0200'
  date_gmt: '2010-10-02 18:51:11 +0200'
  content: 'Ještě k těm readerům je tady moc zajímavý článek: http://northtemple.com/2008/10/07/javascript-and-screen-readers
    - částečné updaty stránky jsou z hlediska přistupnosti skutečně problém. Proto
    předpokládám, že z hlediska přístupnosti preferují uživatelé "noscript" verze.'
- id: 26532
  author: Martin Beránek
  author_email: martin@martinberanek.cz
  author_url: ''
  date: '2010-10-11 05:54:54 +0200'
  date_gmt: '2010-10-11 04:54:54 +0200'
  content: 'Co se týká toho JSF: v JSF2 se partial update standarne pouziva pro vsechny
    AJAXove stranky. Podle toho co jsem četl, se na serveru vždy vyrendruje kompletní
    stránka s odpovědí (ať už to je normální request nebo ajaxový). Pokud je to ajax
    request, tak se z toho vyřízne ta správná část domu a pošle se na klienta jenom
    ta.'
- id: 26542
  author: Tomáš Piňos
  author_email: tomas.pinos@gmail.com
  author_url: http://tom2ee-cs.blogspot.com/
  date: '2010-10-11 19:49:02 +0200'
  date_gmt: '2010-10-11 18:49:02 +0200'
  content: "Pěkný článek. Partial update \"zná intuitivně každý\", ale vysvětlit některé
    důsledky jako bookmarkování nebo historie je cenné.\r\n\r\nLíbí se mi, jak s partial
    update pracuje framework Grails (např. http://grails.org/doc/latest/ref/Tags/remoteLink.html
    nebo http://grails.org/doc/latest/ref/Tags/formRemote.html)."
- id: 26568
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-10-12 13:04:11 +0200'
  date_gmt: '2010-10-12 12:04:11 +0200'
  content: "@Martin Beránek: jestli je to tak, pak se mi zdá, že na serveru se zbytečně
    plýtvá výkonem na vyrenderování celé stránky, když je klientovi servírovaná pouze
    část - to mě u JSF docela překvapuje, protože tam by měli poměrně přesně vědět,
    co je pro jakou komponentu třeba (JSF je postavené nad patternem ViewHelper pokud
    vím)\r\n\r\n@Tomáš Piňos: jestli si to vysvětluji správně, tak v případě Grails,
    musím na serveru počítat s tím, že klient může požadovat pouze \"partial update\"
    odpověď a renderovat mu v takovém případě jen šablonu odpovídající danému \"DIVu\"?
    Tím jsou sice veškeré kvality partial update zachovány, ale vynakládá to náklady
    na vývoj, kdy musím specielně AJAX režim opečovat. Pochopil jsem to tak správně?"
- id: 26585
  author: optik
  author_email: koubel@volny.cz
  author_url: http://www.mirin.cz
  date: '2010-10-12 19:34:47 +0200'
  date_gmt: '2010-10-12 18:34:47 +0200'
  content: "partial update dost pěkně implementuje pomocí komponent v Čechách populární
    php framework Nette, včetně funkce bez javascriptu, podpory zajaxovatění a snippetů
    - možnost označit jen část komponenty, která se bude ajaxovat. Je to v podstatě
    implementované stejně jak to popisuje článek.\r\n\r\nOsobně ale nejsem zastánce
    tohoto přístupu, spíš poslat ajaxem json (třeba seznam článků na dané stránce)
    a js na klientovi updatne dané elementy, na serveru se to automaticky pozná a
    zavolá se jiná obslužná action. Obsluha a podpora non-js řešení je ale o trochu
    pracnější.\r\n\r\nJá trochu doufám, že takovýchto webu s ajax komponentami bude
    ubývat a weby se začnou více dělit na desktop like, které budou komplet v js a
    web like, které zas budou jako klasická webová stránka a tam pak pro partial update
    bude čím dál méně uplatnění."
- id: 26588
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-10-12 21:45:56 +0200'
  date_gmt: '2010-10-12 20:45:56 +0200'
  content: "@optik Právě nad tím jsem přemýšlek, když jsem na letošním WebExpo slyšel
    o novém AJAXu v Nette vyprávět vývojáře okolo mě. Vzhledem k tomu, že jsem Javista,
    jsem PHPkové přednášky programově vynechával, ale řada rysů AJAXových aktualizací
    mi přišla hodně podobná.\r\n\r\nK té tvé vizi. Osobně si nemyslím, že partial
    update vymizí. Možná bude na webu čím dál více \"desktop like\" aplikací, ale
    pro naprostou většinu webových aplikací se tento styl nehodí. Navíc i když se
    o RIA stále mluví, nějaká masivní adopce stále nikde. Dosud, myslím, není vyřešena
    indexace obsahu vyhledávači, přístupnost aplikací je diskutabilní, tlustí klienti
    (Flash, Silverlight, JavaFX) mají každý celou řadu svých vlastních problémů atd.
    atd.\r\n\r\nJavaScriptové knihovny (ExtJS, GWT a jim podobné) se zase velmi špatně
    customizují a mají tendenci vypadat na každé implementaci stejně - což je něco,
    co většina zákazníků na internetu nechce (pokud se jen nesnaží portovat své stávající
    desktop aplikace na web).\r\n\r\nWebů, které by vypadaly jako klasické \"old school\"
    weby, bude sice pořád dost, ale zdá se mi, že stále narůstá podíl webu s velkým
    podílem dynamického obsahu. A právě partial update je pro tyto weby jako dělaný.
    Masivně se podle mého nepoužívá proto, že pro vývojáře není jednoduše uchopitelný
    nebo znamená navýšení pracnosti na projekt.\r\n\r\nUvidíme kam bude vývoj v budoucnosti
    směřovat, ale implementace partial update na takových aplikacích jako je Twitter
    (i když zde probíhá komunikace přes JSON) nebo Facebook mě zatím naplňují optimismem.\r\n\r\nP.S.:
    komunikace přes JSON, kterou zmiňuješ je samozřejmě validní varianta - nicméně
    vyžaduje mít aktualizační rutiny obnovující DOM napsané v JavaScriptu a to je
    zase práce navíc, které jsem se chtěli vyhnout. Současné řešení má pro nás minimální
    náklady na implementaci, proti klasické non-javascriptové verzi. V tom právě vidím
    velkou výhodu, která nám i interně pomůže tuto techniku posadit na víc webů, které
    realizujeme."
- id: 26634
  author: Tomáš Piňos
  author_email: tomas.pinos@gmail.com
  author_url: http://tom2ee-cs.blogspot.com/
  date: '2010-10-13 20:36:46 +0200'
  date_gmt: '2010-10-13 19:36:46 +0200'
  content: "@Grails Ano, proti non-javascriptové verzi by to bylo mírně (nebo spíš
    \"nepatrně\") složitější. \r\n\r\nNa příkladu se seznamem poptávek - stránka by
    se rozdělila na template celé stránky, který by \"includoval\" template pro seznam
    poptávek. Takže soubor celaStranka.gsp by obsahoval následující fragment:\r\n
    \ \r\n     \r\n  \r\nSamotnému seznamu poptávek by odpovídal druhý soubor - _poptavky.gsp.
    Tohle ještě nic nestojí.\r\n\r\nController pro práci se stránkou by pak vedle
    metody pro získání dat celé stránky obsahoval ještě speciální metodu navíc pro
    obsoužení AJAX requestu na obnovu seznamu. Něco v tomto stylu:\r\n\r\nclass PoptavkyController
    {\r\n  def refreshList = {\r\n    ...získání seznamu...\r\n    render(template:
    \"/poptavky\", model: [list: list])\r\n  }\r\n}\r\nTo už je práce navíc, ale pořád
    je to dobře zvladatelné.\r\n\r\nNechci tu vystupovat jako skalní zastánce Grails
    (teprve se je učím). Zmínil jsem Grails jako příklad ne-komponentního frameworku,
    ve kterém se dá partial update taky dobře implementovat."
- id: 26655
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-10-14 05:59:18 +0200'
  date_gmt: '2010-10-14 04:59:18 +0200'
  content: Super, díky za příklad. Myslel jsem, že to bude složitější. Tohle vypadá
    z hlediska náročnosti poměrně v pohodě.
- id: 26669
  author: David
  author_email: wolczyk.david@gmail.com
  author_url: ''
  date: '2010-10-14 12:37:44 +0200'
  date_gmt: '2010-10-14 11:37:44 +0200'
  content: "Neni \"partial update\" trosku kontraproduktivni z hlediska pageranku
    stranky ?\r\nGoogleBot je schopny parsovat i URL, ktere je v ramci javascriptoveho
    bloku, ale\r\njakym zpusobem, pak vyhodnoti  takovy fragment stranky ?"
- id: 26681
  author: Peter
  author_email: peter1000@inmail.sk
  author_url: http://www.nutriscience.com
  date: '2010-10-14 16:35:29 +0200'
  date_gmt: '2010-10-14 15:35:29 +0200'
  content: "@David: podla mna nie je, on aj tak bude indexovat podla non-javascriptu-verzie"
- id: 26696
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-10-14 23:22:17 +0200'
  date_gmt: '2010-10-14 22:22:17 +0200'
  content: "@David @Peter ... přesně tak. Pro GoogleBot a další je non-javascript
    verze plnohodnotně funkční. Partial-update je v podstatě add-on pro klienty, kteří
    ho umějí interpretovat (což je většina)."
- id: 31370
  author: Myšlenky dne otce Fura &raquo; Blog Archive &raquo; Čtvrtý rok Myšlenek
    Otce Fura
  author_email: ''
  author_url: http://blog.novoj.net/2011/01/03/ctvrty-rok-myslenek-otce-fura/
  date: '2011-01-03 10:21:06 +0100'
  date_gmt: '2011-01-03 09:21:06 +0100'
  content: "[...] orientovaného řešení prezentační vrstvy. Ta umožnila extensivní
    využití techniky partial update, která zajistila bleskové odezvy systému i na
    místech, kde bychom toho nebyli schopni s [...]"
- id: 40670
  author: Myšlenky dne otce Fura &raquo; Blog Archive &raquo; GeeCON 2011
  author_email: ''
  author_url: http://blog.novoj.net/2011/05/15/geecon-2011/
  date: '2011-05-15 22:50:11 +0200'
  date_gmt: '2011-05-15 21:50:11 +0200'
  content: "[...] pro mě poměrně překvapivá informace o podpoře partial update v JSF
    2, která se velmi podobá té naší, ke které jsme nezávisle také dospěli. Bohužel
    se mi nikde nepodařilo nalézt, jak se JSF v [...]"
---
<p><img src="http://blog.novoj.net/binary/2010/08/recycle_sign1-150x150.jpg" alt="" title="recycle_sign[1]" width="150" height="150" class="alignleft size-thumbnail wp-image-1055" />Partial update neboli částečná aktualizace stránky (pomocí AJAXu) není technika zrovna nová. Po pravdě řečeno však stále není běžná, přestože její správné použití může velmi pozitivní dopady na celkový výkon systému a také je velmi dobře přijímána uživateli. Na otázku proč, můžeme odpovědět problematickou podporou ve frameworcích - některé se na jedné straně snaží o maximální odstínění programátorů od JavaScriptu, čímž z dané techniky dělají věc více méně magickou - jinde naopak použití vyžaduje větší než malé znalosti "skriptování", což zase většinu Javistů, paradoxně, vyřadí ze hry.</p>
<p>V tomto článku si vysvětlíme základní principy, které jsou s touto technikou spojovány a ukážeme si je na příkladech živé aplikace. Způsob jakým jsme tuto techniku implementovali my, by se měl přibližovat k vlastnímu jádru věci, takže by vám měl být princip zřejmý.</p>
<p><a id="more"></a><a id="more-1042"></a></p>
<p>Webové aplikace pracují typicky tak, že klient (browser) pošle v requestu data, server sestaví výslednou HTML stránku a vrátí ji zpět browseru, který ji následně interpretuje = vykreslí. Partial update na tomto způsobu komunikace mění jen 2 věci: </p>
<ul>
<li>request probíhá na pozadí pomocí AJAXu,</li>
<li>server nesestavuje kompletní stránku, ale jen její část.</li>
</ul>
<p>Vlastní aktualizace obsahu stránky zobrazované uživateli se, po přijetí response, provede jednoduchou manipulací s DOMem (tj. objektovou reprezentací HTML stránky) pomocí JavaScriptu.</p>
<p><a href="http://www.rokjinak.cz/srv/www/qf/cs/ramjet/offers/offerListing" target="_blank">Přiklad partial update v praxi na našem projektu.</a> (klikněte na Záložku poptávky, procházejte seznam přes stránkování dole)</p>
<p>Celé to funguje velmi jednoduše. Náš webový framework je postavený na komponentovém principu a tudíž přesně víme, který kus HTML renderuje jaká komponenta. Jednoduše se to dá prezentovat na následujících odkazech:</p>
<ul>
<li><a href="http://www.rokjinak.cz/srv/www/qf/cs/ramjet/offers/offerListing@filter" target="_blank">Komponenta zobrazující filtrování</a></li>
<li><a href="http://www.rokjinak.cz/srv/www/qf/cs/ramjet/offers/offerListing@listing" target="_blank">Komponenta zobrazující tabulku s výsledky</a></li>
<li><a href="http://www.rokjinak.cz/srv/www/qf/cs/ramjet/offers/offerListing@listing_1" target="_blank">Komponenta zobrazující stránkování</a></li>
<li><a href="http://www.rokjinak.cz/srv/www/qf/cs/ramjet/offers/offerListing@partialUpdateCnt" target="_blank">Komponenta zobrazující kompletní obsah středové části</a></li>
</ul>
<div style="border: 1px solid white; background-color: #333333; font-size: 90%; padding: 20px;">
<strong>Pozn.:</strong> Podle odkazů můžete vidět, že nám stačí na konec url za znak @ uvést identifikátor libovolné komponenty jejíž obsah nás zajímá a dostaneme požadovaný výřez HTML.
</div>
<p>Schopnost přesně ohraničit části stránky, které chceme potenciálně "částečně vykreslovat" je jedna z nutných podmínek použití partial update ve vaší aplikaci. Na serverové části musíte používat knihovny, které vám toto umožní. Velkou výhodu v tomto mají <a href="http://tapestry.formos.com/nightly/tapestry5/guide/ajax.html" target="_blank">komponentově orientované frameworky</a>, které ze své podstaty toto ohraniční komponent a jejich výstupu mají. V případě <a href="http://static.springsource.org/spring-webflow/docs/2.0.x/reference/html/ch11s05.html" target="_blank">MVC frameworků</a> se podobná záležitost dá simulovat pomocí templatovacích knihoven jako jsou např. <a href="http://tiles.apache.org/" target="_blank">Tiles</a>. </p>
<p>MVC frameworky mají ovšem situaci komplikovanější i v dalších ohledech. Schopnost vykreslit jen část výstupu totiž není to jediné, co hraje roli. Druhým velmi podstatným faktorem je umět jednoduše omezit aplikační logiku vykonávanou ve spojitosti s vykreslovaným výstupem - tj. nedotazovat se aplikační vrstvy na něco, co v částečně renderovaném výstupu nebude potřeba. </p>
<p>Komponentové frameworky obvykle využívají patternu <a href="http://java.sun.com/blueprints/corej2eepatterns/Patterns/ViewHelper.html" target="_blank">View helper</a> - což zjednodušeně znamená, že view v rámci vykreslování přímo volá "aplikační logiku". MVC pattern vykonává aplikační logiku již na úrovni controlleru, který je zároveň zodpovědný za přípravu všech dat potřebných pro view (tedy vykreslování) - při partial updatu musíte sami oprogramovat a držet v povědomí, co bude ve view kdy potřeba a co ne. S view helperem tento problém neřešíte - co si view vrstva při vykreslování nezavolá, to se neprovede. View helper přináší na druhou stranu zase problémy spojené s cachováním výstupů aplikační logiky. Jednoduše se totiž stane, že z view zbytečně voláte jednu metodu se stejnými parametry mnohokrát, aniž byste si toho všimli (zvlášť když máte stránku složenou z mnoha nezávislých komponent).</p>
<p>V případě, že jste schopni na straně serveru splnit tyto dvě podmínky, je implementace na straně klienta již velmi jednoduchá. V našem případě jsme vytvořili <a href="http://jquery.com/" target="_blank">jQuery plugin</a>, který dokáže projít všechny odkazy a submit tlačítka v konkrétní oblasti (ohraničené jak jinak než komponentou) a přidat jim "onclick" funkce, které při kliknutí na odkaz / submit, místo refreshe kompletní stránky, provedou odpovídající AJAXový dotaz na server s následným partial updatem:</p>
<p>[source lang="java"]<br />
$("#partialUpdateCnt").partialUpdate();<br />
[/source]</p>
<p>Ekvivalentní zápis, pokud bychom volání chtěli zapisovat k jednotlivým linkům ručně, by vypadal takto:</p>
<p>[source lang="java"]<br />
//první parametr je url pro partial update,<br />
//druhý parametr je ID DOM objektu jehož obsah se má vyměnit po odpovědi serveru<br />
<a href="..." onclick="return $.partialUpdate.execute(this.href, 'partialUpdateCnt');"/><br />
[/source]</p>
<p>Pokud bych odstranil všechen balast a šel až na kost, dostal bych něco takového:</p>
<p>[source lang="java"]<br />
<a href="..."<br />
   onclick="$.post(<br />
                this.href + '@partialUpdateCnt',<br />
                function(data) {<br />
                  $('#partialUpdateCnt').replaceWith(data);<br />
                });<br />
                return false;<br />
           "/><br />
[/source]</p>
<p>Vlastní komunikaci si můžete jednoduše zobrazit na <a href="http://www.rokjinak.cz/srv/www/qf/cs/ramjet/offers/offerListing" target="_blank">odkazovaném příkladě</a> pomocí <a href="http://getfirebug.com/" target="_blank">Firebugu</a>, popřípadě jiných vývojových nástrojů. Firebug je pro monitoring této výměny dat naprosto ideální - hezky v něm uvidíte veškerý obsah request i response serveru. Všimněte si také časů, za které je server schopný vygenerovat odpověď.</p>
<h3>Pozitivní efekty partial update</h3>
<h4>Snížení zatížení serveru</h4>
<p>Zavedením partial update snížíte zatížení serveru hned ve dvou ohledech:</p>
<ul>
<li>omezení vykonávané aplikační logiky
<p>Server neprovádí nic navíc kromě vlastní akce vyvolané uživatelem (např. uložení dat) a vrácení dat pro aktuálně vykreslovanou oblast. Tím se ušetří obrovské množství výkonu - jen se sami na svém aktuálním projektu zamyslete, na co všechno se musíte dotázat aplikační vrstvy, abyste dokázali vykreslit celou HTML stránku - přitom většina věcí se, z pohledu uživatele, mezi jedním a druhým requestem nemění!</p>
</li>
<li>snížení objemu dat pro přenos mezi webserverem a klientem
<p>Kromě toho, že část stránky bude mít vždy menší velikost než stránka celá, je důležité především to, že v této malé části je také <a href="http://developer.yahoo.com/performance/rules.html#num_http" target="_blank">daleko menší počet linkovaných objektů</a> (skripty, styly, obrázky), na které se musí browser zpětně dotázat serveru (i kdyby měl dostat zpět HTTP 304 NOT MODIFIED). Menší počet linkovaných objektů = menší počet HTTP requestů na web server = menší zatížení web serveru jako takového.</p>
</li>
</ul>
<h4>Řádové zrychlení odezvy uživateli = lepší user experience</h4>
<p>Snížením zátěže serveru a snížením objemu přenášených dat a počtu HTTP požadavků na linkované zdroje, partial update skutečně velmi výrazně (řádově) zvyšuje odezvu uživateli aplikace. Odlehčením serveru dostáváte také daleko větší propustnost (throughput) aplikace - tj. více paralelních uživatelů.</p>
<p>Ve vlastní rychlosti hraje velmi důležitou roli i vlastní výměna DOMu - browser má výrazně méně práce sestavit pouze část stránky, než stránku celou. Při vykreslování celé stránky musí browser znovu zpracovat všechny CSS, při prvním načtení (body.onLoad / $(document).ready()) se provádí řada inicializačních procedur linkovaných javascriptových knihoven atd. Obvykle se tak v browseru nevyhnete bliknutí obsahu stránky (<a href="http://www.rokjinak.cz/cs/jsem-zvedavy/co-je-rok-jinak.shtml" target="_blank">porovnejte s přechody mezi statickými stránkami poskytovanými Apachem</a> - klikněte např. na Otázky a odpovědi nebo Výherci). Při částečných výměnách DOM obsahu k podobnému "nepříjemnému" efektu nedochází.</p>
<p>A co se týká "user experience"? Hádejte jestli bude uživatel více spokojen s aplikací, která bude mít odezvy do 1 sekundy, nebo takovou, kde si počká 3-4 vteřiny na vykreslení stránky? Schválně si naměřte odezvy dané části Roku jinak - odpovědi serveru na partial updaty jsou mezi 100 až 150 milisekundami.</p>
<h3>Problémy spojené s partial updatem</h3>
<p>Správná implementace partial update má ovšem i svoji cenu. Existují komplikace, které vám nasazení partial update do vaší aplikace ztíží.</p>
<h4>Zajištění správného kontextu - FORM, ANCHOR</h4>
<p>Na frontendové části musíte ošetřit různé kombinace sběru dat odesílaných na server dle kontextu. Pro jednoduché odkazy stačí vzít HREF a přes jQuery.get (popřípadě post) dotázat server. V případě formuláře musíte serializovat data vyplněná ve formulářových políčkách a ty odesílat jako parametry. jQuery má pro toto jednoduchou metodu:</p>
<p>[source lang="java"]<br />
var data = $("#formId").serializeArray();<br />
[/source]</p>
<h4>Omezení počtu AJAX požadavků na server</h4>
<p>V případě, že uživatel kliká příliš rychle, nebo partial update posadíte na události typu "onmouseover" je dost možné, že se v jednu chvíli seběhne hned několik volání na server. Pro server se jedná o nezávislá volání, takže je možné že pozdější dotaz je vyřízen dřív, popř. že různé odpovědi přijdou klientovi více méně současně. To způsobuje značnou řadu problémů - jednak může klient vidět jinou odpověď než aktuálně čeká (odpovědi se předběhly), popřípadě dochází k chybám při výměně DOM struktury, pokud odpovědi přijdou velmi krátce po sobě (rychlé výměny DOM objektů browserům příliš nesvědčí). Kromě těchto problémů, také velké množství AJAX requestů zbytečně zatěžuje server, aniž by to uživateli něco přinášelo (typicky uživatel chce jen poslední z nich).</p>
<p>Tenhle problém je už trošku větším oříškem. My jsme jej vyřešili integrací <a href="http://plugins.jquery.com/project/AjaxManager" target="_blank">jQuery Ajax Manager pluginu</a>, který umí inteligentně spravovat frontu ajaxových požadavků. Jednak zajistí sériovou komunikaci se serverem, <a href="http://developer.yahoo.com/performance/rules.html#cacheajax" target="_blank">cachování odpovědí pro stejné dotazy</a>, ale také dokáže z fronty vylučovat duplikátní dotazy, které jsou v podstatě zbytečné. Víc detailů je k dispozici na <a href="http://plugins.jquery.com/project/AjaxManager" target="_blank">homepage pluginu</a>.</p>
<p>Kromě výše uvedeného je nutné také uživateli dát najevo, že systém zareagoval na jeho kliknutí (či jinou operaci). V opačném případě si uživatel může myslet, že něco provedl špatně, že se "nic neděje" a kliká zbytečně dál. Toto jsme vyřešili zobrazením animovaného gifu poblíž kurzoru myši, který kopíruje jeho pohyb až do doby, než doběhne proces částečné aktualizace stránky. Po kliknutí tedy uživatel ihned vidí, že systém na pozadí pracuje a už dál nekliká. Navíc jsou uživatelé na animované GIFy v souvislosti s AJAXem zvyklí, takže není třeba nic dál vysvětlovat a podvědomně uživatelé chápou, co se děje.</p>
<h4>Graceful degradation</h4>
<p>V souvislosti s Partial update je nutné také myslet na uživatele s vypnutým JavaScriptem. Možná si řeknete, že ty 2-3 procenta uživatelů směle oželíte, ale </p>
<ol>
<li>každé procento uživatelů je důležité</li>
<li>je to záležitost cti ;-)</li>
</ol>
<p>U nás ve <a href="http://www.fg.cz" target="_blank">Forrestu</a> ctíme pravidlo, že i uživatel s vypnutým JavaScriptem musí být schopný "nějak" zobrazit všechny informace na webu a musí být také schopen provést všechny základní akce (úkony), které s webem souvisí (však si zkuste pustit RokJinak s vypnutým JavaScriptem ;-) ).</p>
<p>Pokud implementujete partial update chytře, nebude pro vás graceful degradation žádný problém. Typický vývoj u nás spočívá v tom, že se vytvoří verze bez partial update - tj. každý klik / submit znamená obnovení celé stránky. Pak jen dynamicky doplníme ke všem linkům / submitům v konkrétní oblasti "onclick" handlery, které provedou její partial update. Na server se posílá vždy kompletní informace, takže serverová část je vždy "plně v obraze" co se děje na klientovi - v žádné chvíli tedy nedochází k tomu, že by se stav na serveru a na klientovi rozešel.</p>
<p>Důležité je, že:</p>
<ol>
<li>vše funguje i bez použití JavaScriptu</li>
<li>nevyvíjí se dvě nezávislé větve kódu, které se musí udržovat</li>
</ol>
<p>Stačí původní kód obohatit jediným voláním JavaScriptu:</p>
<p>[source lang="java"]<br />
$("#doplnIdKomponenty").partialUpdate();<br />
[/source]</p>
<p>Srovnejte náš přístup srovnáte se standardními Ajax komponentami - namátkou třeba DataGridy, které typicky používají nějaký svůj proprietární "protokol" pro komunikaci s backendem na pozadí. Zkuste si v následujících ukázkách vypnout JavaScript a uvidíte, jak dopadnete:</p>
<ul>
<li><a  href="http://component-showcase.icefaces.org" target="_blank">ICE Faces komponenty</a></li>
<li><a  href="http://justajax.com/table/demo.html" target="_blank">JustAjax DataGrid</a></li>
<li><a  href="http://www.activewidgets.com/grid/" target="_blank">ActiveWidgets gridy</a></li>
<li><a  href="http://www.ext-livegrid.com/demo/" target="_blank">Ext Livegrid</a></li>
<li><a  href="http://www.ajaxdaddy.com/demo-sorted-table.html" target="_blank">AjaxDaddy tables</a></li>
<li><a  href="http://wicketstuff.org/wicket14/nested/?wicket:bookmarkablePage=:org.apache.wicket.examples.ajax.builtin.PageablesPage" target="_blank">Jedině Wicket funguje i s vypnutým Javascriptem</a>, což už se bohužel zase nedá říct <a href="http://wicketstuff.org/wicket14/nested/?wicket:bookmarkablePage=:org.apache.wicket.examples.ajax.builtin.TodoList" target="_blank">o této ukázce s Wicketem</a>, takže #fail</li>
</ul>
<h4>Historie navštívených stránek</h4>
<p>Poslední věcí, kterou je nutné brát v úvahu, je údržba správné historie stránek při partial updatech. Částečná aktualizace obsahu se samozřejmě do historie browseru nezapisuje a tak ve chvíli, kdy uživatel vynutí refresh stránky (reload), popřípadě dá Zpět, neberou se tyto změny obsahu v úvahu. Vůči uživateli to není úplně v pořádku, protože pokud máme například scénář - zobrazení listovacího seznamu, přechod na X stránku (partial update), kliknutí na detal položky (přesměrování na novou stránku), a stisknutí tlačítka zpět, uživatel se dostane zpět do listovacího seznamu na první a ne na Xtou stránku, ze které kliknul na detail položky. Obdobně pokud postupně v listovacím seznamu prošel na 5 stránku a dá reload, nezůstane na 5. stránce, jak by čekal, ale na stránce první.</p>
<p>Ovlivňovat historii prohlížeče z Javascriptu v více méně nejde - jednak neexistuje API, a to co máme k dispozici povede k refreshi celé stránky, čímž ztratíme výhody partialUpdate. Existuje jediná možnost, jak si s tímto problémem poradit a tím je využití tzv. "hash" části url. V následujícím příkladě se jedná o string <strong>"kotva"</strong>:</p>
<p>[source:html]<br />
http://www.domena.cz/stranka.html#kotva?parametr1=hodnota1<br />
[/source]</p>
<p>Hash část url se v původním smyslu používá pro navigaci mezi různými částmi stránky. My jej ovšem můžeme využít také pro obejití nedostatečného API pro práci s historií browseru. V případě, že pomocí JavaScriptu zapíšete hodnotu do window.location.hash, browser se pokusí na dané stránce najít element s tímto ID, a pokud jej najde, pokusí se na něj zascrollovat viewport. Pokud jej nenajde, nestane se nic - pouze se změní url v adresní řádce (doplní se tam požadovaný hash) a toto nové změněné url se také zapíše do historie procházení. Důležité je to, že se v tomto případě něděje žádná komunikace se serverem a vše se odehrává pouze na klientovi.</p>
<p>Této techniky využívá řada jQuery pluginů pro správu historie stránek. Např. <a href="http://wiki.github.com/tkyk/jquery-history-plugin/api-reference" target="_blank">jquery.history.js plugin</a> nebo <a href="http://code.google.com/p/reallysimplehistory/" target="_blank">Really Simple History</a>. Problém tohoto a podobných pluginů tkví v tom, že jsou optimalizované pro jedno-stránkovou AJAX aplikaci, jakou je například GMail (vše se děje v jednom okně) a využívají pro monitoring historie skrytý iframe na dané stránce. Při přechodu na jiné url se tedy historie ztrácí.</p>
<p>Pro naše účely jsem napsal vlastní kód, který staví na stejném principu. Při požadavku na partial update dané stránky si uložím parametry jdoucí na server do hash části url (enkóduji nebezpečné znaky a dávám jednoznačný prefix). Takto se mi do historie dostane nový záznam s tímto hashem. Pokud uživatel stiskne tlačítko zpět zabere kód na "onLoad" stránky kontrolující právě tento hash, který případně provede reload stránky s parametry vytaženými právě z tohoto hashe. Je to jedna otočka na server navíc, ale uživatel dostane verzi stránky jakou očekává.</p>
<p>Výše uvedený princip pracuje s různými odchylkami ve všech prohlížečích (testováno IE6+, FFox 1.5+, Chrome). V novějších prohlížečích pokud uživatel zmáčkne tlačítko zpět na stránce, na které před tím provedl partial update, není vyvolán "onLoad" dané stránky (mění se pouze hash, url zůstává stejné) a proto v tuto chvíli naše logika nezabere. Pro tuto situaci je na stránce v určitém intervalu (500ms) spouštěný skript kontrolující změnu hashe aktuálně prohlížené stránky, který v daném případě vyvolá logiku, která se jinak provádí jen při "onLoad". V IE6 zase není do historie zapisována posloupnost hashů na stejné stránce, ale vždy se zaznamená pouze poslední hash stránky.</p>
<p>Přiznávám, že tahle část není úplně triviální, ale nakonec funguje docela dobře :-) .</p>
<h3>Odkazy</h3>
<p>Partial update není náš výmysl a je implementován s různými odchylkami také v řadě jiných web frameworků. Namátkou vybírám některé z nich:</p>
<ul>
<li><a href="http://tapestry.formos.com/nightly/tapestry5/guide/ajax.html" target="_blank">Partial update v Tapestry</a></li>
<li><a href="http://static.springsource.org/spring-webflow/docs/2.0.x/reference/html/ch11s05.html">Podpora partial update ve Spring MVC</a></li>
<li><a href="http://ajaxanywhere.sourceforge.net" target="_blank">JSP knihovna pro Partial Update</a></li>
</ul>
<p>Bohužel se mi nepodařilo najít žádný jednoznačný článek pojednávající o implementaci partial update v JSF, přestože bych tuto podporu zde očekával. Budu vděčen za případné doplnění v komentářích. Zajímavým měřítkem kvality aplikace je úroveň <a href="http://www.dzone.com/links/r/is_graceful_degradation_dead.html" target="_blank">ke graceful degradation</a> - v současnosti je bohužel velmi tristní.</p>
