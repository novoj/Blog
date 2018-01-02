---
status: publish
published: true
title: Spring CgLib Dynamic AOP Proxies - proper Pointcut equals method is simply
  essential
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Dynamic proxies can be very nasty if you don't know what happening under
  the cover. Last week I was searching for the memory leak that caused our application
  to crash. Even though Tomcat had assigned 1GB memory for heap and 0,5GB  for PermGenSpace
  it stood alive for only approximately twelve hours. It's pretty nasty situation
  having known that application is only in betatesting with relatively low traffic.\r\n\r\nWhen
  analyzing generated heap dump I have found, that memory leak was caused by web application
  classloader, that managed thousands of CgLib dynamically generated classes. I was
  using <a href=\"http://www.eclipse.org/mat/\" target=\"_blank\">Eclipse Memory Analyzer</a>,
  that's probably the best tool for memory heap dump analysis I have ever seen. It's
  the third time it quickly identified the suspicious classes, by <a href=\"http://dev.eclipse.org/blogs/memoryanalyzer/2008/05/27/automated-heap-dump-analysis-finding-memory-leaks-with-one-click/\"
  target=\"_blank\">heuristic analysis called Leak suspect</a>.\r\n\r\n"
wordpress_id: 432
wordpress_url: http://blog.novoj.net/?p=432
date: '2009-04-18 21:58:32 +0200'
date_gmt: '2009-04-18 20:58:32 +0200'
categories:
- Programování
- Java
- Spring Framework
tags: []
comments:
- id: 7756
  author: martin
  author_email: reklamax@centrum.cz
  author_url: ''
  date: '2009-04-18 22:52:59 +0200'
  date_gmt: '2009-04-18 21:52:59 +0200'
  content: you`re real java guru. Nice.
- id: 7768
  author: Lukas Vlcek
  author_email: lukas.vlcek@gmail.com
  author_url: ''
  date: '2009-04-19 05:41:19 +0200'
  date_gmt: '2009-04-19 04:41:19 +0200'
  content: Hello Fure, It seems you had a lot of fun digging into inwards. Good post!
- id: 7807
  author: NkD
  author_email: michal.nikodim@gmail.com
  author_url: ''
  date: '2009-04-20 11:33:28 +0200'
  date_gmt: '2009-04-20 10:33:28 +0200'
  content: Congrats. Very usefull informations.
---
<p>Dynamic proxies can be very nasty if you don't know what happening under the cover. Last week I was searching for the memory leak that caused our application to crash. Even though Tomcat had assigned 1GB memory for heap and 0,5GB  for PermGenSpace it stood alive for only approximately twelve hours. It's pretty nasty situation having known that application is only in betatesting with relatively low traffic.</p>
<p>When analyzing generated heap dump I have found, that memory leak was caused by web application classloader, that managed thousands of CgLib dynamically generated classes. I was using <a href="http://www.eclipse.org/mat/" target="_blank">Eclipse Memory Analyzer</a>, that's probably the best tool for memory heap dump analysis I have ever seen. It's the third time it quickly identified the suspicious classes, by <a href="http://dev.eclipse.org/blogs/memoryanalyzer/2008/05/27/automated-heap-dump-analysis-finding-memory-leaks-with-one-click/" target="_blank">heuristic analysis called Leak suspect</a>.</p>
<p><a id="more"></a><a id="more-432"></a></p>
<p>I could identify the offending code fairly quickly. At one place I was creating dynamic proxies around existing instaces, registering advices that took care of caching results of methods' calls on original object. Code looked like that:</p>
<p>[source lang="java"]<br />
public Object getProxiedVersion(Object original) {<br />
    //will create proxy factory based on original object<br />
    ProxyFactory proxyFactory = new ProxyFactory(original);<br />
    //this will add our result caching advisor<br />
    proxyFactory.addAdvisor(<br />
       new DefaultPointcutAdvisor(<br />
          new DataProviderPointcut(),<br />
          new ResultCachingAdvice()<br />
       )<br />
    );<br />
    //this will cause CgLib will be used to generate proxy class<br />
    //and not JDK proxy proxying only interfaces that orignal object implements<br />
    proxyFactory.setProxyTargetClass(true);<br />
    //this is only optimalization thing - means we won't touch advisors<br />
    //after proxy has been created - so Spring could optimalize calls<br />
    proxyFactory.setFrozen(true);<br />
    //this will create dynamic class and instance of it<br />
    return proxyFactory.getProxy();<br />
}<br />
[/source]</p>
<p>I couldn't find out where the problem lies - this code looked right according to <a href="http://static.springframework.org/spring/docs/2.5.x/reference/aop-api.html#aop-prog" target="_blank">Spring documentation</a>.</p>
<p>So I dug deep to the AOP internals and there are things I have discovered:</p>
<h2>Generated classes are never garbage collected</h2>
<p>First I thought that dynamically generated classes could be garbage collected when there are no living instances of them. But that's not true - once class is generated and first instance of it is created it keeps living in classloader object until the classloader itself is garbage collected (in our situation it would infer stopping web application in Tomcat and starting it again). This statement I have proven to myself by this test:</p>
<p>[source lang="java"]<br />
public void testDynamicClassGarbageCollection() {<br />
    //create proxy factory<br />
    ProxyFactory proxyFactory = new ProxyFactory(new Object());<br />
    proxyFactory.setProxyTargetClass(true);<br />
    //we'll force proxy factory to use our own classloader<br />
    //with defining standard classloader as a parent of it<br />
    ClassLoader clsLdr = new ClassLoader(<br />
            Thread.currentThread().getContextClassLoader()<br />
    ) {};<br />
    //create proxy class and intance and keep weak references<br />
    //to them<br />
    WeakReference proxyRef = new WeakReference(<br />
            proxyFactory.getProxy(clsLdr)<br />
    );<br />
    WeakReference proxyClassRef = new WeakReference(<br />
            proxyRef.get().getClass()<br />
    );<br />
    //this should destroy all non referenced instances<br />
    //we have no reference either to proxy or proxy class<br />
    //(WeakReferences don't count)<br />
    System.gc();<br />
    //proxy instance gets garbage collected<br />
    assertNull(proxyRef.get());<br />
    //but class does not!<br />
    assertNotNull(proxyClassRef.get());<br />
    //we have dispose class loader in order to dispose generated<br />
    //proxy class<br />
    clsLdr = null;<br />
    System.gc();<br />
    assertNull(proxyClassRef.get());<br />
}<br />
[/source]</p>
<p>This means that if code of getProxiedVersion method led to the repetitive class generation, there is no way how one could keep Tomcat living for a long time. But such thing would have for sure forced authors of Spring not to recommend programmatical proxy creation - or at least put some kind of warning into the documentation. But that's not true.</p>
<h2>It's easy to check whether your programmatic AOP code leaks PermGenSpace</h2>
<p>I have also wrote simple test, that proved getProxiedVersion metod was flawed:</p>
<p>[source lang="java"]<br />
public void testGetProxiedVersion() {<br />
    long iteration = 0;<br />
    Lookup tested = new Lookup();<br />
    do {<br />
        tested.getProxiedVersion(new Object());<br />
        iteration++;<br />
        if (iteration % 100 == 0) {<br />
            System.out.println("Successfuly proxied: " + iteration + " objects");<br />
        }<br />
    } while (true);<br />
}<br />
[/source]</p>
<p>Running this test with JVM constrained to -XX:MaxPermSize=8m led to quick test fail on OutOfMemoryError (it created roughly about 400 proxied instances and finished with OOME). I played a bit with the getProxiedVersion method and found out that if I comment out following piece of tested code:</p>
<p>[source lang="java"]<br />
//this will add our result caching advisor<br />
proxyFactory.addAdvisor(<br />
   new DefaultPointcutAdvisor(<br />
      new DataProviderPointcut(),<br />
      new ResultCachingAdvice()<br />
   )<br />
);<br />
[/source]</p>
<p>test kept running creating thousands of proxied instances. I tried to exchange my ResultCachingAdvisor for some standard Spring advisor (for example <i>new DefaultIntroductionAdvisor(new ConcurrencyThrottleInterceptor())</i>) and the test was still happily running. So the problem wasn't inside getProxiedVersion method, but in the DefaultPointcutAdvisor code or one of instances passed to the constructor! I was closer to the final solution, but not yet there.</p>
<p>First I blamed my ResultCachingAdvice because it was much more complicated than the pointcut implementation. So I exchanged it for some standard Advice provided by Spring. When leak didn't disappeared, I did the same with Pointcut implementation and ... voila, leak was gone. So the wrong piece of the puzzle was been discovered, but where was the problem?</p>
<p>Pointcut implementation was quite simple - no error visible on the first sight:</p>
<p>[source lang="java"]<br />
public class DataProviderPointcut implements Pointcut {</p>
<p>    public ClassFilter getClassFilter() {<br />
        return new RootClassFilter(DataProvider.class);<br />
    }</p>
<p>    public MethodMatcher getMethodMatcher() {<br />
        return MethodMatcher.TRUE;<br />
    }</p>
<p>}<br />
[/source]</p>
<h2>CgLib optimizes class generation and won't generate the same dynamic class again</h2>
<p>In order to break this mystery we have to know how CgLib works internally with class generation. There is a magic flag useCache in <a href="http://kickjava.com/src/net/sf/cglib/core/AbstractClassGenerator.java.htm" target="_blank">AbstractClassGenerator</a> class that causes CgLib not to generate class it has already created again (see protected method Object create(Object key)). This magic flag is true by default, so in our test there should be only one dynamic proxy class generated and not thousands as it was in my case.</p>
<p>The key to our problem is the mechanism how CgLib recognizes whether two generated classes equals. I won't pretend, that I deeply understand to this mechanism - but key part of it is hidden in the <a href="http://kickjava.com/src/net/sf/cglib/proxy/Enhancer.java.htm" target="_blank">Enhancer</a> class, especially in the method createHelper:</p>
<p>[source lang="java"]<br />
private Object createHelper() {<br />
	validate();<br />
	if (superclass != null) {<br />
		setNamePrefix(superclass.getName());<br />
	} else if (interfaces != null) {<br />
		setNamePrefix(interfaces[ReflectUtils.findPackageProtected(interfaces)].getName());<br />
	}<br />
	return super.create(KEY_FACTORY.newInstance((superclass != null) ?<br />
           superclass.getName() : null,<br />
           ReflectUtils.getNames(interfaces),<br />
           filter,<br />
           callbackTypes,<br />
           useFactory,<br />
           interceptDuringConstruction,<br />
           serialVersionUID)<br />
       );<br />
}<br />
[/source]</p>
<p>We can see in that snippet, that CgLib examines several things to distinguish two classes. For example:</p>
<ul>
<li>superclass of our class</li>
<li>implemented interfaces</li>
<li>callbackTypes</li>
<li>filter</li>
<li>serialVersionUID and so on</li>
</ul>
<p>It's not easy to understand it by just staring at the code, so the debugger might come handy. Problematic part is the filter (CallbackFilter interface implemented by <a href="http://www.docjar.com/html/api/org/springframework/aop/framework/Cglib2AopProxy$ProxyCallbackFilter.java.html" target="_blank">Cglib2AopProxy$ProxyCallbackFilter</a>). Let's examine its equals method (look expecially at the end where advisors are consulted):</p>
<p>[source lang="java"]<br />
public boolean equals(Object other) {<br />
	if (other == this) {<br />
		return true;<br />
	}<br />
	if (!(other instanceof ProxyCallbackFilter)) {<br />
		return false;<br />
	}<br />
	ProxyCallbackFilter otherCallbackFilter = (ProxyCallbackFilter) other;<br />
	AdvisedSupport otherAdvised = otherCallbackFilter.advised;<br />
	if (this.advised == null || otherAdvised == null) {<br />
		return false;<br />
	}<br />
	if (this.advised.isFrozen() != otherAdvised.isFrozen()) {<br />
		return false;<br />
	}<br />
	if (this.advised.isExposeProxy() != otherAdvised.isExposeProxy()) {<br />
		return false;<br />
	}<br />
	if (this.advised.getTargetSource().isStatic() != otherAdvised.getTargetSource().isStatic()) {<br />
		return false;<br />
	}<br />
	if (!AopProxyUtils.equalsProxiedInterfaces(this.advised, otherAdvised)) {<br />
		return false;<br />
	}<br />
	// Advice instance identity is unimportant to the proxy class:<br />
	// All that matters is type and ordering.<br />
	Advisor[] thisAdvisors = this.advised.getAdvisors();<br />
	Advisor[] thatAdvisors = otherAdvised.getAdvisors();<br />
	if (thisAdvisors.length != thatAdvisors.length) {<br />
		return false;<br />
	}<br />
	for (int i = 0; i < thisAdvisors.length; i++) {<br />
		Advisor thisAdvisor = thisAdvisors[i];<br />
		Advisor thatAdvisor = thatAdvisors[i];<br />
		if (!equalsAdviceClasses(thisAdvisor, thatAdvisor)) {<br />
			return false;<br />
		}<br />
		if (!equalsPointcuts(thisAdvisor, thatAdvisor)) {<br />
			return false;<br />
		}<br />
	}<br />
	return true;<br />
}</p>
<p>private boolean equalsAdviceClasses(Advisor a, Advisor b) {<br />
	Advice aa = a.getAdvice();<br />
	Advice ba = b.getAdvice();<br />
	if (aa == null || ba == null) {<br />
		return (aa == ba);<br />
	}<br />
	return aa.getClass().equals(ba.getClass());<br />
}</p>
<p>private boolean equalsPointcuts(Advisor a, Advisor b) {<br />
	// If only one of the advisor (but not both) is PointcutAdvisor, then it is a mismatch.<br />
	// Takes care of the situations where an IntroductionAdvisor is used (see SPR-3959).<br />
	if (a instanceof PointcutAdvisor ^ b instanceof PointcutAdvisor) {<br />
		return false;<br />
	}<br />
	// If both are PointcutAdvisor, match their pointcuts.<br />
	if (a instanceof PointcutAdvisor && b instanceof PointcutAdvisor) {<br />
		return ObjectUtils.nullSafeEquals(((PointcutAdvisor) a).getPointcut(), ((PointcutAdvisor) b).getPointcut());<br />
	}<br />
	// If neither is PointcutAdvisor, then from the pointcut matching perspective, it is a match.<br />
	return true;<br />
}<br />
[/source]</p>
<p>As you can see, advices don't need to have equals method as ProxyCallbackFilter compares only their classes. On the contrary Pointcuts are compared by calling their equals methods. So the exact problem in my case was missing implementation of equals method, that got inherited from java.lang.Object and returned true only for the same object instance comparisement.</p>
<h2>Solution</h2>
<p>When we know all this, the solution is quite simple. Better said, we have a plenty solutions at hand:</p>
<ul>
<li>use prepared Pointcut from Spring - they just work</li>
<li>write a proper equals and hashCode methods in your Pointcut implementations</li>
<li>use static or singleton references to your Pointcuts (as Spring often does - just look at Pointcut.TRUE) - then default equals implementation in java.lang.Object will work as there is only one instance of the Pointcut class</li>
</ul>
<p>This conclusion should be more propagated in Spring documentation, I suppose. But at least this article does it. Happy coding ...</p>
