---
status: publish
published: true
title: 'Část #4: Modulární systémy ve Spring Framework'
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Aplikační události jsou jedním ze základních stavebních kamenů Springu a
  proto by bylo škoda se ochudit o tuto skvělou vlastnost na rozhraní modulů. Je zřejmé,
  že nebudeme chtít otevřít všechny aplikační události svému okolí, nicméně u řady
  událostí bychom chtěli umožnit ostatním modulům reagovat. Jako příklad uvedu interakci
  mezi modulem pro správu uživatelů a notifikačním modulem - notifikační modul se
  stará o rozesílání emailových notifikací v reakci na konkrétní aplikační události
  (samozřejmě obecně - konfigurovatelně). To je typická ukázka stavu, kdy chceme,
  aby uživatelský modul dokázal emitovat třebas událost “založení nového uživatele”
  tak, aby notifikační modul mohl reagovat odesláním emailu.\r\n\r\n"
wordpress_id: 38
wordpress_url: http://blog.novoj.net/2007/10/04/cast-4-modularni-systemy-ve-spring-framework/
date: '2007-10-04 08:07:25 +0200'
date_gmt: '2007-10-04 07:07:25 +0200'
categories:
- Spring Framework
tags: []
comments:
- id: 811
  author: Vlasta
  author_email: vlastimil@vavru.cz
  author_url: http://vavru.cz
  date: '2007-10-04 20:01:21 +0200'
  date_gmt: '2007-10-04 19:01:21 +0200'
  content: Skvělá práce. Pro mě jsou články tohoto typu ty vůbec nejzajímavější.
- id: 813
  author: Tomas
  author_email: hradec@oksystem.cz
  author_url: ''
  date: '2007-10-05 07:55:31 +0200'
  date_gmt: '2007-10-05 06:55:31 +0200'
  content: Výborný seriál, doufám že brzo přibudou další.
- id: 921
  author: Petr
  author_email: pjuza@seznam.cz
  author_url: http://javicka.blogspot.com
  date: '2007-10-29 17:16:31 +0100'
  date_gmt: '2007-10-29 16:16:31 +0100'
  content: "Díky moc za tento článek. Sám vím, kolik je za tím práce dát takovýto
    článek dohromady, takže fakt super. \r\n\r\nS těmi transakcemi si také myslím,
    že nebude problém - jak v rámci jednoho aplikačního kontextu, tak v rámci více
    kontextů resp. root kontextu. Jen v tvém pojetí se bude muset naimplementovat
    transakční interseptor programově, protože ty vkládáš veřejné beany dynamicky
    za běhu."
- id: 923
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-10-30 05:55:02 +0100'
  date_gmt: '2007-10-30 04:55:02 +0100'
  content: "Dík za pochvalu :-) .\r\nJinak myslím, že by nebylo ani potřeba řešit
    transakční interceptor programově. Ony ty beany jsou totiž normálně vytvářené
    Springem a Spring je tudíž může normálně obalit proxy objekty - jen se vše odehraje
    v kontextu nižší úrovně. Já pak jen v závěru už hotovou \"public\" beanu vezmu
    a zaregistruji ji také do nadřízeného kontextu.\r\n\r\nV TODO listu mám zaznamenané,
    abych v tomhle ohledu teorii podpořil praxí, takže jakmile ten test napíšu, hodím
    sem o tom ještě dodatek. Tohle je podle mého názoru právě věc, která v modulárním
    systému postaveném na OSGI nepůjde."
- id: 2677
  author: Jety
  author_email: mail@jetensky.net
  author_url: http://jetensky.net/blog
  date: '2008-08-08 08:50:38 +0200'
  date_gmt: '2008-08-08 07:50:38 +0200'
  content: "Ahoj Honzo, bavil jsem se dnes s naším technologickým šéfem vývoje o projektu
    P@W (PeopleAtWork) a nasazení Springu a modulárnosti. Zjistil jsem, že v P@Wu
    kolega naimplementoval modulární řešení propagovaných bean implementujících rozhraní
    ModulePropagatedBean. Pokud ho beana implementuje, je postrčena do Root kontextu
    a je k dispozici ostatním modulům. Hodně mi to připomínalo tvoje řešení, tak jsem
    mu ukazoval tvoje stránky, a on na to, no vždyť podle tohohle jsem to naprogramoval
    :) :)!\r\n\r\nTakže shrnuto a podtrženo, v našem produktu je použit tvůj návrhový
    vzor pro Spring z tohoto seriálu - řešení modularity jednotlivých komponent a
    poskládání výsledného Spring kontextu tak, aby zároveň vznikl fungující aplikační
    kontext + aby byla udržena nezávislost modulů - balení v samostatném Jaru.\r\n\r\nTušil
    jsem, že ti to udělá radost, tak to píšu ;)."
- id: 2690
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2008-08-10 18:18:13 +0200'
  date_gmt: '2008-08-10 17:18:13 +0200'
  content: No tak to jsem rád, že nápad nezůstane zapomenut. Přesně z tohoto důvodu
    jsem celou sérii psal. Pokud byste měli s řešením nějaké pozitivní / negativní
    zkušenosti, tak vám budu vděčný, pokud je sem připíšete. My to řešení docela uspokojivě
    provozujeme rok, tak by mě zajímala zase vaše zkušenost.
---
<p>Aplikační události jsou jedním ze základních stavebních kamenů Springu a proto by bylo škoda se ochudit o tuto skvělou vlastnost na rozhraní modulů. Je zřejmé, že nebudeme chtít otevřít všechny aplikační události svému okolí, nicméně u řady událostí bychom chtěli umožnit ostatním modulům reagovat. Jako příklad uvedu interakci mezi modulem pro správu uživatelů a notifikačním modulem - notifikační modul se stará o rozesílání emailových notifikací v reakci na konkrétní aplikační události (samozřejmě obecně - konfigurovatelně). To je typická ukázka stavu, kdy chceme, aby uživatelský modul dokázal emitovat třebas událost “založení nového uživatele” tak, aby notifikační modul mohl reagovat odesláním emailu.</p>
<p><a id="more"></a><a id="more-38"></a></p>
<h4>Přeposílání eventů z jednoho modulu do jiného modulu</h4>
<p>Další lahůdkou je možnost posílání událostí z oddělených aplikačních kontextů. Standardně se vám multicaster postará o vyvolání listenerů na úrovni aplikačního kontextu, ze kterého pochází beana, která událost vyvolala (respektive <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/context/ApplicationEventPublisher.html" target="_new">ApplicationEventPublisher</a>, který použijete pro distribuci události). Dále je událost propagována do nadřazených kontextů. Nedostane se vám tedy do aplikačních kontextů, které nejsou ve stromě kontextů nad tím vaším.</p>
<p>V praxi se ovšem může hodit, mít možnost na události "modulu" reagovat v jiném modulu. Některé události v podstatě mohou tvořit část rozhraní daného modulu (jistě většina událostí bude pouze pro vnitřní účely, některé by se ale hodilo propagovat vně a zařadit je jako součást rozhraní).</p>
<p>Jak tedy zajistit propagaci těchto událostí i do modulů na stejné úrovni? Opět k tomu můžeme využít <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/beans/factory/config/BeanPostProcessor.html" target="_new">BeanPostProcessor</a>. Zavedeme nové rozhraní s názvem ExternalEventListener, které budou implementovat ty listenery, které budou chtít naslouchat událostem okolních modulů. Rozhraní ExternalEventListener má metodu getExternalEventClasses, která vrací pole objektů Class těch externích událostí, kterým chtějí naslouchat. </p>
<p>[source lang="java"]<br />
/**<br />
 * Module listeners can implement this interface whenever they need to listen to events fired in other modules.<br />
 * By default events fired in module are listenable only in module itself and in parent (root) context.<br />
 */<br />
public interface ExternalEventListener {</p>
<p>	/**<br />
	 * Method returns class specifications of event types, that should be forwarded to this module<br />
	 * by root context.<br />
	 *<br />
	 * BEWARE: do not listen to events that are fired by your module, this would cause this event<br />
	 * to be forwarded too, and you'll receive it two times!!!<br />
	 *<br />
	 * @return<br />
	 */<br />
	Class[] getExternalEventsTypes();</p>
<p>}<br />
[/source]</p>
<p>Dále zavedeme marker rozhraní PublicEvent, které budou implementovat aplikační události, které modul považuje za veřejné (tzn. zařazuje je do svého rozhraní).</p>
<p>[source lang="java"]<br />
/**<br />
* Marker interface that could be implemented by ApplicationEvent classes to declare, that this i module public event, that could<br />
* be catched and processed by listeners of other modules.<br />
*/<br />
public interface PublicEvent {</p>
<p>}<br />
[/source]</p>
<p>V kořenovém kontextu zaregistrujeme aplikační listener s názvem ExternalEventPropagateListener. Listenerem v root contextu proběhnou všechny události (tedy i události jednotlivých modulů). Tento listener udržuje mapu aplikačních kontextů (respektive libovolných jiných objektů), které si přejí "přeposlat" externí události. Listener si eviduje vždy seznam Class aplikačních událostí, o které má daný objekt zájem a v případě, že takovou událost zachytí, provede přeposlání události danému registrovanému objektu. Před vlastní registrací je prověřeno, zda modul skutečně požaduje přeposílání pouze veřejných událostí - pokud nikoliv, je vyhozena vyjímka IllegalArgumentException.</p>
<p>[source lang="java"]<br />
/**<br />
 * Forwarding listener / publisher that is registered to listen to events in one application context,<br />
 * and if they conform to predefined types publishes them into second application context where they<br />
 * otherwise would not be visible.<br />
 */<br />
public class ExternalEventPropagateListener implements ApplicationListener, DisposableBean {<br />
	private static Log log = LogFactory.getLog(ExternalEventPropagateListener.class);<br />
	public static final String FORWARDING_LISTENER_BEAN_NAME = "externalEventPropagateListener";<br />
	private final List forwards = new ArrayList();<br />
	private final Set currentlyProcesedEvents = new HashSet();</p>
<p>	public void destroy() throws Exception {<br />
		forwards.clear();<br />
	}</p>
<p>	/**<br />
	 * Handle an application event.<br />
	 *<br />
	 * @param event the event to respond to<br />
	 */<br />
	public void onApplicationEvent(ApplicationEvent event) {<br />
		//avoid inifinite loops<br />
		synchronized(currentlyProcesedEvents) {<br />
			if(!currentlyProcesedEvents.contains(event)) {<br />
				currentlyProcesedEvents.add(event);<br />
				try {<br />
					for(int i = 0; i < forwards.size(); i++) {<br />
						ForwardMappingHolder holder = (ForwardMappingHolder)forwards.get(i);<br />
						for(int j = 0; j < holder.getExternalEventClasses().length; j++) {<br />
							Class externalEventClass = holder.getExternalEventClasses()[j];<br />
							if(externalEventClass.isAssignableFrom(event.getClass())) {<br />
								if(log.isDebugEnabled()) {<br />
									log.debug("Forwarding event " + event.toString() + " to child context " + holder.getContextToForwardedTo().toString());<br />
								}<br />
								//observing event class matches - foward event<br />
								holder.getContextToForwardedTo().publishEvent(event);<br />
								//continue checking next holder<br />
								break;<br />
							}<br />
						}</p>
<p>					}<br />
				}<br />
				finally {<br />
					currentlyProcesedEvents.remove(event);<br />
				}<br />
			}<br />
		}<br />
	}</p>
<p>	public synchronized void addEventForwarding(AbstractRefreshableApplicationContext childContext, Class[] wantedEventClasses) {<br />
		for(int i = 0; i < wantedEventClasses.length; i++) {<br />
			Class wantedEventClass = wantedEventClasses[i];<br />
			if (!PublicApplicationEvent.class.isAssignableFrom(wantedEventClass)) {<br />
				String msg = "Cannot register listener to a " + wantedEventClass.getName() + ". This class does not " +<br />
						"implement PublicApplicationEvent interface and thus cannot be externaly observed.";<br />
				if (log.isFatalEnabled()) {<br />
					log.fatal(msg);<br />
				}<br />
				throw new IllegalArgumentException(msg);<br />
			}<br />
		}<br />
		forwards.add(<br />
				new ForwardMappingHolder(<br />
						childContext,<br />
						wantedEventClasses<br />
				)<br />
		);<br />
	}</p>
<p>	public synchronized void removeEventForwarding(AbstractRefreshableApplicationContext childContext) {<br />
		Iterator it = forwards.iterator();<br />
		while(it.hasNext()) {<br />
			ForwardMappingHolder holder = (ForwardMappingHolder)it.next();<br />
			if(holder.getContextToForwardedTo() == childContext) {<br />
				it.remove();<br />
				break;<br />
			}<br />
		}<br />
	}</p>
<p>	/**<br />
	 * Hooks child context to parent reload event listenning.<br />
	 *<br />
	 * @param rootContext<br />
	 * @param childContext<br />
	 */<br />
	public static void registerChildForForwardingEvents(<br />
			AbstractRefreshableApplicationContext rootContext,<br />
			AbstractRefreshableApplicationContext childContext,<br />
			Class[] wantedEventClasses) {<br />
		if(rootContext.isActive()) {<br />
			ForwardingListener forwardingListener = (ForwardingListener)rootContext.getBean(FORWARDING_LISTENER_BEAN_NAME);<br />
			forwardingListener.addEventForwarding(childContext, wantedEventClasses);<br />
		}<br />
		else {<br />
			if(log.isErrorEnabled()) {<br />
				log.error("Cannot register " + childContext.toString() + " for forwarning events: root context is closed!");<br />
			}<br />
		}<br />
	}</p>
<p>	/**<br />
	 * Unhooks child context to parent reload event listenning.<br />
	 *<br />
	 * @param rootContext<br />
	 * @param childContext<br />
	 */<br />
	public static void unregisterChildForForwardingEvents(AbstractRefreshableApplicationContext rootContext, AbstractRefreshableApplicationContext childContext) {<br />
		if(rootContext.isActive()) {<br />
			ForwardingListener forwardingListener = (ForwardingListener)rootContext.getBean(FORWARDING_LISTENER_BEAN_NAME);<br />
			forwardingListener.removeEventForwarding(childContext);<br />
		}<br />
		else {<br />
			if(log.isInfoEnabled()) {<br />
				log.info("Cannot unregister " + childContext.toString() + " from forwarning events: root context already closed!");<br />
			}<br />
		}<br />
	}</p>
<p>	/**<br />
	 * Holds information about one forwarding mapping.<br />
	 */<br />
	private class ForwardMappingHolder {<br />
		private AbstractRefreshableApplicationContext contextToForwardedTo;<br />
		private Class[] externalEventClasses;</p>
<p>		public ForwardMappingHolder(AbstractRefreshableApplicationContext contextToForwardedTo, Class[] externalEventClasses) {<br />
			this.contextToForwardedTo = contextToForwardedTo;<br />
			this.externalEventClasses = externalEventClasses;<br />
		}</p>
<p>		public AbstractRefreshableApplicationContext getContextToForwardedTo() {<br />
			return contextToForwardedTo;<br />
		}</p>
<p>		public Class[] getExternalEventClasses() {<br />
			return externalEventClasses;<br />
		}</p>
<p>	}</p>
<p>}<br />
[/source]</p>
<p>Výše zmíněný <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/beans/factory/config/BeanPostProcessor.html" target="_new">BeanPostProcesor</a> s názvem ExternalEventPropagatePostProcessor nám při startu modulu prověří každou beanu, zda implementuje rozhraní ExternalEventListener a pokud ano, zaregistruje do kořenového kontextu aktuálně procesovaný aplikační kontext se seznamem Class aplikačních eventů, které právě procesovaný listener požaduje.</p>
<p>[source lang="java"]<br />
/**<br />
 * This postprocessor registers for forwarding all events, that listeners in current context<br />
 * wants (via contract of ExternalEventListener interface).<br />
 */<br />
public class ExternalEventListenerPostProcessor implements BeanPostProcessor {<br />
	private static Log log = LogFactory.getLog(ExternalEventListenerPostProcessor.class);<br />
	private AbstractRefreshableApplicationContext rootContext;<br />
	private AbstractRefreshableApplicationContext localContext;</p>
<p>	public ExternalEventListenerPostProcessor(AbstractRefreshableApplicationContext rootContext, AbstractRefreshableApplicationContext localContext) {<br />
		this.rootContext = rootContext;<br />
		this.localContext = localContext;<br />
	}</p>
<p>	public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {<br />
		return bean;<br />
	}</p>
<p>	public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {<br />
		if(bean instanceof ExternalEventListener) {<br />
			ExternalEventListener listener = (ExternalEventListener)bean;<br />
			Class[] classes = listener.getExternalEventsTypes();<br />
			if (classes != null && classes.length > 0) {<br />
				if(log.isInfoEnabled()) {<br />
					log.info("Registering module for obtaining following external events (" + beanName + "): " + convertClassesToString(classes));<br />
				}<br />
				ForwardingListener.registerChildForForwardingEvents(rootContext, localContext, classes);<br />
			}<br />
		}<br />
		return bean;<br />
	}</p>
<p>	/**<br />
	 * Convert class list to simple class name string.<br />
	 * @param classes<br />
	 * @return<br />
	 */<br />
	private String convertClassesToString(Class[] classes) {<br />
		StringBuffer result = new StringBuffer();<br />
		if(classes != null) {<br />
			for(int i = 0; i < classes.length; i++) {<br />
				Class aClass = classes[i];<br />
				String className = aClass.getName();<br />
				result.append(className.substring(className.lastIndexOf(".") + 1));<br />
				if (i < classes.length) result.append(",");<br />
			}<br />
		}<br />
		return result.toString();<br />
	}</p>
<p>}<br />
[/source]</p>
<p>Celý výše uvedený proces jsem ještě zakreslil jako sequence diagram, jelikož při takovém množství kódu by mohla být celková představa o fungování celého procesu poněkud zmatená. Pokud tomu tak je, snad se mi podaří nejasnosti rozptýlit následujícím diagramem:</p>
<div align="center">
<a href='http://blog.novoj.net/binary//2007/09/springmodules_sequence2.PNG' title='Sekvenční diagram znázorňující princip přeposílání událostí mezi moduly'><img src='http://blog.novoj.net/binary//2007/09/springmodules_sequence2.PNG' alt='Sekvenční diagram znázorňující princip přeposílání událostí mezi moduly'  style="width: 100%; height: 100%;"/></a></p>
<div><i>Sekvenční diagram znázorňující princip přeposílání událostí mezi moduly</i></div>
</div>
<h4>Závěr seriálu</h4>
<p>Dnešní díl uzavírá seriál o modulárních systémech ve Springu. Popsané řešení dostatečně naplňuje naše požadavky na modulární serverový systém. Je možné že v budoucnosti třebas sáhneme po OSGI, ale v současné době toto jednoduché řešení postačuje.</p>
<p>Sami vidíte, že popsaná implementace, nejde za hranice Springu a že se jedná jen o nenáročné řešení, která vám nezabere víc jak jeden, dva dny implementace a otestování ve vašich podmínkách.</p>
<p>Hlavní přínos vidím v tom, že je jednoduše možné skládat nezávislé knihovny = moduly s přesným vydefinováním jejich rozhraní (nikoliv na úrovni class API, ale na úrovni živých funkčních objektů daného modulu). Naopak můžeme vydefinovat podmnožinu (typicky servisních bean), které budou pro všechny moduly společné, čímž je možné ve výsledku efektivně zjednodušit správu výsledné kompozice.</p>
<p>S čím si zatím nejsem 100% jistý, zda bude možné bez problémů vytvářet transakce zahrnující operace na beanami z různých modulů (tj. aplikačních kontextů) pomocí AOP. Teoreticky by to mělo fungovat bez větších potíží, ale jelikož nejsem schopný věc zpatra domyslet a nenašel jsem zatím čas si na to napsat test (ještě jsem to nepotřeboval), nechci to tu prezentovat jako fakt. </p>
<div align="center">...</div>
<p>Doufám, že vám seriál líbil a že jej považujete za přínosný. Budu vám vděčný, když mi na závěr napíšete nějaký komentář k němu, i kdyby ten komentář měl být pouze ve smyslu, že čas strávený jeho čtením pro vás nebyl čas ztracený. Předem díky za reakce ... statistiky jsou jedna věc a přímá zpětná vazba je věc jiná :-) .</p>
