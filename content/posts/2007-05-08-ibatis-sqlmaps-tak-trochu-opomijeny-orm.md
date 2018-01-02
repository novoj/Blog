---
status: publish
published: true
title: iBatis SqlMaps - tak trochu opomíjený ORM
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<p>Nedá mi to, abych nenapsal něco o frameworku iBatis. Někteří jej možná
  znáte, někteří jste možná o něm už slyšeli, ale dle trafficu na java.cz konferenci
  bych řekl, že jej většina z vás přehlíží. Zůstal nepovšimnut i v našem krají protřelém
  CZ podcastu číslo 8. Myslím, že je to škoda a proto jsem se rozhodl o malou osvětovou,
  nebo-li, jak by řekl Roumen, evangelizační práci.</p>\r\n<p>Ještě v úvodu bych rád
  podotknul, že někomu se může zdát že to není ten pravý \"entrprase\" framework,
  není kompatibilní s JPA, nemá anotace a vůbec je celý takový jednoduchý. Že je možná
  až tak jednoduchý, že jeho použití ani nemůže přinést tu pravou zábavu ve formě
  hledání příčin mystického chování vaší aplikace. iBatis se navíc nehonosí žádným
  buzzwordem, který by se dal prodat zákazníkovi. Pokud si to myslíte, máte pravdu
  - šetřte své oči, už nemusíte číst dál, protože tento článek určitě není pro vás.</p>\r\n"
wordpress_id: 15
wordpress_url: http://blog.novoj.net/2007/05/08/ibatis-sqlmaps-tak-trochu-opomijeny-orm/
date: '2007-05-08 09:15:30 +0200'
date_gmt: '2007-05-08 08:15:30 +0200'
categories:
- Java
- iBatis
tags: []
comments:
- id: 93
  author: Roman Dagi Pichlik
  author_email: pichlik@seznam.cz
  author_url: http://www.sweb.cz/pichlik/
  date: '2007-05-09 18:24:43 +0200'
  date_gmt: '2007-05-09 17:24:43 +0200'
  content: Nerekl bych, ze iBatis je klasicky ORM nastroj, urcite si na to nehraje.
    iBatis predstavuje velice dobry kompromis mezi ORM nastroji a klasickou praci
    s JDBC. Jeho pouziti bych doporucil tam, kde je obtizne pouzit ORM mapovani a
    nebo tam kde se nevyuziva jeho plna sila. Sveho casu jsem na nej mel education
    session, ze ktere zustala prezentace na <a href="http://sweb.cz/pichlik/ibatis/presentation.pdf"
    rel="nofollow">http://sweb.cz/pichlik/ibatis/presentation.pdf</a>, ale letmym
    proletnutim bych nerekl, ze nejak vyznamne prekracuje informace, ktere poskytuje
    tenhle pekny clanek ;-).
- id: 94
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-05-09 19:22:11 +0200'
  date_gmt: '2007-05-09 18:22:11 +0200'
  content: "JJ Dagi souhlasím. Taky jsem váhal, jestli tam to slůvko ORM mám dát.
    Koneckonců oni v dokumenaci taky tvrdí, že \"to není ORM\". Jenomže jsem se snažil
    pohledat definici ORM, a nikde jsem žádnou rozumnou nenašel. Takže kdybys o nějaké
    věděl, rád se vzdělám.\r\n\r\nNavíc jsem potřeboval do titulku něco úderného,
    co každému hned nahraje o čem bude řeč. Výraz \"tak trochu opomíjený kompromis
    mezi JDBC a ORM\" je kapánek moc dlouhý. :)\r\n\r\nMmch. ta prezentace je super.
    Škoda, že mi jsem ji nevygůglil, když jsem s iBatisem začínal. Vřele doporučuji
    ostatním."
- id: 6644
  author: tronza
  author_email: janekda@seznam.cz
  author_url: ''
  date: '2009-02-27 00:13:42 +0100'
  date_gmt: '2009-02-26 23:13:42 +0100'
  content: v "iBatis in Action" píšou Data Mapper(iBatis)xORM(Hibernate)
- id: 6649
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-02-27 10:13:11 +0100'
  date_gmt: '2009-02-27 09:13:11 +0100'
  content: Pravda - po nějaké době a přečtení dalších zdrojů uznávám, že můj výklad
    termínu ORM byl trochu jinde, než je konsens Java populace. Např. na WIKI (http://en.wikipedia.org/wiki/IBATIS)
    mají iBatis v sekci Persistence Framework. V dnešní době už bych pro iBatis použil
    jiný termín než ORM - pod tímto termínem si totiž už v dnešní době představí JPA
    like řešení.
- id: 61846
  author: martin zemlicka
  author_email: martinzemlicka@seznam.cz
  author_url: http://martinzemlicka.cz
  date: '2012-02-17 21:42:50 +0100'
  date_gmt: '2012-02-17 20:42:50 +0100'
  content: Kromě jednoduchosti je Ibatis velmi flexibilní, co do nezávislosti objektové
    a datové vrstvy. Bohužel to má svou nevýhodu. A to když jste nuceni přebírat projekt
    po někom (například indických programátorech), kdo pracoval "ne zcela úplně koncepčně".
    Tím myslím, že vztah mezi objekty a databází je dán sáhodlouhými a všelijak strukturovanými
    SQL statementy v sqlmap souborech, jejichž smysl je těžko zpětně pochopitelný
    a struktura databáze může být opravdu všelijaká (o absenci unit testů nemluvě).
    JPA je náročnější na to, něco rychle "zplácat". Vazba mezi databází a entitami
    takovouhle volnost nedává (nebo o tom nevím). Každopádně tyto vztahy musí být
    dány, takže si tam nemůže každý dělat cokoliv a výsledek by měl být srozumitelnější
    i pro člověka, který kód nepsal a nenavrhoval.
- id: 61917
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-02-19 08:52:54 +0100'
  date_gmt: '2012-02-19 07:52:54 +0100'
  content: "Myslíš, že člověk, který dokáže nekoncepčně \"zprasit\" iBatis implementaci
    by odvedl kvalitnější práci při použití např. Hibernate? Já mám s Hibernate tedy
    jen malé zkušenosti, ale \"zprasit\" se tam toho dá taky dost. Pokud navíc mají
    pod správou i návrh DB, tak si myslím, že to je jen z bláta do louže. Ale rozumím
    argumentu čitelnosti - na druhou stranu v Hibernate máš taky fůru selectů ve formě
    HQL v kódu, které mohou vypadat všelijak. Tady těžko soudit - museli bychom vidět
    kód napsaný od stejných indů třeba nad Hibernatem a pak bychom asi mohli dělat
    závěry.\r\n\r\nNaštěstí mám štěstí na kolegy, takže si na čitelnost jejich kódu
    nemohu stěžovat."
---
<p>Nedá mi to, abych nenapsal něco o frameworku iBatis. Někteří jej možná znáte, někteří jste možná o něm už slyšeli, ale dle trafficu na java.cz konferenci bych řekl, že jej většina z vás přehlíží. Zůstal nepovšimnut i v našem krají protřelém CZ podcastu číslo 8. Myslím, že je to škoda a proto jsem se rozhodl o malou osvětovou, nebo-li, jak by řekl Roumen, evangelizační práci.</p>
<p>Ještě v úvodu bych rád podotknul, že někomu se může zdát že to není ten pravý "entrprase" framework, není kompatibilní s JPA, nemá anotace a vůbec je celý takový jednoduchý. Že je možná až tak jednoduchý, že jeho použití ani nemůže přinést tu pravou zábavu ve formě hledání příčin mystického chování vaší aplikace. iBatis se navíc nehonosí žádným buzzwordem, který by se dal prodat zákazníkovi. Pokud si to myslíte, máte pravdu - šetřte své oči, už nemusíte číst dál, protože tento článek určitě není pro vás.</p>
<p><a id="more"></a><a id="more-15"></a></p>
<div align="center">...</div>
<p>Po drsnějším úvodu mi doufám zůstali ti praví čtenáři ;). Takže přejděme k práci ...</p>
<p>iBatis je ORM framework, jehož historie sahá někam k roku 2002. Je to stabilní a odladěný kus kódu se skvělou dokumentací a průhlednými zdrojovými kódy, jehož cílem je zjednodušit programátorovi práci s JDBC. Nesnaží se odstínit programátora plně od vlastní databáze, jako to činí JPA compliant frameworky. Zůstává někde na půli cesty mezi plnotučným ORM a prostým JDBC.</p>
<h3>Fíčury</h3>
<p>Základní myšlenky iBatisu by se daly shrnout možná takto:</p>
<ul>
<li>nenutí programátora učit se o moc víc než to co už umí (JDBC) - learning curve je 3 - 8 hodin ... v podstatě už za 3 hodiny můžete programovat, aniž byste mohli udělat nějakou zásadní chybu, která by vás nutila něco předělávat, když budete framework používat intenzivněji a déle</li>
<li>nesnaží se zakrýt práci s DB - tím je jednoduchý a transparentní</li>
<li>poskytuje maximální podporu programátorovi při rutinních činnostech</li>
<ul>
<li>mapuje vrácené result sety na Java objekty (dao třídy, jsou stejně tenké, jako když použijete Hibernate)</li>
<li>nenutí vás fetchovat celé objekty - klidně si vrácený set může převést na mapu: název sloupce / hodnota nebo jen na primitiv</li>
<li>není nutné psát mapování property tříd na sloupce - iBatis podporuje autowire by name</li>
<li>jednoduše řeší vytahování záznamů po stránkách</li>
<li>poskytuje plugovatelnou cachovací logiku - řízení cache je na vás (což možná nemusí být výkonnostně optimální, zato se nikdy neztratíte)</li>
<li>jednoduchá práce s transaction / dávkami příkazů je samozřejmostí</li>
<li>stejně jako ostatní ORM vás oddělí od práce s connection a vlastními resultsety - už nikdy nezapomenete na close() ;)</li>
</ul>
<li>odpovědnost za psaní vlastních SQL dotazů nechává na programátorovi - SQL máte plně pod kontrolou a jednoduše a bez hluboké znalosti frameworku vymáčknete z iBatisu i takové chuťovky jako uložené procedury (a stále máte podporu tohoto frameworku - nejste nuceni se snížit k JDBC)</li>
<li>odděluje SQL dotazy od kódu - při požadavku na přenositelnost mezi DB se velmi jednoduše pouze upraví nekompatibilní SQL dotazy (což je sice oproti např. Hibernate práce navíc, ale když to vezmete kolem a kolem, té práce není zas až tak moc, pokud máte automatické testy)</li>
<li>nenutí vás psát sáhodlouhé XML (s SQL příkazy) - obsahuje řadu vychytávek, které vám ušetří psaní redundantního kódu - dynamické SQL, podmínky v SQL, includy, extenze - a přesto je to všechno strašně jednoduché</li>
</ul>
<h3>Jak iBatis funguje?</h3>
<p>Jak vidno z níže uvedeného schématku vyjmutého z iBatis dokumentace, framework s skládá z následujících části:</p>
<ul>
<li><strong>SqlMapConfig.xml</strong><br>XML soubor, který je pouze rozcestníkem k dalším mapovacím souborům a jenž obsahuje "globální" konfiguraci iBatisu - defakto je to obdoba hibernate.properties souboru</li>
<li><strong>SqlMap.xml</strong><br>Vlastní mapovací soubory (např. User.xml), který obsahuje SQL dostazy spojené se serializací a deserializací objektů do a z databáze - opět obdoba *.hbm z Hibernate</li>
<li><strong>Mapped statementy</strong><br>Z výše uvedených xml souborů iBatis při inicializaci vytvoří "mapped statementy" - tzn. objektovou reprezentaci vaší konfigurace; za běhu si potom pro tyto mapped statementy iBatis postupně vytvoří a zacachuje prepared statementy</li>
<li><strong>Vstupní data</strong><br>tedy parametry jednotlivých dotazů - může se jednat o Java beany, primitivní typy, mapy a nebo XML</li>
<li><strong>Výstupní data</strong><br>tedy výstupní naplněné Java "objekty" - může se jednat o Java beany, primitivní typy, mapy a nebo XML</li>
</ul>
<p><strong>Schémátko vyňaté z iBatis dokumentace:</strong><br />
<a href="http://files.novoj.net/iBatis/schema.png"><img src="http://files.novoj.net/iBatis/schema.png" alt="Schéma iBatis" /></a></p>
<h3>Ukázka práce s iBatis</h3>
<p>V následujícíh odstavcích bych krátce ukázal, jak se s iBatis pracuje.</p>
<h4>Konfigurace</h4>
<p>Začneme konfigurací. Ve verzi 2.x musíme dodat vždy dva typy konfiguračních souborů:</p>
<h5>SqlMapConfig.xml</h5>
<p>[source lang="xml"]<br />
<?xml version="1.0" encoding="UTF-8" ?><br />
<!DOCTYPE sqlMapConfig<br />
    PUBLIC "-//ibatis.apache.org//DTD SQL Map Config 2.0//EN"<br />
    "http://ibatis.apache.org/dtd/sql-map-config-2.dtd"></p>
<p><sqlMapConfig></p>
<p>  <!-- Konfigurace transakčního manažeru, pokud jste v prostředí<br />
        aplikačního serveru, je vhodnější použít jeho transakční<br />
        manažer a managovaný datasource (tedy vytáhnout je z<br />
        JNDI) --><br />
  <!-- tuto část při použití Springu vynecháváte, jelikož ji máte<br />
         již zkonfigurovanou ve springových konfigurácích --></p>
<transactionManager type="JDBC" commitRequired="false">
    <dataSource type="SIMPLE"></p>
<property name="JDBC.Driver" value="org.hsqldb.jdbcDriver"/>
<property name="JDBC.ConnectionURL" value="jdbc:hsqldb:."/>
<property name="JDBC.Username" value="sa"/>
<property name="JDBC.Password" value="sa"/>
    </dataSource><br />
  </transactionManager>
<p>  <!-- Souhrnná konfigurace frameworku - zde je možno<br />
         konfigurovat i základní údaje cache - např. pro vývoj<br />
         cache jednoduše hromadně vypnout, pro runtime<br />
         naopak nahodit --><br />
  <settings<br />
      cacheModelsEnabled="true"<br />
      enhancementEnabled="true"<br />
      lazyLoadingEnabled="true"<br />
      /></p>
<p>  <!-- Seznam SqlMap konfigurací - nahrávají se z classpath a v<br />
         našem případě se nacházejí v package<br />
         com.mydomain.data... --><br />
  <sqlMap resource="com/mydomain/data/Account.xml"/><br />
  <sqlMap resource="com/mydomain/data/Order.xml"/><br />
  <sqlMap resource="com/mydomain/data/Documents.xml"/></p>
<p></sqlMapConfig><br />
[/source]</p>
<h5>a vlastní SqlMap.xml - v našem případě třebas Account.xml</h5>
<p>[source lang="xml"]<br />
<?xml version="1.0" encoding="UTF-8" ?><br />
<!DOCTYPE sqlMap<br />
    PUBLIC "-//ibatis.apache.org//DTD SQL Map 2.0//EN"<br />
    "http://ibatis.apache.org/dtd/sql-map-2.dtd"><br />
<sqlMap namespace="Account"></p>
<p>  <!--<br />
  Použijeme type alias, abychom nemuseli neustále vypisovat celý<br />
  název třídy.<br />
  --><br />
  <typeAlias alias="Account" type="com.mydomain.domain.Account"/></p>
<p>  <!--<br />
  Result mapa popisuje mapování mezi sloupci vrácenými v dotazu<br />
  a property java beany. Tato deklarace není nutná v případě, že<br />
  názvy sloupců sedí na názvy property dané beany (kdo zná<br />
  autowire ze Springu, je mu jasno)<br />
  --><br />
  <resultMap id="AccountResult" class="Account"><br />
    <result property="id" column="ACC_ID"/><br />
    <result property="firstName" column="ACC_FIRST_NAME"/><br />
    <result property="lastName" column="ACC_LAST_NAME"/><br />
    <result property="emailAddress" column="ACC_EMAIL"/><br />
  </resultMap></p>
<p>  <!--<br />
  Select bez parametrů využívá deklaraci result mapy pro Account<br />
  třídu.<br />
  --></p>
<select id="selectAllAccounts" resultMap="AccountResult">
    select * from ACCOUNT<br />
  </select>
<p>  <!--<br />
  Jednoduší příklad selectu, kde se obejdeme bez result mapy.<br />
  Všimněte si že názvy sloupců odpovídají názvům property v<br />
  beaně. Další novinkou je použití vstupního parametru typu<br />
  java.lang.Integer (většina základích typů má již předvytvořené<br />
  type aliasy, takže místo java.lang.Integer nám stačí "int")<br />
  - v dotazu nám stačí použít #id#.<br />
  --></p>
<select id="selectAccountById" parameterClass="int"<br />
    resultClass="Account"><br />
    select<br />
      ACC_ID as id,<br />
      ACC_FIRST_NAME as firstName,<br />
      ACC_LAST_NAME as lastName,<br />
      ACC_EMAIL as emailAddress<br />
    from ACCOUNT<br />
    where ACC_ID = #id#<br />
  </select>
<p>  <!--<br />
  A teď si ukážeme něco z dynamických selectů.<br />
  Chceme vyselektovat account podle:<br />
    1) jména nebo příjmení<br />
    2) emailové adresy<br />
    3) konkrétního id.<br />
  --></p>
<select id="dynamicGetAccountList" resultMap="Account">
    select * from ACCOUNT<br />
    <dynamic prepend="WHERE"><br />
      <isNotNull prepend="AND" property="firstName"<br />
          open="(" close=")"><br />
          ACC_FIRST_NAME = #firstName#<br />
        <isNotNull prepend="OR" property="lastName"><br />
          ACC_LAST_NAME = #lastName#<br />
        </isNotNull><br />
      </isNotNull><br />
      <isNotNull prepend="AND" property="emailAddress"><br />
        ACC_EMAIL like #emailAddress#<br />
      </isNotNull><br />
      <isGreaterThan prepend="AND" property="id" compareValue="0"><br />
        ACC_ID = #id#<br />
      </isGreaterThan><br />
    </dynamic><br />
    order by ACC_LAST_NAME<br />
  </select>
<p>  <!--<br />
  Ukázka INSERT statementu. Vstupním parametrem je pro nás<br />
  třída Account. Pro vložení hodno nám slouží výrazy<br />
  #nazevProperty#.<br />
  V našem příkladě vkládáme i ID, pokud bychom ale chtěli<br />
  vrátit automaticky generované id databází, vložili bychom<br />
  deklaraci selectKey:</p>
<selectKey resultClass="int" >
     kde například pro Oracle by se uvedlo<br />
     SELECT "nazevSekvence".NEXTVAL AS ID FROM DUAL<br />
     pro MSSQL<br />
     SELECT @@IDENTITY AS ID<br />
     atd.<br />
  </selectKey>
  --><br />
  <insert id="insertAccount" parameterClass="Account"><br />
    insert into ACCOUNT (<br />
      ACC_ID,<br />
      ACC_FIRST_NAME,<br />
      ACC_LAST_NAME,<br />
      ACC_EMAIL<br />
    values (<br />
      #id#, #firstName#, #lastName#, #emailAddress#<br />
    )<br />
  </insert></p>
<p>  <!--<br />
  Příklad update - nijak se neodlišuje od příkladu s INSERTEM.<br />
  --><br />
  <update id="updateAccount" parameterClass="Account"><br />
    update ACCOUNT set<br />
      ACC_FIRST_NAME = #firstName#,<br />
      ACC_LAST_NAME = #lastName#,<br />
      ACC_EMAIL = #emailAddress#<br />
    where<br />
      ACC_ID = #id#<br />
  </update></p>
<p>  <!--<br />
  A příklad delete - vstupním parametrem je pouze int s id<br />
  záznamu.<br />
  --><br />
  <delete id="deleteAccountById" parameterClass="int"><br />
    delete from ACCOUNT where ACC_ID = #id#<br />
  </delete></p>
<p></sqlMap><br />
[/source]</p>
<p>A to je vše. Tím máme zkonfigurováno. Již z tohoto příkladu si můžete udělat obrázek, že iBatis neprovádí žádnou náročnou magii jako například Hibernate nebo TopLink. Vše je až neuvěřitelně průhledné, jednoduché a tím pádem minimálně náchylné k chybám.</p>
<h4>DAO - Třída</h4>
<p>Nuže a nyní si ukážeme příklad DAO třídy. Bude to také krátké a průrazné. Navíc od verze 3.0 by nám měla stačit už pouze deklarace interface ... o vlastní implementaci by se iBatis postaral sám.</p>
<h5>AccountDao.java</h5>
<p>[source lang="java"]<br />
package com.mydomain.data;</p>
<p>import com.ibatis.sqlmap.client.SqlMapClient;<br />
import com.ibatis.sqlmap.client.SqlMapClientBuilder;<br />
import com.ibatis.common.resources.Resources;<br />
import com.mydomain.domain.Account;</p>
<p>import java.io.Reader;<br />
import java.io.IOException;<br />
import java.util.List;<br />
import java.sql.SQLException;</p>
<p>/**<br />
 * Vzato z jednoduchécho příkladu přikládaného k iBatis.<br />
 * Pozor toto neberte jako příklad BEST PRACTISES a radši jukněte<br />
 * na příklad JPetStore 5.0 na http://www.ibatis.com<br />
 *<br />
 * V případě integrace se Spring bude vše ještě jednodušší.<br />
 * Stačí pouze podědit z SqlMapClientDaoSupport a o inicializaci<br />
 * máme postaráno.<br />
 */<br />
public class SimpleExample {</p>
<p>  /**<br />
   * Instance SqlMapClient instances jsou thread safe,<br />
   * takže nám stačí pouze jedna. V našem příkladě použijeme<br />
   * singleton.<br />
   */<br />
  private static SqlMapClient sqlMapper;</p>
<p>  /**<br />
   * Opět toto není ideální způsob inicializace, ale pro účely<br />
   * jednoduchého příkladu nám to stačí.<br />
   *<br />
   * Opět v případě použití Springu, tady nemusíme nic dělat.<br />
   * V kódu by nám pak stačilo vždy jen zavolat metodu<br />
   * getSqlMapClientTemplate().<br />
   */<br />
  static {<br />
    try {<br />
      //načtem konfiguraci<br />
      Reader reader = Resources<br />
           .getResourceAsReader("com/mydomain/data/SqlMapConfig.xml");<br />
      //vytvoříme klienta na kterém budeme volat jednotlivé příkazy<br />
      sqlMapper = SqlMapClientBuilder.buildSqlMapClient(reader);<br />
      reader.close();<br />
    } catch (IOException e) {<br />
      // Fail fast.<br />
      throw new RuntimeException(<br />
           "Something bad happened while building the SqlMapClient" +<br />
           " instance." + e, e);<br />
    }<br />
  }</p>
<p>  public static List selectAllAccounts () throws SQLException {<br />
    return sqlMapper.queryForList("selectAllAccounts");<br />
  }</p>
<p>  public static Account selectAccountById  (int id) throws SQLException {<br />
    return (Account) sqlMapper.queryForObject("selectAccountById", id);<br />
  }</p>
<p>  public static void insertAccount (Account account) throws SQLException {<br />
    sqlMapper.insert("insertAccount", account);<br />
  }</p>
<p>  public static void updateAccount (Account account) throws SQLException {<br />
    sqlMapper.update("updateAccount", account);<br />
  }</p>
<p>  public static void deleteAccount (int id) throws SQLException {<br />
    sqlMapper.delete("deleteAccount", id);<br />
  }</p>
<p>}<br />
[/source]</p>
<p>Tím je hotové i DAO a skončili jsme. Další nespornou výhodou je, že o logování se vám postará iBatis, takže když je potřeba, v lozích detailně vidíte, co se vám vlastně na datové vrstvě děje.</p>
<h3>Skvělá dokumentace</h3>
<p>Pro rychlou learning curve je dobrá dokumentace nezbytným základem. V tohle ohledu je iBatis řekl bych opravdu na špičce. Doporučuji si udělat rychlý přehled o použití frameworku na:</p>
<ol>
<li>SimpleExample aplikaci (která je součásti bundle iBatis a částečně jsem ji využil i v uvedených příkladech) - na čtyřech třídách si rychle uděláte přehled</li>
<li>pokračovat krátkým <a href="http://ibatis.apache.org/docs/java/pdf/iBATIS-SqlMaps-2-Tutorial_en.pdf" target="_new">tutorialem</a>, který vás rychle nakopne ... a v podstatě už můžete začít programovat</li>
<li>prostudovat komplexnější JPetStore aplikaci, kde jsou ukázané trochu pokročilejší fíčury spolu s <a href="http://ibatis.apache.org/docs/java/pdf/iBATIS-SqlMaps-2_en.pdf" target="_new">Developer dokumentací</a> - tam je přehledně vše důležité</li>
<li>když nakouknete do zdrojových kódů, lehce zjistíte, že nejsou nijak rozsáhlé, jsou také dobře zdokumentované a přehledné</li>
</ol>
<h3>iBatis vs. JDBC4</h3>
<p>V diskusích se párkrát objevil názor, zda má iBatis po zavedení JDBC stále smysl. Existují různé názory, ale pro iBatis mluví stále pár argumentů:</p>
<ul>
<li>JDBC 4.0 je Java 1.6+ / iBatis je 1.4+ (do verze 2.20 1.3+)</li>
<li>iBatis je tu a umí pracovat i s drivery verze 3.0 a 2.0 (dvojkové JDBC bude ale od určité verze deprecated ... možná už od 2.20, podobně jako JDK 1.3) - většina velkých vendorů ještě JDBC 4.0 drivery ještě ani nemají, nebo mohou podporovat jen nové verze databází (např. Oracle od 11g, která je teprve beta ...)</li>
<li>iBatis je odladěný a vychytaný, s novými JDBC 4.0 drivery nám každý vendor přinese svou snůšku bugů, které jim postupně společně teprve vyladíme</li>
<li>iBatis má možnosti dynamických SQL dotazů, extenzí a includů, které JDBC 4.0 nepodporuje</li>
<li>JDBC 4.0 je zafixované a nebude se rozhodně dynamicky rozvíjet tak jako může iBatis, který s sebou netáhne takovou "mrtvou váhu"</li>
<li>JDBC 4.0 je možné konfigurovat s pomocí anotací (což je poměrně sympatická vlastnost) - iBatis prozatím nikoliv, ale podpora anotací je již v <a href="http://opensource.atlassian.com/confluence/oss/display/IBATIS/iBATIS+3.0+Whiteboard" target="_new">roadmap pro verzi 3.0</a> spolu s dalšími velmi sympatickými fíčurkami, jako např:
<ul>
<li>Interface binding - pro napsání DAO nám bude stačit deklarace interface, o implementaci se postará iBatis sám</li>
<li>Anotace</li>
<li>Konfigurace konvencí - tak tohle bude asi největší masáž a částečné odchýlení od principů, které jsem uvedl na začátku; v podstatě se jedná o to, že by iBatis sám dokázal vygenerovat jednoduché SQL dotazy pro základní sadu jednoduchých SQL příkazů (jako jsou např. insert / update / delete + jednoduchý select) pouze na základě deklarace metody v interface; okolo tohoto bodu se ale ještě vedou další debaty</li>
<li>Více úrovňová konfigurace - vzestupně podle priority konvence, anotace (může předefinovat konvenci), XML (může předefinovat konvenci a anotace) a java kód (může předefinovat cokoliv)</li>
</ul>
</li>
</ul>
<p>Odkazy na primární zdroje (kdybych náhodou něco interpretoval špatně ;)):</p>
<ul>
<li><a href="http://www.mail-archive.com/dev@ibatis.apache.org/msg01646.html" target="_new">mail konference dev@ibatis.apache.org</a></li>
<li><a href="http://www.jroller.com/page/alexRuiz?entry=ibatis_sql_mapping_jdbc_4" target="_new">Alex Ruiz blog</a></li>
<li><a href="http://weblogs.java.net/blog/forax/archive/2006/08/create_or_drop.html" target="_new">a toto je spíš už jen o způsobu práce s JDBC 4.0</a></li>
</ul>
<h3>iBatis DAO</h3>
<p>To co jsem doposud popisoval byly iBatis SqlMaps. Z rodiny iBatis pochází ještě jedna "utilitka" nazvaná iBatis DAO, jejímž cílem je stadnardní cestou programátorovi zpřístupnit práci s transakcemi. iBatis SqlMaps a DAO jsou dvě nezávislé knihovny, které lze použít i  samostatně. Já například používám jen SqlMaps knihovnu, jelikož o transakce a práci s connection se mi stará Spring.</p>
<p>Pro ty, kteří Spring nepoužívají se možná iBatis DAO bude hodit. Umožňuje vám zkonfigurovat přípojení k databázi (simple JDBC, DBCP, JNDI), transakčního manažera a na úrovni kódu vám poskytuje zástupné třídy pro práci s transakcemi. Transakční manažeři jsou pluggovatelní a v současné době si můžete vybrat mezi JDBC, JTA, SqlMap, Hibernate a external transakčním manažerem.</p>
<p>Pro vlastní dao třídy existují Template třídy frameworku, které vám zpřístupňují takové ty metody jako getConnection() (JDBC, JNDI), getSession() (Hibernate) nebo getSqlMapExecutor() (SqlMaps) - podobně jako v případě Springu.</p>
<p>Myslím, si že z tohoto krátkého odstavečku jste asi nemohli pochopit, co přesně iBatis DAO dělá, a proto bych vás rád odkázal na <a href="http://ibatis.apache.org/docs/java/pdf/iBATIS-DAO-2_en.pdf" target="_new">kraťoučkou dokumentaci</a>, která veškerou práci s knihovnou přehledně popisuje.</p>
<h3>Závěrem</h3>
<p>Vřele doporučuji na iBatis kouknout i v případě, že používáte Hibernate, TopLink nebo jiné ORM. Opakuji to tu alespoň po páté, ale budete překvapeni jednoduchostí, průhledností a bezproblémovostí iBatisu. Programátoři s velkou zkušeností s Hibernate pravděpodobně nepřejdou - Hibernate je opravdu mocnější nástroj, ale má řadu úskalí, o které si člověk může ošklivě nabít. Pro programátory začátečníky doporučuji místo JPA / Hibernate / Toplink, začít nejdříve na iBatisu. Ušetří vám opravdu velké množství práce, nebudete muset do něj pronikat nijak dlouho, nenachytá vás do žádné pasti a odmění se vám bezproblémovou službou.</p>
