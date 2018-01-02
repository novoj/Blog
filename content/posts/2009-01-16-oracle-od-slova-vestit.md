---
status: publish
published: true
title: Oracle, od slova věštit
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Ano, ano. Dnes jsem po nasazení nového buildu opět strávil plodné čtyři
  hodiny věštěním z křišťálové koule zvané Oracle Application Server. Ještě ke všemu
  na prostředí, ke kterému není přímý přístup. Kód, který máme již na tuctu instalací,
  který bez problémů běží i na dvou testovacích strojích s \"přibližně\" stejnou konfigurací
  na produkci ne a ne.\r\n\r\nVýsledkem mého pátrání bylo to, že pokud se na konkrétní
  verzi OC4J zavolá metoda getParameterMap() dřív než některá z metod getParameter,
  getParameterNames nebo getParameterValues, tak je výsledkem prázdná mapa, přestože
  se v requestu parametry nachází.\r\n\r\nProtože nejsem žádný dokonalý programátor,
  šel jsem do specifikace, abych si přečetl jestli to nejsem náhodou já, kdo je lamka
  a kdo nezná specifikaci Servletu. No schválně ...\r\n\r\n"
wordpress_id: 347
wordpress_url: http://blog.novoj.net/?p=347
date: '2009-01-16 19:56:10 +0100'
date_gmt: '2009-01-16 18:56:10 +0100'
categories:
- Java
tags: []
comments:
- id: 5911
  author: lzap
  author_email: lzap@seznam.cz
  author_url: ''
  date: '2009-01-17 17:46:04 +0100'
  date_gmt: '2009-01-17 16:46:04 +0100'
  content: Oracle má skvělou databázi. &gt;&gt;&gt; . &lt;&lt;&lt;
- id: 5912
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-01-17 19:17:21 +0100'
  date_gmt: '2009-01-17 18:17:21 +0100'
  content: Souhlasím, ale dost bídnej aplikační server ;-)
- id: 5933
  author: Michal Franc
  author_email: michal.franc@gmail.com
  author_url: ''
  date: '2009-01-19 01:26:19 +0100'
  date_gmt: '2009-01-19 00:26:19 +0100'
  content: Kdyz oni maji tech aplikacu uz ted tolik, ze nevedi kterej poradne podporovat
    :)
- id: 5934
  author: Michal Franc
  author_email: michal.franc@gmail.com
  author_url: ''
  date: '2009-01-19 01:28:28 +0100'
  date_gmt: '2009-01-19 00:28:28 +0100'
  content: Jinak na to co popisujes sem nasel i jako potvrzenou bugu na Metalinku
    .. coz mimochodem dodnes nechapu proc neni otevreny bug tracking system.
- id: 5935
  author: Fess
  author_email: fess@centrum.cz
  author_url: ''
  date: '2009-01-19 07:24:27 +0100'
  date_gmt: '2009-01-19 06:24:27 +0100'
  content: Bídenej aplikační server od Oracle? A ja myslel, že od té doby co koupili
    BEA, tak už to neplatí! ;-)
- id: 5936
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-01-19 08:24:43 +0100'
  date_gmt: '2009-01-19 07:24:43 +0100'
  content: No myslím, že než Oracle převede své zákazníky na WebLogic tak to chvíli
    potrvá a do té doby se budeme stále potýkat s takovými "ptákovinami". Btw. s WebLogicem
    nemám přímou zkušenost, takže nemohu soudit - doufám, že to bude cesta k lepšímu
    a ne z louže pod okap ;-) .
- id: 5950
  author: Jety
  author_email: mail@jetensky.net
  author_url: http://jetensky.net
  date: '2009-01-20 16:46:59 +0100'
  date_gmt: '2009-01-20 15:46:59 +0100'
  content: Hezkej titulek článku :)
- id: 5962
  author: Luba
  author_email: lubos.svoboda@codedynamics.cz
  author_url: http://www.codedynamics.cz
  date: '2009-01-21 14:53:27 +0100'
  date_gmt: '2009-01-21 13:53:27 +0100'
  content: Aplikační server od Oracle je asi ten nejhorší, co sem měl poznat, tak
    mě to vůbec nepřekvapuje.
---
<p>Ano, ano. Dnes jsem po nasazení nového buildu opět strávil plodné čtyři hodiny věštěním z křišťálové koule zvané Oracle Application Server. Ještě ke všemu na prostředí, ke kterému není přímý přístup. Kód, který máme již na tuctu instalací, který bez problémů běží i na dvou testovacích strojích s "přibližně" stejnou konfigurací na produkci ne a ne.</p>
<p>Výsledkem mého pátrání bylo to, že pokud se na konkrétní verzi OC4J zavolá metoda getParameterMap() dřív než některá z metod getParameter, getParameterNames nebo getParameterValues, tak je výsledkem prázdná mapa, přestože se v requestu parametry nachází.</p>
<p>Protože nejsem žádný dokonalý programátor, šel jsem do specifikace, abych si přečetl jestli to nejsem náhodou já, kdo je lamka a kdo nezná specifikaci Servletu. No schválně ...</p>
<p><a id="more"></a><a id="more-347"></a></p>
<p>Citace ze specifikace Servlet 2.3:</p>
<div style="border: 1px solid white; background-color: #333333; font-size: 90%; margin-top: 20px; padding: 10px">
<p><strong>SRV.4.1 HTTP Protocol Parameters</strong></p>
<p>Request parameters for the servlet are the strings sent by the client to a servlet container as part of its request. When the request is a HttpServletRequest object, and conditions set out below are met, the container populates the parameters from the URI query string and POST-ed data.</p>
<p>The parameters are stored as a set of name-value pairs. Multiple parameter values can exist for any given parameter name. The following methods of the ServletRequest interface are available to access parameters:</p>
<ul>
<li>getParameter</li>
<li>getParameterNames</li>
<li>getParameterValues</li>
</ul>
<p>The getParameterValues method returns an array of String objects containing all the parameter values associated with a parameter name. The value returned from the getParameter method must be the first value in the array of String objects returned by getParameterValues.</p>
<p>Data from the query string and the post body are aggregated into the request parameter set. Query string data is presented before post body data. For example, if a request is made with a query string of a=hello and a post body of a=goodbye&amp;a=world, the resulting parameter set would be ordered a=(hello, goodbye, world).</p>
<p>Path parameters that are part of a GET request (as defined by HTTP 1.1) are not exposed by these APIs. They must be parsed from the String values returned by the getRequestURI method or the getPathInfo method.</p>
<p><strong>SRV.4.1.1 When Parameters Are Available</strong></p>
<p>The following are the conditions that must be met before post form data will be populated to the parameter set:</p>
<ol>
<li>The request is an HTTP or HTTPS request.</li>
<li>The HTTP method is POST</li>
<li>The content type is application/x-www-form-urlencoded</li>
<li>The servlet has made an initial call of any of the getParameter family of methods on the request object.</li>
</ol>
<p>If the conditions are not met and the post form data is not included in the parameter set, the post data must still be available to the servlet via the request object’s input stream. If the conditions are met, post form data will no longer be available for reading directly from the request object’s input stream.</p></div>
<p>Když porovnám toto znění se specifikací Servletu 2.4 přibyla k vyjmenovaným metodám i metoda getParameterMap. Nicméně tato metoda již standardně byla už v rozhraní Requestu ve verzi 2.3. Pravděpodobně se tedy ve specifikaci na tuto metodu pozapomělo a programátoři Oracle místo přemýšlení otrocky přetvořili specifikaci do kódu.</p>
<p>Osobně bych větu "The servlet has made an initial call of any of the getParameter family" chápal přirozeně tak, že tam patří i metoda getParameterMap. Naštěstí jsem namátkou vygooglil existenci  <a href="http://kickjava.com/src/com/opensymphony/webwork/dispatcher/DispatcherUtils.java.htm" target="_blank">über nastavení "webwork.dispatcher.parametersWorkaround" prastarého WebWorku</a>:</p>
<p>[source lang="java"]<br />
if (paramsWorkaroundEnabled) {<br />
   // simply read any parameter (existing or not) to "prime" the request<br />
   request.getParameter("foo");<br />
}<br />
[/source]</p>
<p>Z poznámek v kódu jsem vyrozuměl, že podobným výkladem trpí i WebLogic.</p>
<p>Opravdu mám rád kód a knihovny jejichž autoři přemýšlí nad tím, jak a k čemu se bude jejich dílo používat. Třeba takový Spring - ten prostě funguje. A nejen to - každou chvíli tam objevuji věci, které mi jako programátorovi výrazně ulehčují život. To se prostě s OC4J nedá vůbec srovnat.</p>
