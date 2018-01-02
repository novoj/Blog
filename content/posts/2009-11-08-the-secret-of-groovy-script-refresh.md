---
status: publish
published: true
title: The secret of Groovy script refresh
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "The first thing one should undestand before he tries to integrate scripting
  support into his application / framework are class loading issues. One of the main
  reasons (next to the ability to easily switch from Java) why we have chosen Groovy
  as our primary scripting language is very good support for live refresh of Groovy
  classes when source file has changed. But what does Groovy exactly do when it \"refreshes\"
  its loaded classes to conform to a newly modified source file? What about existing
  instances referencing to this class? Is it even possible in JVM to change class
  structure in runtime? Yes JavaRebel can do this, but it needs special setup and
  debug mode for hotswap. And how does all this fit into the existing Spring support?
  From the documentation it seems, that it all just magically works! Dozens of questions
  ran in my mind when I started to strive for Groovy integration in our product. Those
  questions gets answered in this article.\r\n\r\n"
wordpress_id: 548
wordpress_url: http://blog.novoj.net/?p=548
date: '2009-11-08 22:32:04 +0100'
date_gmt: '2009-11-08 21:32:04 +0100'
categories:
- Programování
- Java
- English
- Groovy
tags: []
comments:
- id: 14618
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-11-10 20:34:56 +0100'
  date_gmt: '2009-11-10 19:34:56 +0100'
  content: "Interesting article series from ZeroTurnaround (JavaRebel) about similar
    class loading issues I am describing in this post. Some of my conclusions gets
    confirmed here:\r\n\r\nhttp://www.zeroturnaround.com/blog/reloading-objects-classes-classloaders/\r\n\r\nCheck
    it out."
- id: 36599
  author: Jordan Otterholt
  author_email: Braner@gmail.com
  author_url: http://forum.selid.es/profile.php?mode=viewprofile&amp;u=101548
  date: '2011-03-19 11:33:11 +0100'
  date_gmt: '2011-03-19 10:33:11 +0100'
  content: Whats up rather fantastic blog!! Man .. Beautiful .. Excellent .. I’ll
    bookmark your weblog and take the feeds
- id: 153871
  author: JenSHen
  author_email: admin@codetinkerhack.com
  author_url: http://codetinkerhack.com
  date: '2014-11-08 13:45:40 +0100'
  date_gmt: '2014-11-08 12:45:40 +0100'
  content: Hi, thanks for the post. I've attempted to execute OOM test with HashMaps
    for Instances and Classes and I see that Classloaders actually get collected (number
    of instances varies between 100 to 1000 and does not increase beyond that). So
    looks like there is no classloader leak in this case?
- id: 153952
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2014-11-12 20:05:57 +0100'
  date_gmt: '2014-11-12 19:05:57 +0100'
  content: Post somewhere your version of the test, please. I am really sure that
    holding references to instances of classes created by some classloader will block
    this particular classloader from being garbage collected.
---
<p>The first thing one should undestand before he tries to integrate scripting support into his application / framework are class loading issues. One of the main reasons (next to the ability to easily switch from Java) why we have chosen Groovy as our primary scripting language is very good support for live refresh of Groovy classes when source file has changed. But what does Groovy exactly do when it "refreshes" its loaded classes to conform to a newly modified source file? What about existing instances referencing to this class? Is it even possible in JVM to change class structure in runtime? Yes JavaRebel can do this, but it needs special setup and debug mode for hotswap. And how does all this fit into the existing Spring support? From the documentation it seems, that it all just magically works! Dozens of questions ran in my mind when I started to strive for Groovy integration in our product. Those questions gets answered in this article.</p>
<p><a id="more"></a><a id="more-548"></a></p>
<p>There are several options for integrating groovy into your application according to the <a href="http://groovy.codehaus.org/Embedding+Groovy" target="_blank">Groovy documentation</a>:</p>
<ul>
<li>evaluate scripts or expressions using the shell</li>
<li>generate and use new Java classes with GroovyClassloader</li>
<li>generate and use new Java classes with GroovyScriptEngine</li>
</ul>
<p>All three options can refresh code / class behaviour accorgingly to changes of underlying code. The difference between GroovyClassloader and GroovyScriptEngine regarding refreshing policy is that GroovyScriptEngine is able to recompile class even when that class hasn't directly changed, but any of classes this particular class depends on got changed (consider for example change of constant in interface your class uses).</p>
<p><b>Note:</b> there are several code samples, that are more transparent seeing them in the IDE. I recommend <a href="#download">download them</a> and read them from your prefered IDE.</p>
<h3>Basic recompilation principles</h3>
<p>It's not surprising, that there is no magic involved. The background of Groovy automatic recompilation is as follows:</p>
<ul>
<li>the only way how class can be changed is load it again</li>
<li>its true that <b>oldClass != recompiledClass && <br> <span style="margin-left: 60px">oldClass.getName().equals(recompiledClass.getName())</span></b></li>
<li>once Java Class is created - objects instantiated on its base do not ever change</li>
<li>old classes (even if they become obsolete by recompiled versions of these) won't get garbage collected if there is single instance of them held somewhere by the strong reference</li>
<li>GroovyClassLoader / GroovyScriptingEngine won't get garbage collected if there is single class it has created held somewhere by the strong reference</li>
</ul>
<p>These simple statements, can be proven by following set of tests:</p>
<h4>GroovyScriptingEngine</h4>
<p>[source lang="java"]<br />
public void testReloadGroovyClass() throws Exception {<br />
	//loads class, creates instance of it and calls nonparametrized method helloWorld, all references are<br />
	//then stored in custom class GroovyContext<br />
	GroovyContext ctx = createInstanceAndCallMethod(engine, "com.fg.mock.MainGroovyClass", "helloWorld");<br />
	//initial result of helloWorld method is following<br />
	assertEquals("Hello Universe.", ctx.getGroovyResult());<br />
	//we'll change source file contents so as method returns different value<br />
	modifyGroovyFile(<br />
			"com/fg/mock/MainGroovyClass.groovy",<br />
			"return HELLO_UNIVERSE;",<br />
			"return \"Bye bye\";"<br />
	);<br />
	//existing instances will remain unchanged<br />
	assertEquals("Hello Universe.", ctx.getGroovyMethod().invoke(ctx.getGroovyInstance()));<br />
	//new instances will use new definition<br />
	GroovyContext newCtx = createInstanceAndCallMethod(engine, "com.fg.mock.MainGroovyClass", "helloWorld");<br />
	//and as we see, result gets changed<br />
	assertEquals("Bye bye", newCtx.getGroovyResult());<br />
}</p>
<p>public void testReloadGroovyDependentClass() throws Exception {<br />
	//loads class, creates instance of it and calls nonparametrized method helloWorld, all references are<br />
	//then stored in custom class GroovyContext<br />
	GroovyContext ctx = createInstanceAndCallMethod(engine, "com.fg.mock.MainGroovyClass", "helloWorld");<br />
	//initial result of helloWorld method is following<br />
	assertEquals("Hello Universe.", ctx.getGroovyResult());<br />
	//we'll change source file of the Groovy interface our class implements and use to deduce return value<br />
	//of the helloWorld method call<br />
	modifyGroovyFile(<br />
			"com/fg/mock/GroovyHelloWorldInterface.groovy",<br />
			"HELLO_UNIVERSE = \"Hello Universe.\";",<br />
			"HELLO_UNIVERSE = \"Bye Universe.\";"<br />
	);<br />
	//even if we didn't change the main class it become reloaded as dependent one was changed<br />
	GroovyContext newCtx = createInstanceAndCallMethod(engine, "com.fg.mock.MainGroovyClass", "helloWorld");<br />
	assertEquals("Bye Universe.", newCtx.getGroovyResult());<br />
}<br />
[/source]</p>
<h4>GroovyClassloader</h4>
<p>The single difference in this example is that a class is not reloaded when another class (interface) this class depends on changes (or better - its source code changes).</p>
<p>[source lang="java"]<br />
public void testReloadLoadGroovyClass() throws Exception {<br />
	//loads class, creates instance of it and calls nonparametrized method helloWorld, all references are<br />
	//then stored in custom class GroovyContext<br />
	GroovyContext ctx = createInstanceAndCallMethod(clsLoader, "com.fg.mock.MainGroovyClass", "helloWorld");<br />
	//initial result of helloWorld method is following<br />
	assertEquals("Hello Universe.", ctx.getGroovyResult());<br />
	//we'll change source file contents so as method returns different value<br />
	modifyGroovyFile(<br />
			"com/fg/mock/MainGroovyClass.groovy",<br />
			"return HELLO_UNIVERSE;",<br />
			"return \"Bye bye\";"<br />
	);<br />
	//existing instances will remain unchanged<br />
	assertEquals("Hello Universe.", ctx.getGroovyMethod().invoke(ctx.getGroovyInstance()));<br />
	//new instances will use new definition<br />
	GroovyContext newCtx = createInstanceAndCallMethod(clsLoader, "com.fg.mock.MainGroovyClass", "helloWorld");<br />
	assertEquals("Bye bye", newCtx.getGroovyResult());<br />
}</p>
<p>public void testReloadLoadGroovyDependentClass() throws Exception {<br />
	//loads class, creates instance of it and calls nonparametrized method helloWorld, all references are<br />
	//then stored in custom class GroovyContext<br />
	GroovyContext ctx = createInstanceAndCallMethod(clsLoader, "com.fg.mock.MainGroovyClass", "helloWorld");<br />
	//initial result of helloWorld method is following<br />
	assertEquals("Hello Universe.", ctx.getGroovyResult());<br />
	//we'll change source file of the Groovy interface our class implements and use to deduce return value<br />
	//of the helloWorld method call<br />
	modifyGroovyFile(<br />
			"com/fg/mock/GroovyHelloWorldInterface.groovy",<br />
			"HELLO_UNIVERSE = \"Hello Universe.\";",<br />
			"HELLO_UNIVERSE = \"Bye Universe.\";"<br />
	);<br />
	//Groovy class loader doesn't recompile classes if dependent ones change<br />
	GroovyContext newCtx = createInstanceAndCallMethod(clsLoader, "com.fg.mock.MainGroovyClass", "helloWorld");<br />
	assertEquals("Hello Universe.", newCtx.getGroovyResult());<br />
}<br />
[/source]</p>
<h3>Warranted path to PermGenSpace leaks</h3>
<p>We can deduce from the class loading behaviour documented above, that path to the PermGenSpace leaks is straight and easy. When you create instances of groovy classes and store them in a long living memory scopes (such as static variables, singletons, servlet context or session scopes in case of web applications) and change source code of the groovy classes frequently - letting Groovy recompile them on the fly, it would likely lead to the OutOfMemoryError in PermGenSpace. Moreover there would be a bunch of instances based on currently obsolete code source from different modification stages. If you don't believe me, look at the following test:</p>
<p>[source lang="java"]<br />
/**<br />
 * Run with: -XX:MaxPermSize=1m -Xmx4M<br />
 * @throws Exception<br />
 */<br />
public void testOutOfMemory() throws Exception {<br />
	int iterations = 1000;<br />
	//uncomment this to have a long and happy life<br />
	//WeakHashMap<Class, Boolean> classes = new WeakHashMap<Class, Boolean>(iterations);<br />
	//WeakHashMap<Object, Boolean> instances = new WeakHashMap<Object, Boolean>(iterations);<br />
	//this leads to end with OOME<br />
	HashMap<Class, Boolean> classes = new HashMap<Class, Boolean>(iterations);<br />
	HashMap<Object, Boolean> instances = new HashMap<Object, Boolean>(iterations);<br />
	//this is test map for querying garbage collection of GroovyScriptEngines<br />
	WeakHashMap<GroovyScriptEngine, Boolean> engines = new WeakHashMap<GroovyScriptEngine, Boolean>(iterations);<br />
	//thousand iterations is enough to fail with 1MB of PermGenSize<br />
	int i = 0;<br />
	try {<br />
		for (; i < iterations; i++) {<br />
			//keep modifying source code file<br />
			modifyGroovyFile(<br />
					"com/fg/mock/MainGroovyClass.groovy",<br />
					"return .+;",<br />
					"return \"Hello world " + i + "\";"<br />
			);<br />
			//each time init new engine (even with the same engine it would early fail)<br />
			engine = new GroovyScriptEngine(<br />
					new URL[] {rootFSR.getURL()}<br />
			);<br />
			engines.put(engine, Boolean.TRUE);<br />
			//new instances will use new definition<br />
			GroovyContext ctx = createInstanceAndCallMethod(engine, "com.fg.mock.MainGroovyClass", "helloWorld");<br />
			//store instances in long living scope<br />
			classes.put(ctx.getGroovyClass(), Boolean.TRUE);<br />
			instances.put(ctx.getGroovyInstance(), Boolean.TRUE);<br />
			//each hundred iterations, run manualy GC (this is not necessary, but makes following line more precise)<br />
			if (i % 100 == 0) {<br />
				System.gc();<br />
				System.out.println(<br />
						(i + 1) + ": retained classes - " + classes.size() +<br />
								", retained instances - " + instances.size() +<br />
								", retained engines - " + engines.size()<br />
				);<br />
			}<br />
		}<br />
	} catch(OutOfMemoryError e) {<br />
		//here we are - with the OOME<br />
		String msg = "Out of memory with classes - " + classes.size() +<br />
				", retained instances - " + instances.size() +<br />
				", retained engines - " + engines.size() +<br />
				" on " + (i + 1) + " iterations.";<br />
		System.out.println(msg);<br />
		fail(msg);<br />
	}<br />
}<br />
[/source]</p>
<h3>A safe way around memory leaks</h3>
<p>It seems that the only way how to safely avoid memory leaking with Groovy recompilation is not to work directly with references to Groovy instances. You should use further explained approach everytime you need to store reference to Groovy object into a longer living memory scope - such as:</p>
<ul>
<li>static variables of Java classes *)</li>
<li>global variables of singleton Java instances *)</li>
<li>ServletContext or Session</li>
<li>local variables of long running methods (in daemon Threads and so on)</li>
<li>maybe other places that haven't came into my mind</li>
</ul>
<p>*) Java instance or Java class means in this sense a class loaded by Java classloader (one of the parent classloaders of Groovy class loader)</p>
<p>In such cases you should wrap the reference to Groovy instance into an another object managed by the Java class loader. Simple WeakReference would suffice in this case, but it has at least two big disadvantages:</p>
<ol>
<li>you cannot work with the Groovy instance transparently. Each time you want to call a method on a Groovy instance, you must retrieve encapsulating WeakReference and unwrap Groovy instance in it by calling get() method</li>
<li>you must take care of keeping instance alive another way, as WeakReference doesn't guarantee that Groovy instance object wouldn't get garbage collected (so that there must be another hard reference in static variables of Groovy classloader)</li>
</ol>
<p>On the other way you are safe to work with direct references to groovy instances in:</p>
<ul>
<li>static variables of Groovy classes</li>
<li>global variables of "singleton" Groovy instances</li>
</ul>
<p>You are completely safe to work with references as long as they don't leave the scope of the Groovy class loader (as you are in both above mentioned cases). Providing none of Groovy instance reference escaped from the Groovy scope GC can free all Groovy instances and classes as soon as you drop reference to the GroovyClassloader that created them.</p>
<h3>Spring Framework's solution confirms the idea</h3>
<p>Base clues for my research are based in Spring Groovy scripting implementation. Spring wraps all Groovy based beans into the JDK proxy, that could check original source code changes in specified intervals:</p>
<p>[source lang="xml"]<br />
<lang:groovy id="mainGroovyClass"<br />
                 refresh-check-delay="0"<br />
                 script-source="file:${project.build.directory}/target/test-classes/com/fg/mock/MainGroovyClass.groovy"/><br />
[/source]</p>
<p>Spring implementation, though very clever, has some limitations and I wonder what motivations lay behind chosen solution. Maybe some role plays the fact, that the same scripting layer is also used for other scripting libraries such as JRuby or Beanshell.</p>
<p>Mentioned limitations are:</p>
<ul>
<li><strong>JDK Proxy will allow you to call only methods placed in interfaces located in Java classes (means interfaces loaded by Java class loader)</strong><br>- this is not much cumbersome as long as you work with those instances in plain Java classes, because then you would need to use Reflection to get to the methods not declared on the Java interfaces. But when you forward your instances in some templating solution - such as Velocity of Freemarker, where reflection is used on every call - it's more than desirable to be able to call groovy methods directly without necessity to declare those methods in some Java interfaces.</li>
<li><strong>Spring reflects changes only on beans declared in Spring's application context</strong> - when you directly instantiate Groovy class in the class representing Groovy bean and source code of this "referenced" Groovy class changes, your bean won't notice it - Spring watches only source code of the beans.</li>
</ul>
<p>Again I can prove those limitation by following tests:</p>
<p>[source lang="java"]<br />
public void testReloadLoadGroovyClass() throws Exception {<br />
	JavaHelloWorldInterface myGroovyInstance = (JavaHelloWorldInterface)ctx.getBean("mainGroovyClass");<br />
	assertEquals("Hello Universe.", myGroovyInstance.sayHello());</p>
<p>	modifyGroovyFile(<br />
			"com/fg/mock/MainGroovyClass.groovy",<br />
			"return HELLO_UNIVERSE;",<br />
			"return \"Bye bye\";"<br />
	);</p>
<p>	//Spring will take care of refresh<br />
	assertEquals("Bye bye", myGroovyInstance.sayHello());<br />
}</p>
<p>public void testReloadLoadGroovyDependentClass() throws Exception {<br />
	JavaHelloWorldInterface myGroovyInstance = (JavaHelloWorldInterface)ctx.getBean("mainGroovyClass");<br />
	assertEquals("Hello Universe.", myGroovyInstance.sayHello());</p>
<p>	modifyGroovyFile(<br />
			"com/fg/mock/GroovyHelloWorldInterface.groovy",<br />
			"HELLO_UNIVERSE = \"Hello Universe.\";",<br />
			"HELLO_UNIVERSE = \"Bye Universe.\";"<br />
	);</p>
<p>	//Spring DOESN'T take dependent classes into an account<br />
	assertEquals("Hello Universe.", myGroovyInstance.sayHello());<br />
}</p>
<p>public void testReloadGroovyDependentClassVerifyInstance() throws Exception {<br />
	JavaHelloWorldInterface myGroovyInstance = (JavaHelloWorldInterface)ctx.getBean("referencingGroovyClass");<br />
	assertEquals("Hello Universe.", myGroovyInstance.sayHello());</p>
<p>	modifyGroovyFile(<br />
			"com/fg/mock/MainGroovyClass.groovy",<br />
			"return HELLO_UNIVERSE;",<br />
			"return \"Hei universumissa.\";"<br />
	);</p>
<p>	//Spring can refresh underlying bean even for existing instances (proxy plays its role)<br />
	assertEquals("Hei universumissa.", myGroovyInstance.sayHello());<br />
}<br />
[/source]</p>
<h3>Proof of concept</h3>
<p>These findings and supposed solutions were deduced by studying code of Groovy and Spring and are proven by a set of unit prototyping unit tests. As a novice in Groovy I cannot present my deductions as rock solid so you're welcome to download the tests and either confirm or refutate my conclusions.</p>
<p><a name="download" href="http://files.novoj.net/GroovyIntegration/groovy-test.zip">Download ZIP with sources and tests</a></p>
<h3>What comes next ...</h3>
<p>In the next part of this "Groovy integration serie" I will present solution for programmatic Groovy object instantiation, that will allow you:</p>
<ul>
<li>work with references to Groovy instances safely thorough your codebase - even storing them in long living scopes</li>
<li>keep making profit on Groovy's ability to refresh classes in runtime</li>
<li>access any public method / variable declared on Groovy class from outside (fe. any templating solution)</li>
</ul>
<p>So, stay tuned!</p>
