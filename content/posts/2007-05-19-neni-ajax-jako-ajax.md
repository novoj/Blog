---
status: publish
published: true
title: Není AJAX jako AJAX - GWT vs. DWR
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<p>V projektu, na kterém v současné době pracuji, bylo navrženo poměrně
  extenzivní použití AJAXových funkcí. Proto jsem se, coby AJAXem dosud netknutý vývojář,
  vrhnul do studia knihoven, které by mi realizaci usnadnily. Výsledkem mi bylo zjištění,
  které uvádím v titulku příspěvku - není AJAX jako AJAX. Každá z knihoven tento problém
  řeší velmi odlišně - a přestože mé první kroky vedly k GWT, brzy jsem tento záměr
  opustil.</p>\r\n"
wordpress_id: 16
wordpress_url: http://blog.novoj.net/2007/05/19/neni-ajax-jako-ajax/
date: '2007-05-19 13:55:46 +0200'
date_gmt: '2007-05-19 12:55:46 +0200'
categories:
- Java
tags: []
comments: []
---
<p>V projektu, na kterém v současné době pracuji, bylo navrženo poměrně extenzivní použití AJAXových funkcí. Proto jsem se, coby AJAXem dosud netknutý vývojář, vrhnul do studia knihoven, které by mi realizaci usnadnily. Výsledkem mi bylo zjištění, které uvádím v titulku příspěvku - není AJAX jako AJAX. Každá z knihoven tento problém řeší velmi odlišně - a přestože mé první kroky vedly k GWT, brzy jsem tento záměr opustil.</p>
<p><a id="more"></a><a id="more-16"></a></p>
<p>Jelikož pracuji ve <a href="http://www.fg.cz" target="_new">společnosti</a>, která své krédo staví na velmi propracovaných webech - co se týká použitelnosti, přístupnosti, validity a grafickém vzhledu (o tuhle stránku věci se naštěstí nestarám já ;)) - bylo nutné zajistit, aby stejná funkcionalita byla přístupná s AJAXem i bez něj. Mým prvotním záměrem tedy bylo:</p>
<ul>
<li>HTML generovat servlety,</li>
<li>AJAX by pouze oživoval některé prvky tak, že místo odeslání odkazu / formuláře provede operaci na pozadí a modifikoval DOM bez nutnosti reloadu stránky,</li>
<li>minimalizovat logiku na klientovi a maximum provést na serveru - z důvodů pokrytí testy,</li>
<li>mít možnost pracovat pod přihlášeným uživatelem - tzn. i v AJAXovém volání mít přístupnou session,</li>
<li>pokud možno se vyhnout nějakému ohýbání kódu, kvůli integraci AJAXu,</li>
<li>minimalizovat kód, který by sloužil pouze AJAXu,</li>
<li>docílit přenositelnosti mezi hlavními prohlížeči, aniž bych to já musel nějak příliš řešit.</li>
</ul>
<h3><a href="http://code.google.com/webtoolkit/" target="_new">GWT - Google Web Toolkit</a></h3>
<p>První knihovna, kterou jsem zkoumal byl GWT. Ze zcela racionálních důvodů jsem si myslel, že je to pro mne to pravé. Hodně se o něm mluví, stojí za ním velká korporace (tudíž by měl být poměrně propracovaný), JavaScript se píše v Javě, což je pro Java programátora přeci to ideální. Po několika včerech jsem došel k několika poznatkům:</p>
<ol>
<li>GWT mě nutí dělat věci jeho stylem - každá odchylka se draze platí; musíte použít buď všechno nebo nic (to je vidět už na tom jak si GWT vlastně všechno řeší - včetně takových drobností jako je např. internacionalizace)</li>
<li>jeho použití mě dost připomíná session beany v J2EE - strašně práce kvůli ničemu; musíte nadefinovat dva interfacy - které si navíc ani v deklaraci metod neodpovídají (RemoteService + AsyncCallback), dále pak implemenaci remote služby na straně serveru (? implements vaši RemoteService) + implementaci EntryPointu, který představuje klientskou část + jednu statickou HTML page, ve které se to bude celé odehrávat + CSS + popisný *.gwt.xml soubor - a to ani nemluvím o tom, že všechny DTO, které si vyměňujete přes AJAXové rozhraní musí implementovat marking interface IsSerializable - čímž se vám dependence na GWT dostává i do nižších vrstev (pokud nechete furt překopírovávat data z interních bean do "gwt" bean a zpět)</li>
<li>GWT jde stylem, že do vybraných DOM elemenů stránky dovytvoří dynamicky celou vnořenou HTML strukturu - skoro mi to připadá, jako by se HTML stránka rozdělila na dvě části - část spravovanou GWT a tu druhou; v části spravované GWT se dostanete k objektům, které jsou potomky třídy Widget a můžete s nimi slušně manipulovat - v té druhé části (kterou jste si sami nevytvořili ale už v HTML prostě byla) už takové možnosti nemáte; dostanete se pouze k objektu Element, se kterým nic moc neuděláte, akorát ho můžete vyměňovat přes JSNI (JavaScript Native Interface = vámi natvrdo napsané javascriptové metody) - kde už nemáte takových výhod jako v Java režimu</li>
<li>jak tedy Google řeší, když uživatel nemá zapnutý javascript? Kouknul jsem se na gmail.com - hned na první stránce na vás jukne informace o vypnutém javascriptu a můžete jít na tzv. "noscriptovou" verzi - ovšem ta má pravděpodobně úplně oddělený zdrojový kód od té AJAXové verze (myslím na úrovni prezentační vrstvy) - já ale nechci psát GUI 2x - na to prostě nemám čas</li>
<li>další dost matoucí věc je ta statická HTML stránka - už jenom takováhle hloupost vám zabere dost času - typicky budete mít totiž tuhle stránku generovanou nějakým servletem; takže budete nějakou dobu stejně jako já hledat zda a jak tohle jde vůbec udělat</li>
<li>na stránce můžete mít pouze jeden jediný GWT modul - reuse GWT komponent je totiž na úrovni Widgetů a nikoliv na úrovni EntryPointů (tak jsem tedy alespoň pochopil)</li>
<li>ke GWT je poměrně dost dokumentace, ale ani v jedné vám neřeknou to co přesně vy potřebujete - poznatky, které tu píšu jsem nikde na webu neobjevil - vždy jen nějaké náznaky a částečná řešení problémů; např. i v GWT in Action je více méně jen podrobněji popsáno to, co psal <a href="http://interval.cz/clanky/google-web-toolkit/" target="_new">Dagi na intervalu.cz</a></li>
</ol>
<p>Rozhodně nechci GWT jen strhat. Velkou výhodu GWT vidím v tom, že v něm můžete vytvářet (a znovupoužívat) poměrně rozsáhlé a kombinované JS komponenty a vůbec vytvářet v něm velké AJAX aplikace, aniž byste se dostali do stavu, kdy bude obtížné kód udržovat natož rozšiřovat. Prostě GWT je vhodný na rozsáhlá řešení - pokud byste jej chtěli použít na věci jako sem tam šoupnout našeptávač, sem tam nějakou funkci volat asynchroně atd. je to absolutní overkill.</p>
<p>Ještě bych rád uvedl, že mé poznatky vycházejí asi z týdenního studia po večerech. Pokud na nich chcete stavět, ještě si je stejně radši prověřte - nerad bych někoho přivedl na scestí. Ale věřím, že pokud je tu něco špatně, uvedou zastánci GWT věci na pravou v komentářích pod článkem.</p>
<h3><a href="http://getahead.org/dwr/" target="_new">DWR - Direct Web Remoting</a></h3>
<p>Další knihovna, po které jsem na doporučení mého kolegy sáhnul, byla DWR - Direct Web Remoting. U ní jsem také zůstal, jelikož splňuje všechny mé požadavky. Ideálně se hodí právě pro AJAXové oživení jinak stále bezjavascriptově funkčních web prezentací. Learning curve u této knihovny je asi 2 hodiny, oproti GWT do kterého jsem čučel několik dní </p>
<p>DWR poskytuje v podstatě pouze dvě služby - za to je poskytuje kvalitně a jednoduše:</p>
<ul>
<li>zpřístupnění Java tříd z klienta - tedy zpřístupnění rozhraní na serveru a marshalling / unmarshalling přenášených POJO</li>
<li>poskytnutí základní knihovny odladěných JavaScriptových funkcí pro použití na klientovi (např. nahrazení výběrů v selectech, řádků v tabulkách, nastavování a získávání hodnot aj.)</li>
</ul>
<p>DWR mě poskytnul vše, co jsem hledal. Především generuje JavaScript ad hoc - tzn. nemusím nic překompilovávat do *.js, které bych nějak musel složitě přenášet do mé web aplikace. Ve web.xml si pouze zaregistruji DWR servlet, který mi poskytne všechny *.js on the fly jak je zapotřebí. V konfiguračním souboru dwr.xml (pokud integruji DWR se Springem, vypadne mi i tento konfigurák) si nadefinuji třídy, které budou zvenčí (AJAXem) přístupné a seznam POJO tříd, které v komunikaci protečou. U tříd je možné odfiltrovat pouze určité metody, které mají být přístupné atd. atd.</p>
<p>Další skvělou vlastností DWR je to, že vlastně svůj kód nepotřebujete vůbec nijak upravovat proto, aby jste ho mohli používat AJAXem. Žádné zanášení tříd interfacy DWR a podobně. Místo interfaců, které by stejně na klientovi a serveru nemohly sedět (ani u GWT nesedí) se DWR drží přístupu convention over configuration. Víte, že na straně klienta (v Javascriptu) zavoláte svou metodu stylem server: "nazevMetod(parametr1, parametr2)" - klient: "nazevVystaveneBeany.nazevMetody(parametr1, parametr2, asyncCallback)". To je ten základní a jednoduchý způsob - asyncCallback představuje JavaScriptovou metodu, která se provede jakmile ze serveru přijde odpověď. DWR se dále soustředí na řešení případných výjimečných stavů - tzn. můžeme mít různé callbacky pro případ, kdy volání skončí exception.</p>
<p>Dalším cennou třešničkou na dortu je integrace do rozšířených frameworků - budu jmenovat jen pár: Spring, Hibernate, Acegi Security, JSF ... Můžu z vlastní zkušenosti říct, že např. integrace do Springu je naprosto skvělá (od chvíle, kdy jsem začal studovat DWR mi trvalo asi jen 20 minut, než jsem si zavolal první metodu beany z klienta). Stačí registrovat DWR namespace a pak už jen u vybrané beany označit elementem &lt;dwr:remote .../&gt;. Kompletní návod lze nalézt na <a href="http://bram.jteam.nl/index.php/2007/01/31/spring-dwr-ajax-made-easy/" target="_new">blogu Bram Smeetse</a>. Vývojáři DWR opravdu mysleli na nás ostatní vývojáře - POJO, kterých může být poměrně dost lze označit wildcardy ... např. všechny třídy v package "cz.novoj.ajax.dto.*" - prostě pohodička. Na serveru se dostanete v případě potřeby k session uživatele (což v případě GWT jde určitě taky), jednoduše integrujete bezpečnostní opatření (jak přesným označením povolených metod, tak případně integrací Acegi Security frameworku).</p>
<p>Faktem je, že DWR by se asi nehodil na rozsáhlé kódování na straně klienta - přeci jen vám s JavaScriptem pomůže jen svou "Utils" knihovnou a vše co potřebujete navíc si musíte napsat sami. Tím pádem už začínáte riskovat, že nebude váš kód tak přenositelný mezi prohlížeči jak byste chtěli.</p>
<h3>Závěrem</h3>
<p>Znovu jsem se přesvědčil jak je důležité používat správné nástroje na správné věci. Pro mé potřeby je DWR to ideální - GWT bych musel velmi pracně ohýbat. Škoda jen, že jsem při hledání toho správného kladiva nenarazil na žádný článek, který by mi řekl to, co jsem se snažil já zachytit ve výše uvedených odstavcích. To byl důvod, proč jsem tento příspěvěk napsal - snad mé zkušenosti někomu pomohou.</p>
<h4>Zajímavé odkazy</h4>
<p><i>Google Web Tolkit</i></p>
<ul>
<li><a href="http://code.google.com/webtoolkit/" target="_new">GWT - Google Web Toolkit</a></li>
<li><a href="http://interval.cz/clanky/google-web-toolkit/" target="_new">Úvod do GWT v češtině od Dagiho</a></li>
<li><a href="http://www.jetbrains.com/idea/training/demos/GWT.html" target="_new">velmi luxusní demíčko o podpoře GWT v IntelliJ Idea</a></li>
<li><a href="http://software-wonders.blogspot.com/2007/02/it-is-not-mistery-that-google-web.html" target="_new">integrace GWT se Springem</a></li>
<li><a href="http://www-128.ibm.com/developerworks/java/library/j-ajax4/" target="_new">zajímavý tutorial od Philipa McCarthyho</a> - zajímavá je věta v závěru: "GWT is a comprehensive framework that provides a great deal of useful functionality. However, GWT is something of an all-or-nothing approach, targeted at a relatively small niche in Web application development market."</li>
</ul>
<p><i>Direct Web Remoting</i></p>
<ul>
<li><a href="http://vavru.cz/java/dwr-ajax-knihovna-pro-remotovani-java-objektu/trackback/" target="_new">vyčerpávající článek o DWR od Vlasty Vávrů v češtině</a></li>
<li><a href="http://getahead.org/" target="_new">DWR - Direct Web Remoting</a></li>
<li><a href="http://bram.jteam.nl/index.php/2007/01/31/spring-dwr-ajax-made-easy/" target="_new">integrace do Springu</a></li>
<li><a href="http://www.javaworld.com/javaworld/jw-06-2005/jw-0620-dwr.html" target="_new">tutorial na javaworld.com</a></li>
<li><a href="http://nb.vse.cz/~ZELENYJ/it442/eseje/xsynv01/dwr.htm" target="_new">seminární práce Václava Synáčka o DWR v češtině</a></li>
</ul>
<p><i>A trochu bokem</i></p>
<ul>
<li><a href="http://jquery.com/" target="_new">jQuery knihovna odlěděných JavaScriptových funkcí</a></li>
<li><a href="http://interface.eyecon.ro/" target="_new">koukněte na demíčka ... jsou fakt super</a></li>
</ul>
