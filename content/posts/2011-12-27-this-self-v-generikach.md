---
status: publish
published: true
title: This (self) v generikách
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft size-full wp-image-1742\" title=\"generics\" src=\"http://blog.novoj.net/binary/2011/12/generics.png\"
  alt=\"\" width=\"71\" height=\"53\" />Tohle byl pro mě nějakou dobu oříšek, než
  jsem narazil na pár článků s překvapivým - ne dokonalým, ale přeci jen nějakým řešením.\r\n\r\nProblém
  je jednoduchý, chtěl bych aby bylo možné v nějaké abstraktní třídě definovat cosi
  jako:\r\n\r\n[source lang=\"java\"]\r\n/** poznámka: toto je nesmysl, ale vyjadřuje\r\nmoji
  snahu o vyjádření vazeb **/\r\nabstract class AbstractClass&lt;T is this&gt; {\r\n
  \  T getMe();  \r\n}\r\n[/source]\r\n\r\nCož jsem potřeboval z důvodu získání reference
  na AOP proxy obalující moji třídu - v níže uvedených odkazech podobná potřeba vznikla
  při implementaci <a href=\"http://en.wikipedia.org/wiki/Builder_pattern\" target=\"_blank\">builder
  patternu</a>.\r\n\r\n"
wordpress_id: 1735
wordpress_url: http://blog.novoj.net/?p=1735
date: '2011-12-27 21:50:53 +0100'
date_gmt: '2011-12-27 20:50:53 +0100'
categories:
- Programování
- Java
tags: []
comments:
- id: 57970
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-12-28 08:08:16 +0100'
  date_gmt: '2011-12-28 07:08:16 +0100'
  content: 'Poznámka: jazyk Kotlin od JetBrains bude mít generickou podporu This zabudovanou
    - viz. diskuse zde: http://confluence.jetbrains.net/display/Kotlin/Generics?focusedCommentId=44237386&#comment-44237386'
- id: 57972
  author: Filip Jirsák
  author_email: filip@jirsak.org
  author_url: ''
  date: '2011-12-28 09:02:27 +0100'
  date_gmt: '2011-12-28 08:02:27 +0100'
  content: Je dobré si pamatovat, že přesně touhle konstrukcí je definováno java.lang.Enum.
    Pak už se to hledá snadno :-)
- id: 58040
  author: Tomáš Záluský
  author_email: zalusky@centrum.cz
  author_url: ''
  date: '2011-12-29 10:16:32 +0100'
  date_gmt: '2011-12-29 09:16:32 +0100'
  content: Taky to na pár místech používáme. Je to fajn trik. Akorát když pak vedle
    této hierarchie vznikne nějaká paralelní (např. AbstractParentFactory, FooFactory,
    BarFactory), zatáhnou se generiky i do ní a pak jsou všechny třídy z obou hierarchií
    parametrizovány dvěma typovými parametry, jedním z každé hierachie. Což je někdy
    na škodu čitelnosti, ale pořád je zachována typová bezpečnost.
- id: 58045
  author: Michal Franc
  author_email: michal.franc@gmail.com
  author_url: ''
  date: '2011-12-29 12:25:06 +0100'
  date_gmt: '2011-12-29 11:25:06 +0100'
  content: Parada, zrovna dnes se mi to hodilo :)
- id: 58056
  author: Zdeněk Troníček
  author_email: tronicek@fit.cvut.cz
  author_url: http://java.cz/blog/tronicek
  date: '2011-12-29 15:58:00 +0100'
  date_gmt: '2011-12-29 14:58:00 +0100'
  content: "Častěji používám generickou metodu, protože je jednodušší:\r\n\r\n    @SuppressWarnings(\"unchecked\")\r\n
    \    T getMe() {\r\n        return (T) this;\r\n    }\r\n\r\nHodí se to však pouze
    pro případy, kdy potomci o sobě nevědí, protože je možné toto:\r\n\r\npublic class
    Bar extends AbstractParent {\r\n\r\n    public Bar makeLowerCase() {\r\n        return
    getMe();\r\n    }\r\n    \r\n    public Foo m() {\r\n        return getMe();\r\n
    \   }\r\n}\r\n\r\nVolání m() pak pochopitelně skončí výjimkou."
- id: 58077
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-12-29 21:49:37 +0100'
  date_gmt: '2011-12-29 20:49:37 +0100'
  content: "Ad) Zdeněk Troníček - z příkladu úplně nechápu, jak zajistíš to odvození
    typu na potomka - tj. aby bez castování prošel zápis:\r\n\r\nnew Bar().addText(\"Hello
    \").addText(\"world!\").makeLowerCase().buildString();\r\n\r\nTa volání addText
    by se v tvém případě vyhodnotila na AbstractParent, kde ta metoda makeLowerCase()
    chybí.\r\n\r\nNebo jsem to jen špatně pochopil? Nezmizely ti generiky při přidávání
    komentáře?"
- id: 58162
  author: Zdeněk Troníček
  author_email: tronicek@fit.cvut.cz
  author_url: http://java.cz/blog/tronicek
  date: '2011-12-30 21:36:55 +0100'
  date_gmt: '2011-12-30 20:36:55 +0100'
  content: "No jo, zmizely. Tak ještě jednou:\r\n\r\n   @SuppressWarnings(\"unchecked\")\r\n
    \   &lt;T extends AbstractParent&gt; T getMe() {\r\n        return (T) this;\r\n
    \   }\r\n\r\nJinak ten příklad, který uvádíš, neprojde. V tomto ohledu to samozřejmě
    na Tvoje řešení nemá."
- id: 58331
  author: Felix
  author_email: kooudy@email.cz
  author_url: ''
  date: '2012-01-02 10:12:31 +0100'
  date_gmt: '2012-01-02 09:12:31 +0100'
  content: "Neco podobneho jsem resil pri vytvareni obecneho nodu ve strome, kdy jsem
    chtel zajistit, aby deti byly stejneho typu jako definovany node (selftype), a
    take, aby parent byl stejneho typu. Zaroven zachovat typovou bezpecnost a dedeni
    (genericky typ nahradit potomkem, ktery ma navic nejake atributy):\r\n<a href=\"http://stackoverflow.com/questions/6864315/java-tree-node-recursive-generics\"
    title=\"reseni\" rel=\"nofollow\">"
- id: 58332
  author: Felix
  author_email: kooudy@email.cz
  author_url: ''
  date: '2012-01-02 10:13:15 +0100'
  date_gmt: '2012-01-02 09:13:15 +0100'
  content: "Druhy pokus:\r\nhttp://stackoverflow.com/questions/6864315/java-tree-node-recursive-generics"
- id: 58357
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-01-02 16:12:43 +0100'
  date_gmt: '2012-01-02 15:12:43 +0100'
  content: Tak tohle už je šílenství na druhou :) .. díky moc za odkaz.
- id: 63834
  author: jehovista
  author_email: jehovistovo@gmail.com
  author_url: ''
  date: '2012-03-14 22:59:51 +0100'
  date_gmt: '2012-03-14 21:59:51 +0100'
  content: Bude to asi hloupy dotaz, ale proc je class AbstractParent deklarovana
    abstraktni? Ma to nejaky vyznam v tom prikladu, nebo nad tim premyslim zbytecne?
- id: 63854
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-03-15 08:46:10 +0100'
  date_gmt: '2012-03-15 07:46:10 +0100'
  content: "IMHO - Abstract je možné klidně vynechat a generiky to neovlivní. V příkladu
    je to hlavně proto, aby čtenář očekával, že funkce této třídy je pouze v tom,
    že má sloužit jako předek pro nějaké potomky, který sám o sobě nemá valný význam.\r\n\r\nPravda
    je, že ve svých použitích to mám podobně (včetně abstraktní třídy), protože je
    to poměrně typický use-case - tímto zápisem generik umožňujeme vynutit nějaké
    chování na úrovni potomků a tím pádem by naše třída měla být pouze jako abstraktní
    předek, ze kterého se dědí. Ale určitě mohou být i další usecasy, kdy chceme mít
    už i předka neabstraktního."
---
<p><img class="alignleft size-full wp-image-1742" title="generics" src="http://blog.novoj.net/binary/2011/12/generics.png" alt="" width="71" height="53" />Tohle byl pro mě nějakou dobu oříšek, než jsem narazil na pár článků s překvapivým - ne dokonalým, ale přeci jen nějakým řešením.</p>
<p>Problém je jednoduchý, chtěl bych aby bylo možné v nějaké abstraktní třídě definovat cosi jako:</p>
<p>[source lang="java"]<br />
/** poznámka: toto je nesmysl, ale vyjadřuje<br />
moji snahu o vyjádření vazeb **/<br />
abstract class AbstractClass&lt;T is this&gt; {<br />
   T getMe();<br />
}<br />
[/source]</p>
<p>Což jsem potřeboval z důvodu získání reference na AOP proxy obalující moji třídu - v níže uvedených odkazech podobná potřeba vznikla při implementaci <a href="http://en.wikipedia.org/wiki/Builder_pattern" target="_blank">builder patternu</a>.</p>
<p><a id="more"></a><a id="more-1735"></a></p>
<p>Hezké řešení pro tento problém neexistuje, ale je možné napsat generickou vazbu, která podobný zápis umožní.</p>
<p>[source lang="java"]<br />
public abstract class AbstractParent&lt;SelfType<br />
                extends AbstractParent&lt;SelfType&gt;&gt; {<br />
	protected final StringBuilder data = new StringBuilder();</p>
<p>	@SuppressWarnings(&quot;unchecked&quot;)<br />
	protected SelfType getMe() {<br />
		return (SelfType) this;<br />
	}</p>
<p>	public SelfType addText(String something) {<br />
		data.append(something);<br />
		return getMe();<br />
	}</p>
<p>	public String buildString() {<br />
		return data.toString();<br />
	}</p>
<p>}<br />
/**<br />
*  PRVNÍ POTOMEK - DEFINUJE NOVOU VLASTNÍ METODU, ZBYTEK DĚDÍ<br />
**/<br />
public class Bar extends AbstractParent&lt;Bar&gt; {</p>
<p>	public Bar makeLowerCase() {<br />
		//nasbíraná data jen lowercasneme<br />
		data.replace(0, data.length(), data.toString().toLowerCase());<br />
		return getMe();<br />
	}</p>
<p>}</p>
<p>/**<br />
* DRUHÝ POTOMEK JE ANALOGIE K PRVNÍMU, JEN DEFINUJE JINOU METODU&lt;/pre&gt;<br />
**/public class Foo extends AbstractParent&lt;Foo&gt; {</p>
<p>	public Foo makeUpperCase() {<br />
		//nasbíraná data jen uppercasneme<br />
		data.replace(0, data.length(), data.toString().toUpperCase());<br />
		return getMe();<br />
	}</p>
<p>}<br />
[/source]</p>
<p>Dosažení mého původního cíle mohu dokumentovat na tomto testu, který se podaří zkompilovat (stejně tak funguje správně i auto-completion v IDE):</p>
<p>[source lang="java"]<br />
@Test<br />
public void tryGenerics() {<br />
	assertEquals(<br />
		&quot;hello world!&quot;,<br />
		new Bar().addText(&quot;Hello &quot;).addText(&quot;world!&quot;)<br />
				 .makeLowerCase().buildString()<br />
	);<br />
	assertEquals(<br />
		&quot;HELLO WORLD!&quot;,<br />
		new Foo().addText(&quot;Hello &quot;).addText(&quot;world!&quot;)<br />
				 .makeUpperCase().buildString()<br />
	);<br />
}<br />
[/source]</p>
<p>Duležitá pasáž ve výše uvedeném příkladě je toto (pokud byste sami nepostřehli):</p>
<p><strong>class AbstractParent&lt;SelfType extends AbstractParent&lt;SelfType&gt;&gt;</strong></p>
<p>Což říká, že SelfType musí být potomek stejné třídy jako je ta, kterou právě definujeme. Je to poměrně obskurní zápis, který by mne (přiznám se) rozhodně nenapadl. Důležité je, že potomci musí ve své hlavičce uvést také poměrně zvláštní deklaraci (bez níž správného vyhodnocení generik nedosáhneme):</p>
<p><strong>class Bar extends AbstractParent&lt;Bar&gt;</strong></p>
<p>Možná tenhle trik znáte, ale já jsem o něm docela dlouho nevěděl - nedařilo se mi správně zeptat Googlu, jelikož jsem se motal pořád okolo klíčového slova this, protože intuitivnější by mě skutečně přišlo použití tohoto slova. Klíčem k rozluštění je hledat řetězec <a href="http://www.google.cz/search?q=java+generics+selftype" target="_blank">java generics selftype</a>.</p>
<p>Třeba se Vám můj "objev" bude také hodit.</p>
<h2>Reference k problému</h2>
<ul>
<li><a title="Having a Java generic class return a type reference to its specialized class. Aka, using the self-type." href="http://calliopesounds.blogspot.com/2010/11/having-java-generic-class-return-type.html" target="_blank">Having a Java generic class return a type reference to its specialized class. Aka, using the self-type.</a></li>
<li><a title="Self-bounding generics" href="http://www.artima.com/weblogs/viewpost.jsp?thread=136394" target="_blank">Self-bounding generics by Bruce Eckel</a></li>
<li><a title="Angelika Langer FAQ on Generics" href="http://www.angelikalanger.com/GenericsFAQ/FAQSections/ProgrammingIdioms.html#FAQ205" target="_blank">Angelika Langer FAQ on Generics</a></li>
<li><a title="Closed bug for JDK" href="http://bugs.sun.com/bugdatabase/view_bug.do?bug_id=6479372" target="_blank">Closed bug for JDK</a></li>
</ul>
