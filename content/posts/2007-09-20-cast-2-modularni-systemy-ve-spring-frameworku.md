---
status: publish
published: true
title: 'Část #2: Modulární systémy ve Spring Frameworku'
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "V této části seriálu si rozebereme problematiku refreshe stromu aplikačních
  kontextů. Toto je skvělá vlastnost Springu, která je často nedoceněná a málo používaná.
  Díky ní je možné jednoduše zahodit všechny současné instance bean definované v aplikačním
  kontextu a provést kompletní reinicalizaci kontextu s aktuální konfigurací (tak
  můžeme elegantně změnit chování aplikace bez nutnosti restartu serveru). S refreshem
  aplikačního kontextu se dá vyřešit poměrně dost věcí i v produkčním prostředí -
  navíc netrpí problémem PermGenSpace jako při reloadu kontextu celé aplikace na serveru.
  V situaci, kdy máme ale celý strom aplikačních kontextů se nám situace poměrně komplikuje
  - refresh se totiž stromem sám od sebe nezpropaguje.\r\n\r\n"
wordpress_id: 36
wordpress_url: http://blog.novoj.net/2007/09/20/cast-2-modularni-systemy-ve-spring-frameworku/
date: '2007-09-20 15:41:13 +0200'
date_gmt: '2007-09-20 14:41:13 +0200'
categories:
- Spring Framework
tags: []
comments: []
---
<p>V této části seriálu si rozebereme problematiku refreshe stromu aplikačních kontextů. Toto je skvělá vlastnost Springu, která je často nedoceněná a málo používaná. Díky ní je možné jednoduše zahodit všechny současné instance bean definované v aplikačním kontextu a provést kompletní reinicalizaci kontextu s aktuální konfigurací (tak můžeme elegantně změnit chování aplikace bez nutnosti restartu serveru). S refreshem aplikačního kontextu se dá vyřešit poměrně dost věcí i v produkčním prostředí - navíc netrpí problémem PermGenSpace jako při reloadu kontextu celé aplikace na serveru. V situaci, kdy máme ale celý strom aplikačních kontextů se nám situace poměrně komplikuje - refresh se totiž stromem sám od sebe nezpropaguje.</p>
<p><a id="more"></a><a id="more-36"></a></p>
<h3>Refresh zřetězených aplikačních kontextů</h3>
<p>Spring Framework má jednu skvělou vlastnost, kterou v prostředí web aplikací řada z nás asi nevyužívá. A tou je refresh aplikačních kontextů. V případě, že je konfigurační soubor umístěn na nějakém editovatelném místě (tím je myšleno třebas někde na filesystemu, url ale ne na classpath) je možné po úpravě konfiguračního XML souboru zavolat na aplikačním kontextu refresh, který nám bezpečně refreshne definici bean v něm.</p>
<p>Tento proces má svůj lifecycle. Po zavolání refresh se celý aplikační kontext znovu zčista zinicializuje. Vzniknou tedy nové instance bean, znovu se na nich provede injecting a opětovně jsou zavolány lifecycle akce (jako např. <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/beans/factory/InitializingBean.html" target="_new">afterPropertiesSet</a> apod.). Aplikační kontext o této události také informuje své okolí vysláním události <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/context/event/ContextRefreshedEvent.html" target="_new">ContextRefreshedEvent</a>. Staré beany by měl (pokud jsme si je někde neuvážlivě neuložili do statické proměnné) garbage collector vyhodit. Při zavolání refreshe je dokončen lifecycle původních bean v kontextu (např. v případě <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/beans/factory/DisposableBean.html" target="_new">DisposableBean</a> je zavolána metoda destroy) a naopak v případě nově vytvořených bean jsou zavolány odpovídající lifecycle callback metody (<a href="http://www.jdocs.com/spring/2.0.6/org/springframework/beans/factory/InitializingBean.html" target="_new">afterPropertiesSet</a> například).</p>
<p>Hlídání změn konfiguračních souborů žádný aplikační kontext neprovádí. Ani jsem nenašel žádnou třídu uvnitř Springu, která by podobnou záležitost prováděla. Tzn. hlídání změn konfiguračních souborů si musíme zajistit vlastními silami (a jelikož je to záležitost triviální, nebudu se tu o ní zbytečně rozepisovat :-) ).</p>
<p>Jak je tomu v případě, že máme celý strom aplikačních kontextů? Pokud provedeme refresh kontextu vespod stromu (dejme tomu tedy pouze modulu na nejnižší úrovni) je vše v pořádku. Když ovšem provedeme refresh kořenového kontextu, dostaneme celou struktutru do nekonzistentního stavu - beany podřízených kontextů budou mít stále nasetovány odkazy na původní beany parent kontextu, které v něm byly ještě před refreshem (refresh vytvořil nové, znovu nakonfigurované instance bean). V případě, že se jedná o tzv. <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/beans/factory/DisposableBean.html" target="_new">DisposableBean</a> - teda beany, které si hlídají uzavření kontextu, aby mohly uvolnit systémové zdroje (otevřené kurzory, konekce atd.), dojde pravděpodobně při dalším volání metod na beanách podřízených kontextů k chybě - tyto beany budou mít totiž odkazy na již disposnuté beany z rodičovského kontextu.</p>
<p>Řešení není zase tak složité jak by se mohlo na první pohled zdát. Celý problém lze vyřešit zavedením listeneru, který je dostupný i podřízeným kontextům (využíváme vlastnosti, kdy v podřízených kontextech vidíme beany nadřízeného kontextu). Tento listener naslouchá na event <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/context/event/ContextRefreshedEvent.html" target="_new">ContextRefreshedEvent</a>, který je vyhazován refreshi kontextu a obsahuje list registrovanými objekty, kteří si přejí být notifikovány, když se daný kontext znovu inicializuje. Do tohoto listeneru si zaregistruji i objekty, které mi zajistí následný refresh podřízených kontextů. Pokud tedy provedu refresh root kontextu, kaskádovitě se provedou postupně refreshe i dalších navázaných aplikačních kontextů. Po této kompletní reinicializaci máme ve všech kontextech konzistentní beany s platnými odkazy na dalšími beany.</p>
<p>Tento listener by mohl vypadat například takto:</p>
<p>[source lang="java"]<br />
/**<br />
 * Listens to root application context reload event. Performs refresh of local application context<br />
 * so the beans in local context will be linked properly to new parent ones.<br />
 */<br />
public class GenericRefreshingListener implements ApplicationListener, ApplicationContextAware {<br />
	private static Log log = LogFactory.getLog(GenericRefreshingListener.class);<br />
	private final List childApplicationContexts = new ArrayList();<br />
	private final List notifiedObjects = new ArrayList();<br />
	private ApplicationContext ctxListenerIsDeclaredIn;<br />
	private static final String RELOADING_LISTENER_BEAN_NAME = "reloadingListener";</p>
<p>	public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {<br />
		ctxListenerIsDeclaredIn = applicationContext;<br />
	}</p>
<p>	/**<br />
	 * Handle an application event.<br />
	 *<br />
	 * @param event the event to respond to<br />
	 */<br />
	public void onApplicationEvent(ApplicationEvent event) {<br />
		if(event instanceof ContextRefreshedEvent) {<br />
			ContextRefreshedEvent refreshEvent = (ContextRefreshedEvent)event;<br />
			AbstractRefreshableApplicationContext rootContext =<br />
					(AbstractRefreshableApplicationContext)refreshEvent.getSource();<br />
			//we react only to event fired by context this listener is declared in (the root one)<br />
			if(rootContext == ctxListenerIsDeclaredIn) {<br />
				//switch all children to new parent<br />
				synchronized(childApplicationContexts) {<br />
					for(int i = 0; i < childApplicationContexts.size(); i++) {<br />
						try {<br />
							AbstractRefreshableApplicationContext childContext =<br />
									(AbstractRefreshableApplicationContext)childApplicationContexts.get(i);<br />
							//try to refresh - this is the critical part of process - exception could occur there<br />
							if(log.isInfoEnabled()) {<br />
								log.info("Calling refresh on child context: " + childContext.toString());<br />
							}<br />
							//refresh all beans in childContext<br />
							childContext.refresh();<br />
						}<br />
						catch(Throwable ex) {<br />
							//overgo any exception - just log it, and continue with refreshing other ctxs<br />
							if(log.isErrorEnabled()) {<br />
								log.error("Failed to refresh child context - error occured.", ex);<br />
							}<br />
						}<br />
					}<br />
				}<br />
				//notify all objects that wanted to<br />
				synchronized(notifiedObjects) {<br />
					for(int i = 0; i < notifiedObjects.size(); i++) {<br />
						try {<br />
							IRefreshNotifier notifier = (IRefreshNotifier)notifiedObjects.get(i);<br />
							if(log.isInfoEnabled()) {<br />
								log.info("Calling refresh on registered object: " + notifier.toString());<br />
							}<br />
							notifier.onRefresh(refreshEvent);<br />
						}<br />
						catch(Throwable ex) {<br />
							//overgo any exception - just log it, and continue with notifying other objects<br />
							if(log.isErrorEnabled()) {<br />
								log.error("Failed to notify refresh listener - error occured.", ex);<br />
							}<br />
						}<br />
					}<br />
				}<br />
			}<br />
		}<br />
		if(event instanceof ContextClosedEvent) {<br />
			ContextClosedEvent closedEvent = (ContextClosedEvent)event;<br />
			//switch all children to new parent<br />
			synchronized(childApplicationContexts) {<br />
				for(int i = 0; i < childApplicationContexts.size(); i++) {<br />
					try {<br />
						AbstractRefreshableApplicationContext childContext =<br />
								(AbstractRefreshableApplicationContext)childApplicationContexts.get(i);<br />
						//try to refresh - this is the critical part of process - exception could occur there<br />
						if(log.isInfoEnabled()) {<br />
							log.info("Calling close on child context: " + childContext.toString());<br />
						}<br />
						//refresh all beans in childContext<br />
						childContext.close();<br />
					}<br />
					catch(Throwable ex) {<br />
						//overgo any exception - just log it, and continue with refreshing other ctxs<br />
						if(log.isErrorEnabled()) {<br />
							log.error("Failed to close child context - error occured.", ex);<br />
						}<br />
					}<br />
				}<br />
			}<br />
			//notify all objects that wanted to<br />
			synchronized(notifiedObjects) {<br />
				for(int i = 0; i < notifiedObjects.size(); i++) {<br />
					try {<br />
						IRefreshNotifier notifier = (IRefreshNotifier)notifiedObjects.get(i);<br />
						if(log.isInfoEnabled()) {<br />
							log.info("Calling close on registered object: " + notifier.toString());<br />
						}<br />
						notifier.onClose(closedEvent);<br />
					}<br />
					catch(Throwable ex) {<br />
						//overgo any exception - just log it, and continue with notifying other objects<br />
						if(log.isErrorEnabled()) {<br />
							log.error("Failed to notify refresh listener - error occured.", ex);<br />
						}<br />
					}<br />
				}<br />
			}<br />
		}<br />
	}</p>
<p>	public synchronized void addChildApplicationContext(AbstractRefreshableApplicationContext childContext) {<br />
		if(!childApplicationContexts.contains(childContext)) childApplicationContexts.add(childContext);<br />
	}</p>
<p>	public synchronized void removeChildApplicationContext(AbstractRefreshableApplicationContext childContext) {<br />
		childApplicationContexts.remove(childContext);<br />
	}</p>
<p>	public synchronized void addNotifiedObject(IRefreshNotifier notifier) {<br />
		if(!notifiedObjects.contains(notifier)) notifiedObjects.add(notifier);<br />
	}</p>
<p>	public synchronized void removeNotifiedObject(IRefreshNotifier notifier) {<br />
		notifiedObjects.remove(notifier);<br />
	}</p>
<p>	/**<br />
	 * Hooks child context to parent reload event listenning.<br />
	 *<br />
	 * @param rootContext<br />
	 * @param childContext<br />
	 */<br />
	public static void registerChildForRefreshingEvent(<br />
			AbstractRefreshableApplicationContext rootContext, AbstractRefreshableApplicationContext childContext) {<br />
		if(rootContext.isActive()) {<br />
			GenericRefreshingListener reloadingListener =<br />
					(GenericRefreshingListener)rootContext.getBean(RELOADING_LISTENER_BEAN_NAME);<br />
			reloadingListener.addChildApplicationContext(childContext);<br />
		}<br />
		else {<br />
			if(log.isErrorEnabled()) {<br />
				log.error("Cannot register " + childContext.toString() +<br />
						" for refreshing events: root context is closed!");<br />
			}<br />
		}<br />
	}</p>
<p>	/**<br />
	 * Unhooks child context to parent reload event listenning.<br />
	 *<br />
	 * @param rootContext<br />
	 * @param childContext<br />
	 */<br />
	public static void unregisterChildForRefreshingEvent(<br />
			AbstractRefreshableApplicationContext rootContext, AbstractRefreshableApplicationContext childContext) {<br />
		if(rootContext.isActive()) {<br />
			GenericRefreshingListener reloadingListener =<br />
					(GenericRefreshingListener)rootContext.getBean(RELOADING_LISTENER_BEAN_NAME);<br />
			reloadingListener.removeChildApplicationContext(childContext);<br />
		}<br />
		else {<br />
			if(log.isInfoEnabled()) {<br />
				log.info("Cannot unregister " + childContext.toString() +<br />
						" from refreshing events: root context already closed!");<br />
			}<br />
		}<br />
	}</p>
<p>	/**<br />
	 * Hooks child context to parent reload event listenning.<br />
	 *<br />
	 * @param rootContext<br />
	 * @param notifier<br />
	 */<br />
	public static void registerNotifierForRefreshingEvent(<br />
			AbstractRefreshableApplicationContext rootContext, IRefreshNotifier notifier) {<br />
		if(rootContext.isActive()) {<br />
			GenericRefreshingListener reloadingListener =<br />
					(GenericRefreshingListener)rootContext.getBean(RELOADING_LISTENER_BEAN_NAME);<br />
			reloadingListener.addNotifiedObject(notifier);<br />
		}<br />
		else {<br />
			if(log.isErrorEnabled()) {<br />
				log.error("Cannot register " + notifier.toString() +<br />
						" for refreshing events: root context is closed!");<br />
			}<br />
		}<br />
	}</p>
<p>	/**<br />
	 * Unhooks child context to parent reload event listenning.<br />
	 *<br />
	 * @param rootContext<br />
	 * @param notifier<br />
	 */<br />
	public static void unregisterNotifierForRefreshingEvent(<br />
			AbstractRefreshableApplicationContext rootContext, IRefreshNotifier notifier) {<br />
		if(rootContext.isActive()) {<br />
			GenericRefreshingListener reloadingListener =<br />
					(GenericRefreshingListener)rootContext.getBean(RELOADING_LISTENER_BEAN_NAME);<br />
			reloadingListener.removeNotifiedObject(notifier);<br />
		}<br />
		else {<br />
			if(log.isInfoEnabled()) {<br />
				log.info("Cannot unregister " + notifier.toString() +<br />
						" from refreshing events: root context already closed!");<br />
			}<br />
		}<br />
	}</p>
<p>}<br />
[/source]</p>
<p>Listener automaticky provede refresh zaregistrovaných dětských kontextů a dále dokáže notifikovat i libovolný objekt, který implementuje rozhraní IRefreshNotifier s callback metodami.</p>
<p>[source lang="java"]<br />
/**<br />
 * Can be implemented by any object, that want to be notified when context is<br />
 * refreshed. This interface is meant to be used by object, that are outside<br />
 * spring context itself (beans inside it can react to ContextRefreshed event<br />
 * directly).<br />
 *<br />
 * Could be used for example by servlet Filters, that are instantiated by web<br />
 * server itself and we have no control over them.<br />
 */<br />
public interface IRefreshNotifier {</p>
<p>	/**<br />
	 * Callback method executed on application context refresh.<br />
	 */<br />
	void onReload(ApplicationEvent event);</p>
<p>	/**<br />
	 * Callback method executed on application context closing.<br />
	 */<br />
	void onClose(ApplicationEvent event);</p>
<p>}<br />
[/source]</p>
<p><i><b>Upozornění:</b> tento kód neprošel unit testy - pro naše použití máme poněkud odlišný mechanismus reloadu (uvedený příklad z něj vychází - nepsal jsem to celé z ruky), proto berte příklad spíš jen jako inspiraci, spíš než kód, který byste šoupli do produkce ;-) </i></p>
<p>V řadě případů je prostě skvělé mít možnost rekonfigurovat webaplikaci, aniž bychom museli restartovat celý web kontext aplikace na úrovní serveru - a to jak ve vývojové fázi, tak i při drobných dolaďovačkách při nasazování systému.</p>
<h3>Refresh odkazů v objektech technologií třetích stran</h3>
<p>Dalším problémem, který s refreshem kontextů ve webové aplikaci může souviset jsou objekty třetích knihoven, které jsme se Springem integrovali. Tady musíme být uvážliví. Uvedu dva příklady technologií, se kterými jsme již tuto záležitost řešili a pro své použití i vyřešili.</p>
<h4>Apache Struts</h4>
<p>První technologií jsou Apache Struts - Spring má v sobě již zabudované třídy pro propojení se Strutsy. Jedná se jednak o <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/web/struts/ContextLoaderPlugIn.html" target="_new">ContextLoaderPlugin</a> a potom také o <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/web/struts/DelegatingActionProxy.html" target="_new">DelegatingActionProxy</a>. V souvislosti s tímto nám postačuje jen vyřešit reload podřízeného kontextu při refreshi předka - toto jsem rozebral již v předchozí části. Víc řešit již nemusíme, jelikož třída <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/web/struts/DelegatingActionProxy.html" target="_new">DelegatingActionProxy</a> si vždy znovu sahá do aktuálního aplikačního kontextu pro spring beanu, na kterou deleguje provedení Struts akce. Díky kaskádovému refreshi dostaneme konsistentní beanu.</p>
<h4>Java Server Faces</h4>
<p>Druhou technologií jsou Java Server Faces. Zde probíhá integrace mj. na úrovni <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/web/jsf/DelegatingVariableResolver.html" target="_new">DelegatingVariableResolver</a>, který se stará o injektování Spring bean do managovaných bean JSF. Tady máme problém v tom, že se nám reference na objekty dostávají do objektů, které jsou ve správě JSF. Nám postačovalo jednoduché řešení - které patří mezi best practices JSF - managované beany JSF mít rozdělené na tzv. servisní a modelové. Modelové beany mohou být ukládány v session, jsou serializovatelné a jsou to jen jednoduché POJO, které se na žádné Spring beany neodkazují. Servisní beany jsou typicky bezstavové, jsou striktně ukládány do request nebo none scope a mohou libovolně obsahovat reference na Spring beany nebo na modelové beany. Jelikož jsou tyto servisní beany vytvářeny pro každý request znovu, je vždy v tento moment vyvoláván i <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/web/jsf/DelegatingVariableResolver.html" target="_new">DelegatingVariableResolver</a>, který vždy získá reference na aktuální a konzistentní beany ve Spring kontextu.</p>
<p>Pokud by bylo třeba mít servisní beany s odkazy na spring beany mít ukládané v session scope, napadlo mne jediné řešení. Upravit <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/web/jsf/DelegatingVariableResolver.html" target="_new">DelegatingVariableResolver</a> tak, aby místo injektování referencí na Spring beany injektoval pouze dynamické proxy (s použitím např. CGLIB), které by byly implementované tak, že každé volání na proxy by převedly na volání beany ze Spring kontextu, kterou by si vždy čerstvě vyzvedly. Do tohoto řešení jsem se ale nepouštěl, jelikož jsme jej, díky zavedení výše uvedného pravidla, nakonec nepotřebovali.</p>
<h3>Problém s registrací listenerů</h3>
<p>Pokud se budete trochu více hrabat ve správě listenerů ve spring kontextech, narazíte na jednu věc, která mne trochu zarazila a pár věcí zkomplikovala. Ve standardním aplikačním kontextu (chování je definováno v <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/context/support/AbstractApplicationContext.html" target="_new">AbstractApplicationContext</a>, ze kterého většina - ne-li všechny - aplikační kontexty dědí) není možné přidat nový listener po refreshi aplikačního kontextu.</p>
<p>Máte jen tri možnosti:</p>
<ol>
<li>aplikační listenery definovat přímo v konfiguraci springu - tyto listenery jsou automaticky registrovány standardními BeanPostProcessory po vytvoření příslušné beany v kontextu</li>
<li>aplikačně listenery registrovat před samotným refreshem kontextu - což vyžaduje vytvořit kontext nastavením flagu refresh=false a pak provést refresh manuálně</li>
<li>zaregistrovat si vlastní multicaster, který bude umožňovat registraci nových listenerů do běžícího kontextu (nenarazil jsem na jediný důvod, proč by to nemělo být možné / správné)</li>
</ol>
<p>Osobně jsem nechtěl příliš ohýbat stávající chování a proto jsem se přidržel první možnosti a definuji výše uvedený listener standardně v konfiguraci parent kontextu. Dětské kontexty se do toho listeneru registrují přes statickou metodu, které předají odkaz na parent kontext, ve kterém listener "žije". Statické metody se již postarají o to, aby uvedený listener nalezly podle jeho jména a zaregistrovaly nový objekt.</p>
<p>Prvotní myšlenku, že pro každý nový dětský kontext (resp. libovolný objekt, který si přeje být notifikován) vytvořím novou instanci listeneru a registruji ji za běhu do aplikačního kontextu, jsem nakonec opustil.</p>
<h3>Co bude v dalším díle?</h3>
<p>V přechozím díle jsme si ukázali, jak jednotlivé moduly separovat a propojit ve stromu. V tom dnešním, jak strom udržet konzistentní a refreshovatelný za běhu aplikace. Další díl bude o tom, jak jednotlivé moduly mezi sebou propojit - respektive, jak zajistit interakci mezi jednotlivými moduly.</p>
<p><a href="http://blog.novoj.net/2007/09/27/cast-3-modularni-systemy-ve-spring-framework/">Díl #3: Vystavení “interface” bean modulů</a></p>
