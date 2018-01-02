---
status: publish
published: true
title: Google collections - ušetřete si práci s kolekcemi
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Nedávno mě při poslechu <a href=\"http://www.javaposse.com/\" target=\"_new\">JavaPosse</a>
  zaujala zmínka o <a href=\"\r\nhttp://code.google.com/p/google-collections/\" target=\"_new\">Google
  Collections</a>. Jedná se o knihovnu doplňující funkcionalitu třídy Collections
  ze standardní Javy. Knihovna obsahuje řadu utility tříd, které zpříjemňují život
  s generikami v kolekcích, vytváření kolekcí v kolekcích a další manipulaci dat v
  kolekcích. Jelikož mě knihovna zaujala hned na první pohled, rozhodl jsem se podívat
  se jí na zoubek a podělit se s vámi o své zkušenosti.\r\n\r\n"
wordpress_id: 47
wordpress_url: http://blog.novoj.net/2007/12/09/google-collections-usetrete-si-praci-s-kolekcemi/
date: '2007-12-09 16:48:05 +0100'
date_gmt: '2007-12-09 15:48:05 +0100'
categories:
- Java
tags: []
comments:
- id: 1150
  author: Tomas Kutin
  author_email: tomas.kutin@uhk.cz
  author_url: ''
  date: '2007-12-09 21:38:46 +0100'
  date_gmt: '2007-12-09 20:38:46 +0100'
  content: 'zajimave, pekne, uzitecne : ) libi se mi to!'
- id: 1154
  author: ufak
  author_email: ufak@seznam.cz
  author_url: ''
  date: '2007-12-10 09:11:44 +0100'
  date_gmt: '2007-12-10 08:11:44 +0100'
  content: "A co Appache commons? \r\n\r\nTo jsem netusil, ze prekladac se kouka na
    navratovy typ pri volani \r\nTo je sice elegantni, zajimave, da se to vyuzit i
    natlouct si nos.\r\n\r\n  public static  HashMap newHashMap() {\r\n    return
    new HashMap();\r\n  }\r\n\r\nDokonce zbastil i \r\n\r\nMap&lt;String, java.util.List&gt;
    mSL = newHashMap();\r\n java.util.List list1 = new java.util.ArrayList();\r\n
    list1.add( \"ahoj\");\r\n list1.add( \"nazdar\");\r\n mSL.put( \"prvni\", list1
    ) ;"
- id: 1155
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-12-10 11:05:54 +0100'
  date_gmt: '2007-12-10 10:05:54 +0100'
  content: No Google Collections se mi zdá, že na Apache Commons hodně ideově navazuje.
    Problém s Apache Commons je ten, že nejsou updatované pro generiky. Výše uvedený
    zápis kódu, který jsi poslal mi hlásí. "Unchecked assignment" - což je kompilační
    warning, který s Google collections nemám. Navíc právě to druhé co jsi napsal
    se dá elegantně řešit multimapou.
- id: 1156
  author: ZVrablik
  author_email: vrablik@gmail.com
  author_url: ''
  date: '2007-12-10 14:35:59 +0100'
  date_gmt: '2007-12-10 13:35:59 +0100'
  content: 'No a pokud pouzivate javu 1.4 muzete zkusit neco starsiho, ale docela
    dobre pracujiciho: http://pcj.sourceforge.net/'
- id: 1157
  author: alfonz
  author_email: shitmail@seznam.cz
  author_url: ''
  date: '2007-12-11 10:34:46 +0100'
  date_gmt: '2007-12-11 09:34:46 +0100'
  content: "\"Problém s Apache Commons je ten, že nejsou updatované pro generiky.\"
    ... http://collections15.sourceforge.net/\r\n\r\njinak některé věci jsou zajímavé,
    to rozhodně ano, ale zdá se mi že za některými je skryt příliš pomalý kód. Usnadnění
    vytváření kolekcí je super, ale nenapadá mne jak to udělat jinak než přes reflexi
    a to je prostě o dost pomalejší."
- id: 1158
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-12-11 10:49:40 +0100'
  date_gmt: '2007-12-11 09:49:40 +0100'
  content: "TO: alfonz\r\n\r\nNa odkazovaném linku jsem ani nenašel jak knihovnu pořádně
    stáhnout. Možná se to spíše konvertovalo na projekt: http://larvalabs.com/collections/\r\n\r\nKaždopádně,
    co se týká výkonnosti, dovolil bych si nesouhlasit ... schválně, tady je kód pro
    vytvoření generické mapy:\r\n\r\npublic static &lt;K, V&gt; HashMap&lt;K, V&gt;
    newHashMap() {\r\n    return new HashMap&lt;K, V&gt;();\r\n}\r\n\r\nZde žádnou
    reflection nevidím. Ani v multimapách a dalších věcech, když jsem procházel kódem,
    jsem na žádnou reflexi nenarazil. Na jedinou alchymii jsem narazil v ObjectArrays
    a to:\r\n\r\npublic static &lt;T&gt; T[] newArray(Class&lt;T&gt; type, int length)
    {\r\n    return (T[]) Array.newInstance(type, length);\r\n}\r\n\r\nkde pod Array.newInstance
    se skrývá:\r\n\r\nprivate static native Object newArray(Class componentType, int
    length)\r\n\tthrows NegativeArraySizeException;\r\n\r\nCož je už ale standardní
    Java používající nativní implementaci. Takže s druhou částí tvého tvrzení se mi
    nechce souhlasit."
- id: 1159
  author: Ladislav Thon
  author_email: ladicek@gmail.com
  author_url: ''
  date: '2007-12-11 12:08:53 +0100'
  date_gmt: '2007-12-11 11:08:53 +0100'
  content: "&gt; nenapadá mne jak to udělat jinak než přes reflexi\r\n\r\nTypová inference.\r\n\r\nMap&lt;Integer,
    StringBuffer&gt; bufferIndex = Maps.newHashMap();\r\n\r\nje úplně totéž, jako\r\n\r\nMap&lt;Integer,
    StringBuffer&gt; bufferIndex = Maps.&lt;Integer, StringBuffer&gt;newHashMap();\r\n\r\nakorát
    že typové parametry doplní překladač sám. U konstruktorů to bohužel takhle nefunguje
    (v Javě 7 na to nejspíš bude nějaká obezlička, kterou navrhuje Neal Gafter)."
- id: 1161
  author: alfonz
  author_email: shitmail@seznam.cz
  author_url: ''
  date: '2007-12-11 14:08:02 +0100'
  date_gmt: '2007-12-11 13:08:02 +0100'
  content: ok, pak se omlouvám, mám zjevně solidní mezery ve vzdělání. Má někdo nějakou
    doporučenou literaturu ohledně typové inference?
- id: 1162
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-12-11 17:43:31 +0100'
  date_gmt: '2007-12-11 16:43:31 +0100'
  content: "K typové inferenci jsem našel např. (pro mě je to také nový termín ;-)
    ):\r\nhttp://en.wikipedia.org/wiki/Type_inference"
- id: 1163
  author: Ladislav Thon
  author_email: ladicek@gmail.com
  author_url: ''
  date: '2007-12-11 18:02:30 +0100'
  date_gmt: '2007-12-11 17:02:30 +0100'
  content: 'Česky by se řeklo odvozování typů, takže spíš inference typů, ale víme,
    jak je to s češtinou u lidí z IT :-) Jinak ohledně odvozování typových parametrů
    konkrétně v Javě 5 a výš se dá něco dočíst třeba ve starém dobrém Generics FAQ:
    http://www.angelikalanger.com/GenericsFAQ/JavaGenericsFAQ.html#Type%20Argument%20Inference'
---
<p>Nedávno mě při poslechu <a href="http://www.javaposse.com/" target="_new">JavaPosse</a> zaujala zmínka o <a href="<br />
http://code.google.com/p/google-collections/" target="_new">Google Collections</a>. Jedná se o knihovnu doplňující funkcionalitu třídy Collections ze standardní Javy. Knihovna obsahuje řadu utility tříd, které zpříjemňují život s generikami v kolekcích, vytváření kolekcí v kolekcích a další manipulaci dat v kolekcích. Jelikož mě knihovna zaujala hned na první pohled, rozhodl jsem se podívat se jí na zoubek a podělit se s vámi o své zkušenosti.</p>
<p><a id="more"></a><a id="more-47"></a></p>
<h3>Zkrácení zápisu pro vytvoření nových kolekcí s generikami</h3>
<p>Jedná se možná o drobnost, ale natolik častou, že i drobné vylepšení přinese celkové zpřehlednění zápisu a zrychlení práce. V klasickém Java 1.5 kódu při vytváření generické kolekce typicky píšete např.:</p>
<p>[source lang="java"]<br />
Map<Integer, StringBuffer> bufferIndex<br />
          = new HashMap<Integer, StringBuffer>();<br />
[/source]</p>
<p>Na pravé straně deklarace tedy opakujete generickou informaci - a zbytečně - tato informace se dá přeci odvodit z levé strany přiřazení. Java bohužel tuto informaci vyžadujete, protože pokud byste zadali jednoduše new HashMap(), vytvoříte obyčejnou mapu bez informace o generikách a Java vás bude při kompilaci otravovat hlášením: <i>Unchecked assignment</i>.</p>
<p>Google collection obsahují řadu statických metod pro vytváření standardních kolekcí, které vás zbaví nutnosti opakovat informaci o generikách při vytváření těchto kolekcí. Stejnou mapu jako v předchozím příkladě vytvoříme napsáním:</p>
<p>[source lang="java"]<br />
Map<Integer, StringBuffer> bufferIndex = Maps.newHashMap();<br />
[/source]</p>
<p>Podobných metod je ve třídě Maps řada (namátkou třeba newLinkedHashMap, newConcurrentHashMap, newTreeMap). Podpora existuje nejen pro mapy, ale i pro další typy kolekcí:</p>
<ul>
<li><a href="http://google-collections.googlecode.com/svn/trunk/javadoc/com/google/common/collect/Maps.html" target="_new">Maps</a></li>
<li><a href="http://google-collections.googlecode.com/svn/trunk/javadoc/com/google/common/collect/Lists.html" target="_new">Lists</a></li>
<li><a href="http://google-collections.googlecode.com/svn/trunk/javadoc/com/google/common/collect/Sets.html" target="_new">Sets</a></li>
</ul>
<h3>Konverze polí objektů a primitivních typů</h3>
<p>Všichni známe třídu <a href="http://java.sun.com/j2se/1.5.0/docs/api/java/util/Arrays.html" target="_new">Arrays</a> ze standardní Javy. Ta sice obsahuje velmi užitečné funkce, ale zakrátko člověk zjistí, že si stejně řadu věcí neustále dopisuje sám. Jsou to drobnosti na tři řádky, ale stokrát nic umořilo osla. Google collections nabízí právě tyto drobnosti, které šetří práci.</p>
<h4>Práce s poli objektů</h4>
<p>Jednoduše je možné slučovat pole objektů. Dříve bylo nutné manipulovat s <i>System.arraycopy</i>  - díky knihovně je možné jednoduše zapsat:</p>
<p>[source lang="java"]<br />
Integer[] vysledek = ObjectArrays.concat(<br />
     new Integer[20],<br />
     new Integer[20],<br />
     Integer.class<br />
);<br />
[/source]</p>
<h4>Konverze polí na list a zpět</h4>
<p>Pracovat s poli v Javě má řadu výhod. Kód pro práci s nimi je velmi úsporný a přehledný. Pokud mám seznam objektů, který má být od počátku inicializován, rád používám čitelný zápis inicializace seznamu jako pole: </p>
<p>[source lang="java"]<br />
String[] data = new String[] {"jedna", "dvě", "tři"};<br />
[/source]</p>
<p>Pokud se ovšem stane, že do pole chci přidat další záznam, musím data vložit do listu, jehož inicializace je již na několik řádků a přehlednost se ztrácí. V google collections jsou metody, které tuto práci šetří a zvyšují tak subjektivní použitelnost polí jako takových:</p>
<p>[source lang="java"]<br />
List<Integer> listJakoPole =<br />
     PrimitiveArrays.asList(new int[] {1,2,3});<br />
int[] poleZListu =<br />
     PrimitiveArrays.toIntArray(listJakoPole);<br />
[/source]</p>
<p>Pokud by pro mě byla čitelnost zápisu pro vytvoření seznamu jediným měřítkem, vyplatí se mi použít jinou metodu z nabídky google collections:</p>
<p>[source lang="java"]<br />
List<Integer> poleCisel =<br />
     Lists.newLinkedList(1, 2, 3);<br />
[/source]</p>
<h3>Multimapy</h3>
<p>Snad každý z nás potřebuje a často vytváří mapy, které v hodnotách obsahují nikoliv jediný objekt, ale seznam objektů reprezentovaný např. ArrayListem. Já sám to programoval už asi stokrát - není to moc kódu, takže mě nikdy nenapadlo to přesunout do knihovny, ale zase se to používá tak často, že se to ve výsledku opravdu vyplatí. V daném případě musí totiž člověk ošetřit situaci vložení prvního objektu pod daným klíčem - list totiž neexistuje a proto je třeba vytvořit nejdříve list, do něj vložit prvek a teprve tento list vložit pod klíčem do mapy. V google collections lze jednoduše třebas takto:</p>
<p>[source lang="java"]<br />
ArrayListMultimap<Integer,String> listMultimap =<br />
     Multimaps.newArrayListMultimap();<br />
listMultimap.put(1, "ahoj");<br />
listMultimap.put(1, "ciao");<br />
List<String> greetings = listMultimap.get(1);<br />
[/source]</p>
<p>Výsledkem bude očekávaný list stringů obsahující ahoj a ciao. Google collections obsahují řadu implementací pro tyto Multimapy:</p>
<ul>
<li><a href="http://google-collections.googlecode.com/svn/trunk/javadoc/com/google/common/collect/ArrayListMultimap.html" target="_new">ArrayListMultimap</a></li>
<li><a href="http://google-collections.googlecode.com/svn/trunk/javadoc/com/google/common/collect/HashMultimap.html" target="_new">HashMultimap</a></li>
<li><a href="http://google-collections.googlecode.com/svn/trunk/javadoc/com/google/common/collect/LinkedHashMultimap.html" target="_new">LinkedHashMultimap</a></li>
<li><a href="http://google-collections.googlecode.com/svn/trunk/javadoc/com/google/common/collect/LinkedListMultimap.html" target="_new">LinkedListMultimap</a></li>
<li><a href="http://google-collections.googlecode.com/svn/trunk/javadoc/com/google/common/collect/TreeMultimap.html" target="_new">TreeMultimap</a></li>
<li><a href="http://google-collections.googlecode.com/svn/trunk/javadoc/com/google/common/collect/ForwardingMultimap.html" target="_new">ForwardingMultimap</a></li>
</ul>
<h3>Podpora pro Decorator pattern</h3>
<p>Google poskytuje základní implementace wrapperů nad standardními kolekcemi a iterátory. Zjednodušují tak práci pro implementaci decorator patternu. Stačí vám jen jednoduše podědit z těchto základních Forwarding class a přetížit konkrétní metody, jejichž chování si přejete změnit. Pro přístup k původnímu (backing) objektu slouží metoda delegate().</p>
<h3>Podmínky pro záznamy v kolekcích</h3>
<p>Tato podkapitolka a ta následující mi hodně připomíná použití Closures. Umožňuje jednoduše kontrolovat vkládání nových záznamů do kolekcí. Víte, že list vám umožňuje bez problémů vytvořít záznam s null hodnotou. To může vést k chybám, které nejsou na první pohled úplně patrné. S google collection se dá tomuto případu jednoduše zabránit:</p>
<p>[source lang="java"]<br />
List<Integer> list = Constraints.constrainedList(<br />
		new ArrayList<Integer>(), Constraints.NOT_NULL<br />
	);</p>
<p>Map<String, String> map = MapConstraints.constrainedMap(<br />
		new HashMap<String, String>, MapConstraints.NOT_NULL<br />
	);<br />
[/source]</p>
<p>Constrainty si samozřejmě můžete implementovat vlastní. Jsou aplikovány před vložením nového záznamu do kolekce a jednoduše tak můžete ohlídat hodnoty, které se v listu nachází. To podstatně zvyšuje míru důvěry, kterou takové kolekci ve svém kódu můžete dát.</p>
<h3>Filtrování hodnot v iterátoru</h3>
<p>Velmi elegantně a čitelně lze také filtrovat hodnoty, které poskytuje iterátor nad kolekcí.</p>
<p>[source lang="java"]<br />
import static com.google.common.base.Predicates.*;<br />
...</p>
<p>Iterator originalIterator;<br />
Iterator filteredIterator = Iterators.filter(<br />
		originalIterator,<br />
		not(isNull())<br />
);<br />
[/source]</p>
<p>Predikáty je možné slučovat pomocí and, or nebo negovat jako ve výše uvedeném příkladě. Predikáty je možné volně vytvářet. Čitelnost kódu je daleko lepší než ifování v iteraci. Nyní je predikát definován jako <a href="http://google-collections.googlecode.com/svn/trunk/javadoc/index.html?com/google/common/collect/ForwardingMultimap.html" target="_new">rozhranní s jedinou metodou</a> - ideální adept na zavedení closure.</p>
<p>Třída <a href="http://google-collections.googlecode.com/svn/trunk/javadoc/index.html?com/google/common/collect/ForwardingMultimap.html" target="_new">iterators</a> obsahuje řadu dalších užitečných metod:</p>
<ul>
<li><b>addAll(Collection<T> collection, Iterator<? extends T> iterator) </b> - vloží všechny prvky iterátoru do kolekce</li>
<li><b>all(Iterator<T> iterator, Predicate<? super T> predicate) </b> - vrátí true, pokud všechny prvky iterátoru odpovídají podmínce</li>
<li><b>any(Iterator<T> iterator, Predicate<? super T> predicate) </b> - vrátí true, pokud alespoň jeden prvek odpovídá podmínce</li>
<li><b>concat(....)</b> - různé metody pro slučování více iterátorů do jediného</li>
<li><b>find(Iterator<E> iterator, Predicate<? super E> predicate) </b> - vrátí první prvek iterátoru odpovídající podmínce</li>
<li>a další ;-) </li>
</ul>
<h3>Maven</h3>
<p>Bohužel knihovna není buildována Mavenem, takže si budete muset zajistit upload do vaší firemní repository sami. Pozitivní je, že nevyžaduje žádné další dependence, takže se jedná o velmi jednoduchou operaci.</p>
<h3>Závěrem</h3>
<p>Google collections je knihovna obsahující plno drobných vylepšení, funkcí a utilitek, bez kterých se sice obejdete, ale které vám mohou ušetřit plno řádků kódu (a to nemluvím o kódu testujících váš kód) a které mohou zásadně přispět k zpřehlednění kódu jako takového. Knihovnu využijete až od Javy 1.5, jelikož hlavní podpora je spojená právě s generikami. Knihovnu můžu jen doporučit a díky pánům z JavaPosse za dobrý tip a Googlu za open source.</p>
<p>BTW: nemáte někdo pár akcií na prodej? :-)</p>
<h3>Související odkazy</h3>
<ul>
<li><a href="http://www.infoq.com/news/2007/10/collections-api" target="_new">krátké shrnutí na InfoQ</a></li>
<li><a href="http://publicobject.com/2007/09/series-recap-coding-in-small-with.html" target="_new">velmi hezky provedený popis jednotlivých funkcí knihovny Google Collections</a></li>
</ul>
