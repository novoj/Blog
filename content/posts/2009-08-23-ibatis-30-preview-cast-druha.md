---
status: publish
published: true
title: iBatis 3.0 preview - část druhá
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "V <a href=\"http://blog.novoj.net/2009/08/16/ibatis-30-preview-cast-prvni/\">předchozím
  článku</a> jsme si ukázali vylepšení iBatisu v souvislosti s XML deklaracemi. Tento
  navazující článek rozebírá novinky v oblasti Java API. Základem pro toto rozšíření
  se staly vlastnosti dostupné od verze Javy 1.5 - tedy generiky a anotace. Jednou
  z velkých kritik původního iBatisu bylo množství XML, které bylo nutné psát. Našlo
  se mnoho lidí, kterým tento přístup vadil a kteří by spíše uvítali mít vše na jednom
  místě v kódu. Autoři tyto kritiky vyslyšeli a vytvořili plnohodnotné API, před které
  je možné využít libovolnou funkcionalitu iBatisu.\r\n\r\nPřed tím, než se pustím
  do rozebírání detailů bych se s Vámi rád podělil o jeden velmi zajímavý úryvek z
  dokumentace, který má s výše uvedeným souvislost:\r\n\r\n<cite>Java Annotations
  are unfortunately limited in their expressiveness and flexibility. Despite a lot
  of time spent in investigation, design and trials, the most powerful iBATIS mappings
  simply cannot be built with Annotations – without getting ridiculous that is. C#
  Attributes (for example) do not suffer from these limitations, and thus iBATIS.NET
  will enjoy a much richer alternative to XML. That said, the Java Annotation based
  configuration is not without its benefits.</cite>\r\n\r\nZdá se mi to jen nebo se
  povzdechy nad rigiditou Javy stávají normálním trendem?\r\n\r\n"
wordpress_id: 601
wordpress_url: http://blog.novoj.net/?p=601
date: '2009-08-23 11:22:23 +0200'
date_gmt: '2009-08-23 10:22:23 +0200'
categories:
- Java
- Management
- Testování
- Web
- Stripes
tags: []
comments:
- id: 15399
  author: Tomas Kutin
  author_email: tomas.kutin@gmail.com
  author_url: ''
  date: '2009-12-01 10:38:30 +0100'
  date_gmt: '2009-12-01 09:38:30 +0100'
  content: 'ty generovane DAO dle interface to se mi libi : )'
---
<p>V <a href="http://blog.novoj.net/2009/08/16/ibatis-30-preview-cast-prvni/">předchozím článku</a> jsme si ukázali vylepšení iBatisu v souvislosti s XML deklaracemi. Tento navazující článek rozebírá novinky v oblasti Java API. Základem pro toto rozšíření se staly vlastnosti dostupné od verze Javy 1.5 - tedy generiky a anotace. Jednou z velkých kritik původního iBatisu bylo množství XML, které bylo nutné psát. Našlo se mnoho lidí, kterým tento přístup vadil a kteří by spíše uvítali mít vše na jednom místě v kódu. Autoři tyto kritiky vyslyšeli a vytvořili plnohodnotné API, před které je možné využít libovolnou funkcionalitu iBatisu.</p>
<p>Před tím, než se pustím do rozebírání detailů bych se s Vámi rád podělil o jeden velmi zajímavý úryvek z dokumentace, který má s výše uvedeným souvislost:</p>
<p><cite>Java Annotations are unfortunately limited in their expressiveness and flexibility. Despite a lot of time spent in investigation, design and trials, the most powerful iBATIS mappings simply cannot be built with Annotations – without getting ridiculous that is. C# Attributes (for example) do not suffer from these limitations, and thus iBATIS.NET will enjoy a much richer alternative to XML. That said, the Java Annotation based configuration is not without its benefits.</cite></p>
<p>Zdá se mi to jen nebo se povzdechy nad rigiditou Javy stávají normálním trendem?</p>
<p><a id="more"></a><a id="more-601"></a></p>
<p><strong>Obsah</strong></p>
<ol>
<li><a href="#generics">Využití generik a typově bezpečného kódu</a></li>
<li><a href="#interface">Využití anotací pro psaní SQL dotazů</a></li>
<li><a href="#javastatement">Využití SQL statementů vytvořených přímo Java kódem</a></li>
<li><a href="#extensions">Rozšíření extension pointů</a></li>
<li><a href="#spring">Integrace se Springem</a></li>
<li><a href="#sources">Použité zdroje a závěr</a></li>
</ol>
<h3><a name="generics">Využití generik a typově bezpečného kódu</a></h3>
<p>Pro mě asi nejzásadnější pokrok znamenají automaticky generované DAO implementace na základě mnou definovaného interface. Klíčový princip v novém iBatisu je  jednoznačná vazba mezi interfacem DAO třídy a XML konfiguračním souborem na základě stejnojmenného namespace. Každý konfigurační XML konfigurační soubor by měl ve své hlavičce deklarovat unikátní namespace odpovídající packagové cestě DAO interface, ke kterému se vztahuje:</p>
<p>[source lang="xml"]<br />
<?xml version="1.0" encoding="UTF-8" ?><br />
<!DOCTYPE mapper<br />
        PUBLIC "-//ibatis.apache.org//DTD Mapper 3.0//EN"<br />
        "http://ibatis.apache.org/dtd/ibatis-3-mapper.dtd"></p>
<mapper namespace="domain.blog.mappers.AuthorMapper">
... další definice ...<br />
[/source]</p>
<p>Propojení metody interface se statementem definovaným v XML se děje přes jméno metody. iBatis sám automaticky vygeneruje implementaci interfacu a propojí ho se statementy v XML. Provede i statickou kontrolu vstupních a výstupních parametrů statementů.  Dotazy přes tzv. mappery probíhají následujícím (vcelku intuitivním) způsobem:</p>
<p>[source lang="java"]<br />
SqlSession session = sqlMapper.openSession();<br />
try {<br />
  BlogMapper mapper = session.getMapper(BlogMapper.class);<br />
  List<Map> posts = mapper.selectAllPosts(null, 0, 2);<br />
  assertEquals(2, posts.size());<br />
  assertEquals(1, posts.get(0).get("ID"));<br />
  assertEquals(2, posts.get(1).get("ID"));<br />
} finally {<br />
  session.close();<br />
}<br />
[/source]</p>
<p>Tedy nikdy více už repetitivní implementace tupých DAO objektů. Stačí deklarovat interface a už fungujeme. V kombinaci s transakčními atributy Sprignu (@Transactional), máme v podstatě všechno, co bychom mohli potřebovat.</p>
<p>Prozatím jsem nikde nenašel zmínku o automaticky generovaných SQL statementech pouze na bázi konvence a signatury metody, přestože tato věc byla ve white paperu pro iBatis 3.0 také probírána. Na druhou stranu, ztráta této vlastnosti mi ani moc nevadí - naopak, tím že v iBatisu není, dávají autoři najevo, že iBatis vždy chtěl být a nadále zůstává naprosto transparentní. Není v něm žádná magie automatického generování SQL jaké je vidět v "plnotučných" ORM typu Hibernate.</p>
<h3><a name="interface">Využití anotací pro psaní SQL dotazů</a></h3>
<p>Anotace se těší velké oblibě a proto se pro jejich zavedení rozhodli i autoři iBatisu. S pomocí anotací by mělo být možné zapsat vše (respektive téměř vše), čeho dosáhneme v XML. V krajním případě se tedy můžeme úplně obejít bez jediné čárky v XML. Ukázkové DAO by nyní mohlo vypadat třeba takhle:</p>
<p>[source lang="java"]<br />
public interface BoundBlogMapper {</p>
<p>  @Select({"SELECT * FROM blog"})<br />
  List<Blog> selectBlogs();  </p>
<p>  @Select({"SELECT * FROM blog"})<br />
  List<Map> selectBlogsAsMaps();</p>
<p>  @Select("SELECT * FROM post ORDER BY id")<br />
  @TypeDiscriminator(<br />
      column = "draft",<br />
      javaType = String.class,<br />
      cases = {@Case(value = "1", type = DraftPost.class)}<br />
  )<br />
  List<Post> selectPosts();  </p>
<p>  @Select("SELECT * FROM  blog WHERE id = #{id}")<br />
  Blog selectBlog(int id);  </p>
<p>}<br />
[/source]</p>
<p>Na druhou stranu je velmi lehké z ošklivého XML přejít do ještě ošklivějších anotací. Například v tomto případě, bych já osobně volil spíše přehlednější XML:</p>
<p>[source lang="java"]<br />
@Select("SELECT * FROM post ORDER BY id")<br />
  @Results({<br />
    @Result(id = true, property = "id", column = "id")<br />
      })<br />
  @TypeDiscriminator(<br />
      column = "draft",<br />
      javaType = int.class,<br />
      cases = {@Case(value = "1", type = DraftPost.class,<br />
          results = {@Result(id = true, property = "id", column = "id")})}<br />
  )<br />
List<Post> selectPostsWithResultMap();</p>
<p>@ConstructorArgs({<br />
    @Arg(column = "AUTHOR_ID", javaType = Integer.class)<br />
      })<br />
  @Results({<br />
    @Result(property = "username", column = "AUTHOR_USERNAME"),<br />
    @Result(property = "password", column = "AUTHOR_PASSWORD"),<br />
    @Result(property = "email", column = "AUTHOR_EMAIL"),<br />
    @Result(property = "bio", column = "AUTHOR_BIO")<br />
      })<br />
  @Select({<br />
      "SELECT ",<br />
      "  ID as AUTHOR_ID,",<br />
      "  USERNAME as AUTHOR_USERNAME,",<br />
      "  PASSWORD as AUTHOR_PASSWORD,",<br />
      "  EMAIL as AUTHOR_EMAIL,",<br />
      "  BIO as AUTHOR_BIO",<br />
      "FROM AUTHOR WHERE ID = #{id}"})<br />
Author selectAuthor(int id);<br />
[/source]</p>
<p>Anotace je možné využívat nejen pro Select statementy ale i pro Insert, Update, Delete, definici Cachí apod. K anotacím se však vztahují dvě velké nevýhody:</p>
<ul>
<li>jsou napevno zkompilované v kódu a není je možné za běhu změnit</li>
<li>pokud potřebujeme podporovat více databázových strojů nezbyde nám než duplikovat interfacy nebo jít cestou XML</li>
</ul>
<p>Z pochopitelného důvodu nechce iBatis v anotacích pokrýt všechny kombinace a všechny možné způsoby použití. Řekl bych, že anotace se perfektně hodí k jednoduchým jednoúčelovým aplikacím, kde se nemusíme obávat portace na jiný DB server a jde nám především o rychlost implementace. V jiných případech bych asi pořád volil staré dobré XML. </p>
<p>iBatis umožňuje poměrně bezpečný fallback k XML - pokud totiž máme na metodě interfacu nadefinovanou anotaci a iBatis najde stejně pojemenovaný statement v XML mapování, dá přednost XML. Takže i v případě zakompilované anotace máme šanci s tím stále něco udělat.</p>
<h3><a name="javastatement">Využití SQL statementů vytvořených přímo Java kódem</a></h3>
<p>Dlouho se diskutovalo také nad tím, že velmi komplikované SQL dotazy jsou, přes veškeré možnosti dynamických dotazů, v XML stále obtížně čitelné. Z toho důvodu zavedli autoři možnost tyto výjimečné typy dotazů vytvářet přímo v Javě. Princip je následující - v rozhranní Mapperu je třeba definovat následující anotaci:</p>
<p>[source lang="java"]<br />
public interface BoundBlogMapper {</p>
<p>  @SelectProvider(type = BoundBlogSql.class, method = "selectBlogsSql")<br />
  List<Blog> selectBlogsUsingProvider();</p>
<p>}<br />
[/source]</p>
<p>Následně ve třídě BoundBlogSql nadefinovat metodu selectBlogsSql, která vytvoří požadovaný SQL dotaz:</p>
<p>[source lang="java"]<br />
public class BoundBlogSql {</p>
<p>  public String selectBlogsSql() {<br />
    return "select * from BLOGS";<br />
  }</p>
<p>}<br />
[/source]</p>
<p>Do daného dotazu je možné také předat jeden zvolený parametr libovolného typu. Pro tvorbu SQL dotazů v Javě iBatis nabízí jednoduchý nástroj, který může ušetřit kus práce a více zčitelnit kód sestavující SQL. Tím je nástrojem je třída SelectBuilder obsahující sadu statických metod pro vytváření logických celků SQL dotazu. Jeho použití si pojďme ukázat na následujícím příkladě:</p>
<p>[source lang="java"]<br />
private static String example1() {<br />
	BEGIN();<br />
	SELECT("P.ID, P.USERNAME, P.PASSWORD, P.FULL_NAME");<br />
	SELECT("P.LAST_NAME, P.CREATED_ON, P.UPDATED_ON");<br />
	FROM("PERSON P");<br />
	FROM("ACCOUNT A");<br />
	INNER_JOIN("DEPARTMENT D on D.ID = P.DEPARTMENT_ID");<br />
	INNER_JOIN("COMPANY C on D.COMPANY_ID = C.ID");<br />
	WHERE("P.ID = A.ID");<br />
	WHERE("P.FIRST_NAME like ?");<br />
	OR();<br />
	WHERE("P.LAST_NAME like ?");<br />
	GROUP_BY("P.ID");<br />
	HAVING("P.LAST_NAME like ?");<br />
	OR();<br />
	HAVING("P.FIRST_NAME like ?");<br />
	ORDER_BY("P.ID");<br />
	ORDER_BY("P.FULL_NAME");<br />
	return SQL();<br />
}</p>
<p>private static String example2(String id, String firstName, String lastName) {<br />
	BEGIN();<br />
	SELECT("P.ID, P.USERNAME, P.PASSWORD, P.FIRST_NAME, P.LAST_NAME");<br />
	FROM("PERSON P");<br />
	if(id != null) {<br />
		WHERE("P.ID like #id#");<br />
	}<br />
	if(firstName != null) {<br />
		WHERE("P.FIRST_NAME like #firstName#");<br />
	}<br />
	if(lastName != null) {<br />
		WHERE("P.LAST_NAME like #lastName#");<br />
	}<br />
	ORDER_BY("P.LAST_NAME");<br />
	return SQL();<br />
}<br />
[/source]</p>
<p>Osobně nepatřím mezi kritiky XML zápisu, proto bude tohle asi jedna z vlastností, kterou spíš nevyužiji než naopak. Věřím ale, že se najde plno vývojářů, kteří tuto možnost v portfoliu iBatisu uvítají.</p>
<h3><a name="extensions">Rozšíření extension pointů</a></h3>
<p>V předchozí verzi iBatisu byly k dispozici jediné dva extension pointy:</p>
<ul>
<li><strong>ResultObjectFactory</strong> - rozhranní, které iBatis používá pro vytvoření všech instancí při zpracovávání dotazů (efektivně bylo možno využít např. k obalování tříd dynamickými proxy objekty atp.)</li>
<li><strong>TypeHandlerCallback / TypeHandler</strong> - rozhranní, které iBatis používá k převodu SQL objektů na Java objekty a zpět (bylo nutné použít například, pro převod hodnoty sloupce na Enum, popřípadě na další custom typy)</li>
</ul>
<p>Ve verzi 3.0 tyto rozhraní samozřejmě zůstávají. Rozdíl je pouze v <strong>ResultObjectFactory</strong>, která byla přejmenována na <strong>ObjectFactory</strong> a má podporu pro parametrizovatelné konstruktory. Nově je přidána tzv. Pluginů, které vám umožní vstoupit (intercept) do volání iBatisu na dalších místech:</p>
<ul>
<li><strong>Executor</strong> - pro přerušení následujících typů volání: update, query, flushStatements, commit, rollback, getTransaction, close, isClosed</li>
<li><strong>ParameterHandler</strong> - pro přerušení nastavení parametrů do SQL Statementu (volání metody setParameter)</li>
<li><strong>ResultSetHandler</strong> - pro přerušení načítání objektů z SQL ResultSetu</li>
<li><strong>StatementHandler</strong> - pro přerušení volání nad SQL Statementem: prepare, parameterize, batch, update, query</li>
</ul>
<p>Tyto extension pointy jsou záměrně velmi nízkoúrovňové - což s sebou nese mj. i riziko, že pokud do jejich chodu nějak výrazně nekompatibilně zasáhnete, koledujete si o kompletní selhání iBatisu jako takového. Takže s rozmyslem! :-)</p>
<h3><a name="spring">Integrace se Springem</a></h3>
<p>V iBatisu jako takovém není podpora pro Spring. Očekává se, že naopak Spring začne v dalších verzích podporovat novou verzi iBatisu. Pro překlenovací období se už <a href="http://www.mail-archive.com/user-java@ibatis.apache.org/msg14416.html" target="_blank">na mailing listu objevily první implementace integračních tříd pro Spring 3.0</a> lehce modifikovatelné pro práci se Spring 2.5. V zásadě by měla stačit pouze velmi tenká integrační vrstva.</p>
<h3><a name="sources">Použité zdroje a závěr</a></h3>
<p>Pokud byla minulá verze iBatisu oblíbená, věřím, že ta nejnovější si získá ještě větší množství příznivců. Výsledné API, které vzniklo mi připadá poměrně čisté a ucelené. Úvodní dokumentace je více než dostačující a bezchybnost vlastního kódu ukáže budoucnost (nicméně 2000 automatických testů je poměrně vypovídající ukazatel).</p>
<p>Pokud se tedy přistihnete, že na Hibernate pořád nadáváte - zkuste dát iBatisu šanci. Myslím, že mezi rozhodně nebudete mezi uživateli iBatisu prvními odpadlíky od JPA like frameworků.</p>
<ul>
<li><a href="http://ibatis.apache.org/java.cgi" target="_blank">Homepage iBatisu</a></li>
<li><a href="http://svn.apache.org/repos/asf/ibatis/trunk/java/ibatis-3/doc/en/iBATIS-3-User-Guide.pdf" target="_blank">Dokumentace k třetí verzi iBatisu</a></li>
<li><a href="http://www.opensymphony.com/ognl/" target="_blank">Homepage OGNL</a></li>
</ul>
