---
status: publish
published: true
title: Skryté pastičky v Tomcatu aneb zpětná kompatibilita se všude nenosí
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft size-full wp-image-1953\" title=\"Tomcat Logo\" src=\"http://blog.novoj.net/binary/2012/04/200px-Tomcat-logo.png\"
  alt=\"\" width=\"200\" height=\"133\" />Nespoléhejte se na to, že, tak jako Java
  samotná, budou i základní knihovny a nástroje respektovat důležitost zpětné kompatibility.
  Například v případě Tomcatu se nám už několikrát stalo, že při upgradu na verzi,
  kde se mění pouze číslo patche, se kompletně rozpadla funkčnost aplikace. Poprvé
  to bylo myslím, když v patchi vyupgradovali na novější specku JSP a teď nám zase
  přihodili bombičku v podobě změny obsahu <strong>httpServletRequest.getPathInfo()</strong>,
  která nově vrací i tzv. path parametry.\r\n\r\n"
wordpress_id: 1947
wordpress_url: http://blog.novoj.net/?p=1947
date: '2012-04-29 14:33:35 +0200'
date_gmt: '2012-04-29 13:33:35 +0200'
categories:
- Java
tags:
- tomcat
comments:
- id: 67054
  author: lzap
  author_email: lzap@seznam.cz
  author_url: http://
  date: '2012-04-29 17:23:10 +0200'
  date_gmt: '2012-04-29 16:23:10 +0200'
  content: A prave z techto duvodu je vhodne pouzivat distribuce s dlouhou podporou
    napriklad rhel (tomcat je soucasti) nebo jboss eap. Tam k tomuto nedochazi. ;-)
- id: 67057
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-04-29 17:40:05 +0200'
  date_gmt: '2012-04-29 16:40:05 +0200'
  content: "Počkej, tím chceš říct, že na těchto distribucích se neinstalují bezpečnostní
    patche? Myslím, že je dobrým zvykem patchovat web / app server i z důvodu bezpečnostních
    záplat.\r\n\r\nTj. dřív nebo později na to narazí taky. Leda, že by se postarali
    o nějaký dočasný fix pomocí wrappingu request objektu. Hmm, to se mi ale nějak
    nezdá ..."
- id: 67097
  author: banter
  author_email: lubos.racansky@gmail.com
  author_url: https://twitter.com/#!/banterCZ
  date: '2012-04-30 07:28:02 +0200'
  date_gmt: '2012-04-30 06:28:02 +0200'
  content: Tak určitě je to past. Každopádně jsessionid v url, a to i pokud je to
    pouze na první request, je možná bezpečnostní díra, proto se doporučuje urlRewriting
    vypnout.
- id: 67122
  author: lzap
  author_email: lzap@seznam.cz
  author_url: http://
  date: '2012-04-30 14:23:57 +0200'
  date_gmt: '2012-04-30 13:23:57 +0200'
  content: Patche se vzdy backportuji, chyby tedy mizi, ale verze zustavaji stejne.
    Zpetne se takto udrzuje momentalne cca 20 verzi tomcatu, pokud se budeme bavit
    o rhelu 4, 5 a 6. Zakaznik ma ale na vyber, verze nemusi mit zmrazene. Viz y stream
    vs z stream. Presne tohle je to, proc se za linux plati. Stabilita a zpetna kompatibilita.
- id: 67123
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-04-30 14:34:30 +0200'
  date_gmt: '2012-04-30 13:34:30 +0200'
  content: Dík za info, zkonzultuju to s našima Operations. Vůbec netuším, co kde
    platíme ...
- id: 69518
  author: Ariel
  author_email: ariel@gmail.com
  author_url: ''
  date: '2012-05-21 17:59:19 +0200'
  date_gmt: '2012-05-21 16:59:19 +0200'
  content: "Ahoj\r\n\r\nVyborny clanek, uplne souhlasim.\r\nJen bych upozornila na
    to, ze Path parameter je soucasti Path segmentu, cili jednoho \"adresare\" v URI.
    To znamena, ze zdaleka nemusi byt na konci Stringu getPathInfo(). Proto tvuj kod
    na odstraneni Path parametru je spatne napsany. Pozor, prosim, na to.\r\nJinymi
    slovy, toto je platna adresa:\r\nhttp://www.ariel-is-sexy.com/photos;showHidden=true/photosFromBath;includeNudePhotos=true/index.html\r\n\r\nMejte
    se\r\nAriel"
- id: 69537
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-05-21 20:35:49 +0200'
  date_gmt: '2012-05-21 19:35:49 +0200'
  content: "Díky - tohle je asi nejvíc sexy komentář, co na blogu mám :D\r\n\r\nJe
    v tom pěknej bordel - já jsem zase našel toto: http://www.w3.org/Addressing/rfc1808.txt\r\nKde
    se říká, cituji:\r\n\r\n\"Section 5 of RFC 1738 specifies that the question-mark
    character (\"&#63;\") is allowed in an ftp or file path segment. However, this
    is not true in practice and is believed to be an error in the RFC.  Similarly,
    RFC 1738 allows the reserved character semicolon (\";\") within an http path segment,
    but does not define its semantics; the correct semantics are as defined by this
    document for <params>.\"\r\n\r\nA dále potom:\r\n\r\n\"2.4.5.  Parsing the Parameters\r\n\r\n
    \  If the parse string contains a semicolon \";\" character, then the\r\n   substring
    after the first (left-most) semicolon \";\" and up to the end\r\n   of the parse
    string is the parameters (&lt;params&gt;).  If the semicolon\r\n   is the last
    character, or no semicolon is present, then <params> is\r\n   empty.  The matched
    substring, including the semicolon character, is\r\n   removed from the parse
    string before continuing.\"\r\n\r\nCož by zase dávalo zapravdu tomu mému prvnímu
    řešení. Každopádně pro path matching je umístění path parametrů doprostřed pathInfo
    naprosto nepoužitelná záležitost. Tj. ta jednodušší varianta je více méně stejně
    dostatečně použitelná IMHO.\r\n\r\nKaždopádně jsem kód v zájmu formální správnosti
    převzal ze Spring frameworku, kde to mají předpokládám správně tak, jak jsi mě
    upozorňovala."
- id: 69607
  author: Ariel
  author_email: ariel@gmail.com
  author_url: ''
  date: '2012-05-22 09:47:52 +0200'
  date_gmt: '2012-05-22 08:47:52 +0200'
  content: "Vzdycky me prekvapi, jak je kod ve Spring Frameworku robustni. Oni uz
    na to proste mysleli.\r\nNa SpringSource je spolehnuti. Proc by nekdo pouzival
    neco jineho?\r\n\r\nAriel"
- id: 69615
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-05-22 11:22:48 +0200'
  date_gmt: '2012-05-22 10:22:48 +0200'
  content: Jo, mluvíš mi z duše. Ze čtení Springového kódu jsem se naučil plno věcí.
    Nejčastější proti argument slýchám, že Spring je moc "heavy", což je sice pravda,
    ale ty poklady v něm za sto stojí.
---
<p><img class="alignleft size-full wp-image-1953" title="Tomcat Logo" src="http://blog.novoj.net/binary/2012/04/200px-Tomcat-logo.png" alt="" width="200" height="133" />Nespoléhejte se na to, že, tak jako Java samotná, budou i základní knihovny a nástroje respektovat důležitost zpětné kompatibility. Například v případě Tomcatu se nám už několikrát stalo, že při upgradu na verzi, kde se mění pouze číslo patche, se kompletně rozpadla funkčnost aplikace. Poprvé to bylo myslím, když v patchi vyupgradovali na novější specku JSP a teď nám zase přihodili bombičku v podobě změny obsahu <strong>httpServletRequest.getPathInfo()</strong>, která nově vrací i tzv. path parametry.</p>
<p><a id="more"></a><a id="more-1947"></a></p>
<p>Že nevíte o co se jedná? Jedná se o parametry připojené k url pomocí znaku středník. Zatím jsem neviděl mnoho případů, kdy by se k něčemu využívaly s vyjímkou jediného a tím je <strong>jsessionid</strong> parametr, který je používán k přenosu vygenerovaného SESSION_ID do doby než je známo, jestli klientská strana podporuje Cookies (pak už se toto id předává většinou pomocí cookie). Podrobnosti o zmatcích panujících v této části specky moc hezky rozebírá tento příspěvek (navíc má hezkou statistiku toho, jaký bordel v tom mají různé Servlet kontejnery): <a href="http://cdivilly.wordpress.com/2011/04/22/java-servlets-uri-parameters/">Java Servlet URI Parameters</a>.</p>
<p>Vývojáři Tomcatu se rozhodli, že si tento nepořádek uklidí a udělali tak ve verzi <strong>6.0.33</strong>. Jediné, podle čeho mohlo okolí zjistit (kromě své nefunkční aplikace) byl tento záznam v changelogu:</p>
<p><cite>Improve handling of URLs with path parameters and prevent incorrect 404 responses that could occur when path parameters were present. (kkolinko)</cite></p>
<p>Důvody které je k tomu vedly jsou rozepsány v těchto materiálech:</p>
<ul>
<li><a href="http://tomcat.10.n6.nabble.com/Path-Parameters-Servlet-API-td2085181.html" target="_blank">Diskuse v Tomcat fóru vývojáře podobně překvapeného jako jsem já</a></li>
<li><a href="http://www.springsource.com/security/cve-2010-3700" target="_blank">Odkazovaná chyba Spring Servlet Security, která vzniká právě zneužitím URI path parametrů</a></li>
</ul>
<p>Záměr je to jistě bohulibý, ale provedení typicky Tomcatovské - nic neříkající záznam v changelogu a zvednutí čísla patche. Teď můžeme čekat jak se postupně v mnoha aplikacích začnou objevovat hlášení podobná tomuto: <a href="http://jira.icesoft.org/browse/ICE-7219">Incorrect handling of path parameters in PathDispatcher</a></p>
<p>Takže jestli se vám po upgradu na Apache Tomcat verze 6.0.33 rozpadne vaše webová aplikace, protože webový framework nepočítal s dodatečnými parametry v pathInfo (a to třeba i z toho důvodu, že si mohli vyložit Servlet specku stejně špatně jako dřív sami autoři Tomcatu), už víte o co jde. Při získávání pathInfo je nutné jej takto oříznout:</p>
<p>[source lang="java"]<br />
    /**<br />
     * Removes path parameters from each path segment in the supplied path and truncates sequences of multiple '/'<br />
     * characters to a single '/'.<br />
     *<br />
     * @param path either the {@code servletPath} and {@code pathInfo} from the original request<br />
     *<br />
     * @return the supplied value, with path parameters removed and sequences of multiple '/' characters truncated,<br />
     *  or null if the supplied path was null.<br />
     */<br />
    private String strip(String path) {<br />
        if (path == null) {<br />
            return null;<br />
        }</p>
<p>        int scIndex = path.indexOf(';');</p>
<p>        if (scIndex &lt; 0) {<br />
            int doubleSlashIndex = path.indexOf(&quot;//&quot;);<br />
            if (doubleSlashIndex &lt; 0) {<br />
                // Most likely case, no parameters in any segment and no '//', so no stripping required<br />
                return path;<br />
            }<br />
        }</p>
<p>        StringTokenizer st = new StringTokenizer(path, &quot;/&quot;);<br />
        StringBuilder stripped = new StringBuilder(path.length());</p>
<p>        if (path.charAt(0) == '/') {<br />
            stripped.append('/');<br />
        }</p>
<p>        while(st.hasMoreTokens()) {<br />
            String segment = st.nextToken();<br />
            scIndex = segment.indexOf(';');</p>
<p>            if (scIndex &gt;= 0) {<br />
                segment = segment.substring(0, scIndex);<br />
            }<br />
            stripped.append(segment).append('/');<br />
        }</p>
<p>        // Remove the trailing slash if the original path didn't have one<br />
        if (path.charAt(path.length() - 1) != '/') {<br />
            stripped.deleteCharAt(stripped.length() - 1);<br />
        }</p>
<p>        return stripped.toString();<br />
    }<br />
[/source]</p>
<p><strong>Poznámka ke kódu:</strong> Díky za upozornění Ariel na chybu v mém původním kódu pro ořez. Svůj původní kód jsem nahradil lepším, který jsem <a href="http://www.jarvana.com/jarvana/view/org/springframework/security/spring-security-web/3.0.5.RELEASE/spring-security-web-3.0.5.RELEASE-sources.jar!/org/springframework/security/web/firewall/RequestWrapper.java?format=ok" target="_blank">vybral přímo ze Springu</a>, takže by již měl být v pořádku.</p>
<p>Všechno bych pochopil, co ale nechápu je, proč při nekompatibilních změnách tohoto typu autoři Tomcatu nepoužijí druhé verzovací číslo, aby upozornili na to, že tam může čekat vývojáře nějaký problém. V patchi podobné změny podle mého názoru nikdo nečeká. Určitě by se vyhnuli podobným "hate postům", který jsem právě teď stvořil já.</p>
<p>Fuj!</p>
