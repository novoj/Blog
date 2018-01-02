---
status: publish
published: true
title: Spring One - závěrečný den
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Dnes se mi podařilo vychytat velmi dobré přednášky, takže jsem si po včerejším
  dm Serveru rozhodně spravil chuť. První dnešní přednášky se týkala Groovy a především
  novinek ve verzi 1.6. Zprvu se zdálo, že Guillame pojede pouze po povrchu Groovy,
  ale brzy se přednáška rozjela, takže si z ní člověk nakonec odnesl opravdu hodně.
  Přednáška stavěla na publikovaném článku o <a href=\"http://www.infoq.com/articles/groovy-1-6\"
  target=\"_new\">Grovy 1.6 na InfoQ</a>. Groovy by ve verzi 1.6 mělo být výrazně
  rychlejší (různé micro benchmarky ukazují zlepšení výkonnosti od 150% do 430%),
  díky hotspotu dle Guillama dokonce předběhnou některé jiné dynamické jazyky mimo
  JVM platformu (konkrétně zmiňoval Ruby). Groovy běží bez problémů na GAP - dokonce
  je tam k vyzkoušení volně dostupná <a href=\"http://groovyconsole.appspot.com\"
  target=\"_blank\">Groovy konzole</a>. Rozvoj Groovy jede raketovou rychlostí, řekl
  bych že věci, které tam jsou, v Javě neuvidíme ještě léta a kdo ví jestli vůbec
  (closures, tuples, properties, statická inicializace properties v rámci konstruktoru).
  Jediné co nám brání dosud ve firmě nasadit Groovy, je zajištění aby groovy instance
  vytvořené Springem a naše vlastní instance nad společným Groovy classoaderem sdílely
  podobné rekompilační chování jako nabízí GroovyScriptingEngine. Groovy je ale rozhodně
  směr, kterým se chceme ubírat.\r\n\r\n"
wordpress_id: 468
wordpress_url: http://blog.novoj.net/?p=468
date: '2009-04-29 23:47:04 +0200'
date_gmt: '2009-04-29 22:47:04 +0200'
categories:
- Java
- Spring Framework
- Reportáže
tags:
- SpringOne
comments: []
---
<p>Dnes se mi podařilo vychytat velmi dobré přednášky, takže jsem si po včerejším dm Serveru rozhodně spravil chuť. První dnešní přednášky se týkala Groovy a především novinek ve verzi 1.6. Zprvu se zdálo, že Guillame pojede pouze po povrchu Groovy, ale brzy se přednáška rozjela, takže si z ní člověk nakonec odnesl opravdu hodně. Přednáška stavěla na publikovaném článku o <a href="http://www.infoq.com/articles/groovy-1-6" target="_new">Grovy 1.6 na InfoQ</a>. Groovy by ve verzi 1.6 mělo být výrazně rychlejší (různé micro benchmarky ukazují zlepšení výkonnosti od 150% do 430%), díky hotspotu dle Guillama dokonce předběhnou některé jiné dynamické jazyky mimo JVM platformu (konkrétně zmiňoval Ruby). Groovy běží bez problémů na GAP - dokonce je tam k vyzkoušení volně dostupná <a href="http://groovyconsole.appspot.com" target="_blank">Groovy konzole</a>. Rozvoj Groovy jede raketovou rychlostí, řekl bych že věci, které tam jsou, v Javě neuvidíme ještě léta a kdo ví jestli vůbec (closures, tuples, properties, statická inicializace properties v rámci konstruktoru). Jediné co nám brání dosud ve firmě nasadit Groovy, je zajištění aby groovy instance vytvořené Springem a naše vlastní instance nad společným Groovy classoaderem sdílely podobné rekompilační chování jako nabízí GroovyScriptingEngine. Groovy je ale rozhodně směr, kterým se chceme ubírat.</p>
<p><a id="more"></a><a id="more-468"></a></p>
<p>Další přednáška, která na Groovy volně navazovala, byly DSL jazyky na Groovy základu. Opět přednášel Guillame a jednalo se spíše o úvod do celé problematiky. Výhody vlastních jazyků byly z přednášky jednoduše patrné - při srovnávání ekvivalentního zápisu business pravidel v Javě a Groovy, Groovy jasně výtězilo v čitelnosti a hutnosti kódu. Krom jiného, je možné zapsaný kód okamžitě testovat v konzoli. Do druhé poloviny přednášky Guillame zařadil výklad konstruktů, které nám pro návrh vlastních DSL jazyků Groovy nabízí:</p>
<ul>
<li>možnost psát skripty bez nutnosti deklarace obalujících tříd (Groovy kompilátor provede na pozadí)</li>
<li>nepovinné typování - lze volně vypouštět práci s typy i generikami</li>
<li>jednoduchý a čitelný nativní zápis polí, listů a map</li>
<li>nepovinné závorky a středníky</li>
<li>pojmenované argumenty</li>
<li>používání BigDecimal jako defaultního typu pro numerické hodnoty</li>
<li>closures</li>
<li>přetěžování operátorů</li>
<li>MetaObjectProtocol - možnost přímé modifikace stínových metaclass každého objektu (i finálních tříd z package java.*), definice tzv. Category platných pro omezenou scope, interceptory nad voláním metod (např. pro reakci na volání na metody, která neexistuje - což je princip, na kterém jsou postavené Groovy buildery)</li>
<li>compile time metaprogramming - přímá modifikace AST kompilovaného programu s využitím anotací @GroovyASTTransformation a @GroovyASTTransformationClass</li>
</ul>
<p>Možností nabízí Groovy přehršel - kámen úrazu však tkví ve správném návrhu nového DSL jazyka. V tomto ohledu Guillame dal několik rad ze své praxe (mj. také zmínil jaké různé DSL jazyky pomáhal nad Groovy navrhovat):</p>
<ul>
<li>začněte s v malém měřítku, se nosnými konstrukty / konceptem jazyka</li>
<li>nepoužívejte za každou cenu hned nejtěžší kalibr technických možností, které vám Groovy dává - řada věcí se dá vyřešit základními vlastnosti Groovy - pro použití AST transformací byste měli mít pádný důvod</li>
<li>budujte svůj jazyk postupně, začněte tím, co vám přináší největší užitek (pravidlo 20 / 80)</li>
<li>jezte to, co jste si uvařili - používejte jazyk společně s uživateli, ať vidíte jak dobře se jazyk používá</li>
<li>nesvazujte jazyk zbytečně - jazyk nepatří vám, ale uživatelům, kteří s ním budou pracovat</li>
<li>dělejte krátké iterace, abyste co nejdřív získali zpětnou vazbu</li>
<li>buďte trpěliví - počítejte s tím, že to na první pokus neuděláte správně</li>
<li>novinky testujte v sand boxu, nové vlastnosti publikujte až ve chvíli, kdy už máte nějakou zkušenost</li>
<li>testujte, testujte, testujte</li>
<li>testujte důkladně i chybové chování a soustřeďte se na smysluplné a návodné chybové hlášení - ty jsou pro uživatele jazyka velmi důležité</li>
</ul>
<p>Další zajímavá přednáška byla od Bena Alexe (tvůrce Acegi / Spring Security) o nové verzi Spring Security 2.5, která by měla být uvolněna spolu se Springem 3.0. Z předváděných příkladů bylo hezky vidět jakou cestu urazila Spring Security od doby, kdy se ještě nazývala Acegi. Konfigurace je teď velmi krátká a přehledná, díky možnostem, které nabízejí Spring namespacy. Má implementované takové drobnosti jako defaultní login page, pokud žádnou specielně nenakonfigurujete. Security nabízí v současné době také velkou škálu autentizačních protokolů (JA-SIG CAS, NTLM, OpenId, Attlassian Crowd, JAAS atd.). Velmi pěkná je také integrace s LDAP serverem s využitím projektu Spring LDAP, o kterém jsem dosud neměl ani tušení. Výborná byla ukázka techniky zvané Request Forgery, o které řada lidí neví - a ti co o ní ví zase většinou netuší, jak je triviální. V tomto ohledu Spring Security nabízí také možnost ochránit konkrétní URL patterny proti přístupu jinou HTTP metodou než např. POST (což v původním Acegi ještě nešlo, nebo o tom nevím).</p>
<p>Velmi zajímavá byla část o autorizaci na úrovni volání metod. Toto, pokud vím, bylo ve verzi Acegi, kterou používáme my, teprve ve fázi prototypu. Nyní je to již dotažené do konce a Spring Security nabízí plnohodnoté řešení i na této úrovni. Securita je implementována (jak jinak) pomocí AOP, takže použití je velmi triviální. Security constrainty je možné definovat různě - buď je možné využít anotací z JSR250, deklarativního zápisu v XML konfiguraci nebo specifických anotací Springu @PreAuthorize, @PostAuthorize, @PreFilter, @PostFilter, které budou podporovat Spring EL a díky tomu budou velmi mocné. Velmi mě například zaujmul zápis:</p>
<p>[source lang="java"]<br />
@PreAuthorize('hasRole('ROLE_DIRECTOR') or (hasRole('ROLE_USER') and (#account.balance < 1000))')<br />
public void wihtdrawFromAccount(BigDecimal amount) {<br />
   //do something<br />
}<br />
[/source]</p>
<p>Ten a) způsobí, že pokud nepřihlášený uživatel provede operaci, které znamená vykonání této metody bude vynuceno přihlášení b) pokud má uživatel pouze roli ROLE_USER bude mu povoleno vyvolání metody pouze v případě, že getter getBalance beany Account vrátí hodnotu menší než 1000. Na příkladě je hezky vidět, jak silný muže být Spring EL.</p>
<p>Nenechal jsem si také ujít přednášku o Spring JavaScript projektu, který se na první pohled zdál velmi lákavý. Přestože autoři na začátku tvrdili, že do budoucna budou podporovány i jiné JS frameworky krom DOJO, zdálo se mi, že knihovna je s DOJO poměrně těsně svázaná. Nicméně Jeremy Grelle zmínil, že na JS framework jQuery se jej ptalo už tolik lidí, že s tím pravděpodobně budou muset něco udělat :-) Knihovna v některých částech nabízí i podporu na straně serveru - ta je ale pouze na úrovni Spring MVC frameworku, takže při používání jiných web frameworků by bylo použití funkcionalit jako je partial update pravděpodobně (obtížně?!) nepoužitelné (pro partial update jsou navíc podporovány pouze kombinace JSP/Tiles a JSF/Facelets). Při integraci do templatovacího jazyka je nutné dodat i poměrně hutnou dodatečnou konfiguraci dekorátorů v Javacriptu, což je jistě ve větším měřítku nepříjemné (na druhou stranu si dokážu představit specielní JSP tagy, které by toto mohly překrýt). Knihovna staví na pravidlech Graceful degradation - tzn. aplikace funguje bez javascriptu, ten však dodává přítulnější rozhranní vůči uživateli. Velmi zajímavé jsou nápady na vyhodnocení redirectu poslaného v rámci AJAX odpovědi (to samozřejmě prohlížeč neovlivní, takže se klientský kód musí postarat o "forward redirectu"), nebo možnost zobrazit odpověď partial updatu v popup okně. Při psaní bohatého GUI s využitím složitějších DOJO widgetů přijde vhod možnost lazy loadingu částí JSON objektů, které v kombinaci s Hibernate lazy loadingem, mohou přinést zajímavou úsporu práce při práci se složitými objektovými stromy.</p>
<p>Valnou část poslední přednášky jsem už nestihl, protože jsme musel spěchat na letiště. A zrovna tohle mne velmi mrzí, jelikož to byla přednáška Jorise Kuiperse o AOP. Osobně mám s AOP zkušenosti, ale pouze s nejjednodušší formou Spring Proxy. Joris v přednášce živě přednášel použití AspectJ, jeho dopady a výhody. Migraci ze Spring Proxy na AspectJ, load time weaving a řadu zajímavých věcí.  Je velká škoda, že organizátoři konference neumístili tuto přednášku v dříve.</p>
<p>Co říci závěrem? Snad jen poděkovat lidem ze SpringSource a Trifolku za svěle připravenou konferenci, které se, kromě prachbídné kvality připojení na Internet, nedalo vytknout snad nic. Amsterdam není pro Čecha zrovna levné město, ale Spring One za to určitě stál.</p>
<p>Doufám, že vám budou (alespoň zprostředkovaně) některé informace taky k užitku. A díky všem co reagovali na mé živé tweetování online z přednáškových sálů. Byl to poměrně zajímavý pocit, sledovat <a href="http://search.twitter.com/search?q=springone" target="_blank">agregovaně</a>, jak řada developerů tweetovala své pocity známým do různých koutů světa. Zdá se mi, že skutečně nadešla doba, kdy sdělovacími prostředky a zdrojem informací může být kdokoliv, i ten nejmenší developřík z vesničky uprostřed Evropy ...</p>
