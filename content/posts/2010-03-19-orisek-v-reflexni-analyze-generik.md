---
status: publish
published: true
title: Oříšek v reflexní analýze generik
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Minulý týden jsem řešil zajímavý problém s reflexí a došel jsem k závěru,
  že generiky v reflexním API jsou opravdu velká legrace. Prototypoval jsem myšlenku
  automatického generování implementací nad obecným kontejnerem - dejme tomu Map<String,
  Object> (což není pro účely tohoto článku zase až tak důležité), a došel jsem k
  potřebě správně číst generické informace z deklarací tříd. Právě této, na první
  pohled jednoduché, věci, bych chtěl věnovat dnešní článek.\r\n\r\n"
wordpress_id: 850
wordpress_url: http://blog.novoj.net/?p=850
date: '2010-03-19 08:14:42 +0100'
date_gmt: '2010-03-19 07:14:42 +0100'
categories:
- Programování
- Java
tags:
- reflexe
- generiky
comments:
- id: 21319
  author: Pavel Savara
  author_email: pavel.savara@gmail.com
  author_url: http://zamboch.blogspot.com/
  date: '2010-03-21 17:21:52 +0100'
  date_gmt: '2010-03-21 16:21:52 +0100'
  content: "Ahoj,\r\n\r\nto co tady pises se mi bude casem hodit. Ale nejdrive musim
    vyresit jiny orisek, myslim ze je to jeste o level obtiznejsi.\r\n\r\nDelam po
    vecerech http://jni4net.sf.net, objektovy bridge mezi Javou a C#. Tak jako ty
    pouzivam reflection a z ni generuju proxy. Rozdil je v tom ze k Javovske tride
    generuju C# proxy. A ted ten orisek.\r\n\r\n1) Pro ArrayList&lt;E&gt; na strane
    C# potrebujeme zaroven ArrayList&lt;E&gt; a zaroven ArrayList. \r\nPri cemz ArrayList
    je idealne zdedeny z ArrayList&lt;Object&gt;, co se signatur metod tyce.\r\nAle
    na druhou stranu, prirazeni ArrayList x = new ArrayList&lt;String&gt;(); musi
    byt ok.\r\nDa se to asi prechytracit pomoci implicitnich konverzinch operatoru
    v C#. Ale pouze pro tridy, pro interfacy je to prohrane.\r\n\r\n2) Java ma wildcard
    \"?\". Ten znamena neco ve smyslu, dej si tam co chces, na runtime to bude stejne
    Object. Z toho vyplyva nasledujici:\r\na) Existuje bounded wildcard. V C# existuje
    pouze upper bound. S lower bound je to horsi Collection&lt;? super Person&gt;.
    Ja doufam ze se v prirode vyskytuje vzacne a proto ho muzu zanedbat.\r\nTady se
    da genericky wildcard ? vynechat na deklaraci tridy a pridat na deklaraci metodygenericky
    parametr T, to resi nektere zapeklitosti. Nevim jeste jestli vsechny.\r\n\r\nb)
    Existuje dedicnost z wildcard typu, a to je mazec. Vubec nevim co s tim.\r\nWeakClassKey
    extends WeakReference&lt;Class&lt;?&gt;&gt;{\r\n   Class&lt;?&gt; getClass(){\r\n
    \  }\r\n}\r\n\r\nZatraceny type erasure, jakakoliv dobra rada je mi cenna.\r\nPavel"
- id: 21338
  author: Marián
  author_email: majko@europe.com
  author_url: ''
  date: '2010-03-22 19:36:21 +0100'
  date_gmt: '2010-03-22 18:36:21 +0100'
  content: "Ono je vôbec zaujímavé, že sa to dá takto \"hacknúť'. \r\nZmyslom erasure
    je aj to, aby to nešlo. Kvôli spätnej kompatibilite.\r\nVďaka za tip!"
- id: 21339
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-03-22 21:22:42 +0100'
  date_gmt: '2010-03-22 20:22:42 +0100'
  content: "ad Pavel Savara) přiznám se, že jsem se snažil proniknout do tvých problémů,
    ale moc se mi to nezadařilo. Potřeboval bych asi hlubší poznání toho problému,
    abych dokázal reagovat. Navíc v C# jsem úplný analfabet, takže nevím, jaké možnosti
    / problémy jsou na druhé straně - nicméně věřím, že se snažit implementovat konverzi
    generik z dvou, takto oddělených světů musí být oříšek na druhou.\r\n\r\nDíky
    za komentář, ale za mě se bohužel žádné cenné reakce asi nedočkáš ;-)"
- id: 21450
  author: niko
  author_email: niko@srnet.cz
  author_url: ''
  date: '2010-03-28 20:30:50 +0200'
  date_gmt: '2010-03-28 19:30:50 +0200'
  content: ad Marián) Pokud by bylo záměrem informace o typech zcela skrýt, pak by
    pravděpodobně neexistovaly metody jako Class.getGenericSuperclass(). Smyslem erasure
    je zpětná kompatibilita a ta těžko může být možností inspekce prostřednictvím
    reflexe nějak dotčena.
- id: 21516
  author: benzin
  author_email: benzin@centrum.cz
  author_url: ''
  date: '2010-03-30 08:19:31 +0200'
  date_gmt: '2010-03-30 07:19:31 +0200'
  content: "Tento problem sem taky resil. Nakonec sem rezignoval na genericky primarni
    klic apouzivam String. Pokud z nejakeho duvodu je databaze schopna pracovat rychleji
    s klicem jineho typu (napr. celociselnym, nebo Key v GAE) tak neni problem prevod
    mezi klicem a stringem naimplementovat primo v metode getId() a setId() a mapovat
    ho do jineho fieldu s typem vhodnym pro tu kterou databazi.\r\n\r\nZjistis ze
    si tak usetris strasnou spoustu problemu. Hlavne strasnou spoustu psani. Po nekolika
    hroznych mesicich straveny spodobnymi pokusy sem prisel na to ze generiky na tohle
    fakt nejsou vhodne."
- id: 21517
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-03-30 09:02:41 +0200'
  date_gmt: '2010-03-30 08:02:41 +0200'
  content: ad benzin) musím říct, že to byla trochu škola, ale mám pocit že se mi
    to podařilo protunelovat - knihovnu na řadě instalací už používáme a funguje to
    poměrně intuitivně a hlavně bez dalšího přemýšlení ... složitý kód je v AOP advicách
    ale klientský kód už je velmi přehledný a čitelný
- id: 21580
  author: niko
  author_email: niko@srnet.cz
  author_url: ''
  date: '2010-04-01 12:28:26 +0200'
  date_gmt: '2010-04-01 11:28:26 +0200'
  content: ad Pavel Savara) O C# nevím vůbec nic, nicméně k těm bounded wildcards
    - upper a lower bound tvoří logickou dvojici třeba ve vztahu operátor/operand.
    Například pro setřídění List mohu použít Comparator. Prostě podle toho, co dělám,
    se na hierarchii dědičnosti dívám z jedné nebo druhé strany. Je to dost přirozený
    požadavek, těžko říct, zda se "v přírodě" vyskytuje vzácně.
- id: 21581
  author: niko
  author_email: niko@srnet.cz
  author_url: ''
  date: '2010-04-01 12:32:32 +0200'
  date_gmt: '2010-04-01 11:32:32 +0200'
  content: Ha zmizely špičaté závorky... No ale snad je to jasné, prostě cokoliv typu
    MyType nebo jeho podtypu mohu předhodit čemukoliv co umí pracovat s typem MyType
    nebo jeho nadtypem.
---
<p>Minulý týden jsem řešil zajímavý problém s reflexí a došel jsem k závěru, že generiky v reflexním API jsou opravdu velká legrace. Prototypoval jsem myšlenku automatického generování implementací nad obecným kontejnerem - dejme tomu Map<String, Object> (což není pro účely tohoto článku zase až tak důležité), a došel jsem k potřebě správně číst generické informace z deklarací tříd. Právě této, na první pohled jednoduché, věci, bych chtěl věnovat dnešní článek.</p>
<p><a id="more"></a><a id="more-850"></a></p>
<p>Problém mohu ukázat na příkladě:</p>
<p>Chtěl bych mít jednotné API pro přístup k primárnímu klíči.</p>
<p>[source lang="java"]<br />
public interface IdAccessor<T> {<br />
   T getId();<br />
   void setId(T id);<br />
}<br />
[/source]</p>
<p>Pak mám obecného předka Album:</p>
<p>[source lang="java"]<br />
public abstract class Album<S extends Media> implements IdAccessor<Long> {<br />
   public abstract S getFeaturedMediaItem();<br />
   public abstract List<S> getMediaItems()<br />
   //další metody<br />
}<br />
[/source]</p>
<p>A konkrétní implementace (PhotoAlbum, VideoAlbum, AudioAlbum) atd.:</p>
<p>[source lang="java"]<br />
public abstract class PhotoAlbum extends Album<Photo> {}<br />
[/source]</p>
<p>V AOP proxy mám následně přístup k reflexnímu obrazu metody getFeaturedMediaItem a rád bych vrátil dynamickou proxy třídy, která typově odpovídá deklaraci. Volání: </p>
<p>[source lang="java"]<br />
Album.class.getDeclaredMethod("getFeaturedMediaItem").getReturnType()<br />
[/source]</p>
<p>mi však vrátí třídu Media. V kontextu třídy PhotoAlbum bych ale rád získal specifický typ Media a to je Photo - to je přeci z deklarace Java třídy krásně vidět. Tak jak se k této informaci dostat pomocí reflexe? Na rovinu říkám, že čím víc o generikách vím, tím víc mi připadají jako velmi komplexní rébus. Připadám si trošku jako když účetní nakoukne do učebnic kvantové fyziky.</p>
<p>Když odhlédnu od toho, že mě zajímá obecný princip jak se dostat k informaci o konkrétní třídě odpovídající zástupnému generickému symbolu, mohu se v tomto případě k cílovému typu dostat takto:</p>
<p>[source lang="java"]<br />
public void testGenerics() throws Exception {<br />
	Class resolvedClass = null;<br />
	//toto je naše S<br />
	Type searchedType = Album.class.getDeclaredMethod("getFeaturedMediaItem").getGenericReturnType();<br />
	//tako získáme kontextovou informaci, co je S v případě třídy PhotoAlbum<br />
	ParameterizedType genericSuperClass = ((ParameterizedType)PhotoAlbum.class.getGenericSuperclass());<br />
	//na předkovi se podíváme na deklarované parametry<br />
	Type[] typeParameters = PhotoAlbum.class.getSuperclass().getTypeParameters();<br />
	//na generickém obrazu nadřízené třídy se podíváme na "vyhodnocené" generické argumenty<br />
	Type[] resolvedParameters = genericSuperClass.getActualTypeArguments();<br />
	//projdeme všechny deklarované parametry na třídě, a porovnáme je s hledaným typem v návratové hodnotě<br />
	for(int i = 0; i < typeParameters.length; i++) {<br />
		Type rawParameter = typeParameters[i];<br />
		if(searchedType.equals(rawParameter)) {<br />
			resolvedClass = (Class)resolvedParameters[i];<br />
		}<br />
	}<br />
	//a našli jsme námi hledanou třídu Photo<br />
	assertSame(Photo.class, resolvedClass);<br />
}<br />
[/source]</p>
<p>Legrační že? Mě tedy trvalo docela dlouho, než jsem do toho trošku pronikl. Teď ještě vymyslet způsob, jak tuto analýzu provést obecně na libovolné hierarchii tříd. V reflexním API se pracuje s obecným interfacem <strong>Type</strong>, který může být reprezentován několika různými podtypy:</p>
<ul>
<li><strong>Class:</strong> klasický jednoduchý typ jako třeba String nebo Integer[] - to je v podstatě to, co hledáme</li>
<li><strong>TypeVariable:</strong> proměnný typ -  např. T - to je něco co potřebujeme vyhodnotit</li>
<li><strong>ParameterizedType:</strong> parametrizovaný typ, např. List<String> nebo Set<? extends Number> - to je něco, co nám dokáže poskytnout informace o přiřazení TypeVariable na Class, minimálně jsme schopni přes to získat tzv. "upper bounds"</li>
<li><strong>GenericArrayType:</strong> generické pole - tedy List<?>[] nebo T[]</li>
<li><strong>WildcardType:</strong> wildcard, např. ? extends Number nebo ? super Long - tady na tomhle objektu jsme schopní se zeptat na "upper bounds" a "lower bounds"</li>
</ul>
<p>Pouze v případě ParameterizedType se dokážeme zjistit, jestli některému proměnnému typu nebyla přiřazena konkrétní class -  díky volání metody getActualTypeArguments(). Problémem zůstává jak zjistit, co bylo čemu vlastně přiřazeno. Tady musíme porovnávat původní typy získané přes getTypeParameters() s naším hledaným typem v TypeVariable. Celé je to dost zamotané, protože vyhodnocené typy a původní typy získáváme přes různá volání - tj. getSuperClass() a getGenericSuperClass(). Porovnání typů se navíc nesmí dělat porovnáním referencí (==), ale přes volání metody equals(). Zkrátka a prostě, je to taková dobrá mentální rozcvička. Po pár hodinách zkoušení jsem ve svém kódu došel k implementaci, která mi dokázala vyhodnotit konkrétní typy přes celou hierarchii nadřízených tříd a všech odkazovaných interfaců (<a href="http://files.novoj.net/Generics/GenericUtils.java">ke stažení zde</a>).</p>
<p>Nejvtipnější na tom celém je to, že když jsem do celé záležitosti jakž tak pronikl, tak jsem našel <a href="http://www.jdocs.com/spring/2.5.2/org/springframework/core/GenericTypeResolver.html" target="_blank">hledanou utilitu hotovou a vyladěnou ve Spring Frameworku</a>. Pro příklad uvádím jednoduchý test, který získá informace, které jsem hledal (plus další test na extenzi generické HashMap pro ukázku resolvování generického typu v argumentu metody):</p>
<p>[source lang="java"]<br />
public class GenericsTest extends TestCase {</p>
<p>	public void testGenericsWithSpring() throws Exception {<br />
		Class resolvedClass = GenericTypeResolver.resolveReturnType(<br />
				Album.class.getDeclaredMethod("getFeaturedMediaItem"), PhotoAlbum.class<br />
		);<br />
		assertSame(Photo.class, resolvedClass);<br />
	}</p>
<p>	public void testGenericsMapWithSpring() throws Exception {<br />
		Class resolvedType = GenericTypeResolver.resolveParameterType(<br />
				new MethodParameter(<br />
						HashMap.class.getDeclaredMethod("put", Object.class, Object.class), 0<br />
				), MyMap.class<br />
		);<br />
		assertSame(String.class, resolvedType);<br />
	}</p>
<p>	private static class MyMap extends HashMap<String, String> {}</p>
<p>}<br />
[/source]</p>
<p>Tím, že jsem si prošel delší a trnitější cestou, jsem se minimálně donutil vztahům v reflexi generik trošku porozumět (i když na rovinu říkám, že si pořád nejsem moc jistý v kramflecích). Na druhou stranu se čím dál víc přesvědčuji o tom, že knihovna Springu v sobě skrývá nečekané poklady - jen je umět najít. Neuplyne půl roku abych nějaký podobný poklad neobjevil.</p>
<p>Jen mě stále trápí otázka, proč tak jednoduché API pro dotazování generik jaké má Spring - zopakujme si:</p>
<p>[source lang="java"]<br />
class GenericTypeResolver {<br />
   static Class resolveParameterType(MethodParameter methodParam, Class clazz);<br />
   static Class resolveReturnType(Method method, Class clazz);<br />
}<br />
[/source]</p>
<p><strong>UŽ NENÍ K DISPOZICI V ZÁKLADNÍCH BALÍCÍCH JAVY !!!</strong></p>
<h2>Zdroje ze kterých jsem čerpal</h2>
<ul>
<li><a href="http://blog.xebia.com/2009/03/12/a-general-purpose-utility-to-retrieve-java-generic-type-values/" target="_blank">Velmi pěkně popsané pozadí analýzy generik pomocí reflexe</a></li>
<li><a href="http://blog.xebia.com/2009/02/07/acessing-generic-types-at-runtime-in-java/" target="_blank">Tohle je tak trošku předskokan prvně uvedeného článku - s tímhle bych doporučoval začít</a></li>
<li><a href="http://www.artima.com/weblogs/viewpost.jsp?thread=208860" target="_blank">Základ metody v mém článku v podstatě vznikl na základě tohoto článku</a></li>
<li><a href="http://www.angelikalanger.com/GenericsFAQ/FAQSections/ProgrammingIdioms.html#Topic9" target="_blank">FAQ dotazy ohledně generik a reflexe</a></li>
</ul>
