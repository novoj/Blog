---
status: publish
published: true
title: Testing Aspect Pointcuts - is there an easy way?
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<p>Nice thing about Aspect Oriented Programming is that you can easily add
  piece of logic to several (possibly other way not connected) parts of your application.
  You'll only write an Advice (piece of code that should be weaved into original code
  and executed at exactly specified point of time) and define Pointcut (an expression
  defining which classes and methods shall be advised). Please, keep in mind, that
  above description is somewhat simplyfying and that AOP could be much broader than
  this. Describing AOP is not the aim of this post - the aim lies in something else,
  and that is - testing. What's the best approach to test application logic modified
  in runtime (or compile time) with AOP process?</p>\r\n\r\n"
wordpress_id: 61
wordpress_url: http://blog.novoj.net/2008/09/20/testing-aspect-pointcuts-is-there-an-easy-way/
date: '2008-09-20 11:26:39 +0200'
date_gmt: '2008-09-20 10:26:39 +0200'
categories:
- Programování
- Java
- Testování
- Spring Framework
tags: []
comments:
- id: 24534
  author: Myšlenky dne otce Fura &raquo; Blog Archive &raquo; When does your Spring
    @Transactional attribute apply on CgLib proxies
  author_email: ''
  author_url: http://blog.novoj.net/2010/08/10/when-does-your-spring-transactional-attribute-apply-on-cglib-proxies/
  date: '2010-08-10 20:05:48 +0200'
  date_gmt: '2010-08-10 19:05:48 +0200'
  content: "[...] easy as we usually use Springs&#8217; transaction rollback on tear
    down testing approach. Though there are solutions to test aspect oriented logic
    it&#8217;s not without a price. More than that &#8211; we very much got used relying
    on easy-to-use [...]"
- id: 48884
  author: bob
  author_email: spoon.reloaded@gmail.com
  author_url: ''
  date: '2011-08-16 00:29:56 +0200'
  date_gmt: '2011-08-15 23:29:56 +0200'
  content: "testedAdviceClass.isAssignableFrom(advisor.getAdvice().getClass())\r\n\r\nshould
    be written as\r\n\r\ntestedAdviceClass.isInstance(advisor.getAdvice())"
- id: 48973
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-08-16 20:37:16 +0200'
  date_gmt: '2011-08-16 19:37:16 +0200'
  content: Yes, thanks - it's been a long time I've written this. I would use this
    now for sure.
---
<p>Nice thing about Aspect Oriented Programming is that you can easily add piece of logic to several (possibly other way not connected) parts of your application. You'll only write an Advice (piece of code that should be weaved into original code and executed at exactly specified point of time) and define Pointcut (an expression defining which classes and methods shall be advised). Please, keep in mind, that above description is somewhat simplyfying and that AOP could be much broader than this. Describing AOP is not the aim of this post - the aim lies in something else, and that is - testing. What's the best approach to test application logic modified in runtime (or compile time) with AOP process?</p>
<p><a id="more"></a><a id="more-61"></a></p>
<p>We can quite easily test the Advice - it's a plain piece of code, that could be decomposed to several methods that could be tested and verified one by one. But what about the other part of aspect? Pointcut is hard to test - often it's only a matter of configuration (as in Spring). So the only choice to setup more expensive integration test. While writing integration test it could be hard to test advice itself (for example how can we verify that we've configured Spring's TransactionInterceptor right and that it works well?) and maybe senseless when the advice has been unit tested (as I am sure TransactionInterceptor was). In such cases it would suffice only to test that advice is properly called. But even that you can achieve with difficulty.</p>
<h3>Checking Spring Advised interface</h3>
<p>In Spring there is a way how to find out whether you are working with object modified by weaving process. Such objects (or better proxies) are implementing org.springframework.aop.framework.Advised interface. This interface declares method getAdvisors() that returns a list of advisors, each holding reference to a single advice. You can take advantage from this Spring's behaviour by checking you pointcut settings.</p>
<p>This is presented on following example. Method testAdvice will check all beans in map for weaved advice of testedAdviceClass.</p>
<p>[source lang="java"]<br />
private void testAdvice(Map beans, Class testedAdviceClass) {<br />
	Iterator it = beans.keySet().iterator();<br />
	while(it.hasNext()) {<br />
		String beanName = (String)it.next();<br />
		Object strg = beans.get(beanName);<br />
		if(strg instanceof Advised) {<br />
			Advised advised = ((Advised)strg);<br />
			Advisor[] advisors = advised.getAdvisors();<br />
			boolean transactionAdvice = false;<br />
			for(int i = 0; i < advisors.length; i++) {<br />
				Advisor advisor = advisors[i];<br />
				if(testedAdviceClass.isAssignableFrom(advisor.getAdvice().getClass())) {<br />
					transactionAdvice = true;<br />
				}<br />
			}<br />
			assertTrue(beanName + " has no " + testedAdviceClass.getName() + " advice on it.", transactionAdvice);<br />
		}<br />
		else {<br />
			fail(beanName + " is not Advised!");<br />
		}<br />
	}<br />
}<br />
[/source]</p>
<p>This approach is valid only for Spring and cannot be used in other environments. Next disadvantage of this test logic is that you can verify only presence of advice on a object (class respectivelly). It cannot ensure you that advice will participate in a particular method call.</p>
<h3>Using logging facility for verification of pointcuts</h3>
<p>Other approach could be to use standard logging facility (such as Java Logging, SL4J or Log4J) for checking whether particular piece of code was executed or not. Assuming that every class has its internal log calls, we could check out if advice participated in our business object call. Beauty of this solution is that it doesn't require special test setup - it could be part of standard integration test that you should have in anyway.</p>
<p>Let's take Spring declarative transaction management as our example. We don't have to test whether Spring's TransactionInterceptor works well - it was tested by Rod Johnson and Juergen Hoeller. But we should test integration of this advice with our business logic. If we look into TransactionInterceptor code we can see that it calls TransactionAspectSupport when dealing with transaction. Examining further the code (or logging output) we can see that when opening transaction Spring logs:</p>
<p>[source lang="xml"]<br />
Getting transaction for [className.methodName]<br />
[/source]</p>
<p>When completing transaction (commit or rollback - example in the same order) it logs:</p>
<p>[source lang="xml"]<br />
Completing transaction for [className.methodName]<br />
Completing transaction for [className.methodName] after exception<br />
[/source]</p>
<p>Easiest form of such test could be as follows (test uses custom appender implementation TestAppender, that just holds log events in memory):</p>
<p>[source lang="java"]<br />
public void testCreateUserWithProperties() throws Exception {<br />
	if(log.isInfoEnabled()) {<br />
		log.info("***************************************************************");<br />
		log.info("      SWITCHING TO TEST CONTROLLED LOGGING ENVIRONMENT         ");<br />
		log.info("***************************************************************");<br />
	}<br />
	LogManager.resetConfiguration();<br />
	Logger logger = LogManager.getLogger(TransactionInterceptor.class.getName());<br />
	logger.setLevel(Level.TRACE);<br />
	logger.addAppender(testAppender);</p>
<p>	//this executes real integration test<br />
	super.testCreateUserWithProperties();<br />
        //there we just verify that expected logs have been recorded<br />
	assertTrue(testAppender.containsLogRecord("Getting transaction for [cz.novoj.business.UserManager.createUserWithProperties]"));<br />
	assertTrue(testAppender.containsLogRecord("Completing transaction for [cz.novoj.business.UserManager.createUserWithProperties]"));<br />
}<br />
[/source]</p>
<p>This example represents the idea (I hope) in quite understandable way, but for real usage I would recommend different test implementation. We have to consider, that logging certainly isn't part of class API but it belongs to class internals that could be changed any time without notice. So if we would create dozens of tests of this type, it could costs us a lot of time to adapt tests when log messages change. Keeping object oriented approach I would recommend creating special Appender implementation for each Advice that encapsulates log checking logic.</p>
<p>Let's create base class that will contain all common test logic:</p>
<p>[source lang="java"]<br />
/**<br />
 * Base test appender used to capture logging events for test purposes.<br />
 *<br />
 * @author Jan Novotný<br />
 * @version $Id: $<br />
 */<br />
public class TestAppender extends AppenderSkeleton {<br />
	private static Log log = LogFactory.getLog(TestAppender.class);<br />
	private final Class[] monitoredClasses;<br />
	private final LoggerInfo[] backedUpLoggers;<br />
	private final List<LoggingEvent> events = new ArrayList<LoggingEvent>();</p>
<p>	public TestAppender(Class monitoredClass) {<br />
		this(new Class[] {monitoredClass});<br />
	}</p>
<p>	public TestAppender(Class[] monitoredClasses) {<br />
		super();<br />
		this.monitoredClasses = monitoredClasses;<br />
		if(log.isInfoEnabled()) {<br />
			log.info("***************************************************************");<br />
			log.info("        APPENDING TEST CONTROLLED LOGGING ENVIRONMENT          ");<br />
			log.info("***************************************************************");<br />
		}<br />
		backedUpLoggers = new LoggerInfo[monitoredClasses.length];<br />
		for(int i = 0; i < monitoredClasses.length; i++) {<br />
			Class monitoredClass = monitoredClasses[i];<br />
			Logger logger = LogManager.getLogger(monitoredClass);<br />
			backedUpLoggers[i] = new LoggerInfo(logger.getLevel(), logger.getAdditivity());<br />
			logger.setLevel(Level.TRACE);<br />
			logger.addAppender(this);<br />
			logger.setAdditivity(true);<br />
		}<br />
	}</p>
<p>	public void clearLogChanges() {<br />
		for(int i = 0; i < monitoredClasses.length; i++) {<br />
			Class monitoredClass = monitoredClasses[i];<br />
			Logger logger = LogManager.getLogger(monitoredClass);<br />
			logger.setLevel(backedUpLoggers[i].getOriginalLevel());<br />
			logger.setAdditivity(backedUpLoggers[i].isOriginalAdditivity());<br />
			logger.removeAppender(this);<br />
		}<br />
		if(log.isInfoEnabled()) {<br />
			log.info("***************************************************************");<br />
			log.info("         REMOVED TEST CONTROLLED LOGGING ENVIRONMENT           ");<br />
			log.info("***************************************************************");<br />
		}<br />
	}</p>
<p>	protected void append(LoggingEvent event) {<br />
		synchronized(events) {<br />
			events.add(event);<br />
			System.out.println(">>> Capturing : " + event.getMessage());<br />
		}<br />
	}</p>
<p>	public int countLogRecord(String messagePart) {<br />
		int counter = 0;<br />
		for(LoggingEvent event : events) {<br />
			String message = (String)event.getMessage();<br />
			if(message != null && message.indexOf(messagePart) > -1) {<br />
				counter ++;<br />
			}<br />
		}<br />
		return counter;<br />
	}</p>
<p>	public int countExactLogRecord(String comparedMessage) {<br />
		int counter = 0;<br />
		for(LoggingEvent event : events) {<br />
			String message = (String)event.getMessage();<br />
			if(message != null && message.equals(comparedMessage)) {<br />
				counter ++;<br />
			}<br />
		}<br />
		return counter;<br />
	}</p>
<p>	public boolean containsLogRecord(String messagePart) {<br />
		return countLogRecord(messagePart) > 0;<br />
	}</p>
<p>	public boolean containsSingleLogRecord(String messagePart) {<br />
		return countLogRecord(messagePart) == 1;<br />
	}</p>
<p>	public boolean containsExactLogRecord(String completeMessage) {<br />
		return countExactLogRecord(completeMessage) > 0;<br />
	}</p>
<p>	public boolean containsExactSingleLogRecord(String completeMessage) {<br />
		return countExactLogRecord(completeMessage) == 1;<br />
	}</p>
<p>	public void close() {<br />
		events.clear();<br />
		clearLogChanges();<br />
	}</p>
<p>	public boolean requiresLayout() {<br />
		return false;<br />
	}</p>
<p>	private class LoggerInfo {<br />
		Level originalLevel;<br />
		boolean originalAdditivity;</p>
<p>		public LoggerInfo(Level originalLevel, boolean originalAdditivity) {<br />
			this.originalLevel = originalLevel;<br />
			this.originalAdditivity = originalAdditivity;<br />
		}</p>
<p>		public Level getOriginalLevel() {<br />
			return originalLevel;<br />
		}</p>
<p>		public boolean isOriginalAdditivity() {<br />
			return originalAdditivity;<br />
		}<br />
	}</p>
<p>}<br />
[/source]</p>
<p>Then we will create specialized descendants testing log output of particular interceptors. This one for example checks output of standard Spring TransactionInterceptor advice (as we discussed above):</p>
<p>[source lang="java"]<br />
/**<br />
 * Log4J appender optimalized to check Spring transaction operations being processed.<br />
 *<br />
 * @author Jan Novotný, FG Forrest a.s. (c) 2007<br />
 * @version $Id: $<br />
 */<br />
public class SpringTransactionTestAppender extends TestAppender {</p>
<p>	public SpringTransactionTestAppender() {<br />
		super(TransactionInterceptor.class);<br />
	}</p>
<p>	public boolean isTransactionOpened(Class forClass, String forMethod) {<br />
		return containsExactSingleLogRecord("Getting transaction for [" + forClass.getName() + "." + forMethod + "]");<br />
	}</p>
<p>	public boolean isTransactionCommited(Class forClass, String forMethod) {<br />
		return containsExactSingleLogRecord("Completing transaction for [" + forClass.getName() + "." + forMethod + "]");<br />
	}</p>
<p>	public boolean isTransactionRollbacked(Class forClass, String forMethod) {<br />
		return containsSingleLogRecord("Completing transaction for [" + forClass.getName() + "." + forMethod + "] after exception");<br />
	}</p>
<p>}<br />
[/source]</p>
<p>Our test then will look like this (can you see the simplicity?!):</p>
<p>[source lang="java"]<br />
@RunWith(SpringJUnit4ClassRunner.class)<br />
@ContextConfiguration(<br />
		locations = {<br />
				"classpath:spring/spring-datasource.xml",<br />
				"classpath:spring/spring-dao.xml",<br />
				"classpath:spring/spring-business.xml",<br />
				"classpath:spring/spring-transaction.xml"<br />
				},<br />
		loader = HostConfigurableContextLoader.class<br />
)<br />
@Transactional<br />
public class UserManagerIntegrationTest extends UserManagerTest {<br />
	@Autowired(required = true)<br />
	UserManager userManager;<br />
	SpringTransactionTestAppender transactionTestAppender;</p>
<p>	@Before<br />
	public void initLogger() {<br />
		transactionTestAppender = new SpringTransactionTestAppender();<br />
	}</p>
<p>	@After<br />
	public void closeLogger() {<br />
		transactionTestAppender.close();<br />
	}</p>
<p>	@Test<br />
	public void testCreateUserWithPropertiesTransaction() throws Exception {<br />
                //again we run our integration test<br />
		super.testCreateUserWithProperties();</p>
<p>                //and now we verify, that opening and closing transaction operations were made by the TransactionInterceptor<br />
		String methodName = "createUserWithProperties";<br />
		assertTrue(transactionTestAppender.isTransactionOpened(UserManager.class, methodName));<br />
		assertTrue(transactionTestAppender.isTransactionCommited(UserManager.class, methodName));<br />
		assertFalse(transactionTestAppender.isTransactionRollbacked(UserManager.class, methodName));<br />
	}</p>
<p>}<br />
[/source]</p>
<p>You can see that when Rod or Juergen decide to change log output it will mean for us only to change few lines in SpringTransactionTestAppender to adapt (ok, we are relying that they will log somenting meaningful in such moments as open, commit and rollback transaction). When you test your own advices it's even simplier - you have everything in your hands.</p>
<p>Even I thought that this idea is my own (or ours own, because it was invented on way back home from CZJUG meeting in discussion with my friend Pavel Jetenský) I found out that NetBeans guys were the first. In their article <a href="http://openide.netbeans.org/tutorial/test-patterns.html" target="_new">Test patterns</a> they recommend logging for testing parallel execution problems (such as deadlock, race conditions and so) in chapters Analyzing Random Failures, Advanced usage of Logging, Execution Flow Control using Logging. It's hard to be the first these times ;-) ...</p>
<p>Examples shown in this article are available to <a href="http://files.novoj.net/LogTesting/sources.zip">download</a>. So you can examine them more properly in your IDE and even run the tests.</p>
<p><strong><a href="http://files.novoj.net/LogTesting/sources.zip">Example sources</a></strong></p>
