---
status: publish
published: true
title: Beans introspection - základy Springu
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Je tomu už drahně let, co jsem používal k populaci JavaBean <a href=\"http://commons.apache.org/beanutils/\"
  target=\"_new\">Commons-BeanUtils z rodiny Apache Jakarta</a>. Od chvíle, kdy stavím
  svoje aplikace nad Springem, pozbývá používání této knihovny smysl - naopak bylo
  by bláhové se této knihovny držet, když Spring nabízí již ve svém základu mnohem
  víc. Prostým logickým úsudkem lze odvodit, že Spring coby IoC kontejner bude obsahovat
  promyšlenou logiku pro injektování dat do Java Bean. Nicméně v dokumentaci o tom
  najdete jen poměrně krátkou kapitolu <a href=\"http://static.springframework.org/spring/docs/2.5.x/reference/validation.html\"
  target=\"_new\">Validation</a>. Proto jsem se rozhodl vyextrahovat ze svého kódu
  pár příkladů, které standardní Spring dokumentaci trochu rozvádí do podrobností.\r\n\r\n"
wordpress_id: 76
wordpress_url: http://blog.novoj.net/2008/08/10/beans-introspection-zaklady-springu/
date: '2008-08-10 18:40:22 +0200'
date_gmt: '2008-08-10 17:40:22 +0200'
categories:
- Programování
- Java
- Spring Framework
tags: []
comments: []
---
<p>Je tomu už drahně let, co jsem používal k populaci JavaBean <a href="http://commons.apache.org/beanutils/" target="_new">Commons-BeanUtils z rodiny Apache Jakarta</a>. Od chvíle, kdy stavím svoje aplikace nad Springem, pozbývá používání této knihovny smysl - naopak bylo by bláhové se této knihovny držet, když Spring nabízí již ve svém základu mnohem víc. Prostým logickým úsudkem lze odvodit, že Spring coby IoC kontejner bude obsahovat promyšlenou logiku pro injektování dat do Java Bean. Nicméně v dokumentaci o tom najdete jen poměrně krátkou kapitolu <a href="http://static.springframework.org/spring/docs/2.5.x/reference/validation.html" target="_new">Validation</a>. Proto jsem se rozhodl vyextrahovat ze svého kódu pár příkladů, které standardní Spring dokumentaci trochu rozvádí do podrobností.</p>
<p><a id="more"></a><a id="more-76"></a></p>
<h3>BeanWrapper</h3>
<p>Pro jednoduchou populaci dat do JavaBean je možné použít BeanWrapper - respektive BeanWrapperImpl jako jeho jedinou implementaci. S pomocí tohoto objektu je možné jednoduše do jakéhokoliv objektu dodržujícího pravidla JavaBean nasetovat property, nebo jeho property číst. Tyto operace lze předvést jednoduše na následujícím příkladě (<a href="#download">kompletní zdrojové kódy lze stáhnout na konci článku</a>):</p>
<p>[source lang="java"]<br />
//create custom pojo instance<br />
User myJavaBean = new User();<br />
//create wrapper<br />
BeanWrapper wrapper = new BeanWrapperImpl(myJavaBean);</p>
<p>//use simple population<br />
wrapper.setPropertyValue("login", "novoj");<br />
wrapper.setPropertyValue("password", "heslo");<br />
//check it<br />
assertEquals("novoj", myJavaBean.getLogin());<br />
assertEquals("heslo", myJavaBean.getPassword());</p>
<p>//use collected values population<br />
MutablePropertyValues pvs = new MutablePropertyValues();<br />
pvs.addPropertyValue("address.street", "U řeky 1");<br />
pvs.addPropertyValue("address.town", "Královec");<br />
pvs.addPropertyValue("address.country", "Česká republika");<br />
wrapper.setPropertyValues(pvs);<br />
//check it<br />
assertEquals("U řeky 1", myJavaBean.getAddress().getStreet());<br />
assertEquals("Královec", myJavaBean.getAddress().getTown());<br />
assertEquals("Česká republika", myJavaBean.getAddress().getCountry());</p>
<p>//populate list data<br />
wrapper.setPropertyValue("tags[0]", "redTeam");<br />
wrapper.setPropertyValue("tags[1]", "management");<br />
//check it<br />
assertTrue(myJavaBean.getTags().contains("redTeam"));<br />
assertTrue(myJavaBean.getTags().contains("management"));</p>
<p>//populate even map properties<br />
wrapper.setPropertyValue("properties[blogger]", Boolean.FALSE);<br />
wrapper.setPropertyValue("properties[degree]", "university");<br />
//check it<br />
assertEquals(Boolean.FALSE, myJavaBean.getProperties().get("blogger"));<br />
assertEquals("university", myJavaBean.getProperties().get("degree"));</p>
<p>//let's look at more difficult types - PropertyEditors come handy<br />
wrapper.setPropertyValue("email", "Otec Fura (novotnaci@gmail.com)");<br />
//check it<br />
assertEquals("Otec Fura", myJavaBean.getEmail().getName());<br />
assertEquals("novotnaci@gmail.com", myJavaBean.getEmail().getAddress());</p>
<p>//will throw exception<br />
try {<br />
   wrapper.setPropertyValue("notExistingProperty", "doesn't matter");<br />
   fail("Exception expected!");<br />
} catch(BeansException ex) {<br />
   //that is ok<br />
}<br />
[/source]</p>
<p>Jedinou instanci BeanWrapperu je možné použít pro populaci libovolného počtu různých java bean - beanwrapper si nedrží žádné stavové údaje, které by ho vázaly k jediné JavaBeaně. Údaje je možné setovat jednotlivě nebo více naráz (pomocí PropertyValues). Dále je možné nasetovat data do kolekcí - stačí mít getter vracející instanci kolekce (pozor kolekce musí existovat - instanci nemůže wrapper vytvořit sám protože nezná konkrétní implementaci) a o zbytek se již postará Spring sám. Obdobně funguje populace do mapy - opět stačí mít getter vracející instanci java.util.Map (opět je třeba zajistit aby se nevrátila null hodnota).</p>
<p>Tuto funkcionalitu jste schopni dosáhnout i s pomocí Commons-BeanUtils. Co je však v případě Commons-BeanUtils nepříjemné je ten fakt, že při práci s indexovanými nebo map property vyžadují specifické deklarace metod (např. public void setIndexedProperty(int index, Object value); nebo public void setMapProperty(String key, Object value);). Spring dokáže pracovat se standardními gettery vracejícími Collection nebo Mapu.</p>
<p>Kromě populace můžete samozřejmě použít BeanWrapper i k zjištění informací o JavaBean - nicméně tím se v tomto článku nechci zabývat.</p>
<p>Dosud v článku nezaznělo nic extra zajímavého - vydržte a čtěte dál, teprve začínáme ;-)</p>
<h3>DataBinder - hrajeme si s chybovými hlášeními</h3>
<p>DataBinder se vám bude hodit v případě, že máte hrst neznámých dat, které chcete napopulovat do vaší JavaBean. Strukturu své JavaBean a její omezení / pravidla znáte - nicméně netušíte, co se může nacházet ve vstupních datech. Při použití BeanWrapperu byste brzy narazili na nějakou exception (např. pokud by se ve vstupních datech nacházela položka, ke které by v JavaBean nebyla odpovídající property nebo pokud by se nepodařila konverze na cílový typ). Opracování těchto stavů byste si museli zajišťovat sami a bylo by to poměrně dost kódování.</p>
<p>Pro tento usecase poskytuje Spring třídu DataBinder. Tato chytrá třída vám jednoduše umožní:</p>
<ul>
<li>ignorovat hodnoty, pro které nemá JavaBean odpovídající settery (<i>setIgnoreUnknownFields(true)</i>)</li>
<li>ignorovat hodnoty, které nelze napopulovat z důvodu null hodnot v property (např. u indexovaných nebo map property, kdy getter vrací null) (<i>setIgnoreInvalidFields(true)</i>)</li>
<li>nastavit property, jejichž hodnota nesmí být změněna i kdyby ve vstupních hodnotách byla odpovídající položka (<i>setDisallowedFields(seznam property)</i>)</li>
<li>nastavit property, které musí být ze vstupních hodnot napopulovány (<i>setRequiredFields(seznam property)</i>)</li>
<li>zjistit chyby, ke kterým při populaci došlo a odpovídajícím způsobem je zobrazit uživateli</li>
</ul>
<p>Uvedené vlastnosti jsou předvedeny v následujícím příkladě:</p>
<p>[source lang="java"]<br />
//create custom pojo instance<br />
User myJavaBean = new User();<br />
myJavaBean.setLogin("novoj");<br />
myJavaBean.setPassword("password");<br />
myJavaBean.setEmail(new EmailAddress("novotnaci@gmail.com", "Otec Fura"));<br />
myJavaBean.setProperty("degree", "high school");<br />
myJavaBean.setProperty("blogger", Boolean.TRUE);<br />
//create data binder<br />
DataBinder binder = new DataBinder(myJavaBean);<br />
binder.setIgnoreUnknownFields(true);<br />
binder.setIgnoreInvalidFields(false);<br />
binder.setDisallowedFields(new String[] {"login", "address.*"});<br />
binder.setRequiredFields(new String[] {"password", "properties[degree]"});<br />
//create input values map<br />
MutablePropertyValues pvs = new MutablePropertyValues();<br />
//will be ignored - is in disallowed fields<br />
pvs.addPropertyValue("login", "newLogin");<br />
//will be populated<br />
pvs.addPropertyValue("password", "newPassword");<br />
//would trigger exception if ignoreUnknownfields == false<br />
pvs.addPropertyValue("nonExistingField", "doesn't matter");<br />
//will result in error in binding ressult<br />
pvs.addPropertyValue("email", Boolean.FALSE);<br />
//will result in required error in result if commented out<br />
//pvs.addPropertyValue("properties[degree]", "university");<br />
//bind values at one single shot<br />
binder.bind(pvs);<br />
//check errors<br />
BindingResult result = binder.getBindingResult();<br />
assertEquals(2, result.getErrorCount());<br />
assertEquals("novoj", myJavaBean.getLogin());<br />
assertEquals("newPassword", myJavaBean.getPassword());<br />
assertEquals("Otec Fura", myJavaBean.getEmail().getName());<br />
assertEquals("novotnaci@gmail.com", myJavaBean.getEmail().getAddress());<br />
assertEquals("high school", myJavaBean.getProperties().get("degree"));<br />
[/source]</p>
<p>Při populaci (bind) z DataBinderu nikdy nevyletí vyjímka. Při problematických situacích DataBinder vytváří chybové hlášky, které lze po skončení populace získat pomocí binder.getBindingResult(). V tomto objektu jsou potom dostupné instance <a href="http://static.springframework.org/spring/docs/2.0.x/api/org/springframework/context/MessageSourceResolvable.html" target="_new">MessageSourceResolvable</a> reprezentující vzniklé chyby. Strategii tvorby chyb lze poměrně detailně ovlivnit (pokud byste to vůbec potřebovali) nastavením implementací rozhraní <a href="http://static.springframework.org/spring/docs/2.0.x/api/org/springframework/validation/MessageCodesResolver.html" target="_new">MessageCodesResolver</a> a <a href="http://static.springframework.org/spring/docs/2.0.x/api/org/springframework/validation/BindingErrorProcessor.html" target="_new">BindingErrorProcessor</a>.</p>
<p>Tato třída je používána především ve Spring-MVC části Springu, nicméně i v případě, že pro webovou vrstvu využíváte jiné frameworky (my například Stripes), narazíte na řadu use-case, kdy se vám možnost populace libovolných dat do libovolné JavaBeany s detailní kontrolou nad tímto procesem může hodit. V našem případě to je například při načítání konfigurace aplikace z konfiguračních souborů.</p>
<p>Tuto funkcionalitu budete v Commons-BeanUtils těžko hledat.</p>
<h3>PropertyEditor - hrajeme si s daty</h3>
<p>Co činí BeanWrapper / DataBinder zajímavějším, je možnost populovat do typových property (např. Integer, Boolean) řetězcové hodnoty (String). Spring k tomu využívá tzv. PropertyEditory, které jsou v původním standardu JavaBean. Pokud je setovaná hodnota String a odlišuje se od typu požadovaného setterem, pokusí se Spring najít odpovídající PropertyEditor, který by k jejímu převodu mohl použít. Více o PropertyEditorech se dozvíte buď <a href="http://static.springframework.org/spring/docs/2.5.x/reference/validation.html" target="_new">v dokumentaci Springu</a>, nebo <a href="http://vavru.cz/java/property-editory-ve-spring-frameworku/" target="_new">v článku českého bloggera Vlasty Vávrů</a>.</p>
<p>Principy jsou v obou odkazovaných dokumentech popsány poměrně podrobně a proto je tu nebudu opakovat. Co bych však chtěl zdůraznit je to, že přestože je možné Springu říci, pro jaký typ má použít jaký PropertyEditor, existuje i jednodušší cesta. Stačí implementaci PropertyEditoru umístit do stejné package jako je deklarace původního objektu, který property editor konvertuje (dále je nutné zachovat základ názvu class a přidat na konec slůvko "Editor"). Takové editory budou Springem nalezeny automaticky, aniž bychom museli kdekoliv cokoliv registrovat. Je to, řekl bych, nejjednodušší způsob, jak PropertyEditory zavádět. Pro vytváření nových PropertyEditorů využijte Spring předka PropertyEditorSupport, který vám ušetří mnoho práce.</p>
<p>V Commons-BeanUtils podobný problém řeší tzv. <a href="http://commons.apache.org/beanutils/v1.8.0-BETA/apidocs/org/apache/commons/beanutils/Converter.html" target="_new">Convertory</a>.</p>
<h3>ResourceLoader - řekněte Springu ke má co hledat</h3>
<p>A v poslední kapitolce bych chtěl naťuknout ResourceLoadery ve Springu. Je to věc, která by možná zasloužila vlastní příspěvek, ale vezmu to letem světem. <a href="v" target="_new">ResourceLoader</a> je abstrakce Springu, která se stará o vytvoření instancí implementací rozhraní <a href="http://static.springframework.org/spring/docs/2.0.x/api/org/springframework/core/io/Resource.html" target="_new">Resource</a>, které je další abstrakcí Springu nad libovolnými binárními zdroji. Zni to složitě ale princip je báječně jednoduchý. Rozhraní Resource jsme adoptovali do našich projektů a osobně si tento krok nemůžu vynachválit. Resource se svým charakterem podobá třídě <a href="http://java.sun.com/javase/6/docs/api/java/io/File.html" target="_new">java.io.File</a> - je nezávislá na existenci zdroje, na který se odkazuje, umožňuje získat InputStream a konverzi na URL. Resource může však reprezentovat libovolný objekt binárního charakteru, java.io.File rozhraní se k tomu už příliš nehodí. V našem CMS systému používáme kromě standardních Spring resource implementací také vlasní implementace reprezentující soubory uložené v databázi a virtuálních úložištích.</p>
<p>ResourceLoader umožňuje Springu převést cestu (ve formátu String) na výslednou Resource implementaci. Ve většině případů si asi vystačíte se standardním ResourceLoaderem (<a href="http://static.springframework.org/spring/docs/2.0.x/api/org/springframework/core/io/DefaultResourceLoader.html" target="_new">DefaultResouceLoader</a>, který vám umožní zpřístupnit zdroje na classpath, filesystému a síti).</p>
<p>Pokud byste však chtěli vytvořit vlastní abstrakci pro umístění resourců, není problém vytvořit si vlastní ResourceLoader nebo i implementaci Resource rozhranní. V následujícím příkladě si vytvoříme specializovaný ResourceLoader, který bude rozeznávat "protokol" corpWeb, který bude hledat zdroje na web stránkách naší společnosti. V rámci "protokolu" se již budeme odkazovat relativně. Takováto jednoduchá implementace může vypadat následovně:</p>
<p>[source lang="java"]<br />
/**<br />
 * Custom resource loader - remember, you can have also your custom Resource types. This is our aim.<br />
 *<br />
 * @author Jan Novotný<br />
 * @version $Id: $<br />
 */<br />
public class CustomResourceLoader extends DefaultResourceLoader {<br />
	private static final String CORP_WEB_PREFIX = "corpWeb:";</p>
<p>	public Resource getResource(String location) {<br />
		if (location.startsWith(CORP_WEB_PREFIX)) {<br />
			try {<br />
				return new UrlResource(new URL("http", "www.fg.cz", location.substring(CORP_WEB_PREFIX.length())));<br />
			}<br />
			catch(MalformedURLException e) {<br />
				return super.getResource(location);<br />
			}<br />
		} else {<br />
			return super.getResource(location);<br />
		}<br />
	}<br />
}<br />
[/source]</p>
<p>Použití vlastní instance ResourceLoaderu v kombinaci s BeanWrapperem (obdobně i DataBinderem) je velmi přímočará. Následující test nám potvrzuje předpokládané chování. V první části testu použijeme standardní Spring DefaultResourceLoader. Ten sice vytvoří jakousi instanci Resource (konkrétně ClassPathResource), ale ta samozřejmě nebude odkazovat na existující zdroj, protože na classpath takový zdroj není. Pokud zaregistrujeme vlastní ResourceLoader (druhá část testu), vrátí se naprosto jiná implementace Resource rozhraní, která již dokáže najít existující zdroj dat.</p>
<p>[source lang="java"]<br />
//create custom pojo instance<br />
User myJavaBean = new User();<br />
//create wrapper<br />
BeanWrapper wrapper = new BeanWrapperImpl(myJavaBean);<br />
//bind custom resource<br />
wrapper.setPropertyValue("photo", "corpWeb:/img/u/logo_title.gif");<br />
//because default resource editor doesn't know corpWeb<br />
//location handling it will use classpath resource<br />
assertNotNull(myJavaBean.getPhoto());<br />
//that mean, that such resource won't be accessible<br />
assertFalse(myJavaBean.getPhoto().exists());</p>
<p>//but when we register custom resource loader being able to<br />
//process corpWeb location situation changes<br />
wrapper.registerCustomEditor(<br />
   Resource.class,<br />
   new ResourceEditor(<br />
      new CustomResourceLoader()<br />
   )<br />
);<br />
//bind custom resource<br />
wrapper.setPropertyValue("photo", "corpWeb:/img/u/logo_title.gif");<br />
//check that photo exists<br />
assertNotNull(myJavaBean.getPhoto());<br />
assertTrue(myJavaBean.getPhoto().exists());<br />
[/source]</p>
<p>ResourceLoader je základním konceptem celého Springu. Zde si z něj ukazujeme jen malou část - jednoduché použití, které je však součástí nejužšího jádra Spring Frameworku.</p>
<h3><a name="download">Závěrem</a></h3>
<p>V článku srovnávám Spring především s Commons-BeanUtils. Jsem si vědom toho, že populačních knihoven je velká spousta - namátkou mohu zmínit např. <a href="http://www.ognl.org/" target="_new">OGNL</a>, která je používána frameworkem Struts 2 (a o které se také proslýchá, že není z nejrychlejších ;-) ). Přidržel jsem se však toho, co detailně znám a nechtěl jsem se pouštět do srovnávání s knihovnami, o kterých jsem si pouze něco přečetl. Pokud budete mít zajímavé postřehy z použití konkurenčních řešení, neváhejte a pište své komentáře.</p>
<p><a href="http://files.novoj.net/SpringIntrospection/SpringIntrospection.zip ">Kompletní zdrojové kódy lze stáhnout zde.</a></p>
<p><strong>Pozn.:</strong> pokud programujete web aplikaci, nezapomeňte do web.xml přidat deklaraci listeneru <a href="http://static.springframework.org/spring/docs/2.0.x/api/org/springframework/web/util/IntrospectorCleanupListener.html" target="_new">IntrospectorCleanupListener</a> (viz. dovětky k článku <a href="http://blog.novoj.net/2008/04/11/permgenspace-problem-no-problem/">PermGenSpace problem? No problem!</a>)</p>
