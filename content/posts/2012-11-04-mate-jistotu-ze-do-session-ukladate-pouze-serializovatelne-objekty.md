---
status: publish
published: true
title: Máte jistotu, že do session ukládáte pouze serializovatelné objekty?
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft  wp-image-2347\" title=\"Http Session Persistence\"
  src=\"http://blog.novoj.net/binary/2012/10/persistence.jpg\" alt=\"\" width=\"124\"
  height=\"93\" />Jestli ano, tak by mne velmi zajímalo, jak to děláte. My jsme totiž
  ještě donedávna žádnou jistotu neměli - vše záleželo na poctivosti a důslednosti
  programátorů. Jenže v Javě není tahle záležitost vůbec jednoduchá a tak vám může
  díky nějaké referenci hluboko ve stromu objektů uniknout, že to, co ukládáte do
  session, má vazbu na objekt, který serializovatelný není. Výsledkem je ztráta session
  při restartech aplikačního serveru nebo zamezení možnosti <a href=\"http://docs.oracle.com/cd/E13222_01/wls/docs90/cluster/failover.html\"
  target=\"_blank\">session replikovat</a> mezi nody clusteru.\r\n\r\nMy s tímto problémem
  bojujeme dlouho a průběžně - naše zbraně však byly dosud poměrně neefektivní. V
  podstatě jsme se spoléhali na chybové hlášení při restartu Tomcatu, který vypisovalo
  problémové (neserializovatelné) objekty, kvůli kterým nebylo možné obnovit session.
  Jinými slovy - spoléhali jsme se na náhodu.\r\n\r\nNa nedávném hackathonu jsme si
  však vyrobili nástroj, který nám umožní s tímto problémem bojovat lépe.\r\n\r\n"
wordpress_id: 2340
wordpress_url: http://blog.novoj.net/?p=2340
date: '2012-11-04 21:15:31 +0100'
date_gmt: '2012-11-04 20:15:31 +0100'
categories:
- Programování
- Java
- Web
tags: []
comments:
- id: 103828
  author: banter
  author_email: lubos.racansky@gmail.com
  author_url: http://blog.zvestov.cz/
  date: '2012-11-04 22:57:19 +0100'
  date_gmt: '2012-11-04 21:57:19 +0100'
  content: "Dobrý! Matně si vzpomínám na warningy, pokud se do session ukládal neserializovatelný
    objekt. Pravda, vyžaduje to od programátorů aktivnější přístup než vyhození výjimky.\r\n\r\nJeden
    šťouravý dotaz, respektive bych se i rád něčemu přiučil. Koukám, že máte logger
    jako private static final a název malými písmeny. Co na to sonar? Máte nějaké
    pravidlo, které názvy loggerů nezařazuje mezi violation?"
- id: 103873
  author: Tomas
  author_email: tomas.adamek@droid.co.nz
  author_url: http://www.droid.co.nz
  date: '2012-11-05 03:24:54 +0100'
  date_gmt: '2012-11-05 02:24:54 +0100'
  content: Pouzivame plugin Findbugs do Eclipse - funguje to pekne a jenkins takovy
    plugin ma taky (az me to nekdy sere ze to tak pekne funguje kdyz potrebuju rychle
    neco jen tak zmastit :-)
- id: 103937
  author: bedla
  author_email: nemam@email.cz
  author_url: ''
  date: '2012-11-05 07:47:56 +0100'
  date_gmt: '2012-11-05 06:47:56 +0100'
  content: Jste bych zminil -Dsun.io.serialization.extendedDebugInfo=true pri hledani
    neserializovatelnych objektu v grafu.
- id: 103963
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-11-05 09:53:33 +0100'
  date_gmt: '2012-11-05 08:53:33 +0100'
  content: "No Sonar jsme sice experimentálně nasadili na pár projektech, ale nějak
    jsme si na něj nezvykli. Používáme statickou analýzu z IntelliJ Idey, která problémy
    napovídá už v rámci psaní kódu. A ta si na logger s malými písmeny nestěžuje -
    i když u konstant to vyžaduje. Oni mají tu inspekci totiž docela chytrou - cituji
    dokumentaci:\r\n\r\n<cite>This inspection reports any constants whose names are
    either too short, too long, or do not follow the specified regular expression
    pattern. Constants are fields declared static final.\r\nUse the fields provided
    below to specify minimum length, maximum length and regular expression expected
    for constant names (Regular expressions are in standard java.util.regex format).
    Use the checkbox below to specify that only immutable static final fields should
    be checked by this inspection.</cite>\r\n\r\nTj. tím, že logger není immutable,
    tak ta inspekce neřve. Idea je v tomhle prostě boží .)"
- id: 103964
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-11-05 09:55:13 +0100'
  date_gmt: '2012-11-05 08:55:13 +0100'
  content: A odhalí ta inspekce findbugs i problémy s deep serializovatelností? Tj.
    že když do session uložíte Mapu, která serializovatelná je a pak jinde v kódu
    do té mapy uložíte neserializovatelný objekt tak to taky ten problém odhalí? To
    by mě totiž docela překvapilo, protože tohle diagnostikovat není vůbec jednoduché.
    Například Idea tyhle problémy odhalit neumí.
- id: 103966
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-11-05 09:58:10 +0100'
  date_gmt: '2012-11-05 08:58:10 +0100'
  content: Bomba - díky za tip, o tomhle jsem neměl tušení!
- id: 103993
  author: dkl
  author_email: daniel@kolman.cz
  author_url: http://blog.kolman.cz/
  date: '2012-11-05 12:10:18 +0100'
  date_gmt: '2012-11-05 11:10:18 +0100'
  content: My jsme to řešili např. u message a DTO objektů tak, že byl jeden unit
    test, kterej vzal všechny typy z určitýho namespace a zroundtripoval je, tzn.
    vytvořil instanci do který nacpal náhodný hodnoty (případně i referencovaný objekty),
    serializoval, deserializoval a pak porovnal jestli jsou si rovný. Testovalo to
    binární i XML serializaci.
- id: 104000
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-11-05 12:21:43 +0100'
  date_gmt: '2012-11-05 11:21:43 +0100'
  content: "Chápu, a pak byl prostě standard - chceš-li něco strčit do session, vyrob
    DTO v tomhle namespace a dej ho tam - a nesmíš používat obecné kolekce, do kterých
    lze strčit cokoliv. Pak na to zaberou automatizované testy, které ověří mj. i
    serializovatelnost.\r\n\r\nTj. základem je disciplína."
- id: 104036
  author: Dkl
  author_email: daniel@kolman.cz
  author_url: http://
  date: '2012-11-05 15:45:22 +0100'
  date_gmt: '2012-11-05 14:45:22 +0100'
  content: 'No to byl system napsanej v C#, což je (na rozdíl od Javy) staticky typovej
    jazyk, takže s kolekcema nebyl problém. Věci jako Object[] patřej do Ruby :-P
    #hehe #flame'
- id: 104061
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-11-05 17:38:59 +0100'
  date_gmt: '2012-11-05 16:38:59 +0100'
  content: Gotcha! :D
- id: 104092
  author: Tomas
  author_email: tomas.adamek@droid.co.nz
  author_url: http://www.droid.co.nz
  date: '2012-11-05 20:50:20 +0100'
  date_gmt: '2012-11-05 19:50:20 +0100'
  content: "Ted doufam ze jsem pochopil co mas na mysli - kdyz udelam tohle:\r\n\r\n<pre>import
    java.util.HashMap;\r\nimport java.util.Map;\r\nimport javax.servlet.http.HttpSession;\r\nimport
    com.google.inject.Inject;\r\npublic class TestFindbugs\r\n{\r\n  @Inject\r\n  HttpSession
    session;\r\n\r\n  private Map myMap = new HashMap();\r\n\r\n  public static class
    MyObject  {}\r\n\r\n  public void save() {\r\n    session.setAttribute(\"test\",
    \"test\");\r\n    session.setAttribute(\"test\", new MyObject()); &lt;----- Findbugs
    reports a bug\r\n  }\r\n}</pre>\r\n\r\nTak me jenkins (a eclipse) padne s tim
    ze se snazim ulozit neserializovatelny (kurna to je slovo) object do session na
    radku dve v metode save - tohle me zachyti v celym kodu, cross-class, nezalezi
    kde do te session/mapy ukladam. Odchyti mi i kdyz ukladam deep structured object
    kde treba jen jen attribut tridy nekde ve stromu neni serializovatelny."
- id: 104242
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-11-06 08:50:50 +0100'
  date_gmt: '2012-11-06 07:50:50 +0100'
  content: "A kdyby to bylo zapsané takhle?\r\n\r\n<pre>import java.util.HashMap;\r\nimport
    java.util.Map;\r\nimport javax.servlet.http.HttpSession;\r\nimport com.google.inject.Inject;\r\npublic
    class TestFindbugs {\r\n  @Inject\r\n  HttpSession session;\r\n\r\n  public static
    class MyObject  {}\r\n\r\n  private Map getMap() {\r\n     Map result = new HashMap();\r\n
    \    result.put(\"nonSerializable\", new MyObject());\r\n     return result;\r\n
    \ }\r\n\r\n  public void save() {\r\n    session.setAttribute(\"test\", \"test\");\r\n
    \   session.setAttribute(\"test\", getMap());\r\n  }\r\n}\r\n</pre>"
- id: 104243
  author: banter
  author_email: lubos.racansky@gmail.com
  author_url: http://blog.zvestov.cz
  date: '2012-11-06 08:51:05 +0100'
  date_gmt: '2012-11-06 07:51:05 +0100'
  content: To zní slibně. Sonar má tu výhodu, že je to centrální místo s reporty a
    statistikou, jak se dané měřené hodnoty měnily v čase.
- id: 104245
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-11-06 08:57:07 +0100'
  date_gmt: '2012-11-06 07:57:07 +0100'
  content: "Jo to dává logiku. V teamcity, je teda taky možné pouštět inspekce z Idey
    centrálně a získávat reporty. Nicméně - hmm, nepoužíváme to ... asi máme ještě
    dost prostoru pro zlepšování svého vývojového procesu ;)\r\n\r\nMáš nějakou přímou
    zkušenost, jak tyhle statistiky zlepšují kvalitu vašeho kódu? Je někdo vyčleněný,
    kdo to pravidelně sleduje a pak dává náměty na zlepšení? Nebo ty výsledky sledují
    všichni? Ono to totiž může zabrat dost času a na rovinu - business chce fíčury,
    kvalitu kódu cheme my v devu. Takže jde o to časově rozumně vyvážit ."
- id: 104298
  author: banter
  author_email: lubos.racansky@gmail.com
  author_url: http://blog.zvestov.cz
  date: '2012-11-06 12:35:38 +0100'
  date_gmt: '2012-11-06 11:35:38 +0100'
  content: Sami od sebe statistiky kvalitu nezlepší, jsou to jen hlídací psi. Sledovat
    by to měl každý, zabere jim to tak pět minut týdně, jako kontrolu, zda se projekt
    nezhoršuje. Já nasazuji sonar u zákazníků k definování stavu nula (to se většinou
    sonar málem pomine a já taky), od kterého musí být vše lepší. Od určitého bodu
    chaosu je totiž hrozně pracné nové fíčury přidávat na tak chatrný domeček z karet,
    aby se nezřítil.
- id: 104319
  author: Guido
  author_email: vit.kotacka@gmail.com
  author_url: http://www.sw-samuraj.cz/
  date: '2012-11-06 14:22:58 +0100'
  date_gmt: '2012-11-06 13:22:58 +0100'
  content: Zajímavý řešení, zkusím si ho zapamatovat. My jsme vždycky sledovali logy,
    někdy to řve přímo framework (třeba Wicket).
- id: 104321
  author: Guido
  author_email: vit.kotacka@gmail.com
  author_url: http://www.sw-samuraj.cz/
  date: '2012-11-06 14:27:11 +0100'
  date_gmt: '2012-11-06 13:27:11 +0100'
  content: Statistiky sami o sobě nezlepšují kvalitu. Ale pokud jsou spojený s notifikacemi
    z CI (a kontrola se provede hned po komitu), tak to funguje velmi dobře.
- id: 104458
  author: Tomas
  author_email: tomas.adamek@droid.co.nz
  author_url: http://www.droid.co.nz
  date: '2012-11-07 01:49:03 +0100'
  date_gmt: '2012-11-07 00:49:03 +0100'
  content: Z nejakeho duvodu nemuzu odpovedet na prispevek dole tak je pro poradek
    hlasim, ze ten uvedeny priklad finbugs neodhali.
- id: 104541
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-11-07 08:26:55 +0100'
  date_gmt: '2012-11-07 07:26:55 +0100'
  content: "Jo ty diskuse jsou jen 2-úrovňové, takže se pak musí reagovat na vyšší
    příspěvek.\r\n\r\nJá jsem si to myslel, že to tenhle scénář neodhalí, protože
    to technicky není vůbec jednoduché. Idea to taky nenahlásí. Pravda je, že pokud
    je disciplinovaný tým a do session se strkají pouze generifikované DTO, kde je
    všechno striktně serializovatelné (jak píše Dkl), tak riziko nehrozí .... ale
    realita je dost často někde jinde ... a proto ten náš záchytný Servlet filtr :)"
- id: 148527
  author: julio
  author_email: julio@example.com
  author_url: ''
  date: '2013-01-24 19:40:32 +0100'
  date_gmt: '2013-01-24 18:40:32 +0100'
  content: "Fail-faster:\r\nsince servlet spec. 2.3\r\n\r\nhttp://docs.oracle.com/javaee/6/api/javax/servlet/http/HttpSessionAttributeListener.html\r\nhttp://www.mkyong.com/servlet/a-simple-httpsessionattributelistener-example/\r\n\r\n---\r\n\r\nhttp://martinfowler.com/eaaCatalog/dataTransferObject.html\r\nhttp://www.bookdepository.com/Patterns-Enterprise-Application-Architecture-Martin-Fowler/9780321127426"
---
<p><img class="alignleft  wp-image-2347" title="Http Session Persistence" src="http://blog.novoj.net/binary/2012/10/persistence.jpg" alt="" width="124" height="93" />Jestli ano, tak by mne velmi zajímalo, jak to děláte. My jsme totiž ještě donedávna žádnou jistotu neměli - vše záleželo na poctivosti a důslednosti programátorů. Jenže v Javě není tahle záležitost vůbec jednoduchá a tak vám může díky nějaké referenci hluboko ve stromu objektů uniknout, že to, co ukládáte do session, má vazbu na objekt, který serializovatelný není. Výsledkem je ztráta session při restartech aplikačního serveru nebo zamezení možnosti <a href="http://docs.oracle.com/cd/E13222_01/wls/docs90/cluster/failover.html" target="_blank">session replikovat</a> mezi nody clusteru.</p>
<p>My s tímto problémem bojujeme dlouho a průběžně - naše zbraně však byly dosud poměrně neefektivní. V podstatě jsme se spoléhali na chybové hlášení při restartu Tomcatu, který vypisovalo problémové (neserializovatelné) objekty, kvůli kterým nebylo možné obnovit session. Jinými slovy - spoléhali jsme se na náhodu.</p>
<p>Na nedávném hackathonu jsme si však vyrobili nástroj, který nám umožní s tímto problémem bojovat lépe.</p>
<p><a id="more"></a><a id="more-2340"></a><br />
Vycházíme z principu <a href="http://en.wikipedia.org/wiki/Fail-fast" target="_blank">fail-fast</a> - tedy pokud se nám povede do session uložit neserializovatelný objekt, chceme o tom vědět co nejdříve, aby se nám jednodušeji hledal údaj a akce, která do session závadný objekt ukládá. Zároveň není možné se spolehnout pouze na monitoring operace <a href="http://docs.oracle.com/javaee/1.2.1/api/javax/servlet/http/HttpSession.html#setAttribute(java.lang.String, java.lang.Object)" target="_blank">setAttribute</a>, protože tou jsme mohli do session uložit pouze referenci na kontejnerový objekt (např. Map), do kterého se teprve později uloží reference na neserializovatelný objekt.</p>
<h2>Implementované řešení</h2>
<p>V případě, že aplikace běží ve <a href="http://blog.novoj.net/2009/08/07/odlisujete-v-aplikaci-vyvojove-testovaci-a-produkcni-prostredi/" target="_blank">vývojovém režimu</a>, prochází zpracování requestu servletovým <a href="http://docs.oracle.com/javaee/6/api/javax/servlet/Filter.html" target="_blank">filtrem</a>, který po ukončení zpracování requestu projde všechny atributy session a vyzkouší, zda je možné je všechny serializovat. Ukázku takového filtru přikládám níže (vyhodnocení vývojového režimu je už na vás):</p>
<p>[source language="java"]<br />
public class SerializabilityCheckFilter implements Filter {<br />
    private static final Log log = LogFactory.getLog(SerializabilityCheckFilter.class);</p>
<p>    public void init(FilterConfig filterConfig) throws ServletException {<br />
        //nothing necessary to do<br />
    }</p>
<p>    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)<br />
            throws IOException, ServletException {<br />
        try {<br />
            chain.doFilter(request, response);<br />
        } finally {<br />
            if (request instanceof HttpServletRequest) {<br />
                HttpServletRequest httpRequest = (HttpServletRequest) request;<br />
                HttpSession session = httpRequest.getSession(false);<br />
                if (session != null) {<br />
                    boolean serializable = true;<br />
                    StringBuilder items = new StringBuilder();<br />
                    Enumeration&lt;String&gt; names = session.getAttributeNames();<br />
                    while (names.hasMoreElements()) {<br />
                        String attrName = names.nextElement();<br />
                        boolean attributeSerializable = serialize(<br />
                                attrName, session.getAttribute(attrName)<br />
                        );<br />
                        if (!attributeSerializable) {<br />
                            if (items.length() &gt; 0) {<br />
                                items.append(&quot;, &quot;);<br />
                            }<br />
                            items.append(attrName);<br />
                        }<br />
                        serializable &amp;= attributeSerializable;<br />
                    }</p>
<p>                    if (!serializable) {<br />
                        throw new ObjectNotSerializableException(<br />
                                &quot;These objects stored in session attributes &quot; +<br />
                                    &quot;are not serializable (see detailed log): &quot; +<br />
                                    items<br />
                        );<br />
                    }<br />
                }<br />
            }<br />
        }<br />
    }</p>
<p>    public void destroy() {<br />
        //nothing necessary to do<br />
    }</p>
<p>    /**<br />
     * Serializes object into byteArray<br />
     *<br />
     * @param attrName<br />
     * @param object<br />
     * @return<br />
     */<br />
    private boolean serialize(String attrName, Object object) {<br />
        ByteArrayOutputStream bos = null;<br />
        ObjectOutput out = null;<br />
        try{<br />
            bos = new ByteArrayOutputStream();<br />
            out = new ObjectOutputStream(bos);<br />
            out.writeObject(object);<br />
            return true;<br />
        } catch (IOException ex) {<br />
            String msg = &quot;Failed to serialize attribute: &quot; + attrName;<br />
            log.error(msg, ex);<br />
            return false;<br />
        } finally {<br />
            IOUtils.closeQuietly(bos);<br />
            if (out != null) {<br />
                try { out.close(); } catch (IOException ignored) {}<br />
            }<br />
        }<br />
    }</p>
<p>}<br />
[/source]</p>
<h2>Výhody řešení</h2>
<p>... jsou zřejmé:</p>
<ul>
<li>chyby serializace a výkonnostní penalizace se projeví pouze ve vývojovém režimu - v testovacím ani produkčním se již logika neaplikuje</li>
<li>díky vyhazované vyjímce je vývojář NUCEN se problémem zabývat - jinak se mu bude obtížně aplikace vyvíjet</li>
<li>v textu vyjímky jsou přehledně uvedený názvy atributů, které se nedaří serializovat - takže vývojář přesně ví, kde je problém a i to, kdy problém nastal, protože to muselo být v aktuálním requestu</li>
<li>vývojář je veden k udržování malé velikosti session, jinak se mu bude zpracování requestů zpomalovat díky nutnosti celou session po každém requestu serializovat</li>
<li>je velká pravděpodobnost, že většina problémů - ne-li všechny se vychytají průběžně při vývoji aplikace</li>
</ul>
<p>Výše uvedený nástroj používáme teprve týden a už se nám tímto způsobem podařilo vychytat asi 10 problémů, které v naší aplikaci byly aniž bychom o nich věděli. Řešení každého problému trvalo jen pár minut a každý z nás má teď větší jistotu, že se mu nepovede do aplikace zavléci problém podobného charakteru. Máme totiž v záloze automat, který nikdy nespí!</p>
