---
status: publish
published: true
title: Groovy - making existing objects refreshable
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "In the last post I described the basic principles I found behind the scenes
  of GroovyScript refresh. Now imagine that you want to create your own long living
  Groovy instances with auto-refresh behaviour when source code changes. You can use
  out-of-the-box Spring support - but there are some limitations I stated in the previous
  article.\r\n\r\nIn this post I am going to present an alternative solution that
  addresses some of the painful issues I noticed. As I stated before, key is to <cite>wrap
  the reference to Groovy instance into an another object managed by the Java class
  loader</cite> and that is exactly the main point of the solution presented.\r\n\r\n"
wordpress_id: 648
wordpress_url: http://blog.novoj.net/?p=648
date: '2009-11-29 10:50:47 +0100'
date_gmt: '2009-11-29 09:50:47 +0100'
categories:
- Programování
- Java
- English
- Groovy
tags: []
comments:
- id: 17271
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-01-29 13:06:15 +0100'
  date_gmt: '2010-01-29 12:06:15 +0100'
  content: Pokud by měl někdo zájem o reálné použití, napište mi na email - knihovnu
    jsme ještě drobet vyladili, našlo se pár nedokonalostí v integraci s Groovy. Máme
    i upgradovanou verzi pro Groovy 1.7, ve kterém jsme reportovali dokonce několik
    chyb s GroovyScriptEnginem a Springem souvisejících. Nyní ji pomaličku začínáme
    nasazovat produkčně na menších instalacích.
- id: 24922
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-08-27 08:27:01 +0200'
  date_gmt: '2010-08-27 07:27:01 +0200'
  content: "Aktualizoval jsem zdrojové kódy na naši poslední odladěnou verzi. Můžete
    stahovat tímto linkem:\r\n\r\nhttp://files.novoj.net/GroovyIntegration/groovy-integration.zip"
---
<p>In the last post I described the basic principles I found behind the scenes of GroovyScript refresh. Now imagine that you want to create your own long living Groovy instances with auto-refresh behaviour when source code changes. You can use out-of-the-box Spring support - but there are some limitations I stated in the previous article.</p>
<p>In this post I am going to present an alternative solution that addresses some of the painful issues I noticed. As I stated before, key is to <cite>wrap the reference to Groovy instance into an another object managed by the Java class loader</cite> and that is exactly the main point of the solution presented.</p>
<p><a id="more"></a><a id="more-648"></a></p>
<p>My inspiration was based on the Spring's approach to the issue. It wraps each and every groovy instance into the JDK proxy, that is safe to handle out and store anywhere developer wants (even in the long living scopes). Implementation of this proxy delegates method call to inner Groovy instance, but is also able to check whether the underlying code haven't changed. If it has, it drops current Groovy instance and creates new one, that immediately initializes by configured dependency injection rules.</p>
<p>To overcome <a href="http://blog.novoj.net/2009/11/08/the-secret-of-groovy-script-refresh/">the main issues connected with Spring's solution</a>, I decided to:</p>
<ol>
<li>base my solution on CgLib proxy instead of JDK Proxy - this way we could also use methods of the Java classes our Groovy class extends from and not only methods declared on interfaces</li>
<li>use GroovyScripting engine instead of simple GroovyClassloader to reflect changes not only in the instantiated class itself, but also in classes it uses</li>
<li>add easy method for unwrapping inner Groovy instance - so we could easily use methods declared on the Groovy class (for example in templating engines) without need of having Java interface that contains them (though programming for interfaces is a good approach, I don't see and advantage of having interface ever having only single implementation)</li>
<li>provide callback for custom initialization logic after instance recreation (refresh)</li>
</ol>
<p><b>Note: </b> please, be warned, this post contains a lot of code that might not be as readable as I have wished it to be. If you feel that you don't get the point, download the sources with JUnit tests and feel free to fiddle with it a little bit. I am sure the topic is not so hard to undestand as it looks for the first sight.</p>
<p>Enough talking - let's look at the code. I use unified my own interface ScriptingFactory for creating new scripting instances (I try to abstract from the underlying Groovy scripting support at the base interfaces):</p>
{% highlight java %}
/**
 * This interface conceals logic connected with instantiating scripting (Groovy, JRuby ...) classes.
 */
@SuppressWarnings({"RawUseOfParameterizedType"})
public interface ScriptingFactory {
	/**
	 * Returns scripting classloader.
	 * @return this factory classloader
	 */
	ClassLoader getScriptingClassLoader();
	/**
	 * Returns true if class is loaded by ScriptingClassloader.
	 * @param clazz to analyze
	 * @return true if specified class is instantiated by this scripting factory classloader
	 */
	boolean isClassLoadedByScriptingClassloader(Class clazz);
	/**
	 * Loads class of specified name.
	 * @param className full class name with package
	 * @return class for specified name
	 * @throws ClassLoadingException whrown when source file cannot be found or is corrupted
	 */
	Class loadClass(String className) throws ClassLoadingException;
	/**
	 * Instantiates object of specified class.
	 * @param className full class name with package
	 * @param args constructor arguments
	 * @return class instance
	 * @throws ClassInstantiationException thrown when class instantiation fails
	 */
	Object createInstance(String className, Object... args) throws ClassInstantiationException;
	/**
	 * Instantiates object of specified class.
	 * @param clazz to be instantiated
	 * @param args constructor arguments
	 * @return class instance
	 * @throws ClassInstantiationException thrown when class instantiation fails
	 */
	Object createInstance(Class clazz, Object... args) throws ClassInstantiationException;
	/**
	 * Returns interval in miliseconds after that a class validity according to underlying source should be examined.
	 * @return refresh interval in miliseconds
	 */
	long getRefreshInterval();
	/**
	 * Closes ScriptingFactory, so no more queries will be handled by it.
	 */
	void close();
	/**
	 * Returns state of the scripting factory.
	 * @return true if factory is closed
	 */
	boolean isClosed();
}
{% endhighlight %}
<p>For this interface there are two Groovy implementations - ProductionGroovyFactory and DevelopmentGroovyFactory. </p>
<p><strong>ProductionGroovyFactory</strong> creates instances of Groovy classes that never refresh. Returned instances are pure instances of specified Groovy classes. References passed around will potentialy prevent Groovy class and classloader being garbage collected, but that wouldn't be likely necessary in production (no refreshes occur there). On the other hand this implementation represents easiest and most performant way to providing Groovy instances. This implementantion is not interesting for the sake of this article, so I skip it.</p>
<p><strong>DevelopmentGroovyFactory</strong> creates instances of Groovy classes wrapped in proxies. This will allow us to safely hand around references to those instances without worrying about refresh behaviour when underlying source code changes. Proxies will maintain refreshing logic, checking source code change in specified intervals and eventually freeing old instances and creating new fresh one based on new classes corresponding to latest source code state.</p>
<p>Moreover the system is setup the way that programmer doesn't need to take care of proper reference handling to avoid PermGenSpace memory leaks. Returned references doesn't have anything common with Groovy class - they are derived from first Java ancestor class in an ancestor hierarchy and implement all interfaces loaded by pure Java classloader. All Groovy related things are located in the proxy, so the swapping can be handled safely.</p>
<p>[source lang="java"]<br />
@SuppressWarnings({"RawUseOfParameterizedType"})<br />
public class DevelopmentGroovyFactory implements ScriptingFactory {<br />
	private static final Log log = LogFactory.getLog(DevelopmentGroovyFactory.class);<br />
	private final GroovyScriptEngine engine;<br />
	private final long refreshInterval;<br />
	private ResourceConnector resourceConnector;<br />
	private boolean closed;</p>
<p>	public DevelopmentGroovyFactory(ClassLoader parentClassLoader, String[] urls, long refreshInterval) {<br />
		try {<br />
			this.engine = new GroovyScriptEngine(urls, parentClassLoader);<br />
			this.engine.getGroovyClassLoader().setShouldRecompile(true);<br />
			this.refreshInterval = refreshInterval * 1000L;<br />
			GroovyGarbageCollectorMonitor.addGroovyScriptEngineToMonitoring(engine);<br />
		} catch(IOException ex) {<br />
			String msg = "Invalid source urls: " + ex.getLocalizedMessage();<br />
			log.error(msg);<br />
			throw new RuntimeException(msg, ex);<br />
		}<br />
	}</p>
<p>	public DevelopmentGroovyFactory(ClassLoader parentClassLoader, URL[] urls, long refreshInterval) {<br />
		this.engine = new GroovyScriptEngine(urls, parentClassLoader);<br />
		this.engine.getGroovyClassLoader().setShouldRecompile(true);<br />
		this.refreshInterval = refreshInterval * 1000L;<br />
		GroovyGarbageCollectorMonitor.addGroovyScriptEngineToMonitoring(engine);<br />
	}</p>
<p>	public DevelopmentGroovyFactory(ClassLoader parentClassLoader, ResourceConnector rc, long refreshInterval) {<br />
		this.engine = new GroovyScriptEngine(rc, parentClassLoader);<br />
		this.engine.getGroovyClassLoader().setShouldRecompile(true);<br />
		this.refreshInterval = refreshInterval * 1000L;<br />
		this.resourceConnector = rc;<br />
		GroovyGarbageCollectorMonitor.addGroovyScriptEngineToMonitoring(engine);<br />
	}</p>
<p>	/**<br />
	 * Returns Groovy classloader.<br />
	 *<br />
	 * @return<br />
	 */<br />
	public ClassLoader getScriptingClassLoader() {<br />
		checkClosed();<br />
		return engine.getGroovyClassLoader();<br />
	}</p>
<p>	/**<br />
	 * Returns true if class is loaded by GroovyClassloader.<br />
	 *<br />
	 * @param clazz<br />
	 * @return<br />
	 */<br />
	public boolean isClassLoadedByScriptingClassloader(Class clazz) {<br />
		checkClosed();<br />
		ClassLoader parameterClassLoader = clazz.getClassLoader();<br />
		ClassLoader engineClassLoader = engine.getGroovyClassLoader();<br />
		do {<br />
			if (parameterClassLoader == engineClassLoader) {<br />
				return true;<br />
			}<br />
			parameterClassLoader = parameterClassLoader.getParent();<br />
		} while (parameterClassLoader != ClassLoader.getSystemClassLoader());<br />
		return false;<br />
	}</p>
<p>	/**<br />
	 * @see #createInstance(Class, Object[])<br />
	 *<br />
	 * @param className<br />
	 * @param args<br />
	 * @return<br />
	 * @throws ScriptException<br />
	 * @throws ResourceException<br />
	 * @throws InstantiationException<br />
	 * @throws IllegalAccessException<br />
	 */<br />
	public Object createInstance(String className, Object... args) throws ClassInstantiationException {<br />
		checkClosed();<br />
		Class aClass = loadClass(className);<br />
		return createInstance(aClass, args);<br />
	}</p>
<p>	/**<br />
	 * Creates groovy class instance. Returned instance is not directly groovy class instance but rather dynamic Proxy of<br />
	 * that class. This proxy wraps original groovy class instance but extends not from this instance, but from nearest<br />
	 * superclass that is loaded by Java classloader, also this proxy implements all interfaces, that are comming out of<br />
	 * Java classloaders. Proxy itself encapsulates refreshing logic, so that if underlying instance doesn't conform to<br />
	 * the source script it is automatically discarded and new instance is created instead. Reference to this proxy can<br />
	 * be safely stored in long living memory scopes without having to fear that refreshing logic would cause pergenspace<br />
	 * leaking. When you need to call method, that is defined only on the Groovy class but has no backing in Java superclass<br />
	 * or any of interfaces, you can use the unwrap() method that returns reference of the wrapped Groovy instance. This<br />
	 * reference must not be stored anywhere as it is a key to hell of permgenspace leaks.<br />
	 *<br />
	 * Single limitation of this approach is that you cannot change java superclass or java interface implementation set<br />
	 * on the fly. Once generated proxy cannot adapt to this change.<br />
	 *<br />
	 * @param className<br />
	 * @param args<br />
	 * @return<br />
	 * @throws ClassNotFoundException<br />
	 * @throws InstantiationException<br />
	 * @throws IllegalAccessException<br />
	 * @throws ScriptException<br />
	 * @throws ResourceException<br />
	 */<br />
	public Object createInstance(Class className, Object... args) throws ClassInstantiationException {<br />
		checkClosed();<br />
		Object instance;<br />
		try {<br />
			//load a groovy class and make an instance<br />
			if (args.length == 0) {<br />
				instance = className.newInstance();<br />
			} else {<br />
				Class[] parameterTypes = new Class[args.length];<br />
				for(int i = 0; i < args.length; i++) {<br />
					Object arg = args[i];<br />
					parameterTypes[i] = arg.getClass();<br />
				}<br />
				Constructor constructor = className.getConstructor(parameterTypes);<br />
				instance = constructor.newInstance(args);<br />
			}<br />
		} catch (Exception ex) {<br />
			String msg = "Cannot create instance of class: " + className.getName() + " (" + ex.getLocalizedMessage() + ')';<br />
			log.error(msg, ex);<br />
			throw new ClassInstantiationException(msg, ex, className);<br />
		}</p>
<p>		if (isClassLoadedByScriptingClassloader(className)) {<br />
			//analyze class and create proxy<br />
			BuildProxyDescriptor bpd = getJavaAncestorsForProxy(className, engine.getParentClassLoader());<br />
			ProxyFactory factory = new ProxyFactory(new Class[0]);<br />
			factory.setTargetSource(<br />
					new JavaRealmHotswappableTargetSource(instance, bpd.getSuperClassToExtend())<br />
			);<br />
			factory.setInterfaces(bpd.getInterfacesToImplement());<br />
			factory.addAdvisor(new DefaultIntroductionAdvisor(new GroovyProxyMixin(this, instance)));<br />
			factory.setProxyTargetClass(true);<br />
			factory.setExposeProxy(true);<br />
			factory.setFrozen(true);</p>
<p>			return factory.getProxy();<br />
		} else {<br />
			return instance;<br />
		}<br />
	}</p>
<p>	/**<br />
	 * Returns refresh interval passed to this object via constructor.<br />
	 * @return<br />
	 */<br />
	public long getRefreshInterval() {<br />
		checkClosed();<br />
		return refreshInterval;<br />
	}</p>
<p>	/**<br />
	 * Loads class from GroovyScriptingEngine - respecting code source changes of this and dependent classes.<br />
	 * Might return each time different class object instance - due to source code modifications.<br />
	 * @param className<br />
	 * @return<br />
	 * @throws ScriptException<br />
	 * @throws ResourceException<br />
	 */<br />
	public Class loadClass(String className) throws ClassLoadingException {<br />
		checkClosed();<br />
		try {<br />
			//firstly imitate GroovyScriptingEngine and find out whether there is script of this name<br />
			String scriptName = className.replace('.', File.separatorChar) + ".groovy";<br />
			URLConnection connection;<br />
			if (resourceConnector != null) {<br />
				connection = resourceConnector.getResourceConnection(scriptName);<br />
			} else {<br />
				connection = engine.getResourceConnection(scriptName);<br />
			}<br />
			InputStream is = null;<br />
			try {<br />
				//if so load class from script<br />
				is = connection.getInputStream();<br />
				IOUtils.closeQuietly(is);<br />
				Class groovyClass = engine.loadScriptByName(className);<br />
				GroovyGarbageCollectorMonitor.addGroovyClassToMonitoring(groovyClass);<br />
				return groovyClass;<br />
			} catch(Exception ignored) {<br />
				//ups no script of this name found - lets load class on parent classloader<br />
				return engine.getParentClassLoader().loadClass(className);<br />
			} finally {<br />
				IOUtils.closeQuietly(is);<br />
			}<br />
		} catch (Exception ex) {<br />
			String msg = "Cannot load class: " + className + " (" + ex.getLocalizedMessage() + ')';<br />
			log.error(msg, ex);<br />
			throw new ClassLoadingException(msg, ex);<br />
		}<br />
	}</p>
<p>	/**<br />
	 * Closes GroovyFactory, so no more queries will be handled by it.<br />
	 */<br />
	public void close() {<br />
		this.closed = true;<br />
	}</p>
<p>	/**<br />
	 * Returns true if factory is closed.<br />
	 *<br />
	 * @return<br />
	 */<br />
	public boolean isClosed() {<br />
		return closed;<br />
	}</p>
<p>	/**<br />
	 * Checks whether this GroovyFactory is closed and when so - IllegalStateException is thrown.<br />
	 * @throws IllegalStateException<br />
	 */<br />
	private void checkClosed() throws IllegalStateException {<br />
		if (closed) {<br />
			throw new IllegalStateException("This GroovyFactory is closed - no more operations will be accepted.");<br />
		}<br />
	}</p>
<p>	/**<br />
	 * Finds first superclass, that is loaded by Java classloader and all interfaces groovy class implements, that are<br />
	 * also loaded by Java classloader.<br />
	 *<br />
	 * @param groovyClass<br />
	 * @param javaClassLoader<br />
	 * @return<br />
	 */<br />
	private BuildProxyDescriptor getJavaAncestorsForProxy(Class groovyClass, ClassLoader javaClassLoader) {<br />
		//find first ancestor that is loaded by pure Java classloader<br />
		Class superClassToExtend = null;<br />
		Class currentClass = groovyClass;<br />
		do {<br />
			currentClass = currentClass.getSuperclass();<br />
			if (ClassUtils.isVisible(currentClass, javaClassLoader)) {<br />
				superClassToExtend = currentClass;<br />
			}<br />
		} while (currentClass != null && superClassToExtend == null);<br />
		//gather all interfaces, that are not loaded by Groovy classloader<br />
		Class[] interfaces = ClassUtils.getAllInterfacesForClass(groovyClass, javaClassLoader);<br />
		return new BuildProxyDescriptor(superClassToExtend, interfaces);<br />
	}</p>
<p>	/**<br />
	 * Contains Java class description needed for Groovy proxy creation.<br />
	 */<br />
	public static class BuildProxyDescriptor {<br />
		private final Class superClassToExtend;<br />
		private final Class[] interfacesToImplement;</p>
<p>		public BuildProxyDescriptor(Class superClassToExtend, Class[] interfacesToImplement) {<br />
			this.superClassToExtend = superClassToExtend;<br />
			this.interfacesToImplement = interfacesToImplement;<br />
		}</p>
<p>		public Class getSuperClassToExtend() {<br />
			return superClassToExtend;<br />
		}</p>
<p>		public Class[] getInterfacesToImplement() {<br />
			return interfacesToImplement;<br />
		}<br />
	}</p>
<p>	/**<br />
	 * Custom implementation of HotSwappableTargetSource that returns first Java parent class available for inner<br />
	 * Groovy class instead of returning Groovy class itself.<br />
	 */<br />
	public static class JavaRealmHotswappableTargetSource extends HotSwappableTargetSource {<br />
		private static final long serialVersionUID = -6962339257859210715L;<br />
		private final Class superClassToExtend;</p>
<p>		public JavaRealmHotswappableTargetSource(Object target, Class superClassToExtend) {<br />
			super(target);<br />
			this.superClassToExtend = superClassToExtend;<br />
		}</p>
<p>		@Override<br />
		public synchronized Class getTargetClass() {<br />
			return superClassToExtend;<br />
		}</p>
<p>	}</p>
<p>}<br />
[/source]</p>
<p>DevelopmentGroovyFactory wraps Groovy instances into the AOP dynamic proxy. This proxy always implements this interface:</p>
<p>[source lang="java"]<br />
/**<br />
 * Groovy proxy interface declares method available for wrap and unwrap inner scripting instance, and set instance initializer<br />
 * that initializes instance after eventual inner instance reinstantiation when source code changes.<br />
 */<br />
public interface ScriptingProxy extends RawTargetAccess {</p>
<p>	/**<br />
	 * Sets instance initalizer that initializes reinstantiated object after source code change.<br />
	 * @param factory for initializing new inner scripting instance<br />
	 */<br />
	void setInstanceInitializer(ProxyInstanceFactory factory);</p>
<p>	/**<br />
	 * Returns set instance initializer.<br />
	 * @see #setInstanceInitializer(ProxyInstanceFactory)<br />
	 * @return instance initializer that should be used to newly created inner scripting instance<br />
	 */<br />
	ProxyInstanceFactory getInstanceInitializer();</p>
<p>	/**<br />
	 * Sets inner scripting instance.<br />
	 * @param scriptingInstance to wrap in this proxy<br />
	 */<br />
	void wrap(Object scriptingInstance);</p>
<p>	/**<br />
	 * Returns inner scripting instance.<br />
	 * Please do not store reference to this instance in any long living scope (static variables, session, servlet<br />
	 * context, singletons and so on)<br />
	 * @return pure scripting instance hidden inside this proxy<br />
	 */<br />
	Object unwrap();</p>
<p>	/**<br />
	 * Performs up to date check and potentialy updated outdated inner instance.<br />
	 *<br />
	 * @return false when inner scripting instance was updated<br />
	 */<br />
	boolean isUpToDate();</p>
<p>}<br />
[/source]</p>
<p>As you can see proxy uses so called ProxyInstanceFactory for creating new inner instances of the Groovy classes when corresponding source code changes. This interface could be optionaly used not only for instantiation itself, but also for initial setup of the instance, such as dependency injection and so on.</p>
<p>[source lang="java"]<br />
/**<br />
 * This interface allows to create instance created after refresh of the scripting class inside ScriptingProxy.<br />
 */<br />
public interface ProxyInstanceFactory {</p>
<p>	/**<br />
	 * Reinstantiate inner groovy instance.<br />
	 * @param clazz<br />
	 * @return new instance<br />
	 */<br />
	Object createInstance(Class clazz) throws ClassInstantiationException;</p>
<p>}<br />
[/source]</p>
<p>Last piece of the puzzle is GroovyProxyMixin, that implements ScriptingProxy interface and REALLY does the magic around monitoring source code changes and reinstantiation of the inner Groovy instance. Let's examine the code:</p>
<p>[source lang="java"]<br />
/**<br />
 * Basic and probably unique GroovyProxy implementation.<br />
 */<br />
@SuppressWarnings({"serial", "NonSerializableFieldInSerializableClass", "AccessToStaticFieldLockedOnInstance"})<br />
public class GroovyProxyMixin extends DelegatingIntroductionInterceptor implements ScriptingProxy {<br />
	private static final Log log = LogFactory.getLog(GroovyProxyMixin.class);<br />
	private static final ProxyInstanceFactory DEFAULT_INSTANCE_FACTORY = new DefaultProxyInstanceFactory();<br />
	private final WeakReference<ScriptingFactory> groovyFactory;<br />
	private final Object monitor = new Object();<br />
	private Object groovyInstance;<br />
	private ProxyInstanceFactory instanceFactory;<br />
	private long nextCheckTimestamp;</p>
<p>	public GroovyProxyMixin(ScriptingFactory groovyFactory, Object groovyInstance) {<br />
		this.groovyFactory = new WeakReference<ScriptingFactory>(groovyFactory);<br />
		this.nextCheckTimestamp = System.currentTimeMillis() + groovyFactory.getRefreshInterval();<br />
		wrap(groovyInstance);<br />
	}</p>
<p>	public void setInstanceInitializer(ProxyInstanceFactory factory) {<br />
		this.instanceFactory = factory;<br />
	}</p>
<p>	public ProxyInstanceFactory getInstanceInitializer() {<br />
		if (instanceFactory == null) {<br />
			return DEFAULT_INSTANCE_FACTORY;<br />
		} else {<br />
			return instanceFactory;<br />
		}<br />
	}</p>
<p>	public void wrap(Object scriptingInstance) {<br />
		this.groovyInstance = scriptingInstance;<br />
	}</p>
<p>	public Object unwrap() {<br />
		return groovyInstance;<br />
	}</p>
<p>	public boolean isUpToDate() {<br />
		//check groovy factory is still living<br />
		ScriptingFactory groovyFactory = this.groovyFactory.get();<br />
		if (groovyFactory == null || groovyFactory.isClosed()) {<br />
			this.groovyInstance = null;<br />
			this.instanceFactory = null;<br />
			throw new IllegalStateException("Groovy factory is already closed - this object reference is simply dead.");<br />
		}<br />
		//check inner groovy instance uptodate status<br />
		long currentTimestamp = System.currentTimeMillis();<br />
		if (currentTimestamp > nextCheckTimestamp) {<br />
			nextCheckTimestamp = currentTimestamp + groovyFactory.getRefreshInterval();<br />
			synchronized(monitor) {<br />
				Class oldGroovyClass = groovyInstance.getClass();<br />
				Class groovyClass = groovyFactory.loadClass(oldGroovyClass.getName());<br />
				if(oldGroovyClass == groovyClass) {<br />
					return true;<br />
				} else {<br />
					if(log.isDebugEnabled()) {<br />
						log.debug("Class " + groovyClass.getName() + " changed - refreshing instance!");<br />
					}<br />
					GroovyGarbageCollectorMonitor.addGroovyClassToMonitoring(groovyClass);<br />
					//underlying script has changed and Groovy classloader reloaded the class<br />
					groovyInstance = getInstanceInitializer().createInstance(groovyClass);<br />
					//change proxy target for the next call<br />
					Advised advised = (Advised)AopContext.currentProxy();<br />
					HotSwappableTargetSource targetSource = (HotSwappableTargetSource)advised.getTargetSource();<br />
					targetSource.swap(groovyInstance);<br />
					//clear introspection cache to be able to free classes<br />
					CachedIntrospectionResults.clearClassLoader(groovyFactory.getScriptingClassLoader());<br />
					Introspector.flushFromCaches(oldGroovyClass);<br />
					return false;<br />
				}<br />
			}<br />
		}<br />
		return true;<br />
	}</p>
<p>	@Override<br />
	protected Object doProceed(MethodInvocation mi) throws Throwable {<br />
		if(isUpToDate()) {<br />
			return super.doProceed(mi);<br />
		} else {<br />
			//as we cannot change method invocation for this call, manually run method on newly created object<br />
			//and immitate that the result goes from the existing MethodInvocation<br />
			//possible exeptions of NoSuchMethodException and SecurityException propagate<br />
			Class groovyClass = groovyInstance.getClass();<br />
			Method originalMethod = mi.getMethod();<br />
			Method newMethod = groovyClass.getMethod(originalMethod.getName(), originalMethod.getParameterTypes());<br />
			return newMethod.invoke(groovyInstance, mi.getArguments());<br />
		}<br />
	}</p>
<p>	/**<br />
	 * Default implementation.<br />
	 */<br />
	public static class DefaultProxyInstanceFactory implements ProxyInstanceFactory {</p>
<p>		public Object createInstance(Class clazz) throws ClassInstantiationException {<br />
			try {<br />
				return clazz.newInstance();<br />
			}<br />
			catch(Exception e) {<br />
				String msg = "Cannot reinstantiate class: " + clazz.getName() + " (" + e.getLocalizedMessage() + ")";<br />
				log.error(msg);<br />
				throw new ClassInstantiationException(msg, e, clazz);<br />
			}<br />
		}</p>
<p>	}</p>
<p>}<br />
[/source]</p>
<h3>Example of the API usage</h3>
<p>Thought horrible it might look like - the important side of the matter is how it'll be used by the client code that will use this API. And there, I think, we are at the much more solid ground:</p>
<p>[source lang="java"]<br />
public void testRealWorldUsage() throws Exception {<br />
	Resource rootFSR = new FileSystemResource("/www/project/classes/");<br />
	groovyFactory = new DevelopmentGroovyFactory(<br />
			Thread.currentThread().getContextClassLoader(), //parent classloader<br />
			new URL[] {rootFSR.getURL()}, //source codes<br />
			0 //refresh interval<br />
	);<br />
	//create groovy instance<br />
	MySpecificJavaClass groovyInstance = (MySpecificJavaClass)<br />
			groovyFactory.createInstance("com.fg.mock.MainGroovyClass");<br />
	/** uncomment this to set up custom intance factory<br />
	 * (possibly intitializing the instance for example by dependency injection)<br />
	 * ((ScriptingProxy)groovyInstance).setInstanceInitializer(... custom factory ...);<br />
	 **/<br />
	assertTrue(groovyInstance instanceof JavaHelloWorldInterface);<br />
	assertEquals("Hello Universe.", ((JavaHelloWorldInterface)groovyInstance).sayHello());<br />
}<br />
[/source]</p>
<p>This doesn't look difficult, does it? </p>
<p>References that you receive from the DevelopmentScriptingFactory could be passed around without fear of PermGenSpace leaks and yet the behaviour would dynamically adapt source code changes. In Java code we could safely cast to any of Java interfaces or Java classes our Groovy class extends from. When we need to use created Groovy instance in templating engine (such as Freemarker or Velocity) we could unwrap original Groovy instance from the returned ScriptingProxy, so the engine could call any method declared on the Groovy class by the reflection. Unwrapping inner instance is somewhat dangerous, but for the purpose of the templating activities we could afford this. Template engines usually create a context used for single request processing only, so the unwrapped instance references stored in such context will soon fade off as the request gets processed and context itself dies. Similarly we could safely store unwrapped Groovy instances into the request attributes or other short lived objects, making profit of the direct access to the Groovy class instance.</p>
<h3>Source code with tests download</h3>
<p>Here you can download source code with IntelliJ Idea project files to examine. I recommend to play with it a little bit in a debug mode, as well as creating some more tests on your own. After all, I could be terribly wrong, thought the tests confirm my theories.</p>
<p><a href="http://files.novoj.net/GroovyIntegration/groovy-integration.zip">Source code download.</a></p>
<h3>What comes next ...</h3>
<p>There is yet another part of this serie, where I will present an integration of current solutions into the Spring via implementing BeanFactory and simple solution for refreshing Spring context trees when Spring configuration or any of the monitored bean changes. Will I make it till Christmas? I don't know as there isn't a comma of it written. Be patient, please ...</p>
