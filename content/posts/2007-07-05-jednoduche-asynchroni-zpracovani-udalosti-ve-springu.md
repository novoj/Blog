---
status: publish
published: true
title: Jednoduché asynchronní zpracování událostí ve Springu
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<p>Spring framework má \"od přírody\" k dispozici implementaci Observer
  patternu. To není nic jiného než mechanismus \"listenerů\" tak, jak jej známe například
  ze Swingu. Základní a defaultní implementace je velmi jednoduchá, kdekoliv v managovaných
  beanách můžete přes tzv. Publisher (což je typicky aplikační kontext, kterým je
  daná beana vytvořena) vyslat informaci o události. Tuto událost pak může zpracovat
  jakákoliv třída implementující ApplicationListener rozhraní, a která je správně
  zaregistrovaná do fronty listenerů. Registrace se provádí velmi jednoduše - pouze
  deklarací beany v context.xml. AbstractApplicationContext (předchůdce všech specifických
  implementací aplikačního kontextu) při své inicializaci všechny beany implementující
  zmíněné rozhraní zaregistruje.</p>\r\n\r\n<p>Výchozí implementace distribuce / zpracování
  eventů je velmi jednoduchá a také postačuje ve valné většině případů. Jedná se o
  synchronní zpracování vyslaných událostí. Tzn. okamžitě, jakmile přes Publisher
  zveřejníte událost, jsou notifikování všichni zaregistrovaní listeneři, kteří událost
  opět okamžitě ve stejném Threadu zpracují - a operace pokračuje dál, až všichni
  se svou činností skončí. Někdy se ovšem hodí, když se mohou vybrané události zpracovat
  asynchronně - nezávisle na threadu, který událost vyvolal.</p>\r\n\r\n<p>Situace,
  kdy bychom mohli chtít oddělit zpracování událostí do jiného threadu, jsou mají
  společné tyto základní vlastnosti:\r\n   <ul>\r\n      <li>nejsou blokující pro
  poskytnutí odezvy uživateli (tzn. operace je pouze vedlejším produktem operace,
  kterou uživatel vykonal)</li>\r\n      <li>náklady na její zpracování jsou větší
  než nepatrné - tzn. zpracováním události v jiném vlákně urychlíme odezvu uživateli</li>\r\n
  \     <li>o případné selhání této operace nemusí být uživatel nutně informován</li>\r\n
  \  </ul>\r\n</p>\r\n\r\n<p>Otázka zní, jak tohoto docílit ...</p>\r\n\r\n"
wordpress_id: 21
wordpress_url: http://blog.novoj.net/2007/07/05/jednoduche-asynchroni-zpracovani-udalosti-ve-springu/
date: '2007-07-05 14:58:56 +0200'
date_gmt: '2007-07-05 13:58:56 +0200'
categories:
- Java
- Spring Framework
tags: []
comments: []
---
<p>Spring framework má "od přírody" k dispozici implementaci Observer patternu. To není nic jiného než mechanismus "listenerů" tak, jak jej známe například ze Swingu. Základní a defaultní implementace je velmi jednoduchá, kdekoliv v managovaných beanách můžete přes tzv. Publisher (což je typicky aplikační kontext, kterým je daná beana vytvořena) vyslat informaci o události. Tuto událost pak může zpracovat jakákoliv třída implementující ApplicationListener rozhraní, a která je správně zaregistrovaná do fronty listenerů. Registrace se provádí velmi jednoduše - pouze deklarací beany v context.xml. AbstractApplicationContext (předchůdce všech specifických implementací aplikačního kontextu) při své inicializaci všechny beany implementující zmíněné rozhraní zaregistruje.</p>
<p>Výchozí implementace distribuce / zpracování eventů je velmi jednoduchá a také postačuje ve valné většině případů. Jedná se o synchronní zpracování vyslaných událostí. Tzn. okamžitě, jakmile přes Publisher zveřejníte událost, jsou notifikování všichni zaregistrovaní listeneři, kteří událost opět okamžitě ve stejném Threadu zpracují - a operace pokračuje dál, až všichni se svou činností skončí. Někdy se ovšem hodí, když se mohou vybrané události zpracovat asynchronně - nezávisle na threadu, který událost vyvolal.</p>
<p>Situace, kdy bychom mohli chtít oddělit zpracování událostí do jiného threadu, jsou mají společné tyto základní vlastnosti:</p>
<ul>
<li>nejsou blokující pro poskytnutí odezvy uživateli (tzn. operace je pouze vedlejším produktem operace, kterou uživatel vykonal)</li>
<li>náklady na její zpracování jsou větší než nepatrné - tzn. zpracováním události v jiném vlákně urychlíme odezvu uživateli</li>
<li>o případné selhání této operace nemusí být uživatel nutně informován</li>
</ul>
<p>Otázka zní, jak tohoto docílit ...</p>
<p><a id="more"></a><a id="more-21"></a></p>
<h3>K dispozici jsou v podstatě dvě základní řešení:</h3>
<h4>Použití JMS - Java Messaging Service</h4>
<p>Od <a href="http://static.springframework.org/spring/docs/2.0.x/reference/jms.html#jms-asynchronousMessageReception" target="_blank">verze 2.0 Spring Frameworku</a> je možné pro asynchronní zpracování událostí použít JMS ze stacku J2EE. O této variantě se můžete více dočíst například <a href="http://www.onjava.com/pub/a/onjava/2006/02/22/asynchronous-messaging-with-spring-jms.html" target="_blank">v článku na serveru OnJava</a>. JMS je pouze specifikace API, takže implementaci si <a href="http://www.quepublishing.com/articles/article.asp?p=26270&rl=1" target="_blank">posléze můžete zvolit</a>. JMS jako takové je možné <a href="http://openjms.sourceforge.net/" target="_blank">v řadě případů</a> provozovat samostatně bez aplikačního serveru.</p>
<p>Základními výhodami této varianty je především:</p>
<ul>
<li>robustnost,</li>
<li>spolehlivost (je garantováno doručení zpráv) - typicky jsou zprávy persistovány do databáze,</li>
<li>distribuovatelnost = škálovatelnost</li>
</ul>
<p>Mezi nevýhody naopak patří:</p>
<ul>
<li>složitější deployment,</li>
<li>zanesení další technologie (produktu) do projektu,</li>
<li>složitější správa.</li>
</ul>
<h4>Rekonfigurace Multicaster objektu na použití jiného TaskExecutoru</h4>
<p>Pokud nemáme takové nároky na spolehlivost a škálovatelnost mechanismu pro asynchronní zpracování událostí, můžeme se vydat radikálně jednodušší cestou pouhé rekonfigurace Springu s doplněním asi tří chybějících tříd.</p>
<p>Spring pracuje při správě událostí s následujícími rozhraní a implementacemi:</p>
<ul>
<li><strong>ApplicationEventPublisher</strong> - obsahuje metodu publishEvent(ApplicationEvent event), přes kterou vaše třídy mohou "vysílat" své události; toto rozhraní typicky implementuje instance aplikačního kontextu, ke kterému se dostanete např. přes callback rozhraní ApplicationContextAware</li>
<li><strong>ApplicationEventMulticaster</strong> - obsahuje metody jako je např. addListener / removeListener a také metodu multicastEvent(ApplicationEvent event); multicaster je používán Publisherem pro rozesílání událostí zaregistrovaným listenerům a také spravuje onu množinu registrovaných listenerů</li>
<li><strong>SimpleApplicationEventMulticaster</strong> - toto je výchozí implementace multicasteru používaná Springem - obsahuje instanci TaskExecutoru, který zajišťuje zpracování jednotlivých listenerů</li>
<li><strong>TaskExecutor</strong> - TaskExecutor se obecněji stará o běh Runnable instancí - zde jej zmiňuji proto, že každé zpracování události listenerem je obaleno do Runnable objektu</li>
<li><strong>SyncTaskExecutor</strong> - výchozí implementace TaskExecutoru v SimpleApplicationEventMulticasteru; vykonává jednotlivé listenery ve stejném threadu jako běží aplikační objekt, který událost vyvolal (tzn. váš aplikační objekt čeká než SyncTaskExecutor vyřídí všechny listenery)</li>
</ul>
<p>Pro to abychom tedy změnili výchozí zpracování událostí na asynchronní nám pouze stačí vyměnit implementaci TaskExecutoru například na TimerTaskExecutor, který provede běh listenerů asynchronně v novém threadu (nicméně instanciuje pouze jeden thread, ve kterém potom zpracování daných listenerů už provádí synchronně).</p>
<p>K tomu nám postačuje znát, že AbstractApplicationContext při své inicializaci nejdříve hledá v context.xml deklaraci beany s názvem "applicationEventMulticaster", kterou by dosadil na místo svého "multicastera" a teprve když ji nenajde vytvoří si vlastní defaultní instanci třídy SimpleApplicationEventMulticaster. Potom můžeme jednoduše v konfiguraci uvést:</p>
<p>[source lang="xml"]<br />
<bean id="applicationEventMulticaster" class="org.springframework.context.event.SimpleApplicationEventMulticaster"></p>
<property name="taskExecutor">
		<bean class="org.springframework.scheduling.timer.TimerTaskExecutor"/>
	</property>
</bean><br />
[/source]</p>
<p>Tím ovšem způsobíme, že se v asynchronním vlákně vykonají VŠECHNY ApplicationListenery, které v deklaraci daného aplikačního kontextu uvedeme. Negativním nechtěným efektem je to, že pokud při zpracování události dojde k chybě = výjimce, nedoví se o tom aplikační objekt, který událost vyvolal a tím pádem např. neselže operace, kterou vyvolal uživatel. To je stav, o který typicky nestojíme - ve většině případů dokonce potřebujeme, aby při selhání operace v listeneru došlo k pozastavení zpracování prováděné operace a byl informován uživatel.</p>
<p>I toho ale lze poměrně jednoduše docílit. Nahradíme celý objekt multicasteru, který se stará o správu registrovaných listenerů a broadcasting událostí. Vytvoříme třídu, která při registraci listenery rozhodí do různých "podřízených" multicasterů podle určitého klíče. Tzn. vytvoří defakto dvouúrovňový strom multicasterů, kde každý zaregistrovaný listener bude zařazen do jednoho z multicasterů druhé úrovně. V druhé úrovni budeme potom mít dva multicastery - jeden se synchronním TaskExecutorem a druhý s asynchronním.</p>
<p>[source lang="java"]<br />
/**<br />
 * DistributingEventMulticaster wraps different multicaster "contexts" allowing listener registration<br />
 * only to those, that match filter criterias. Criteria specification and resolution is dedicated to IMulticasterFilterResolver.<br />
 */<br />
public class DistributingEventMulticaster implements ApplicationEventMulticaster {<br />
	private static Log log = LogFactory.getLog(DistributingEventMulticaster.class);<br />
	private IMulticasterFilterResolver multicasterFilterResolver;</p>
<p>	public IMulticasterFilterResolver getMulticasterFilterResolver() {<br />
		return multicasterFilterResolver;<br />
	}</p>
<p>	public void setMulticasterFilterResolver(IMulticasterFilterResolver multicasterFilterResolver) {<br />
		this.multicasterFilterResolver = multicasterFilterResolver;<br />
	}</p>
<p>	/**<br />
	 * Add a listener to be notified of all events.<br />
	 *<br />
	 * @param listener the listener to add<br />
	 */<br />
	public void addApplicationListener(ApplicationListener listener) {<br />
		ApplicationEventMulticaster multicaster =<br />
				getMulticasterFilterResolver().getApplicableMulticastContexts(listener);</p>
<p>		multicaster.addApplicationListener(listener);<br />
		if(log.isDebugEnabled()) {<br />
			log.debug("Adding listener " + listener.getClass().getSimpleName() +<br />
					" into context of multicaster " + multicaster.getClass().getSimpleName());<br />
		}</p>
<p>	}</p>
<p>	/**<br />
	 * Remove a listener from the notification list.<br />
	 *<br />
	 * @param listener the listener to remove<br />
	 */<br />
	public void removeApplicationListener(ApplicationListener listener) {<br />
		ApplicationEventMulticaster multicaster =<br />
				getMulticasterFilterResolver().getApplicableMulticastContexts(listener);</p>
<p>		multicaster.removeApplicationListener(listener);<br />
		if(log.isDebugEnabled()) {<br />
			log.debug("Removing listener " + listener.getClass().getSimpleName() +<br />
					" from context of multicaster " + multicaster.getClass().getSimpleName());<br />
		}</p>
<p>	}</p>
<p>	/**<br />
	 * Remove all listeners registered with this multicaster.<br />
	 * It will perform no action on event notification until more<br />
	 * listeners are registered.<br />
	 */<br />
	public void removeAllListeners() {<br />
		Collection<ApplicationEventMulticaster> multicastContexts =<br />
				getMulticasterFilterResolver().getAllMulticastContexts();</p>
<p>		for(ApplicationEventMulticaster multicaster : multicastContexts) {<br />
			multicaster.removeAllListeners();<br />
			if(log.isDebugEnabled()) {<br />
				log.debug("Removing all listeners from context of multicaster "<br />
						+ multicaster.getClass().getSimpleName());<br />
			}<br />
		}</p>
<p>	}</p>
<p>	/**<br />
	 * Multicast the given application event to appropriate listeners.<br />
	 *<br />
	 * @param event the event to multicast<br />
	 */<br />
	public void multicastEvent(ApplicationEvent event) {<br />
		Collection<ApplicationEventMulticaster> multicastContexts =<br />
				getMulticasterFilterResolver().getAllMulticastContexts();</p>
<p>		for(ApplicationEventMulticaster multicaster : multicastContexts) {<br />
			multicaster.multicastEvent(event);<br />
			if(log.isDebugEnabled()) {<br />
				log.debug("Multicasting event " + event.getClass().getSimpleName() +<br />
						" to context of multicaster " + multicaster.getClass().getSimpleName());<br />
			}<br />
		}</p>
<p>	}</p>
<p>}<br />
[/source]</p>
<p>Pro rozhození listenerů si nadefinujeme rozhraní IMulticasterFilterResolver, které nám zakrývá implementace jak z instance listeneru zjistit, který multicaster (synchronní / asynchronní) má být vlastně použit.</p>
<p>[source lang="java"]<br />
public interface IMulticasterFilterResolver {</p>
<p>	/**<br />
	 * Returns collection of all available multicasters.<br />
	 * @return<br />
	 */<br />
	public Collection<ApplicationEventMulticaster> getAllMulticastContexts();</p>
<p>	/**<br />
	 * Returns multicaster where particular listener shall be registered.<br />
	 *<br />
	 * @param listener<br />
	 * @return<br />
	 */<br />
	public ApplicationEventMulticaster getApplicableMulticastContexts(ApplicationListener listener);</p>
<p>}<br />
[/source]</p>
<p>Jako základní a jednoduchou implementaci můžeme použít rozeznávání listenerů podle jejich typu (nicméně stejně jednoduše můžeme vytvořit implementace rozeznávající typy listenerů např. na základě anotací, jejich pojmenování, zařazení ve struktuře packají atd. atd.). Podívejme se tedy do těla třídy ClassTypeMulticasterResolver.</p>
<p>[source lang="java"]<br />
public class ClassTypeMulticasterResolver implements IMulticasterFilterResolver {<br />
	private List<MulticasterContextConfig> separatedMulticastContexts;</p>
<p>	public List<MulticasterContextConfig> getSeparatedMulticastContexts() {<br />
		return separatedMulticastContexts;<br />
	}</p>
<p>	public void setSeparatedMulticastContexts(List<MulticasterContextConfig> separatedMulticastContexts) {<br />
		this.separatedMulticastContexts = separatedMulticastContexts;<br />
	}</p>
<p>	/**<br />
	 * Returns collection of all available multicasters.<br />
	 *<br />
	 * @return<br />
	 */<br />
	public Collection<ApplicationEventMulticaster> getAllMulticastContexts() {<br />
		List<ApplicationEventMulticaster> result = new ArrayList<ApplicationEventMulticaster>();<br />
		for(MulticasterContextConfig cfg : separatedMulticastContexts) {<br />
			result.add(cfg.getMulticaster());<br />
		}<br />
		return result;<br />
	}</p>
<p>	/**<br />
	 * Returns multicaster where particular listener shall be registered.<br />
	 *<br />
	 * @param listener<br />
	 * @return<br />
	 */<br />
	public ApplicationEventMulticaster getApplicableMulticastContexts(ApplicationListener listener) {<br />
		ApplicationEventMulticaster result = null;</p>
<p>		//iterate through multicaster map to get the applicable multicaster list<br />
		List<MulticasterContextConfig> contexts = getSeparatedMulticastContexts();<br />
		Iterator<MulticasterContextConfig> iterator = contexts.iterator();</p>
<p>		for(MulticasterContextConfig cfg : contexts) {<br />
			Set<Class> patterns = cfg.getPatternClasses();<br />
			for(Class patternClass : patterns) {<br />
				if(patternClass.isAssignableFrom(listener.getClass())) {<br />
					return cfg.getMulticaster();<br />
				}<br />
			}<br />
		}</p>
<p>		return null;<br />
	}</p>
<p>	/**<br />
	 * Holds single multicaster configuration.<br />
	 */<br />
	public static class MulticasterContextConfig {<br />
		private ApplicationEventMulticaster multicaster;<br />
		private Set<Class> patternClasses;</p>
<p>		public ApplicationEventMulticaster getMulticaster() {<br />
			return multicaster;<br />
		}</p>
<p>		public void setMulticaster(ApplicationEventMulticaster multicaster) {<br />
			this.multicaster = multicaster;<br />
		}</p>
<p>		public Set<Class> getPatternClasses() {<br />
			return patternClasses;<br />
		}</p>
<p>		public void setPatternClasses(Set<Class> patternClasses) {<br />
			this.patternClasses = patternClasses;<br />
		}<br />
	}</p>
<p>}<br />
[/source]</p>
<p>Pokud se tedy vrátíme k našemu původnímu záměru - tedy mít některé listenery zpracovávané asynchronně a jiné synchronně - můžeme jednoduchou konfigurací výše uvedených tříd našeho záměru dosáhnout. Řekněme, že všechny listenery implementující "markable" rozhraní IAsynchronousListener (které neobsahuje žádné metody a slouží jen jako "diskriminátor") budou prováděny asynchronně a zbytek listenerů synchronně. Konfigurace by byla potom následující:</p>
<p>[source lang="xml"]<br />
<!-- touto deklarací vnutíme aplikačnímu kontextu, aby jako multicaster použil tento námi definovaný --><br />
<bean id="applicationEventMulticaster" class="com.fg.trtn.business.multicaster.DistributingEventMulticaster"><br />
        <!-- pro DistributingEventMulticaster nadefinujeme implementaci filtru,<br />
              který vrací konkrétní multicastery druhé úrovně --></p>
<property name="multicasterFilterResolver">
		<!-- zvolíme filter rozeznávající listenery na základě typovosti --><br />
		<bean class="com.fg.trtn.business.multicaster.ClassTypeMulticasterResolver"><br />
			<!-- zde nakonfigurujeme seznam dvou multicasterů - asynchronního a synchronního --><br />
			<!-- na pořadí záleží, lister bude zařazen k prvnímu multicasteru, kterému bude odpovídat jeho typ --></p>
<property name="separatedMulticastContexts">
<list>
					<!-- priority 1: asynchronní multicaster pro třídy implementující IAsyncListener --><br />
					<bean class="com.fg.trtn.business.multicaster.ClassTypeMulticasterResolver$MulticasterContextConfig"></p>
<property name="multicaster">
							<bean id="asyncEventMulticaster"<br />
								  class="org.springframework.context.event.SimpleApplicationEventMulticaster"></p>
<property name="taskExecutor">
									<bean class="org.springframework.scheduling.timer.TimerTaskExecutor"/>
								</property>
							</bean>
						</property>
						<!-- seznam tříd, vůči kterým má být listener porovnáván při filtrování --></p>
<property name="patternClasses">
							<set><br />
								<value>com.fg.trtn.business.listener.IAsyncListener</value><br />
							</set>
						</property>
					</bean><br />
					<!-- priority 2: pro všechny ostatní listenery použij synchronní multicaster --><br />
					<bean class="com.fg.trtn.business.multicaster.ClassTypeMulticasterResolver$MulticasterContextConfig"></p>
<property name="multicaster">
							<bean id="syncEventMulticaster"<br />
								  class="org.springframework.context.event.SimpleApplicationEventMulticaster"/>
						</property>
						<!-- všechny listenery musí implementovat rozhraní ApplicationListener, --><br />
						<!-- takže zde skončí zbytek našich listenerů --></p>
<property name="patternClasses">
							<set><br />
								<value>org.springframework.context.ApplicationListener</value><br />
							</set>
						</property>
					</bean>
				</list>
			</property>
		</bean>
	</property>
</bean><br />
[/source]</p>
<p>Tímto jsme poměrně jednoduše vyřešili náš problém s prováděním asynchronních událostí v aplikaci. V článku možná vypadá řešení možná složitěji, než ve skutečnosti (když si prohlédnete dané třídy) je. Výhodou řešení je, že nám stačí pouze Spring framework a vše zůstává průhledné a jednoduché. Nevýhodou naopak je, že pokud by zpracování listenerů bylo výpočetně náročnější, mohla by se nám plnit asynchronní fronta událostí, o které bychom při pádu / restartu serveru mohli přijít. Proto bych mezi asynchronní listenery nezařazoval žádné vitálně důležité funkce / operace.</p>
<p>Přestože by se mohlo na první pohled zdát, že pokud požadujete pro své operace zaručené zpracování / škálovatelnost, musíte jít cestou JMS, není to 100% pravda. Podobné vlastnosti vám může dodat i v případě druhého způsobu řešení (které je "pouze v paměti") např. nasazení <a href="http://www.terracotta.org/" target="_blank">clustrovaného řešení pro Spring od Terracota</a>. V takovém případě by fronta s událostmi ke zpracování byla duplikovaná na více serverech, takže:</p>
<ul>
<li>při selhání jednoho serveru, by se zpracování událostí postaral server druhý</li>
<li>zpracování událostí by se rozdělilo mezi více serverů a tudíž by řešení začalo "škálovat" :)</li>
</ul>
