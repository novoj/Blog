---
status: publish
published: true
title: 'Část #3: Modulární systémy ve Spring Framework'
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "V prvním díle jsme si ukázali, jak jednotlivé moduly separovat a propojit
  ve stromu. V předchozím pak způsob, jak strom udržet konzistentní a refreshovatelný
  za běhu aplikace. Dnešní díl bude o tom, jak jednotlivé moduly mezi sebou propojit
  - respektive, jak zajistit interakci mezi jednotlivými moduly. \r\n\r\n"
wordpress_id: 34
wordpress_url: http://blog.novoj.net/2007/09/27/cast-3-modularni-systemy-ve-spring-framework/
date: '2007-09-27 20:04:25 +0200'
date_gmt: '2007-09-27 19:04:25 +0200'
categories:
- Spring Framework
tags: []
comments: []
---
<p>V prvním díle jsme si ukázali, jak jednotlivé moduly separovat a propojit ve stromu. V předchozím pak způsob, jak strom udržet konzistentní a refreshovatelný za běhu aplikace. Dnešní díl bude o tom, jak jednotlivé moduly mezi sebou propojit - respektive, jak zajistit interakci mezi jednotlivými moduly. </p>
<p><a id="more"></a><a id="more-34"></a></p>
<h3>Vystavení "interface" bean modulů</h3>
<p>Pokud se vydáte cestou tvorby stromu z aplikačních kontextů, pravděpodobně narazíte na problém rozhraní jednotlivých modulů. Vraťme se k našemu příkladu reportovacího modulu, modulu uživatelů a web aplikace. Jak vyřešit velmi pravděpodobný usecase, kdy z web aplikace budeme chtít v reportu zobrazit seznam uživatelů? Jedná se o propojení všech třech modulů, které jsou nezávislé (mají oddělené životní prostory a jeden nevidí k druhému) a které jsou ve stromu na stejné úrovni - podřízené stejnému root contextu.</p>
<p>Tuto záležitost lze řešit kombinací <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/beans/factory/config/BeanPostProcessor.html" target="_new">BeanPostProcessoru</a> a anotací nebo použitím marker interfacu (popř. zavedením vlastního <a href="http://www.springframework.org/docs/reference/extensible-xml.html#extensible-xml-namespacehandler" target="_new">namespace handleru</a> - nové fíčurky springu od verze 2.X). Do aplikačního kontextu zaregistrujeme <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/beans/factory/config/BeanPostProcessor.html" target="_new">BeanPostProcesor</a>, kterému do konstruktoru vložíme odkaz na root kontext. Tento post procesor každou beanu po inicializaci prověří na přítomnost anotace (nebo implementaci marker interfacu), a pokud vyhovuje dané podmínce, zaregistruje tuto beanu jako singleton v root kontextu s pomocí metody <a href="http://www.jdocs.com/spring/1.2.8/org/springframework/beans/factory/config/ConfigurableBeanFactory.html?m=M-registerSingleton(String,Object)#M-registerSingleton(String,Object)" target="_new">registerSingleton</a> dostupnou na bean factory aplikačního kontextu.</p>
<p>Výřez <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/beans/factory/config/BeanPostProcessor.html" target="_new">BeanPostProcessoru</a>, který toto zajišťuje je zobrazen v následujícím příkladu:</p>
<p>[source lang="java"]<br />
/**<br />
 * This postprocessor exports all beans marked as ModulePublicInterface into root CPS<br />
 * application context.<br />
 */<br />
public class ModulePublicInterfacePostProcessor implements BeanPostProcessor {<br />
	private static Log log = LogFactory.getLog(ModulePublicInterfacePostProcessor.class);<br />
	private AbstractRefreshableApplicationContext rootContext;</p>
<p>	public ModulePublicInterfacePostProcessor(AbstractRefreshableApplicationContext rootContext) {<br />
		this.rootContext = rootContext;<br />
	}</p>
<p>	public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {<br />
		return bean;<br />
	}</p>
<p>	public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {<br />
		if (bean instanceof ModulePublicInterface) {<br />
			if (log.isInfoEnabled()) {<br />
				log.info("Exporting module public interface bean: " + beanName);<br />
			}<br />
			DefaultListableBeanFactory rootFactory = (DefaultListableBeanFactory)rootContext.getBeanFactory();<br />
			rootFactory.registerSingleton(beanName, bean);<br />
		}<br />
		return bean;<br />
	}<br />
}<br />
[/source]</p>
<p><a href="http://www.jdocs.com/spring/2.0.6/org/springframework/beans/factory/config/BeanPostProcessor.html" target="_new">BeanPostProcessor</a> testuje beany na implementaci jednoduchého marker interfacu:</p>
<p>[source lang="java"]<br />
/**<br />
 * Marker interface signalizing, that class of this type could be used as public intefrace<br />
 * of particular module. ModulePublicInterfacePostProcessor exports all beans<br />
 * with this marker to root application context, so they are reachable by any<br />
 * other modules or web application contexts.<br />
 */<br />
public interface ModulePublicInterface {}<br />
[/source]</p>
<p>Při refreshi aplikačního kontextu následujícího inicializovaného modulu již dokáže tuto beanu Spring automaticky nasetovat (respektive, vy jste schopni ji dynamicky voláním metody getBean v aplikačním kontextu takového modulu získat). Pak už je důležité se jen vyvarovat cyklických závislostí mezi moduly a zajistit, aby se moduly inicializovaly ve správném pořadí. Celý princip je možné ukázat na popisu inicializační sekvence našeho ukázkového příkladu:</p>
<div align="center">
<a href='http://blog.novoj.net/binary/2007/09/springmodules_sequence1.PNG' title='Sekvenční diagram znázorňující princip inicializace modulů'><img src='http://blog.novoj.net/binary/2007/09/springmodules_sequence1.PNG' alt='Sekvenční diagram znázorňující princip inicializace modulů'  style="width: 100%; height: 100%;"/></a></p>
<div><i>Sekvenční diagram znázorňující princip inicializace modulů</i></div>
</div>
<p>Tímto principem neporušujeme zapouzdřenost daného modulu - moduly jsou stále oddělené a mají své životní prostory. Pouze výběrově zpřístupňujeme beany, které tvoří rozhraní modulu. Beany rozhraní jsou již správně inicializované, takže z programového hlediska nemusíme už nic dělat - stačí nechat Spring aplikaci kompletně sestavit. V sekvenčním diagramu je naznačeno, že kompozici jednotlivých modulů s root kontextem zajišťuje "aplikace" - nicméně i tuto část můžeme nahradit Springem. Pokud v konfiguračním souboru springu uvedete deklaraci beany, která je aplikačním kontextem, zajistí vytvoření a propojení oddělených spring kontextů sám Spring. Registraci bean post procesorů opět může zajistit Spring - pokud najde beany typu <a href="http://www.jdocs.com/spring/2.0.6/org/springframework/beans/factory/config/BeanPostProcessor.html" target="_new">BeanPostProcessor</a> v konfiguraci automaticky je použije.</p>
<p>Testovat moduly je možné aniž by ke svému běhu potřebovaly mít nahozenou celou infrastrukturu. Při testech pouze modulu "dohodíme" chybějící beany, které modul vyžaduje od svého okolí (např. dataSource z root kontextu). Místo bean rozhraní ostatních modulů můžeme v testech použít mock beany - popřípadě můžeme dané beany označit jako lazy-init="true", takže pokud si na ně test vyloženě nesáhne (nebo je nebude vyžadovat jiná ne-lazy beana) vynechá je Spring z inicializace a tudíž mu ani nebude vadit, že nemá dostupnou beanu, kterou si přejete injektovat.</p>
<h3>BeanPostProcessor vs. BeanFactoryPostProcessor</h3>
<p>Musím uvést výše uvedený sekvenční diagram na pravou míru. Aplikační kontext jako takový neakceptuje BeanPostProcessory (jak je pro zjednodušení zakresleno v diagramu), ale pouze BeanFactoryPostProcessory. Jsou to dvě rozdílná rozhraní, která mají rozdílný kontrakt.</p>
<p><b><a href="http://www.jdocs.com/spring/2.0.6/org/springframework/beans/factory/config/BeanFactoryPostProcessor.html" target="_new">BeanFactoryPostProcessor</a></b>: implementace tohoto rozhraní lze zaregistrovat pouze na aplikačním kontextu a aplikační kontext je zavolá ve chvíli, kdy je inicializována BeanFactory avšak před tím, než BeanFactory instanciuje jednotlivé beany - rozhraní slouží k "modifikaci" inicializované BeanFactory před tím, než se zprocesují beany z konfigurací této BeanFactory</p>
<p><b><a href="http://www.jdocs.com/spring/2.0.6/org/springframework/beans/factory/config/BeanPostProcessor.html" target="_new">BeanPostProcessor</a></b>: implementace tohoto rozhraní lze zaregistrovat pouze na BeanFactory a rozhraní je voláno po vytvoření a "nasetování" instance každé beany v konfiguraci dané BeanFactory, implementace BeanPostProcessoru mohou tedy volně nakládat s zinicializovanými beany ihned po jejich vytvoření</p>
<p>Z výše uvedného vyplývá, že není možné na aplikačním kontextu přímo zaregistrovat námi požadovaný ModulePublicInterfacePostProcessor. Ani není možné zavolat si getBeanFactory a aplikačním kontextu před jeho refreshem (vyletí vyjímka signalizující, že kontext není připraven). Po refreshi už je nám to zase na nic, protože PostProcessory po refreshi už nezaberou (museli bychom znovu zavolat refresh, což je zbytečné).</p>
<p>Problém lze vyřešit obalením BeanPostProcessoru do BeanFactoryPostProcessoru, jak je naznačeno v následujícím příkladě:</p>
<p>[source lang="java"]<br />
/**<br />
 * BeanFactoryPostProcessor, that can register BeanPostProcessors to BeanFactory just in time BeanFactory prepared to accept them.<br />
 */<br />
public class DelayedBeanPostProcessorRegistrator implements BeanFactoryPostProcessor {<br />
	List beanPostProcessors = new ArrayList();</p>
<p>	public void addBeanPostProcessor(BeanPostProcessor bpp) {<br />
		beanPostProcessors.add(bpp);<br />
	}</p>
<p>	public void postProcessBeanFactory(ConfigurableListableBeanFactory beanFactory) throws BeansException {<br />
		for(int i = 0; i < beanPostProcessors.size(); i++) {<br />
			BeanPostProcessor beanPostProcessor = (BeanPostProcessor)beanPostProcessors.get(i);<br />
			beanFactory.addBeanPostProcessor(beanPostProcessor);<br />
		}<br />
	}<br />
}<br />
[/source]</p>
<h3>Co bude v dalším díle?</h3>
<p>V minulém článku jsem sice původně avizoval, že tento díl bude poslední, nicméně se ukázalo, že by byl přeci jenom trochu dlouhý. Proto vás čeká ještě jeden, teď už opravdu poslední díl. V něm proberu druhou část rozhaní modulů a tou jsou aplikační události. Aplikační události jsou jedním ze základních stavebních kamenů Springu a proto by bylo škoda se ochudit o tuto skvělou vlastnost na rozhraní modulů. Je zřejmé, že nebudeme chtít otevřít všechny aplikační události svému okolí, nicméně u řady událostí bychom chtěli umožnit ostatním modulům reagovat. Jako příklad uvedu interakci mezi modulem pro správu uživatelů a notifikačním modulem - notifikační modul se stará o rozesílání emailových notifikací v reakci na konkrétní aplikační události (samozřejmě obecně - konfigurovatelně). To je typická ukázka stavu, kdy chceme, aby uživatelský modul dokázal emitovat třebas událost "založení nového uživatele" tak, aby notifikační modul mohl reagovat odesláním emailu.</p>
<p><a href="http://blog.novoj.net/2007/10/04/cast-4-modularni-systemy-ve-spring-framework/">Díl #4: Aplikační události jako "interface" modulů</a></p>
