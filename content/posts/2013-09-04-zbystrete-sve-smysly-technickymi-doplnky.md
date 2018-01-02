---
status: publish
published: true
title: Zbystřete své smysly technickými doplňky
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<div><img class=\"alignleft  wp-image-2736\" alt=\"HTML 5 Notifications\"
  src=\"http://blog.novoj.net/binary/2013/09/html5notifications.png\" width=\"185\"
  height=\"175\" />Nevím jak vám, ale nám se při vývoji často stává, že vývojáři některé
  věci přehlíží a to se nám negativně odráží na produktivitě a kvalitě výstupu. Člověk
  je tvor omylný, ale inteligentní a proto se snaží se vybavit takovými nástroji,
  které jeho nedokonalosti dokáží vyvážit. Na posledním hackathonu kolega <a id=\"\"
  href=\"https://www.facebook.com/michal.kolesnac\" target=\"_blank\" shape=\"rect\">Michal
  Kolesnáč</a> přišel s nápadem a prototypem rozšíření našeho <a href=\"http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/\"
  target=\"_blank\">existujícího doplňku</a> pro Google Chrome, které pomocí <a id=\"\"
  href=\"http://www.html5rocks.com/en/tutorials/notifications/quick/\" target=\"_blank\"
  shape=\"rect\">HTML 5 notifikací</a> upozorní vývojáře na potenciální problémy na
  prohlížené web stránce. Minulý týden jsme řešení dotáhli do konce a myslím, že stojí
  za to, abych se s Vámi o tento nápad podělil.</div>\r\n<div>"
wordpress_id: 2697
wordpress_url: http://blog.novoj.net/?p=2697
date: '2013-09-04 16:24:30 +0200'
date_gmt: '2013-09-04 15:24:30 +0200'
categories:
- Programování
- Java
- Softwarové nástroje
- Web
- JavaScript
tags: []
comments:
- id: 152070
  author: frc
  author_email: franc@fg.cz
  author_url: http://
  date: '2013-09-04 19:07:17 +0200'
  date_gmt: '2013-09-04 18:07:17 +0200'
  content: Potvrzuju ze je to silne motivacni. Po prvnim dnu jsem fixnul dlouhodobe
    spatne fungujici cache v uloziati zabezpečení.
- id: 152071
  author: Zuzi
  author_email: zuzi.oko@seznam.cz
  author_url: http://prodej-bytu.hotel-luxus.info/
  date: '2013-09-05 10:42:55 +0200'
  date_gmt: '2013-09-05 09:42:55 +0200'
  content: no já se těšila že to okomentuju páč mě zaujal ten nadpis a vyvolal takové
    emoce že až... Zbystřete své smysly technickými doplňky ale k tomuto nemám až
    zas tak co říct, jen snad to že na to snad budu mít někdy čas a vyzkouším
---
<div><img class="alignleft  wp-image-2736" alt="HTML 5 Notifications" src="http://blog.novoj.net/binary/2013/09/html5notifications.png" width="185" height="175" />Nevím jak vám, ale nám se při vývoji často stává, že vývojáři některé věci přehlíží a to se nám negativně odráží na produktivitě a kvalitě výstupu. Člověk je tvor omylný, ale inteligentní a proto se snaží se vybavit takovými nástroji, které jeho nedokonalosti dokáží vyvážit. Na posledním hackathonu kolega <a id="" href="https://www.facebook.com/michal.kolesnac" target="_blank" shape="rect">Michal Kolesnáč</a> přišel s nápadem a prototypem rozšíření našeho <a href="http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/" target="_blank">existujícího doplňku</a> pro Google Chrome, které pomocí <a id="" href="http://www.html5rocks.com/en/tutorials/notifications/quick/" target="_blank" shape="rect">HTML 5 notifikací</a> upozorní vývojáře na potenciální problémy na prohlížené web stránce. Minulý týden jsme řešení dotáhli do konce a myslím, že stojí za to, abych se s Vámi o tento nápad podělil.</div>
<div><a id="more"></a><a id="more-2697"></a></div>
<div>Na úvod se podívejte, jak nám výsledné řešení pomáhá v praxi:</div>
<div></div>
<div>[youtube=https://www.youtube.com/watch?v=dluseSIN3tU]</div>
<h2>
Princip fungování</h2>
<div>Princip je relativně obecný a je určitě přenositelný i do vašeho vývojového ekosystému. O vývoji rozšíření pro Chrome toho už bylo <a id="" href="http://www.zdrojak.cz/clanky/vytvarime-rozsireni-pro-prohlizec-chrome/" target="_blank" shape="rect">napsáno i v češtině</a> docela dost a proto zde nepůjdu do úplných podrobností.</div>
<div></div>
<div>Celý princip je zachycen na následujícím sequence diagramu (btw. vytvořený v <a id="" href="http://www.ckwnc.com/#1002204" target="_blank" shape="rect">http://www.ckwnc.com/</a> ... což je krásná služba pro generování sequence diagramů - jen nedoplňuje popisky k aktorům):</div>
<div></div>
<div><a href="http://blog.novoj.net/binary/2013/09/sequence1.png"><img class="aligncenter  wp-image-2702" alt="Sekvenční diagram komunikace" src="http://blog.novoj.net/binary/2013/09/sequence1.png" width="580" height="480" /></a></div>
<div>Jednoduše řečeno - každý požadavek na webovou aplikaci prochází servletovým filtrem, který při každém požadavku vygeneruje unikátní token a zapíše do hlaviček odpovědi cookie obsahující URL, na kterém bude v budoucnu odpovídat na požadavky pro zobrazení zpráv spojených s tímto requestem. Po ukončení zpracování HTTP požadavku filtr zanalyzuje aktuální stav aplikace a případně zapíše zprávy pro vývojáře ohledně věcí, kterým by měl věnovat pozornost.</div>
<div></div>
<div>Chrome plugin monitoruje změny cookies a pokud narazí na změnu v cookie se sledovaným názvem, vybere z ní URL, vytvoří XmlHttpRequest a AJAXem se dotáže serveru na seznam zpráv k zobrazení. Požadavek zachytí opět náš servletový filtr, podle unikátního tokenu si ze session vytáhne dříve vygenerovaný seznam zpráv. Nakonec vytvoří JSON zprávu s odpovědí, která obsahuje buď prázdné pole, nebo seznam notifikací s dodatečnými informacemi (např. důležitostí sdělení). JSON je pluginem rozparsován a uživateli jsou prezentovány zprávy jako HTML 5 notifikace. Je důležité si uvědomit, že najednou mohou být zobrazeny pouze 3 notifikace (omezení prohlížeče) a proto je potřeba ty zprávy koncipovat spíše jako odkazy někam dál. V našem případě otvírám po kliknutí na notifikaci <a href="http://blog.novoj.net/2012/09/04/nastroje-pro-vyvoj-web-aplikaci-ve-forrestu/" target="_blank">RamJet Inspektor</a>, kde je k nalezení už konkrétní rozpad problému.</div>
<div></div>
<div>Cílem rozhodně není zahltit vývojáře informacemi - notifikace mají zobrazovat jen informace o důležitých problémech, které vyžadují pozornost a je riziko, že by je vývojář mohl přehlížet. Naopak pokud by je chtěl přehlížet, tak by mu měly notifikace jeho ignoranci alespoň znepříjemnit :).</div>
<div></div>
<div>V našem případě aktuálně monitorujeme tyto problémy:</div>
<div>
<ul>
<li>pomalá odezva stránky (více jak 1 vteřina na vrácení kompletního výstupu)</li>
<li>pomalé SQL dotazy při zpracování požadavku (více jak 200ms na zpracování SQL příkazu)</li>
<li>duplicitní SQL dotazy (špatné použití cachování)</li>
<li>chyby při zpracování stránky (jak při akci, tak i v rámci renderingu) - obvykle by měly být vidět samy od sebe, ale někdy se skryjí ve &lt;script&gt; blocích nebo na stránce chybí komponenta pro výpis chybových hlášení</li>
<li>chyby při aplikaci změn v konfiguraci (refresh Spring kontextů selhal) - jelikož se jede z poslední známé funkční konfigurace, vývojář často problém s reloadem nepostřehne a marně pátrá proč se aplikace nechová tak, jak by podle poslední konfigurace měla</li>
<li>(zvažujeme) použití deprekovaných komponent a funkcí</li>
<li>(plánujeme) zobrazení informace o nelokalizovaných textových popiscích na stránce</li>
</ul>
<p>A také tyto významné informace v životním cyklu aplikace:</p>
<ul>
<li>vypálení události do Spring kontextu (na události navazujeme např. e-mailové notifikace a další <a href="http://en.wikipedia.org/wiki/Observer_pattern" target="_blank">observer</a> akce)</li>
<li>reload konfigurace (tj. aplikování změn v konfiguraci)</li>
</ul>
</div>
<h2>Realizace</h2>
<div>Základem každého plugin je soubor <a id="" href="http://developer.chrome.com/extensions/manifest.html" target="_blank" shape="rect">manifest.json</a>, kam je nutné doplnit seznam oprávnění, které bude naše rozšíření vyžadovat - v našem případě potřebujeme oprávnění: notifications (11), cookies (9) a také komunikaci s aplikačním serverem na stejné doméně po zabezpečeném i nezabezpečeném protokolu (12 a 13). Také si musíme povolit přístup k seznamu ikon, které budeme chtít v notifikacích zobrazovat (15-19) a připojit i JavaScriptový soubor (6), který bude obsahovat logiku, která nám vše oživí.</div>
<p>[source lang="js" highlight="6,9,11"]<br />
{<br />
    &quot;name&quot;:&quot;Ramjet Inspector&quot;,<br />
    &quot;version&quot;:&quot;1.8&quot;,<br />
    ... další povinné informace ...<br />
    &quot;background&quot;:{<br />
        &quot;scripts&quot;: [&quot;background.js&quot;]<br />
    },<br />
    &quot;permissions&quot;:[<br />
        &quot;cookies&quot;,<br />
        &quot;tabs&quot;,<br />
        &quot;notifications&quot;,<br />
        &quot;http://*/*&quot;,<br />
        &quot;https://*/*&quot;,<br />
    ],<br />
    &quot;web_accessible_resources&quot;:[<br />
        &quot;skin/INFO.png&quot;,<br />
        &quot;skin/WARNING.png&quot;,<br />
        &quot;skin/ERROR.png&quot;<br />
    ]<br />
}[/source]</p>
<p>A takhle vypadá obsah JavaScript souboru <strong>background.js</strong>, který obstarává naslouchání na změny v cookies a následné zobrazování notifikací (soubor jsem zkrátil a upravil do srozumitelnější podoby - originál je podstatně delší):</p>
<p>[source lang="js"]<br />
var openNotifications = 0;</p>
<p>//REGISTRACE LISTENERU NA ZMĚNY V COOKIES<br />
chrome.cookies.onChanged.addListener(function (data) {<br />
    //zajímá nás pouze vytvoření cookie<br />
    if (data.cause == &quot;explicit&quot; &amp;&amp; data.removed == false) {<br />
        //s tímto názvem<br />
        if (&quot;RAMJET_COOKIE_NOTIFICATIONS&quot; == data.cookie.name) {<br />
            fetchAndDisplayNotifications(data.cookie);<br />
        }<br />
    }<br />
});</p>
<p>//ZÍSKÁNÍ SEZNAMU NOTIFIKACÍ AJAXEM ZE SERVERU<br />
function fetchAndDisplayNotifications(cookie) {<br />
    var xhr = new XMLHttpRequest();<br />
    var url = getUrlFromCookie(cookie);<br />
    xhr.open(&quot;GET&quot;, url, true);<br />
    xhr.onload = function () {<br />
        //o výsledek se má zajímat jen když server odpověděl OK<br />
        if (this.status == 200) {<br />
            //v JSONu nám přijde kolekce objektů<br />
            var notifications = JSON.parse(this.responseText);<br />
            for(var i in notifications) {<br />
                showNotification(notifications[i]);<br />
            }<br />
        }<br />
    };<br />
    xhr.send();<br />
}</p>
<p>//ZÍSKÁNÍ URL STRINGU Z COOKIE A ÚPRAVA PROTOKOLU<br />
function getUrlFromCookie(cookie) {<br />
    var url = cookie.value;<br />
    url = url.replace(new RegExp(&quot;\&quot;&quot;, 'g'), &quot;&quot;);<br />
    if(&quot;http&quot; != url.substring(0, 4)) {<br />
        var prefix = cookie.secure ? &quot;https://&quot; : &quot;http://&quot;;<br />
        url = prefix + cookie.domain + url;<br />
    }<br />
    url = url.replace(new RegExp(&quot;\&quot;&quot;, 'g'), &quot;&quot;);<br />
    return url;<br />
}</p>
<p>//ZOBRAZENÍ NOTIFIKACE<br />
function showNotification(serverNotification) {<br />
    //výchozí callback pouze zruší automatické zmizení notifikace<br />
    var defaultCallback = function () {<br />
        clearTimeout(timeout);<br />
    };</p>
<p>    //notifikaci vytvoříme pouze pokud je místo na obrazovce<br />
    if (openNotifications &lt; 3) {<br />
        var notification = window.webkitNotifications.createNotification(<br />
                'skin/' + serverNotification.severity + '.png',<br />
                'Ramjet inspector',<br />
                serverNotification.text<br />
        );<br />
        notification.show();<br />
        openNotifications++;<br />
        //po 5 vteřinách se notifikace sama zavírá<br />
        var timeout = setTimeout(function () {<br />
            notification.cancel();<br />
            openNotifications--;<br />
        }, 5000);</p>
<p>        //tady řešíme po kliku otevření správného debug okna inspektora<br />
        notification.onclick = defaultCallback<br />
    } else {<br />
        //jinak odložíme zobrazení notifikace o 5 vteřin<br />
        setTimeout(function() { showNotification(notification); }, 5001)<br />
    }<br />
}<br />
[/source]</p>
<p>A takhle vypadá obsah JSON zprávy, která odchází ze servlet filtru:</p>
<p>[source lang="js"]<br />
[<br />
   {<br />
      &quot;severity&quot;: &quot;warning&quot;,<br />
      &quot;toolWindow&quot;: &quot;debugger&quot;,<br />
      &quot;toolWindowTab&quot;: &quot;sqlQueries&quot;,<br />
      &quot;text&quot;: &quot;Při generování stránky se opakují 3 dotazy celkem 5x. Pravděpodobně plýtváš výkonem!&quot;<br />
   },<br />
   {<br />
      &quot;severity&quot;: &quot;info&quot;,<br />
      &quot;toolWindow&quot;: &quot;events&quot;,<br />
      &quot;toolWindowTab&quot;: null,<br />
      &quot;text&quot;: &quot;Při zpracování požadavku došlo k vyvolání události userCreated.&quot;<br />
   }<br />
]<br />
[/source]</p>
<h2>A dál?</h2>
<p>Především se potřebujeme přesvědčit, že tento způsob informování vývojáře je použitelný - tedy aby ho naopak zbytečně neobtěžoval. I proto jsem vybíral k notifikaci pouze zásadní situace a problémy v souvislosti s vývojem aplikace (i když si nejsem jist třeba u notifikace pomalé odezvy stránky, která nastává často v souvislosti s debugováním). Pokud se ale osvědčí, budeme chtít udělat podobnou funkcionalitu i pro náš Firefox plugin. Firefox <a href="http://news.softpedia.com/news/Firefox-22-Aurora-Adds-Support-for-HTML5-Desktop-Notifications-344220.shtml" target="_blank">od verze 22</a> totiž již <a href="http://devseo.co.uk/blog/using-the-web-notifications-api" target="_blank">podporuje HTML 5 notifikace</a>. Nicméně vyvíjet pluginy pro Firefox je daleko větší pruda než pro Chrome, takže ten je aktuálně až druhý v pořadí.</p>
<p>Co si o prototypu myslíte? Připadne vám to jako dobrý nápad?</p>
