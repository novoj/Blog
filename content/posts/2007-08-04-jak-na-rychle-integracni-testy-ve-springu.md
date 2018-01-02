---
status: publish
published: true
title: Jak na rychlé integrační testy ve Springu
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Integrační testy spočívají v testování konkrétní kódu spolu s okolními částmi,
  se kterými spolupracuje. Cílem je snaha otestovat kód ve stavu, který se blíží reálnému
  nasazení. Obvykle takto testujeme datovou vrstvu aplikace (jelikož tam klasické
  jednotkové testy ztrácejí smysl - chceme přeci otestovat správné dotazování databáze,
  tudíž databázi k testu potřebujeme) a v řadě případů se nám nevyplatí <a href=\"http://blog.novoj.net/2007/01/19/mock-testing-potemkinovy-vesnice/\"
  target=\"_new\">mockovat</a> ani na úrovni business vrstvy. Dokonce i <a href=\"http://www.infoq.com/presentations/system-integration-testing-with-spring\"
  target=\"_new\">Rod Johnson ve své prezentaci</a> (kterou byl inspirován tento článek)
  zdůrazňuje důležitost integračních testů.\r\n\r\nHlavní problém integračních testů,
  u kterých máte ve spodu relační databázi je rychlost. Každý test spoléhá na nějaká
  data v DB - ty mohou být (a jsou) ostatními testy poškozena a proto je nedílnou
  částí všech testů setUp / tearDown operace, která se o tuto přípravu a uklizení
  stará. Jelikož jsou programátoři cháska líná a nechtějí se zabývat přípravou pouze
  minimální potřebné sady pro každý test, obvykle si vytvoří nějakého předka, který
  obsahuje setUp a tearDown, pro všechny testy najednou. Tím pádem se vždycky inicializuje
  kompletní sada dat a to si bere významné množství času. Odhadoval bych, že 80% času
  testů se stráví v této přípravě dat a pouze 20% času běží skutečné testy.\r\n\r\n"
wordpress_id: 28
wordpress_url: http://blog.novoj.net/2007/08/04/jak-na-rychle-integracni-testy-ve-springu/
date: '2007-08-04 11:53:38 +0200'
date_gmt: '2007-08-04 10:53:38 +0200'
categories:
- Java
- Testování
- Spring Framework
tags: []
comments:
- id: 322
  author: Roman Dagi Pichlik
  author_email: pichlik@seznam.cz
  author_url: http://www.sweb.cz/pichlik/
  date: '2007-08-07 07:54:39 +0200'
  date_gmt: '2007-08-07 06:54:39 +0200'
  content: Pristup s rollbacknutim transakce rozjete v testu ma jeste jednu vyhodu
    a to, ze je mozne diky defaultni izolaci transakce bezet vice konkurentnich testu
    nad jednou databazi a to aniz by se testy ovlivnily. Pokud test potrebuje udelat
    neco, co zmeni trvale stav databaze a tudiz by doslo k nekonzistenci dat, tak
    by nebylo spatne poskytnout v tom predkovi kompenzacni metodu, ktera by to vratila
    do puvodniho stavu. Predek by ji jednak volal a jednak sam implementoval jako
    prazdnou, potomek by mohl v pripade potreby dodat patricne chovani.
- id: 324
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-08-07 10:44:20 +0200'
  date_gmt: '2007-08-07 09:44:20 +0200'
  content: "No to je přesně to, co dělá AbstractDatabaseSpringTestCase (se základní
    implementací v AbstractProjectDatabaseTestCase), jehož kód jsem uvedl v článku.
    Test v takovém případě buď \r\n\r\na) změní počty řádků v tabulkách - předek to
    detekuje a refreshne data v DB \r\nb) zavolá metodu setDatabaseDirty a předek
    v tearDown zareaguje stejně\r\n\r\nNicméně řekl bych, že jakmile máš jeden jediný
    test, který neběží v transakci a modifikuje natvrdo data v databázi, zavírá si
    tím člověk vrátka ke konkurentnímu běhu více testů najednou - jistota je už ta
    tam."
- id: 326
  author: Roman Dagi Pichlik
  author_email: pichlik@seznam.cz
  author_url: http://www.sweb.cz/pichlik/
  date: '2007-08-07 15:10:37 +0200'
  date_gmt: '2007-08-07 14:10:37 +0200'
  content: Ja jsem to myslel tak, ze potomek si udela tu opravu sam. Napriklad meni
    pouze data jednoho radku, tak je zbytecne aby se musela znovytvaret cela tabulka
    pripadne cast databaze kvuli referencni integrite. Tahle kompemnzacni metoda by
    byla jenom volitelna.
- id: 327
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-08-07 15:50:30 +0200'
  date_gmt: '2007-08-07 14:50:30 +0200'
  content: JJ, jasně - tohle je výkonnější varianta. Asi jsem radikální, nechtělo
    se mi riskovat, že ten programátor špatně uklidí a padne mi to třeba o pět testů
    dál. Někdy si říkám, že než riskovat takovéhle nepříjemné chyby, je možná lepší
    stisknout VELKÝ ČERVENÝ KNOFLÍK :).
- id: 411
  author: Kamil Ševeček
  author_email: kamil@sevecek.com
  author_url: ''
  date: '2007-08-19 13:25:01 +0200'
  date_gmt: '2007-08-19 12:25:01 +0200'
  content: "1) Problém je v tom, že když potom ladíš test, který běží celý v transakci,
    nemůžeš se v půlce testu (když je kód zastaven na breakpointu) podívat na data
    v databázi (jestli jsou v správně).\r\n\r\n2) Naše projekty používají často web
    servicy (máme stromovou strukturu projektů, které se navzájem využívají pomoci
    SOAPu) a s těmi mi lokální DB transakce moc nepomůže."
- id: 413
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-08-19 14:47:37 +0200'
  date_gmt: '2007-08-19 13:47:37 +0200'
  content: "Jasně - žádné řešení není stoprocentní. Když ladím test, zatím to pro
    mě problém nebyl, že jsem nevěděl co mám v tu chvíli v databázi - obvykle totiž
    jeden test nevygeneruje tolik nových dat, které v DB už nejsou před započetím
    testu.\r\n\r\nZrychlení a zjednodušení testů rozhodně stojí za tuhle malou nevýhodu.\r\n\r\nAd
    2) v tomto případě to půjde těžko aplikovat - leda na integrační testy subsystému,
    schovaného za danou WS\r\n\r\nSpíš jde to to, že čím dál víc přicházím na to,
    že pokud se chce efektivně testovat, tak to obvykle jde - jen na řadu věcí přicházím
    o dost později, než bych potřeboval nebo chtěl ;)."
- id: 2005
  author: Pavel Jetenský
  author_email: mail@jetensky.net
  author_url: ''
  date: '2008-05-07 13:24:10 +0200'
  date_gmt: '2008-05-07 12:24:10 +0200'
  content: "Zrovna teď se mi to bude moc hodit, zavádím testy do projektu, kde je
    potřeba připravit hodně provázaných dat a měl jsem trochu obavy, jak to udělat
    aby měl test při každým spuštění čistý data a aby netrval dlouho pro každou metodu.\r\n\r\nTakže
    Honzo díky :)"
- id: 157400
  author: Nástroje pro podporu vývoje na platformě Java | SKOUMAL
  author_email: ''
  author_url: http://new.skoumal.net/cs/nastroje-pro-podporu-vyvoje-na-platforme-java/
  date: '2015-09-19 11:00:18 +0200'
  date_gmt: '2015-09-19 10:00:18 +0200'
  content: "[&#8230;] je možné vyřešit uzavřením celého testu do transakce, která
    je na konci testu rollbacknuta (více zde). Funkční testy testují hotový systém
    jako celek. Testy se provádějí tzv. [&#8230;]"
---
<p>Integrační testy spočívají v testování konkrétní kódu spolu s okolními částmi, se kterými spolupracuje. Cílem je snaha otestovat kód ve stavu, který se blíží reálnému nasazení. Obvykle takto testujeme datovou vrstvu aplikace (jelikož tam klasické jednotkové testy ztrácejí smysl - chceme přeci otestovat správné dotazování databáze, tudíž databázi k testu potřebujeme) a v řadě případů se nám nevyplatí <a href="http://blog.novoj.net/2007/01/19/mock-testing-potemkinovy-vesnice/" target="_new">mockovat</a> ani na úrovni business vrstvy. Dokonce i <a href="http://www.infoq.com/presentations/system-integration-testing-with-spring" target="_new">Rod Johnson ve své prezentaci</a> (kterou byl inspirován tento článek) zdůrazňuje důležitost integračních testů.</p>
<p>Hlavní problém integračních testů, u kterých máte ve spodu relační databázi je rychlost. Každý test spoléhá na nějaká data v DB - ty mohou být (a jsou) ostatními testy poškozena a proto je nedílnou částí všech testů setUp / tearDown operace, která se o tuto přípravu a uklizení stará. Jelikož jsou programátoři cháska líná a nechtějí se zabývat přípravou pouze minimální potřebné sady pro každý test, obvykle si vytvoří nějakého předka, který obsahuje setUp a tearDown, pro všechny testy najednou. Tím pádem se vždycky inicializuje kompletní sada dat a to si bere významné množství času. Odhadoval bych, že 80% času testů se stráví v této přípravě dat a pouze 20% času běží skutečné testy.</p>
<p><a id="more"></a><a id="more-28"></a></p>
<p>Na začátku projektu toto obvykle člověku nevadí, časem se to ale stane docela velkou bolestí. Na projektu, který jsem právě ukončil trvá běh testů na integračním serveru už něco kolem 30 minut. Spustit si takové testy na lokálním vývojovém prostředí je už prostě neúnosné (ještě že ty integrační servery máme ;)). Proto chce přemýšlet nad tímto problémem už od začátku - měnit princip fungování testů v pokročilé fázi projektu už stojí docela dost času.</p>
<p>Jedním z řešení, které například používají na rozsáhlém projektu pro bankovní sféru ve společnosti mého kolegy, je výměna datové vrstvy z cílové platformy (Oracle) za databázi v paměti (HSQL). Na začátku testů vytvoří v paměti kompletní nové schéma, které naplní daty a na konci testu celou databázi opět dropnou. Rychlost provádění se tím samozřejmě drasticky zvýší nicméně aplikaci už netestujeme na "finální" databázi, takže jsou naše testy částečně znehodnoceny. Navíc toto lze rozumně použít pouze v případě, kdy používáme ORM, který nám zakryje rozdíly mezi databázemi. V případě použití klasického JDBC nebo např. iBatisu (jako používáme my) bychom museli připravit dvě implementace a testy by už vůbec neplnily svůj smysl.</p>
<h3>Řešení existuje!</h3>
<p>Všechny problémy mají svá řešení a dobrá řešení se šíří jako lavina. Spring Framework je toho příkladem a i pro podporu testů obsahuje v balíku <b>spring-mock</b> dobré nápady. Částečně jsme toto rozkryli již v prezentaci mého kolegy <a href="http://blog.novoj.net/2007/07/01/podcast-basics-of-unit-testing-with-spring/" target="_new">základy testování ve Springu</a>, do větší hloubky to však rozebírá sám Rod Johnson v prezentaci <a href="http://www.infoq.com/presentations/system-integration-testing-with-spring" target="_new">integrační testování ve Springu</a>. Krom základního předka <b>AbstractDependencyInjectionSpringContextTests</b> (který se vám postará o načtení a zacachování spring contextu + nasetování bean přes settery do instance testu) jsou ve zmíněné knihovně ještě další třídy <b>AbstractTranactionalSpringContextTests</b>, <b>AbstractTransactionalDataSourceSpringContextTests</b> a <b>AbstractJPATests</b>, jejich použití si v tomto článku ukážeme.</p>
<p>Princip, o kterém Rod hovoří, je poměrně jednoduchý. Základem je, že máte v databázi stabilní sadu s daty, na kterých provádíte své testy. Všechny testy se mohou spolehnout na to, že v DB budou tato data a žádná jiná. Před započetím testu se AbstractTranactionalSpringContextTests postará o to, aby byla nastartovaná nová transakce, ve které test běží, a na konci je tato transakce rollbacknutá. Veškeré operace s daty, které byly v rámci testu provedeny jsou tedy vráceny zpět a další test opět běží nad stabilní datovou bází aniž bychom museli provádět nějaké extenzivní operace v setUp / tearDown.</p>
<p>Toto řešení má poměrně dost kladných dopadů:</p>
<ul>
<li>testy se řádově zrychlí - toto zrychlení je vidět už i v případě, že spouštíme testy pouze jedné třídy</li>
<li>průměrná délka v řádcích konkrétní testové třídy se výrazně zmenší</li>
<li>vlastní psaní testů je daleko rychlejší a člověk z něj není tolik unaven - většinou se zabývá tím co chce skutečně testovat a netráví tolik času otravnou přípravou a uklízení dat</li>
</ul>
<p>Třída AbstractTransactionalDataSourceSpringContextTests už přidává pouze několik pomocných metod, které vám umožní přistoupit k datasourcu, se kterým testy pracují a provést nad ním některé často používané operace (např. zjisti počet řádků v tabulce, vymaž všechny záznamy v tabulkách, proveď nějaký SQL příkaz).</p>
<p>Třída AbstractJPATests je optimalizovaná pro projekty, které používají na datové vrstvě ORM frameworky, které provádějí instrumentaci POJO a dalších potřebných tříd. Pro tento účel je vytvořen tzv. ShadowingClassLoader, který izoluje takto instrumentované třídy a je možné jej i se všemi třídami zrušit v případě potřeby (nicméně přiznám, že na tuhle oblast nejsem expert, takže vám k tomu víc neřeknu).</p>
<h3>Příklad z praxe</h3>
<p>V této části uvedu pár příkladových tříd z projektu, na kterém v současnosti pracuji. Vytvořil jsem si ještě jednoho předka, který mi zaručí konzistenci datové báze pro testy. Ve zkratce se tento předek před započetím transakce zeptá na jména tabulek a očekávaný počet řádků v těchto tabulkách - před startem každého testu se provádí tato jednoduchá kontrola. V případě, že počty sedí test počítá s tím, že data jsou v pořádku a test se spustí. Pokud by test nastartoval a databáze by byla prázdná, nebo by někdo ručně změnil data v databázi, došlo by k obnovení dat, se kterými test počítá. Vlastní testy běží v transakci, takže data neovlivní - ale v některých případech potřebujeme pro test toto chování vyřadit (např. potřebujeme právě otestovat správné chování transakcí) a k ovlivnění dat v DB dojde. V takovém případě se data před startem dalšího testu znovu vytvoří (tedy pokud došlo ke změně počtu řádků, pokud nikoliv může programátor zavolat metodu setDatabaseDirty a k obnovení dat si tímto vynutí). Takové případy, kdy ale potřebujeme jet mimo "testovou" transakci je ale dost málo, takže těch pár "kompletních" inicializací už nečiní takový problém, jako když se inicializace dělaly před každým testem.</p>
<p>Kód tohoto předka je zde:</p>
<p>[source lang="java"]<br />
/**<br />
 * Performs the same funcionality as AbstractTransactionalDataSourceSpringContextTests but more than that<br />
 * it contains coherent logic for keeping state of the database in consistency with prepared testing data.<br />
 * See #AbstractTransactionalDataSourceSpringContextTests documentation for more hints on testing.<br />
 */<br />
public abstract class AbstractDatabaseSpringTestCase extends AbstractTransactionalDataSourceSpringContextTests {<br />
	/**<br />
	 * Flag signalizing, that test modified data in database outside transaction, but the rowcount<br />
	 * in tables stood the same.<br />
	 */<br />
	private static boolean databaseIsDirty;</p>
<p>	/**<br />
	 * Subclasses can override this method to perform any setup operations,<br />
	 * such as populating a database table, <i>before</i> the transaction<br />
	 * created by this class. Only invoked if there <i>is</i> a transaction:<br />
	 * that is, if {@link #preventTransaction()} has not been invoked in<br />
	 * an overridden {@link #runTest()} method.<br />
	 *<br />
	 * @throws Exception simply let any exception propagate<br />
	 */<br />
	protected void onSetUpBeforeTransaction() throws Exception {<br />
		super.onSetUpBeforeTransaction();<br />
		refreshDatabase(true);<br />
	}</p>
<p>	/**<br />
	 * Subclasses can override this method to perform cleanup after a transaction<br />
	 * here. At this point, the transaction is <i>not active anymore</i>.<br />
	 *<br />
	 * @throws Exception simply let any exception propagate<br />
	 */<br />
	protected void onTearDownAfterTransaction() throws Exception {<br />
		super.onTearDownAfterTransaction();<br />
		if(databaseIsDirty) refreshDatabase(false);<br />
	}</p>
<p>	/**<br />
	 * Performs refresh of the data in database.<br />
	 * @param checkCounts when true check whether counts in tables has changed<br />
	 *        - if not skip refreshment<br />
	 */<br />
	private void refreshDatabase(boolean checkCounts) {<br />
		TableCountHolder[] tablesWithCounts = getTablesToBeCheckedForCount();<br />
		if(tablesWithCounts != null) {<br />
			if(!checkCounts || isDataInconsistent(tablesWithCounts)) {<br />
				String[] tableNames = createTableNames(tablesWithCounts);<br />
				deleteFromTables(tableNames);<br />
				populateEmptyTables();<br />
				databaseIsDirty = false;<br />
			}<br />
		}<br />
	}</p>
<p>	/**<br />
	 * This method should be called by test, when it changes data outside a transaction and<br />
	 * possible does not change rowcount in tables.<br />
	 */<br />
	protected void setDatabaseDirty() {<br />
		AbstractDatabaseSpringTestCase.databaseIsDirty = true;<br />
	}</p>
<p>	/**<br />
	 * Converts set into array of tablenames.<br />
	 *<br />
	 * @param tablesWithCounts<br />
	 * @return<br />
	 */<br />
	private String[] createTableNames(TableCountHolder[] tablesWithCounts) {<br />
		String[] result = new String[tablesWithCounts.length];<br />
		for(int j = 0; j < tablesWithCounts.length; j++) {<br />
			result[j] = tablesWithCounts[j].getTableName();<br />
		}<br />
		return result;<br />
	}</p>
<p>	/**<br />
	 * Returns true if data is not consistent in database.<br />
	 *<br />
	 * @param tablesWithCounts<br />
	 */<br />
	private boolean isDataInconsistent(TableCountHolder[] tablesWithCounts) {<br />
		for(int i = 0; i < tablesWithCounts.length; i++) {<br />
			TableCountHolder tableInfo = tablesWithCounts[i];<br />
			String tableName = tableInfo.getTableName();<br />
			if(tableInfo.getExpectedRowCount() != countRowsInTable(tableName)) {<br />
				logger.info("Table " + tableName + " inconsistent, forcing data refresh.");<br />
				return true;<br />
			}<br />
			else {<br />
				logger.info("Table " + tableName + " consistent, can reuse existing data.");<br />
			}<br />
		}</p>
<p>		return false;<br />
	}</p>
<p>	/**<br />
	 * Method to be overriden by subclasses.<br />
	 * Should populate data into all tables mentioned in getTablesToBeCheckedForCount method.<br />
	 * This class ensures that all tables are emptied before calling this method.<br />
	 */<br />
	protected void populateEmptyTables() {<br />
		//let the subclass do what it needs<br />
	}</p>
<p>	/**<br />
	 * Method to be overriden by subclasses.<br />
	 *<br />
	 * It is important to have items in array in right order optimized for<br />
	 * possible record deletion sequence.<br />
	 *<br />
	 * @return<br />
	 */<br />
	protected TableCountHolder[] getTablesToBeCheckedForCount() {<br />
		return null;<br />
	}</p>
<p>	/**<br />
	 * Holds information about expected rowcount in a table.<br />
	 */<br />
	public static class TableCountHolder {<br />
		private String tableName;<br />
		private int expectedRowCount;</p>
<p>		public TableCountHolder(String tableName, int expectedRowCount) {<br />
			this.tableName = tableName;<br />
			this.expectedRowCount = expectedRowCount;<br />
		}</p>
<p>		public String getTableName() {<br />
			return tableName;<br />
		}</p>
<p>		public void setTableName(String tableName) {<br />
			this.tableName = tableName;<br />
		}</p>
<p>		public int getExpectedRowCount() {<br />
			return expectedRowCount;<br />
		}</p>
<p>		public void setExpectedRowCount(int expectedRowCount) {<br />
			this.expectedRowCount = expectedRowCount;<br />
		}<br />
	}</p>
<p>}<br />
[/source]</p>
<p>V projektu si potom vytvářím ještě dalšího předka, který implementuje strategii obnovy dat pro projektové testy. V předku mám statické pole se seznamem POJO objektů, které reprezentují data v databázi a se kterými mohou testy dále pracovat. Tyto POJO objekty jsou v <b>populateEmptyTables</b> metodě vloženy do databáze.</p>
<p><i>Pozn.:</i> Možná by bylo vhodnější data vkládat způsobem nezávislým na kódu naší aplikace kterou testujeme (tedy nikoli přes daoRole.createRole(...)), jenže tento způsob je prostě o mnoho jednodušší a přistupuji na tu nevýhodu, že pokud bude chyba v této metodě, nerozjedou se ani testy.</p>
<p>[source lang="java"]<br />
/**<br />
 * Project database test ancestor. Contains database population logic.<br />
 */<br />
public abstract class AbstractProjectDatabaseTestCase extends AbstractDatabaseSpringTestCase {<br />
	protected SqlMapClient sqlMapClient;<br />
	protected IRoleStorage daoRole = null;</p>
<p>	protected static IRole[] roles = new IRole[]{<br />
		//creates populated POJO Role object: id, systemName, name, description<br />
		PojoFactory.getRole(1, "SUPERVIZOR", "Oprávnění supervizora", "Role s maximálními oprávněními."),<br />
		PojoFactory.getRole(2, "ADMINISTRATOR", "Administrátor", "Administrační práva."),<br />
		PojoFactory.getRole(3, "PUBLISHER", "Pisatel", "Umožňuje psát články."),<br />
		PojoFactory.getRole(4, "READER", "Čtenář", "Umožňuje číst články."),<br />
		PojoFactory.getRole(5, "REDACTOR", "Redaktor", "Schvaluje články.")<br />
	};</p>
<p>	public void setDaoRole(IRoleStorage daoRole) {<br />
		this.daoRole = daoRole;<br />
	}</p>
<p>	public void setSqlMapClient(SqlMapClient sqlMapClient) {<br />
		this.sqlMapClient = sqlMapClient;<br />
	}</p>
<p>	protected void populateEmptyTables() {<br />
		try {<br />
			for(int i = 0; i < roles.length; i++) daoRole.createRole(roles[i]);<br />
		}<br />
		catch(Exception ex) {<br />
			throw new RuntimeException("Cannot prepare database for tests!", ex);<br />
		}<br />
	}</p>
<p>	protected TableCountHolder[] getTablesToBeCheckedForCount() {<br />
		return new TableCountHolder[]{<br />
				new TableCountHolder("T_FGUSER_AUTHORITY", roles.length),<br />
	}<br />
}<br />
[/source]</p>
<p>Vlastní testová třída již vypadá velmi jednoduše. Testy se skutečně soustředí na logiku aplikace, píšou se velmi jednoduše a na mém počítači trvá spuštění všech testů této třídy asi 3 vteřiny, z čehož přes 2 vteřiny trvá inicializace Springu a získání konekce z databáze. Když rozšířím sadu testů na pět (každý má zhruba stejný počet metod), trvá celý běh asi o 0,6 vteřiny déle. Původním způsobem s inicializací DB před každým testem bych byl minimálně na 30 sekundách.</p>
<p>[source lang="java"]<br />
public class RoleStorageTest extends AbstractProjectDatabaseTestCase {</p>
<p>	public void testCreateRole() throws Exception {<br />
		IRole role = getSomeNewRole();<br />
		daoRole.createRole(role);<br />
		assertTrue(role.getId() > 0);<br />
	}</p>
<p>	public void testCreateRoleTwice() throws Exception {<br />
		IRole role = ((Role)roles[0]).getClone();<br />
		try {<br />
			role.setId(0);<br />
			daoRole.createRole(role);<br />
			fail("Exception should have been thrown.");<br />
		}<br />
		catch(ObjectAlreadyExists e) {<br />
			//yup, this is right<br />
		}<br />
	}</p>
<p>	public void testGetRoleNonExisting() throws Exception {<br />
		assertNull(daoRole.getRoleById(-1));<br />
		assertNull(daoRole.getRoleBySystemName("nejaka nesmyslna"));<br />
	}</p>
<p>	public void testGetRoleById() throws Exception {<br />
		IRole role = daoRole.getRoleById(roles[0].getId());<br />
		assertTrue("Roles should be the same", roles[0].match(role));<br />
	}</p>
<p>	public void testGetRoleBySystemName() throws Exception {<br />
		IRole role = daoRole.getRoleBySystemName(roles[0].getSystemName());<br />
		assertTrue("Roles should be the same", roles[0].match(role));<br />
	}</p>
<p>	public void testUpdateRole() throws Exception {<br />
		Role role = ((Role)roles[0]).getClone();<br />
		int id = role.getId();<br />
		role.setSystemName("WHATEVER");<br />
		role.setName("Whatever name");<br />
		role.setDescription("Whatever description");<br />
		daoRole.updateRole(role);<br />
		IRole role2 = daoRole.getRoleBySystemName("WHATEVER");<br />
		assertTrue("Roles should be the same", role.match(role2));<br />
		assertEquals(id, role2.getId());<br />
	}</p>
<p>	public void testRemoveRole() throws Exception {<br />
		assertTrue(daoRole.removeRole(roles[0].getId()));<br />
		assertNull(daoRole.getRoleBySystemName(roles[0].getSystemName()));<br />
	}</p>
<p>	public void testRemoveRoleNonExisting() throws Exception {<br />
		assertFalse(daoRole.removeRole(-1));<br />
	}</p>
<p>	public void testListRoles() throws Exception {<br />
		List list;<br />
		list = daoRole.listRoles(new HashMap(), null, null, 0, 20);<br />
		assertNotNull(list);<br />
		assertTrue(list.size() == users.length);<br />
		assertEquals("ADMINISTRATOR", ((IRole)list.get(0)).getSystemName());</p>
<p>		list = daoRole.listRoles(new HashMap(), RoleStorage.ORDER_BY_DESCRIPTION, Boolean.FALSE, 0, 20);<br />
		assertEquals("PUBLISHER", ((IRole)list.get(0)).getSystemName());</p>
<p>		HashMap conditions = new HashMap();<br />
		conditions.put("description", "Umožňuje%");<br />
		list = daoRole.listRoles(conditions, null, null, 0, 20);<br />
		assertTrue(list.size() == 2);<br />
	}</p>
<p>	private IRole getSomeNewRole() {<br />
		return PojoFactory.getRole("EVICTOR", "Mazač", "Role která umožňuje mazání.");<br />
	}</p>
<p>}<br />
[/source]</p>
<h3>Závěr a odkazy</h3>
<p>Na vyzkoušení tohoto způsobu implementace testů mne upozornila již několikrát zmiňovaná přednáška Roda Johnsona o integračním testování. Přednáška má cca. 90 minut a rozhodně stojí za shlédnutí - Rod tam rozebírá ještě další věci, takže pokud už celý Spring nemáte v malíku, doporučuji.</p>
<p>Detailní popisky o fungování Spring test tříd jsou v javadocech, proto v závěru článku uvedu odkazy. O základech testování ve Springu přednáší kolega v prezentaci Basics of JUnit testing with Spring. Pokud vás zajímají základy, doporučuji jeho přednášku.</p>
<p><b>Odkazy:</b></p>
<ul>
<li><a href="http://www.infoq.com/presentations/system-integration-testing-with-spring" target="_new">Rod Johnson: System Integration Testing Using Spring</a></li>
<li><a href="http://www.springframework.org/docs/api/org/springframework/test/AbstractTransactionalSpringContextTests.html" target="_new">JavaDoc ke třídě AbstractTransactionalSpringContextTests</a></li>
<li><a href="http://blog.novoj.net/2007/07/01/podcast-basics-of-unit-testing-with-spring/" target="_new">Podcast: Basics of JUnit testing with Spring - základy psaní testů ve Springu</a></li>
<li><a href="http://www.haloscan.com/comments.php?user=dagi&comment=8995187702221665433" target="_new">zajímavá diskuse na DagBlogu k článku Grid Testy, kde byla zpochybněna použitelnost tohoto řešení pro Hibernate</a></li>
</ul>
