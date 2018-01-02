---
status: publish
published: true
title: iBatis 3.0 preview - část první
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Po letech jsme se konečně dočkali třetí verze populární knihovny iBatis.
  Nová verze přináší velkou řadu novinek a jedná se o kompletní rewrite, který využívá
  generik, anotací a dalšího API Javy 1.5. iBatis je prozatím ve verzi Beta 1 (doposud
  ještě není dostupný ani v Maven repository), ale doufejme že nebude dlouho trvat
  a dočkáme se verze stabilní. \r\n\r\nSpolečně s iBatisem vychází i úplně nový produkt
  iBATIS Schema Migration System inspirovaný Rails Migrations. Migrations představují
  podporu pro konzistentní úpravy databázových schémat s důrazem na: konzistenci,
  opakovatelnost, reverzibilnost, verzování, auditovatelnost a automatizaci. Jedná
  se o nástroj pro příkazovou řádku, s jehož pomocí je možné systémově vytvářet a
  spravovat databázové change skripty, které jsou přehledné, dají se kdykoliv revertovat
  a měly by výrazně ulehčit práci v týmu (pro čtenáře z Forresta: pokud vám to připomíná
  náš DbAutoupdater, jste doma :-) ).\r\n\r\nV této sérii článků se ale soustřeďme
  na iBatis 3.0 a co nového nás v něm čeká. Sérii zmiňuji pro to, že novinek je příliš
  mnoho na to, aby se vešly do jediného článku a proto jsem jej rozdělil na dvě části,
  které vyjdou s týdenním postupem. Těšte se tedy ještě na jeden článek příští pondělí.\r\n\r\n"
wordpress_id: 595
wordpress_url: http://blog.novoj.net/?p=595
date: '2009-08-16 11:22:27 +0200'
date_gmt: '2009-08-16 10:22:27 +0200'
categories:
- Programování
- Java
- iBatis
tags: []
comments: []
---
<p>Po letech jsme se konečně dočkali třetí verze populární knihovny iBatis. Nová verze přináší velkou řadu novinek a jedná se o kompletní rewrite, který využívá generik, anotací a dalšího API Javy 1.5. iBatis je prozatím ve verzi Beta 1 (doposud ještě není dostupný ani v Maven repository), ale doufejme že nebude dlouho trvat a dočkáme se verze stabilní. </p>
<p>Společně s iBatisem vychází i úplně nový produkt iBATIS Schema Migration System inspirovaný Rails Migrations. Migrations představují podporu pro konzistentní úpravy databázových schémat s důrazem na: konzistenci, opakovatelnost, reverzibilnost, verzování, auditovatelnost a automatizaci. Jedná se o nástroj pro příkazovou řádku, s jehož pomocí je možné systémově vytvářet a spravovat databázové change skripty, které jsou přehledné, dají se kdykoliv revertovat a měly by výrazně ulehčit práci v týmu (pro čtenáře z Forresta: pokud vám to připomíná náš DbAutoupdater, jste doma :-) ).</p>
<p>V této sérii článků se ale soustřeďme na iBatis 3.0 a co nového nás v něm čeká. Sérii zmiňuji pro to, že novinek je příliš mnoho na to, aby se vešly do jediného článku a proto jsem jej rozdělil na dvě části, které vyjdou s týdenním postupem. Těšte se tedy ještě na jeden článek příští pondělí.</p>
<p><a id="more"></a><a id="more-595"></a></p>
<p><strong>Obsah</strong></p>
<ol>
<li><a href="#environment">Rozlišení konfigurace pro typizovaná prostředí</a></li>
<li><a href="#immutable">Podpora immutable objektů (podpora předávání dat do konstruktorů POJO)</a></li>
<li>
      <a href="#onetoone">Práce s tabulkami ve vztahu 1:1</a></p>
<ol>
<li><a href="#onetooneselect">Vnořený select</a></li>
<li><a href="#onetoonemap">Vnořený výsledek (join)</a></li>
</ol>
</li>
<li>
      <a href="#onetomany">Práce s tabulkami ve vztahu 1:N</a></p>
<ol>
<li><a href="#onetomanyselect">Vnořený select</a></li>
<li><a href="#onetomanymap">Vnořený výsledek (join)</a></li>
</ol>
</li>
<li><a href="#compositekey">Kompozitní klíče</a></li>
<li><a href="#discriminator">Oficiální podpora diskriminátoru</a></li>
<li><a href="#ognl">OGNL EL v dynamických SQL dotazech</a></li>
<li><a href="#ending">Závěrem</a></li>
</ol>
<style>h5 { font-size: 1em; font-weight: strong; font-style: italic; text-decoration: underline; }</style>
<p>Abychom nezačínali hned tak zhurta, podívejme se na změny v XML konfiguraci, která byla dosud jediným prostředkem jak s iBatisem pracovat. Kdo již máte s iBatisem nějaké zkušenosti nemusíte mít žádné obavy, protože se jedná pouze o výrazné zjednodušení.</p>
<h3><a name="environment">Rozlišení konfigurace pro typizovaná prostředí</a></h3>
<p>V iBatisu se poprvé objevuje podpora rozlišení různých běhových prostředí (jedná se o stejný princip, který jsem popisoval v článku <a href="http://blog.novoj.net/2009/08/07/odlisujete-v-aplikaci-vyvojove-testovaci-a-produkcni-prostredi/">Odlišujete v aplikaci vývojové, testovací a produkční prostředí?</a>). V základním konfiguračním souboru SqlMapConfig.xml je možné definovat:</p>
<p>[source lang="xml"]<br />
<environments default="production"><br />
    <environment id="development"></p>
<transactionManager type="JDBC">
<property name="" value=""/>
        </transactionManager>
        <dataSource type="UNPOOLED"></p>
<property name="driver" value="${driver}"/>
<property name="url" value="${url}"/>
<property name="username" value="${username}"/>
<property name="password" value="${password}"/>
        </dataSource><br />
    </environment><br />
    <environment id="production"></p>
<transactionManager type="MANAGED">
<property name="" value=""/>
        </transactionManager>
        <dataSource type="POOLED"></p>
<property name="driver" value="${driver}"/>
<property name="url" value="${url}"/>
<property name="username" value="${username}"/>
<property name="password" value="${password}"/>
<property name="poolMaximumActiveConnections" value="20"/>
<property name="poolMaximumIdleConnections" value="5"/>
        </dataSource><br />
    </environment><br />
</environments><br />
[/source]</p>
<p>S tím, že výběr běhové prostředí se definuje při vytváření SqlSessionFactory:</p>
<p>[source lang="java"]<br />
//tímto voláním vytvoříme factory pro defaultní prostředí, což je "production"<br />
SqlSessionFactory factory = sqlSessionFactoryBuilder.build(reader);<br />
SqlSessionFactory factory = sqlSessionFactoryBuilder.build(reader,properties);<br />
//výběr development prostředí<br />
SqlSessionFactory factory = sqlSessionFactoryBuilder.build(reader, "development");<br />
//nebo<br />
SqlSessionFactory factory = sqlSessionFactoryBuilder.build(reader, "development",properties);<br />
[/source]</p>
<h3><a name="immutable">Podpora immutable objektů (podpora předávání dat do konstruktorů POJO)</a></h3>
<p>První změnou je možnost používat pro vytvářené intance POJO tříd parametrické konstruktory. Tím se nám otevírá možnost definovat POJO jako immutable objekty, které mají daleko lepší použitelnost v paralelním programování.</p>
<p>[source lang="xml"]<br />
<resultMap id="selectImmutableAuthor" type="domain.blog.ImmutableAuthor"><br />
    <constructor><br />
        <idArg column="id" javaType="int"/><br />
        <arg column="username" javaType="string"/><br />
        <arg column="password" javaType="string"/><br />
        <arg column="email" javaType="string"/><br />
        <arg column="bio" javaType="string"/><br />
        <arg column="favourite_section" javaType="domain.blog.Section"/><br />
    </constructor><br />
</resultMap><br />
[/source]</p>
<p>Při definici argumentů ZÁLEŽÍ na pořadí a správném typu, protože Java dosud buhužel v reflexi neumožňuje přístup k názvům argumentů konstruktorů. Rozlišení primárního klíče (idArg element, popřípadě id element pro standardní bean property) není povinné nicméně mělo by výrazně napomáhat výkonnosti iBatisu. Dokumentace tento rozdíl popisuje takto:</p>
<p><cite>The only difference between the two is that id will flag the result as an identifier property to be used when comparing object instances. This helps to improve general performance, but especially performance of caching and nested result mapping (i.e. join mapping).</cite></p>
<p>Další novinkou, která myslím dříve nebyla možná je použití privátních property Java Beany, nicméně to je praktika více než diskutabilní, pokud můžeme využít konstruktorů tříd.</p>
<h3><a  name="onetoone">Práce s tabulkami ve vztahu 1:1</a></h3>
<p>V tomto ohledu došlo řekl bych k mírnému pokroku v mezích zákona - jedná se pouze o vylepšení zápisu, které vede k výraznému vylepšení výsledné čitelnosti a použitelnosti. Srovnejme si původní a nové zápisy asociací 1:0..1 mezi objekty:</p>
<h4><a  name="onetooneselect">Vnořený select</a></h4>
<p>Tady ještě rozdíly v zápisu nejsou tak drastické - je potřeba jen jediná definice ResultMapy navíc pro iBatis 2.X:</p>
<p><i>iBatis 2.x</i></p>
<p>[source lang="xml"]<br />
<resultMap id="blogResult" class="Blog"><br />
    <result property="author" column="blog_author_id"<br />
                 resultMap="Author" select="selectAuthor"/><br />
</resultMap></p>
<p><resultMap id="authorResult" class="Author"/></p>
<select id="selectBlog" parameterClass="int" resultMap="blogResult">
    SELECT * FROM BLOG WHERE ID = #value#<br />
</select>
<select id="selectAuthor" parameterClass="int" resultMap="authorResult">
    SELECT * FROM AUTHOR WHERE ID = #value#<br />
</select>
<p>[/source]</p>
<p><i>iBatis 3.x</i></p>
<p>[source lang="xml"]<br />
<resultMap id="blogResult" type="Blog"><br />
    <association property="author" column="blog_author_id"<br />
                 javaType="Author" select="selectAuthor"/><br />
</resultMap></p>
<select id="selectBlog" parameterType="int" resultMap="blogResult">
    SELECT * FROM BLOG WHERE ID = #{id}<br />
</select>
<select id="selectAuthor" parameterType="int" resultType="Author">
    SELECT * FROM AUTHOR WHERE ID = #{id}<br />
</select>
<p>[/source]</p>
<h4><a  name="onetoonemap">Vnořený výsledek (join)</a></h4>
<p>Ovšem tady už začíná být úspora a čitelnost znát:</p>
<p><i>iBatis 2.x</i></p>
<p>[source lang="xml"]<br />
<resultMap id="blogResult" class="Blog"><br />
    <result property="blog_id" column="id"/><br />
    <result property="title" column="blog_title"/><br />
    <result property="author" column="blog_author_id" resultMap="authorResult"/><br />
</resultMap></p>
<p><resultMap id="authorResult" class="Author"><br />
    <result property="id" column="author_id"/><br />
    <result property="username" column="author_username"/><br />
    <result property="password" column="author_password"/><br />
    <result property="email" column="author_email"/><br />
    <result property="bio" column="author_bio"/><br />
</resultMap></p>
<select id="selectBlog" parameterClass="int" resultMap="blogResult">
    select<br />
    B.id as blog_id,<br />
    B.title as blog_title,<br />
    B.author_id as blog_author_id,<br />
    A.id as author_id,<br />
    A.username as author_username,<br />
    A.password as author_password,<br />
    A.email as author_email,<br />
    A.bio as author_bio<br />
    from Blog B<br />
    left outer join Author A on B.author_id = A.id<br />
    where B.id = #{id}<br />
</select>
<p>[/source]</p>
<p><i>iBatis 3.x</i></p>
<p>[source lang="xml"]<br />
<resultMap id="blogResult" type="Blog"><br />
    <id property="blog_id" column="id"/><br />
    <result property="title" column="blog_title"/><br />
    <association property="author" column="blog_author_id" javaType="Author"><br />
        <id property="id" column="author_id"/><br />
        <result property="username" column="author_username"/><br />
        <result property="password" column="author_password"/><br />
        <result property="email" column="author_email"/><br />
        <result property="bio" column="author_bio"/><br />
    </association><br />
</resultMap></p>
<select id="selectBlog" parameterType="int" resultMap="blogResult">
    select<br />
        B.id as blog_id,<br />
        B.title as blog_title,<br />
        B.author_id as blog_author_id,<br />
        A.id as author_id,<br />
        A.username as author_username,<br />
        A.password as author_password,<br />
        A.email as author_email,<br />
        A.bio as author_bio<br />
    from Blog B<br />
    left outer join Author A on B.author_id = A.id<br />
    where B.id = #{id}<br />
</select>
<p>[/source]</p>
<p>Vytvoření nového klíčového slova <strong>association</strong> vylepšuje čitenost v tom, že člověk okamžitě ví bez většího studia konfigurace, že se jedná o multiplicitu 1:0..1. Dále poměrně dost vypomůže inlinování definice mapy do jiné mapy. V iBatis 2.X bylo nutné vždy result mapy definovat samostatně a provazovat je přes id (tato možnost je stále zachována, ale vyplatí se vám pouze v případě reusu mapování).</p>
<h3><a name="onetomany">Práce s tabulkami ve vztahu 1:N</a></h3>
<p>V tomto ohledu je už vyčištění zápisu poměrně drastičtější. Srovnejme si původní a nové zápisy asociací 1:0..* mezi objekty:</p>
<h4><a  name="onetomanyselect">Vnořený select</a></h4>
<p><i>iBatis 2.x</i></p>
<p>[source lang="xml"]<br />
<resultMap id="blogResult" class="Blog"><br />
    <result property="posts" javaType="ArrayList" column="blog_id"<br />
                resultMap="postResult" select="selectPostsForBlog"/><br />
</resultMap></p>
<p><resultMap id="postResult" class="Post"/></p>
<select id="selectBlog" parameterClass="int" resultMap="blogResult">
    SELECT * FROM BLOG WHERE ID = #value#<br />
</select>
<select id="selectPostsForBlog" parameterClass="int" resultMap="postResult">
    SELECT * FROM POST WHERE BLOG_ID = #value#<br />
</select>
<p>[/source]</p>
<p><i>iBatis 3.x</i></p>
<p>[source lang="xml"]<br />
<resultMap id="blogResult" type="Blog"></p>
<collection property="posts" javaType="ArrayList" column="blog_id"<br />
                ofType="Post" select="selectPostsForBlog"/><br />
</resultMap></p>
<select id="selectBlog" parameterType="int" resultMap="blogResult">
    SELECT * FROM BLOG WHERE ID = #{id}<br />
</select>
<select id="selectPostsForBlog" parameterType="int" resultType="Author">
    SELECT * FROM POST WHERE BLOG_ID = #{id}<br />
</select>
<p>[/source]</p>
<p>V zápisu pro iBatis 2.x byl zápis shodný jako pro vztah 1:0..1 -  v třetí verzi iBatisu je multiplicita vztahu patrná na první pohled. Navíc opět nepotřebujeme dvojí deklaraci result map - vše je hezky čitelné jediném zápise.</p>
<h4><a  name="onetomanymap">Vnořený výsledek (join)</a></h4>
<p><i>iBatis 2.x</i></p>
<p>[source lang="xml"]<br />
<resultMap id="blogResult" class="Blog" groupBy="id"><br />
    <result property="id" column="blog_id"/><br />
    <result property="title" column="blog_title"/><br />
    <result property="posts" column="post_id" resultMap="postResult"/><br />
</resultMap></p>
<p><resultMap id="postResult" class="Post"><br />
    <result property="id" column="post_id"/><br />
    <result property="subject" column="post_subject"/><br />
    <result property="body" column="post_body"/><br />
</resultMap></p>
<select id="selectBlog" parameterClass="int" resultMap="blogResult">
    select<br />
        B.id as blog_id,<br />
        B.title as blog_title,<br />
        B.author_id as blog_author_id,<br />
        P.id as post_id,<br />
        P.subject as post_subject,<br />
        P.body as post_body<br />
    from Blog B<br />
    left outer join Post P on B.id = P.blog_id<br />
    where B.id = #value#<br />
</select>
<p>[/source]</p>
<p><i>iBatis 3.x</i></p>
<p>[source lang="xml"]<br />
<resultMap id="blogResult" type="Blog"><br />
    <id property="id" column="blog_id" /><br />
    <result property="title" column="blog_title"/></p>
<collection property="posts" ofType="Post">
        <id property="id" column="post_id"/><br />
        <result property="subject" column="post_subject"/><br />
        <result property="body" column="post_body"/><br />
    </collection>
</resultMap></p>
<select id="selectBlog" parameterType="int" resultMap="blogResult">
    select<br />
        B.id as blog_id,<br />
        B.title as blog_title,<br />
        B.author_id as blog_author_id,<br />
        P.id as post_id,<br />
        P.subject as post_subject,<br />
        P.body as post_body<br />
    from Blog B<br />
    left outer join Post P on B.id = P.blog_id<br />
    where B.id = #{id}<br />
</select>
<p>[/source]</p>
<p>Myslím si, že v tomto případě zlepšení čitelnosti zápisu není třeba obhajovat.</p>
<h3><a  name="compositekey">Kompozitní klíče</a></h3>
<p>Nově jsou ve vnořených selectech podporovány i kompozitní klíče. Stačí nám k tomu poměrně intuitivní zápis:</p>
<p>[source lang="xml"]<br />
<resultMap id="blogResult" type="Blog"></p>
<collection property="posts" javaType="ArrayList" column="{id=blog_id,section=blog_section}"<br />
                ofType="Post" select="selectPostsForBlog"/><br />
</resultMap></p>
<select id="selectBlog" parameterType="int" resultMap="blogResult">
    SELECT * FROM BLOG WHERE ID = #{id}<br />
</select>
<select id="selectPostsForBlog" parameterType="int" resultType="Author">
    SELECT * FROM POST WHERE BLOG_ID = #{id} AND BLOG_SECTION = #{section}<br />
</select>
<p>[/source]</p>
<h3><a  name="discriminator">Oficiální podpora diskriminátoru</a></h3>
<p>Již v přechozí verzi existovala nezdokumentovaná podpora diskriminátoru - nyní se tato vlastnost stala zdokumentovanou. Diskriminátor vám umožňuje na základu hodnoty sloupce odlišit typ výsledného objektu. Např. podle hodnoty sloupce "vehicle_type" je možné vytvořit buď instanci java třídy cz.example.Car, cz.example.Van nebo cz.example.Truck. To umožňuje velmi pěkně využívat objektové dědičnosti:</p>
<p>[source lang="xml"]<br />
<resultMap id="vehicleResult" type="Vehicle"><br />
    <id property="id" column="id" /><br />
    <result property="vin" column="vin"/><br />
    <result property="year" column="year"/><br />
    <result property="model" column="model"/><br />
    <discriminator javaType="int" column="vehicle_type"><br />
        <case value="1" resultType="cz.example.Car"><br />
            <result property="doorCount" column="door_count" /><br />
        </case><br />
        <case value="2" resultType="cz.example.Truck"><br />
            <result property="maximumLoad" column="load" /><br />
        </case><br />
        <case value="3" resultType="cz.example.Van"><br />
            <result property="length" column="length" /><br />
            <result property="height" column="height" /><br />
            <result property="width" column="width" /><br />
        </case><br />
    </discriminator><br />
</resultMap><br />
[/source]</p>
<h3><a  name="ognl">OGNL EL v dynamických SQL dotazech</a></h3>
<p>Dynamické SQL doznalo velmi výrazných změn. Byla opuštěna cesta vlastních podmínkových elementů jako je známe z verze 2 (tj. &lt;isNotPropertyAvailable/&gt;, &lt;isNotNull/&gt; atd.) ve prospěch obecně použitelnějšího expression language. Volba padla na OGNL, které používá i řada dalších projektů jako např. Struts 2, Tapestry nebo Spring WebFlow. Z toho také vyplývá, že řada z vás již bude s tímto jazykem dobře obeznámena.</p>
<p>To umožnilo snížit počet potřebných podmínkových elementu na čtyři základní:</p>
<ul>
<li>if</li>
<li>choose (when, otherwise)</li>
<li>trim (where, set)</li>
<li>foreach</li>
</ul>
<p>Níže uvádím pár příkladů využití, které si myslím jsou v podstatě samopopisné:</p>
<p>[source lang="xml"]</p>
<select id="findActiveBlogLike"<br />
        parameterType="Blog" resultType="Blog"><br />
    SELECT * FROM BLOG WHERE state = ‘ACTIVE’<br />
    <if test="title != null"><br />
        AND title like ${title}<br />
    </if><br />
    <if test="author != null && author.name != null"><br />
        AND title like ${author.name}<br />
    </if><br />
</select>
<select id="findActiveBlogLike"<br />
        parameterType="Blog" resultType="Blog"><br />
    SELECT * FROM BLOG WHERE state = ‘ACTIVE’<br />
    <choose><br />
        <when test="title != null"><br />
            AND title like ${title}<br />
        </when><br />
        <when test="author != null && author.name != null"><br />
            AND title like ${author.name}<br />
        </when><br />
        <otherwise><br />
            AND featured = 1<br />
        </otherwise><br />
    </choose><br />
</select>
<select id="selectPostIn" resultType="domain.blog.Post">
    SELECT *<br />
    FROM POST P<br />
    WHERE ID in<br />
    <foreach item="item" index="index" collection="list"<br />
             open="(" separator="," close=")"><br />
        #{item}<br />
    </foreach><br />
</select>
<p>[/source]</p>
<p>Situace je trošičku složitější s Trim elementem. Ten nám umožňuje řešit situace, kdy by mohlo zapodmínkováním částí dotazu dojít k vytvoření nevalidního SQL statementu. Typický příklad:</p>
<p>[source lang="xml"]</p>
<select id="findActiveBlogLike"<br />
        parameterType="Blog" resultType="Blog"><br />
    SELECT * FROM BLOG WHERE<br />
    <if test="title != null"><br />
        AND title like ${title}<br />
    </if><br />
    <if test="author != null && author.name != null"><br />
        AND title like ${author.name}<br />
    </if><br />
</select>
<p>[/source]</p>
<p>Může na základě různých hodnot dojít k následujícím dvěma nevalidním variantám:</p>
<p>[source:sql]<br />
SELECT * FROM BLOG WHERE;<br />
SELECT * FROM BLOG WHERE AND title like ?;<br />
[/source]</p>
<p>Přesně tuto situaci nám umožňuje řešit TRIM element a jeho dvě varianty WHERE a SET -  které mají stejný význam, ale jsou optimalizované pro jednoduché použití. Výše uvedný příklad by se jednoduše řešil tímto zápisem:</p>
<p>[source lang="xml"]</p>
<select id="findActiveBlogLike"<br />
        parameterType="Blog" resultType="Blog"><br />
    SELECT * FROM BLOG<br />
    <where><br />
        <if test="title != null"><br />
            AND title like ${title}<br />
        </if><br />
        <if test="author != null && author.name != null"><br />
            AND title like ${author.name}<br />
        </if><br />
    </where><br />
</select>
<p>[/source]</p>
<p>Ten pro iBatis znamená, že použije klíčové SQL slovo WHERE pouze za přepokladu, že obsah tohoto elementu není prázdný (tj. alespoň jedna podmínka se vyhodnotila jako pravdivá). Navíc pokud tento obsah začíná klíčovými slovy AND nebo OR, dokáže iBatis toto slůvko odříznout. To elegantně a jednoduše řeší celý problém. WHERE je pouze optimalizovaná varianta TRIM - výše uvedenému zápisu odpovídá toto:</p>
<p>[source lang="xml"]</p>
<select id="findActiveBlogLike"<br />
        parameterType="Blog" resultType="Blog"><br />
    SELECT * FROM BLOG</p>
<trim prefix="WHERE" prefixOverrides="AND |OR ">
        <if test="title != null"><br />
            AND title like ${title}<br />
        </if><br />
        <if test="author != null && author.name != null"><br />
            AND title like ${author.name}<br />
        </if><br />
    </trim>
</select>
<p>[/source]</p>
<p>V atributech elementu TRIM říkáme iBatisu:</p>
<ul>
<li>pokud je vrácený obsah elementu neprázdný, prefixuj ho slovem WHERE</li>
<li>pokud vrácený obsah začíná na AND nebo OR odřízni tento začátek (pozn. mezera za těmito slovy je důležitá - iBatis obsah porovnává naprosto přesně)</li>
</ul>
<p>Vidíme tedy, že TRIM je víceúčelové slovo, které si můžeme přizpůsobit na míru svým potřebám, nicméně 90% případů by nám měly vyřešit předdefinované kombinace WHERE a SET.</p>
<h3><a  name="ending">Závěrem</a></h3>
<p>Tímto uzavíráme první díl preview iBatisu verze 3.0. V tom následujícím, který vyjde přesně za týden, si popíšeme novinky související s Java přístupem k iBatis dotazům, využitím anotací a generik.</p>
