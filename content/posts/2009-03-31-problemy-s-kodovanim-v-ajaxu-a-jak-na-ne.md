---
status: publish
published: true
title: Problémy s kódováním v AJAXu a jak na ně
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "V prosinci jsem znovu řešil problém s kódováním českých znaků při AJAXové
  komunikaci se serverem. Znovu říkám proto, že jsem stejný problém řešil před pár
  měsíci, ale řešení  jsem stihnul úplně zapomenout. Tentokrát jsem si ale poklepal
  na čelo a říkám si: \"Furo tvá paměť se horší, zapiš to nebo nad tím budeš za měsíc
  trávit čas znovu\".\r\n\r\n"
wordpress_id: 202
wordpress_url: http://blog.novoj.net/?p=202
date: '2009-03-31 20:47:33 +0200'
date_gmt: '2009-03-31 19:47:33 +0200'
categories:
- Programování
- Java
- JavaScript
tags: []
comments: []
---
<p>V prosinci jsem znovu řešil problém s kódováním českých znaků při AJAXové komunikaci se serverem. Znovu říkám proto, že jsem stejný problém řešil před pár měsíci, ale řešení  jsem stihnul úplně zapomenout. Tentokrát jsem si ale poklepal na čelo a říkám si: "Furo tvá paměť se horší, zapiš to nebo nad tím budeš za měsíc trávit čas znovu".</p>
<p><a id="more"></a><a id="more-202"></a></p>
<p>Problém je poměrně obecného charakteru - kdysi jsem na to narazil při používání knihovny <a href="http://www.prototypejs.org/" target="_new">Prototype.js</a>, nyní to byla <a href="http://jquery.com/" target="_new">jQuery</a> s Tomcatem na straně serveru. Obě dvě knihovny mají pro AJAX (<a href="http://docs.jquery.com/Ajax" target="_new">jQuery</a>, <a href="http://prototypejs.org/api/ajax" target="_new">Prototype.js</a>) velmi pěknou podporu - ačkoliv bych řekl, že Prototype.js je v tomto ohledu o kousek dál.</p>
<p>V případě, že používáte AJAX pro odesílání obsahu formulářů padnou vám do oka metody, které v obou frameworcích nesou shodný název "serialize()". Např.:</p>
<p>[source lang="java"]<br />
//jQuery<br />
//serializes all form fields into field1=value1&field2=value2 form<br />
var params = $("#myForm").serialize();<br />
//serializes all form fields into simple JSON object<br />
var jsonData = $("#myForm").serializeArray();</p>
<p>//Prototype.js<br />
//serializes all form fields into field1=value1&field2=value2 form<br />
var params = $("#myForm").serialize();<br />
//serializes all form fields into simple JSON object<br />
var jsonData = $("#myForm").serialize(true);<br />
[/source]</p>
<p>Intuitivně potom člověk použije serializovanou formu jako součást GET url:</p>
<p>[source lang="java"]<br />
//jQuery<br />
var params = $("#myForm").serialize();<br />
$.get(url + ? + params,  function(result) {alert(result);});<br />
var jsonData = $("#myForm").serializeArray();<br />
$.get(url, jsonData, function(result) {alert(result);});<br />
//Prototype.js<br />
var params = $("#myForm").serialize();<br />
new Ajax.Request(url + "?" + params, {<br />
  onSuccess: function(result) {alert(result);}<br />
});<br />
var jsonData = $("#myForm").serialize(true);<br />
new Ajax.Request(url, {<br />
  parameters: params,<br />
  onSuccess: function(result) {alert(result);}<br />
});<br />
[/source]</p>
<p>Jenže právě tady padne kosa na kámen. Pokud formulář obsahuje data s národními znaky, ty se cestou na server pomrší - a to zcela spolehlivě. Otázka zní, kde se pomrší a proč?!</p>
<p>Problém je v tom, že HTTP protokol (snad s vyjímkou nefinalizované verze HTML 5) dodnes nezná způsob jak z klienta předat na server informaci o tom v jakém kódování je url requestu. Velmi zajímavá je věta z <a href="http://jetty.mortbay.org/jetty5/faq/faq_s_900-Content_t_International.html" target="_new">Jetty FAQ</a>:</p>
<p><cite>"Current standards (July 2002) provide no basis for the reliable transmission of international characters using the URL %HH escape mechanism."</cite></p>
<p>Tento FAQ dokument vřele doporučuji k přečtení, protože je to asi nejdetailnější rozbor této nepříjemné situace, která nás pálí i v roce 2009 - tedy sedm let po vydání tohoto FAQ!</p>
<p>Aby nebylo celé legrace konec, dočteme se, že různé web kontejnery a dokonce různé verze web kontejnerů překládají obsah URL různě - jen autoři Jetty serveru přiznávají, že URL očekávají v kódování ISO-8859-1, KROMĚ verze 4.0, kde URL očekávali v UTF-8. Nechci ani domýšlet, jak si standard vykládají další typy web kontejnerů.</p>
<p>Když se podíváme na stranu klienta - tedy web browseru. Ani tady nepanuje při kódování URL jednotný přístup. Zajímavou tabulku nabízí článek <a href="http://code.google.com/p/browsersec/wiki/Part1#Unicode_in_URLs" target="_new">Google Browser Security Handbook</a>.</p>
<h2>Co s tím</h2>
<p>Jediným víceméně spolehlivým způsobem je pro posílání parametrů, které by mohly používat národní znaky NIKDY NEPOUŽÍVAT HTTP GET metodu, ale vždy se přidržet POST. Potom můžeme jednotně aplikovat Servlet Filtr, který zavolá metodu setCharsetEncoding na kódování, ve kterém byla vrácena HTML stránka s daným formulářem (viz. např. článek <a href="http://wiki.apache.org/tomcat/Tomcat/UTF-8" target="_blank">Tomcat/UTF-8</a>).</p>
<p>V případě Tomcatu bychom za jistých podmínek mohli vyřešit i přenos národních znaků v rámci URL (GET metoda). Pokud budeme vracet HTML stránku s formulářem v UTF-8, měla by většina browserů encodovat URI v UTF-8 kódování (některé totiž berou pro kódování URI kódování UTF-8 jako standard, jiné používají po kódování URI kódování dané HTML stránky - viz. <a href="http://code.google.com/p/browsersec/wiki/Part1#Unicode_in_URLs" target="_new">Google Browser Security Handbook</a>).</p>
<p>Na straně Tomcatu potom můžeme v <strong>server.xml</strong> konfiguračním souboru na elementu <strong>&lt;Connector&gt;</strong> definovat jeden z následujících atributů:</p>
<ul>
<li>URIEncoding="UTF-8"
<p>This specifies the character encoding used to decode the URI bytes, after %xx decoding the URL. If not specified, ISO-8859-1 will be used. </p>
</li>
<li>useBodyEncodingForURI="true"
<p>This specifies if the encoding specified in contentType should be used for URI query parameters, instead of using the URIEncoding. This setting is present for compatibility with Tomcat 4.1.x, where the encoding specified in the contentType, or explicitely set using Request.setCharacterEncoding method was also used for the parameters from the URL. The default value is false. </p>
</li>
</ul>
<p>Nicméně toto nastavení bude potom platné pro všechny virtuální hosty daného Tomcatu, což může být pro využití této funkce limitující. Z tohoto důvodu jsem výše popsané řešení ani netestoval a spokojil jsem se s tím, že veškerá data obsahující národní znaky AJAXem vždy POSTuji.</p>
<h2>Na závěr</h2>
<p>Tento článek nepřináší v podstatě žádné nové informace. Tenhle problém je tu s námi již řadu let. Řadu let už používáme osvědčené workaroundy, které nám víceméně fungují a řekl bych, že ještě pěknou řádku let s nimi budeme muset vystačit.</p>
<p>Tuhle kapitolku jsem tu otevřel proto, že na tento problém můžeme narazit z odlišného úhlu - při odesílání dat pomocí AJAXu, kde nám tento problém nemusí přijít tak zřejný a je navíc velmi lákavé zůstat u defaultních hodnot javascriptových knihoven, které typicky znamenají GET požadavek na stranu serveru.</p>
<p>Přestože webové aplikace píšu už nějaký ten pátek, strávil jsem na analýze problému při AJAXovém volání poměrně dost času. A to dokonce dvakrát :-) ... ale potřetí už ne, protože až na si naběhnu znovu, tak si budu moci přečíst už jen závěry v tomhle článku.</p>
<h2>Zdroje</h2>
<ul>
<li><a href="http://java.sun.com/developer/technicalArticles/Intl/HTTPCharset/" target="_blank">Character Conversions from Browser to Database</a> - základní popis problémů s kódovám při odesílání dat z browser na servlet</li>
<li><a href="http://jetty.mortbay.org/jetty5/faq/faq_s_900-Content_t_International.html" target="_blank">How do I work with international characters?</a> - naprosto skvělý článek od tvůrců Jetty serveru popisující detailně problematiku rozeznávání kódování na straně serveru</li>
<li><a href="http://wiki.apache.org/tomcat/Tomcat/UTF-8" target="_blank">Tomcat/UTF-8</a> - návod na implementaci charset filtru - s několika tipy pro kódování GET parametrů pro server Tomcat - viz. můj článek</li>
<li><a href="http://www.nabble.com/request-parameters-mishandle-utf-8-encoding-td18720039.html" target="_new">Hlášení chyby o špatném dekódování UTF-8 znaků z URL v trackeru Apache Tomcatu</a> <a href="http://marc.info/?l=tomcat-user&m=121738798803004&w=2" target="_new">a ještě jednou</a> - it's not a bug, it's a feature :-) </li>
<li><a href="http://unspecified.wordpress.com/2008/07/08/browser-uri-encoding-the-best-we-can-do/" target="_new">Browser URI encoding: The best we can do</a> - naděje svítá s HTML v. 5</li>
</ul>
