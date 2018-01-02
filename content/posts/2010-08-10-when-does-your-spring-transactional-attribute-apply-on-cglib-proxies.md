---
status: publish
published: true
title: When does your Spring @Transactional attribute apply on CgLib proxies
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<a href=\"http://blog.novoj.net/binary/2010/08/spring-logo-blue.gif\"><img
  src=\"http://blog.novoj.net/binary/2010/08/spring-logo-blue.gif\" alt=\"\" title=\"spring-logo-blue\"
  width=\"243\" height=\"107\" class=\"alignleft size-full wp-image-1005\" /></a>Testing
  transactional aspect of your application is not easy as we usually use Springs'
  transaction rollback on tear down testing approach. Though <a href=\"http://blog.novoj.net/2008/09/20/testing-aspect-pointcuts-is-there-an-easy-way/\">there
  are solutions to test aspect oriented logic</a> it's not without a price. More than
  that - we very much got used relying on easy-to-use Spring @Transaction annotation
  so that we don't usually take an effort to do it. There is a few standard Spring
  rules for rollbacking transaction in relation to method resolution:\r\n\r\n<ul>\r\n
  \  <li>transaction is automatically rollbacked only on unchecked exeption (RuntimeException)</li>\r\n
  \  <li>rollback will also occur for exception types specified in rollback-for attribute
  of the annotation or XML element</li>\r\n   <li>rollback will not occur for exception
  types specified in no-rollback-for attribute of the annotation or XML element</li>\r\n
  \  <li>transaction demarcation will aplly only to the external calls of the bean
  method (consider use-case when external logic calls a public method on your bean,
  that is not annotated with @Transactionaidl and this method will call in its body
  another public method of the same class that has @Transaction annotation - in such
  case Spring will not start and manage transaction)</li>\r\n</ul>\r\n\r\nBut there
  is yet another one - your @Transactional annotation must be resolved by Spring bean
  post processing logic in the first place. Usually it is, but when using CgLib based
  proxies (proxy-target-class) there is a catch which will cause omitting @Transactional
  annotation on your method declaration. \r\n\r\n"
wordpress_id: 943
wordpress_url: http://blog.novoj.net/?p=943
date: '2010-08-10 20:05:39 +0200'
date_gmt: '2010-08-10 19:05:39 +0200'
categories:
- Java
- Spring Framework
- English
- Databáze
tags:
- CgLib
comments:
- id: 34769
  author: 私家偵探
  author_email: Sherburne568@gmail.com
  author_url: http://tw.myblog.yahoo.com/t4h51rg
  date: '2011-02-25 07:04:04 +0100'
  date_gmt: '2011-02-25 06:04:04 +0100'
  content: Your page is looks mercy, your graphics are charming, and what’s more,
    you use reference that are relevant to what you are saying,2
- id: 38387
  author: Wilbur Pingel
  author_email: Bann1055@comcast.com
  author_url: http://www.bullshit.com/member.php?4924-Kashazxc
  date: '2011-04-15 10:25:33 +0200'
  date_gmt: '2011-04-15 09:25:33 +0200'
  content: I would like to thnkx for the efforts you've put in writing this blog.
    I'm hoping the same high-grade blog post from you in the upcoming as well. Actually
    your creative writing skills has inspired me to get my own web site now. Really
    the blogging is spreading its wings rapidly. Your write up is a good example of
    it.
---
<p><a href="http://blog.novoj.net/binary/2010/08/spring-logo-blue.gif"><img src="http://blog.novoj.net/binary/2010/08/spring-logo-blue.gif" alt="" title="spring-logo-blue" width="243" height="107" class="alignleft size-full wp-image-1005" /></a>Testing transactional aspect of your application is not easy as we usually use Springs' transaction rollback on tear down testing approach. Though <a href="http://blog.novoj.net/2008/09/20/testing-aspect-pointcuts-is-there-an-easy-way/">there are solutions to test aspect oriented logic</a> it's not without a price. More than that - we very much got used relying on easy-to-use Spring @Transaction annotation so that we don't usually take an effort to do it. There is a few standard Spring rules for rollbacking transaction in relation to method resolution:</p>
<ul>
<li>transaction is automatically rollbacked only on unchecked exeption (RuntimeException)</li>
<li>rollback will also occur for exception types specified in rollback-for attribute of the annotation or XML element</li>
<li>rollback will not occur for exception types specified in no-rollback-for attribute of the annotation or XML element</li>
<li>transaction demarcation will aplly only to the external calls of the bean method (consider use-case when external logic calls a public method on your bean, that is not annotated with @Transactionaidl and this method will call in its body another public method of the same class that has @Transaction annotation - in such case Spring will not start and manage transaction)</li>
</ul>
<p>But there is yet another one - your @Transactional annotation must be resolved by Spring bean post processing logic in the first place. Usually it is, but when using CgLib based proxies (proxy-target-class) there is a catch which will cause omitting @Transactional annotation on your method declaration. </p>
<p><a id="more"></a><a id="more-943"></a></p>
<p>Please read carefully following part of Spring documentation:</p>
<div  style="border: 1px solid white; background-color: #333333; font-size: 90%; padding: 20px;">
<cite>The Spring team's recommendation is that you only annotate concrete classes with the @Transactional annotation, as opposed to annotating interfaces. You certainly can place the @Transactional annotation on an interface (or an interface method), but this will only work as you would expect it to if you are using interface-based proxies. The fact that annotations are not inherited means that if you are using class-based proxies (proxy-target-class="true") or the weaving-based aspect (mode="aspectj") then the transaction<br />
settings will not be recognised by the proxying/weaving infrastructure and the object will not be wrapped in a transactional proxy (which would be decidedly bad). So please do take the Spring team's advice and only annotate concrete classes (and the methods of concrete classes) with the @Transactional annotation.</cite>
</div>
<p>You wouldn't probably understand to this paragraph entirely unless you run into the mentioned catch. I've prepared a test suite (<a href="http://github.com/novoj/SpringTransactionTest" target="_blank">download from GitHub</a>) that shows this fact in real code situation. When you run the test suite you'll see that the test <i>ProgramaticFactoryBeanUserManagerIntegrationTest</i> won't pass. In this test we use a object created by our FactoryBean that returns not directly instance of our class but a CgLib derived class extension instance. CgLib creates a new class that extends our class and overrides all methods making them final. Unfortunatelly when overriding methods it doesn't copy their annotations specified in the parent class (<a href="http://sourceforge.net/tracker/?func=detail&aid=2255414&group_id=56933&atid=482371" target="_blank">there is an long time open issue</a>). Furthermore annotations placed on the methods shouldn't get resolved in the inheritance chain (compared to the annotations placed on classes) as mentioned <a href="https://jira.springframework.org/browse/SPR-975?page=com.atlassian.jira.plugin.system.issuetabpanels%253Aall-tabpanel" target="_blank">in Jurgen Hoellers' resolved issue</a>. </p>
<div style="border: 1px solid white; background-color: #333333; font-size: 90%; padding: 20px;">
<strong>Note: </strong> As you can see other @Transactional use-cases work well - either @Transactional annotation declared on the class (case of <i>ClassWideAnnotationUserManager</i> class) or @Transactional annotation placed on methods of interface, that is afterwards implemented by our manager (case of <i>InterfaceBasedUserManager</i> class). Both of these cases are resolved ok.
</div>
<p>So the Spring transactional infracture in our case considers only methods on the CgLib derived class where annotations are missing. And that is the exact point of this paragraph in the documentation and the main problem of mine as I use this in my codebase a lot. Luckily there is simple undocumented solution to this problem.</p>
<h3>Solution for the hopeless</h3>
<p>In order to trigger Spring @Transactional annotation resolution we usually use following statement in our Spring XML configuration:</p>
<p>[source lang="xml"]<br />
<tx:annotation-driven proxy-target-class="true"/><br />
[/source]</p>
<p>In such case standard Spring resolution logic will aplly, which would lead us into the error situation. This decaration could be also rewritten in more explicit way:</p>
<p>[source lang="xml"]<br />
<bean class="org.springframework.aop.framework.autoproxy.DefaultAdvisorAutoProxyCreator"></p>
<property name="proxyTargetClass" value="true"/>
</bean></p>
<p><bean class="org.springframework.transaction.interceptor.TransactionAttributeSourceAdvisor"></p>
<property name="transactionInterceptor" ref="transactionInterceptor"/>
</bean></p>
<p><bean id="transactionInterceptor" class="org.springframework.transaction.interceptor.TransactionInterceptor"></p>
<property name="transactionManager" ref="transactionManager"/>
<property name="transactionAttributeSource">
		<bean class="cz.novoj.business.transactionalRelover.CglibOptimizedAnnotationTransactionAttributeSource"/>
	</property>
</bean><br />
[/source]</p>
<p>As you see in this configuration we can redefine <i>transactionAttributeSource</i> property of the <i>transactionInterceptor</i> that finally does the annotation resolution. Then we could slightly modify original Spring logic for annotation resolving in following way:</p>
<p>[source lang="java"]<br />
public class CglibOptimizedAnnotationTransactionAttributeSource extends AnnotationTransactionAttributeSource {<br />
	private static final Log log = LogFactory.getLog(CglibOptimizedAnnotationTransactionAttributeSource.class);</p>
<p>	@Override<br />
	protected TransactionAttribute findTransactionAttribute(Method method) {<br />
		Class<?> declaringClass = method.getDeclaringClass();<br />
		if (AopUtils.isCglibProxyClass(declaringClass)) {<br />
			try {<br />
				//find appropriate method on parent class<br />
				Method superMethod = declaringClass.getSuperclass().getMethod(method.getName(), method.getParameterTypes());<br />
				return super.findTransactionAttribute(superMethod);<br />
			} catch (Exception ex) {<br />
				if(log.isWarnEnabled()) {<br />
					log.warn("Cannot find superclass method for Cglib method: " + method.toGenericString());<br />
				}<br />
				return super.findTransactionAttribute(method);<br />
			}<br />
		} else {<br />
			return super.findTransactionAttribute(method);<br />
		}<br />
	}</p>
<p>}<br />
[/source]</p>
<p>As you can see - in case that we run at CgLib generated proxy we won't search for the annotation on that particular class (as we know that CgLib doesn't copy annotation definitions), but instead on the parent class relevant methods. This way our @Transactional annotation on all methods gets resolved and transactions will start to work.</p>
<div style="border: 1px solid white; background-color: #333333; font-size: 90%; padding: 20px;">
<strong>Note: </strong> You can test this solution by changing linked Spring configuration file in AbstractUserManagerTransactionalTest class  <br>from:<i>classpath:spring/spring-transaction.xml</i><br>to: <i>classpath:spring/spring-transaction-solution.xml</i>
</div>
<p>I've also setup <a href="https://jira.springframework.org/browse/SPR-7448" target="_blank">an issue in the Spring Framework issue tracker</a>, that suggests to adopt this solution into the standard Spring codebase. We'll see how the Spring guys will react. Until then you could take advantage of this solution.</p>
<h3>Resources</h3>
<ul>
<li><a href="http://github.com/novoj/SpringTransactionTest" target="_blank">Test suite with proposed solution ready to download from GitHub</a></li>
<li><a href="http://sourceforge.net/tracker/?func=detail&aid=2255414&group_id=56933&atid=482371" target="_blank">Long time untouched issue on CgLlib proxying mechanism</a></li>
<li><a href="https://jira.springframework.org/browse/SPR-975?page=com.atlassian.jira.plugin.system.issuetabpanels%253Aall-tabpanel" target="_blank">Original Jurgen Hoellers' expression to the similar issue in Spring 1.2.X</a></li>
<li><a href="https://jira.springframework.org/browse/SPR-7448" target="_blank">Issue for this problem at Spring tracker</a></li>
</ul>
