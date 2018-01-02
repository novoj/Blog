---
status: publish
published: true
title: Combining custom annotations for securing methods with Spring Security
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft  wp-image-1858\" title=\"spring_security\" src=\"http://blog.novoj.net/binary/2012/03/spring_security_extjs_login-e1332024054704.png\"
  alt=\"\" width=\"149\" height=\"58\" /> <a href=\"http://static.springsource.org/spring-security/site/\"
  target=\"_blank\">Spring security</a> is really powerful library in its current
  version and I like it much. You can secure your application on method level several
  years now (this feature was introduced by <a href=\"http://www.nofluffjuststuff.com/blog/craig_walls/2008/04/method_level_security_in_spring_security_2_0\"
  target=\"_blank\">Spring Security 2 in 4/2008</a>) but we've upgraded from old Acegi
  Security only recently. When using method access control in larger scale I started
  to think about security rules encapsulation into standalone annotation definitions.
  It's something you can live without but in my opinion it could help readibility
  and maintainability of the code. Let's present some options we have now ...\r\n\r\n"
wordpress_id: 1857
wordpress_url: http://blog.novoj.net/?p=1857
date: '2012-03-27 21:42:36 +0200'
date_gmt: '2012-03-27 20:42:36 +0200'
categories:
- Programování
- Java
- Spring Framework
- English
tags:
- security
comments:
- id: 64798
  author: Victor Dario Martinez
  author_email: dariovmartine@gmail.com
  author_url: ''
  date: '2012-03-29 18:47:06 +0200'
  date_gmt: '2012-03-29 17:47:06 +0200'
  content: I just voted in jira. good luck!
- id: 65138
  author: Zubbate
  author_email: glubokaya@gmail.com
  author_url: ''
  date: '2012-04-05 16:39:13 +0200'
  date_gmt: '2012-04-05 15:39:13 +0200'
  content: This approach is almost exactly what I need. But I tried to configure secutiry
    context the way you wrote but got no security handling. I see that my methods
    are called w/o interception. Could you please help me out what can be wrong?
- id: 65164
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-04-06 07:02:30 +0200'
  date_gmt: '2012-04-06 06:02:30 +0200'
  content: I'd like to, but it's hard to guess without any data. Would it be possible
    for you to send me your project / part of the project with some failing tests?
    I might find out what's wrong then.
- id: 73769
  author: "&raquo; How do YOU test access control of your application? Myšlenky dne
    otce Fura"
  author_email: ''
  author_url: http://blog.novoj.net/2012/06/14/how-do-you-test-access-control-of-your-application/
  date: '2012-06-14 23:11:10 +0200'
  date_gmt: '2012-06-14 22:11:10 +0200'
  content: "[...] If you wonder what @Allowed* annotations mean you might want to
    read another my article Custom annotations for Spring Security &#8211; but in
    short you can imagine them as multiple @PreAuthorize annotations with some SpEL
    in [...]"
- id: 148464
  author: "&raquo; Šestý rok Myšlenek dne otce Fura Myšlenky dne otce Fura"
  author_email: ''
  author_url: http://blog.novoj.net/2013/01/01/sesty-rok-myslenek-dne-otce-fura/
  date: '2013-01-01 00:01:19 +0100'
  date_gmt: '2012-12-31 23:01:19 +0100'
  content: "[...] vpřed především díky poměrně masivnímu nasazení Spring Security,
    o kterém jsem psal i několik [...]"
- id: 152059
  author: Spring Security - Custom annotation for securing methods | Java CodeBook
  author_email: ''
  author_url: http://javacodebook.com/2013/07/05/spring-security-custom-annotation-for-securing-methods/
  date: '2013-08-04 19:30:48 +0200'
  date_gmt: '2013-08-04 18:30:48 +0200'
  content: "[...] http://blog.novoj.net/2012/03/27/combining-custom-annotations-for-securing-methods-with-spring-secur...
    Page Visitors: 4 [...]"
- id: 156241
  author: NoSuchBeanDefinitionException, but bean is defined | FYTRO SPORTS
  author_email: ''
  author_url: http://fytro.info/nosuchbeandefinitionexception-but-bean-is-defined/
  date: '2015-06-16 16:06:22 +0200'
  date_gmt: '2015-06-16 15:06:22 +0200'
  content: "[&#8230;] I am attempting to get the configurations into Spring Boot using
    Java based config instead of XML config from this blog post: http://blog.novoj.net/2012/03/27/combining-custom-annotations-for-securing-methods-with-spring-secur&#8230;
    [&#8230;]"
- id: 157545
  author: "&raquo; Reportáž z GeeCON Praha 2015 Myšlenky dne otce Fura"
  author_email: ''
  author_url: http://blog.novoj.net/2015/10/26/reportaz-z-geecon-praha-2015/
  date: '2015-10-26 10:35:34 +0100'
  date_gmt: '2015-10-26 09:35:34 +0100'
  content: "[&#8230;] kompozice anotací (je velká škoda, že podobnou věc nelze udělat
    i ve Spring Security &#8211; což sice lze obejít, ale dost pracně). Zdůrazňoval
    respektování použitých generik v třídách autowirovaných [&#8230;]"
---
<p><img class="alignleft  wp-image-1858" title="spring_security" src="http://blog.novoj.net/binary/2012/03/spring_security_extjs_login-e1332024054704.png" alt="" width="149" height="58" /> <a href="http://static.springsource.org/spring-security/site/" target="_blank">Spring security</a> is really powerful library in its current version and I like it much. You can secure your application on method level several years now (this feature was introduced by <a href="http://www.nofluffjuststuff.com/blog/craig_walls/2008/04/method_level_security_in_spring_security_2_0" target="_blank">Spring Security 2 in 4/2008</a>) but we've upgraded from old Acegi Security only recently. When using method access control in larger scale I started to think about security rules encapsulation into standalone annotation definitions. It's something you can live without but in my opinion it could help readibility and maintainability of the code. Let's present some options we have now ...</p>
<p><a id="more"></a><a id="more-1857"></a></p>
<h2>Problem decomposition - how to organize our rules?</h2>
<h3>Have no system at all</h3>
<p>This is usually the first approach one can take after reading documentation of Spring Security framework and start to use it in own code. All rules are represented by Strings of <a href="http://static.springsource.org/spring/docs/3.0.5.RELEASE/reference/expressions.html" target="_blank">SpEL</a> as follows:</p>
<p>[source lang="java"]<br />
@PreAuthorize(&quot;principal.userObject.administrator&quot;)<br />
public void approveOrganization(Organization organization) {<br />
   //... content ...<br />
}</p>
<p>@PreAuthorize(&quot;principal.userObject.isOwnerOf(#organization.id)<br />
               or principal.userObject.administrator&quot;)<br />
public void updateOrganization(Organization organization) {<br />
   //... content ...<br />
}</p>
<p>@PreAuthorize(&quot;(branch.isPartOf(organization) and principal.userObject.isManagerOf(#branch.id))<br />
                or principal.userObject.isOwnerOf(#organization.id)<br />
                or principal.userObject.administrator&quot;)<br />
public void updateOrganizationBranch(Organization organization, Branch branch) {<br />
   //... content ...<br />
}</p>
<p>//and more ... example was shortened<br />
[/source]</p>
<p>After a while you might notice that certain rules keep repeating. You can see these rules repeat in our example class:</p>
<p>[source lang="java"]<br />
principal.userObject.administrator<br />
// means administrator with super rights is logged in<br />
principal.userObject.isOwnerOf(#organization.id)<br />
// means user that is owner of particular organization<br />
//(has super rights related to his organization) is logged in<br />
branch.isPartOf(organization) and principal.userObject.isManagerOf(#branch.id)<br />
// means user that is manager of particular branch<br />
// (has rights for operations connected with his branch) is logged in<br />
[/source]</p>
<p>As we all know Strings are evil - you can't refactor them safely and they tend to break your code much more often. So after a while you start to ...</p>
<h3>Extract rules into constants</h3>
<p>So the code starts to look like this:</p>
<p>[source lang="java"]<br />
private static final String ALLOWED_FOR_ADMINISTRATOR = &quot;principal.userObject.administrator&quot;;<br />
private static final String ALLOWED_FOR_OWNER = &quot;principal.userObject.isOwnerOf(#organization.id)&quot;;<br />
private static final String ALLOWED_FOR_BRANCH_MANAGER = &quot;(branch.isPartOf(organization) and principal.userObject.isManagerOf(#branch.id))&quot;;</p>
<p>@PreAuthorize(ALLOWED_FOR_ADMINISTRATOR)<br />
public void approveOrganization(Organization organization) {<br />
   //... content ...<br />
}</p>
<p>@PreAuthorize(ALLOWED_FOR_OWNER + &quot; or &quot; + ALLOWED_FOR_ADMINISTRATOR)<br />
public void updateOrganization(Organization organization) {<br />
   //... content ...<br />
}</p>
<p>@PreAuthorize(ALLOWED_FOR_OWNER + &quot; or &quot; +<br />
              ALLOWED_FOR_ADMINISTRATOR + &quot; or &quot; +<br />
			  ALLOWED_FOR_BRANCH_MANAGER)<br />
public void updateOrganizationBranch(Organization organization, Branch branch) {<br />
   //... content ...<br />
}</p>
<p>//and more<br />
[/source]</p>
<p>Or you could create central shared repository of security rules to keep them in single place to have some control over them:</p>
<p>[source lang="java"]<br />
public abstract class SecurityRules {<br />
   public static final String ALLOWED_FOR_ADMINISTRATOR = &quot;principal.userObject.administrator&quot;;<br />
   public static final String ALLOWED_FOR_OWNER = &quot;principal.userObject.isOwnerOf(#organization.id)&quot;;<br />
   public static final String ALLOWED_FOR_BRANCH_MANAGER = &quot;(branch.isPartOf(organization) and<br />
                                                    principal.userObject.isManagerOf(#branch.id))&quot;;<br />
}<br />
[/source]</p>
<p>Bad things happen when you'd like to share some rules across different libraries. For example we have a legacy system using its own security solution for accessing backend administration. SuperAdministrators are authenticated by this legacy system and have supervisor rights in most of our simple applications - so when such admin is authenticated all Spring Security rules should be overriden and all methods should become accessible for such user. But how to share this common rule across different customer installations? I can make up only single solution possible with standard Spring Security behaviour:</p>
<p>[source lang="java"]<br />
@PreAuthorize(SharedSecurityRules.ALLOWED_FOR_SUPERVISOR + &quot; or &quot; +<br />
              SecurityRules.ALLOWED_FOR_ADMINISTRATOR)<br />
public void approveOrganization(Organization organization) {<br />
   ... content ...<br />
}</p>
<p>@PreAuthorize(SharedSecurityRules.ALLOWED_FOR_SUPERVISOR + &quot; or &quot; +<br />
              SecurityRules.ALLOWED_FOR_OWNER + &quot; or &quot; +<br />
              SecurityRules.ALLOWED_FOR_ADMINISTRATOR)<br />
public void updateOrganization(Organization organization) {<br />
   ... content ...<br />
}</p>
<p>@PreAuthorize(SharedSecurityRules.ALLOWED_FOR_SUPERVISOR + &quot; or &quot; +<br />
              SecurityRules.ALLOWED_FOR_OWNER + &quot; or &quot; +<br />
              SecurityRules.ALLOWED_FOR_ADMINISTRATOR + &quot; or &quot; +<br />
              SecurityRules.ALLOWED_FOR_BRANCH_MANAGER)<br />
public void updateOrganizationBranch(Organization organization, Branch branch) {<br />
   ... content ...<br />
}<br />
[/source]</p>
<p>And I don't see this kind of notation much more readable than our first attempt with raw SpEL strings. What could be done with this?</p>
<h3>Extract rules into custom annotations</h3>
<p>You can extract your rules into custom annotations and Spring would find them. If you look at AnnotationUtils class you would realize that Spring tries to find annotation not only on method itself but also on annotations of this method. So you can have following custom annotation:</p>
<p>[source lang="java"]<br />
@Target({ElementType.METHOD, ElementType.TYPE})<br />
@Retention(RetentionPolicy.RUNTIME)<br />
@Inherited<br />
@Documented<br />
@PreAuthorize(AllowedForOrganizationOwner.IS_ORGANIZATION_OWNER)<br />
public @interface AllowedForOrganizationOwner {<br />
    String IS_ORGANIZATION_OWNER = &quot;principal.userObject.isOwnerOf(#organization.id)&quot;;<br />
}<br />
[/source]</p>
<p><strong>But there is ONE BIG "BUT"</strong></p>
<p>You can't mix multiple annotations together - Spring will find only the first applicable annotation and uses this one. So we get no further. This solution seems unusable at the first glance. </p>
<p>Wouldn't it be great if we could define something like this?:</p>
<p>[source lang="java"]<br />
@AllowedForAdministrator<br />
public class MyManager {</p>
<p>   public void approveOrganization(Organization organization) {<br />
      ... content ...<br />
   }</p>
<p>   @AllowedForOrganizationOwner<br />
   public void updateOrganization(Organization organization) {<br />
      ... content ...<br />
   }</p>
<p>   @AllowedForOrganizationOwner<br />
   @AllowedForBranchManager<br />
   public void updateOrganizationBranch(Organization organization, Branch branch) {<br />
      ... content ...<br />
   }</p>
<p>}<br />
[/source]</p>
<p>Do you like it? Does it seem more readable for you?</p>
<p>If so read on - there is a way how to achieve this ...</p>
<h2>Compositing security annotations</h2>
<p>Let's define following composition system:</p>
<ul>
<li>if there are multiple security annotation placed on the same place (ie. method or class) they represent disjunction (ie. logical OR) ... but we might have a way how to change composition behavior to logical AND if necessary</li>
<li>rules placed on class level combine with method rules always by logical OR - if class defined rules say access allowed they should override possible access denied vote from the rules placed on method</li>
</ul>
<p>Let's have some examples:<br />
[source lang="java"]<br />
@AllowedForAdministrator<br />
public class MyManager {</p>
<p>   public void approveOrganization(Organization organization) {<br />
      //has no method annotation - class annotation will be used instead<br />
   }</p>
<p>   @AllowedForOrganizationOwner<br />
   public void updateOrganization(Organization organization) {<br />
      //method and class annotations are combined with OR relation<br />
   }</p>
<p>   @AllowedForOrganizationOwner<br />
   @AllowedForBranchManager<br />
   public void updateOrganizationBranch(Organization organization, Branch branch) {<br />
      //method annotations are combined by default with OR relation<br />
      //result it then combined with class annotation with OR relation<br />
      //results in administrator or organization owner or branch manager<br />
   }</p>
<p>   @AllowedForAnyone<br />
   public Organization getOrganizationById(Integer id) {<br />
      //we want to let this method to by called by anyone but if we would<br />
      //not annotate it at all class annotation will deny execution to all<br />
      //but the administrator - so we need to add following annotation:<br />
      //AllowedForAnyone =&gt; @PreAuthorize(&quot;true&quot;)<br />
   }</p>
<p>   @RulesRelation(BooleanOperation.AND)<br />
   @IsAuthenticatedFully<br />
   @AllowedForOrganizationOwner<br />
   public void removeOrganizationById(Integer id) {<br />
      //when we want to change relationship to require all rules to be satisfied<br />
      //we have to use special annotation @RulesRelation changing default relationship among rules<br />
      //execution of this method requires user to be manually logged in in current session<br />
      //and to represent an organization owner, of course administrator could call this<br />
      //method too because class annotations are always added with OR relation<br />
   }</p>
<p>}<br />
[/source]</p>
<h2>Tweaking the Spring Security</h2>
<p>If you integrate Spring Security into your project you'd probably use the shortcut way represented by <a href="http://static.springsource.org/spring-security/site/docs/3.0.x/reference/ns-config.html#ns-method-security" target="_blank">security namespace</a>. Unfortunatelly interface that needs to be overriden is was not exposed by this namespace and is somehow supported by the most recent version 3.1 somehow (see <a href="https://jira.springsource.org/browse/SEC-1383" target="_blank">issue SEC-1383</a>). But I wasn't able to make it running and was forced to initialize method security in the old way as a set of aspects:</p>
<p>[source lang="xml"]<br />
&lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?&gt;<br />
&lt;beans xmlns=&quot;http://www.springframework.org/schema/beans&quot;<br />
       xmlns:xsi=&quot;http://www.w3.org/2001/XMLSchema-instance&quot; xmlns:aop=&quot;http://www.springframework.org/schema/aop&quot;<br />
       xsi:schemaLocation=&quot;http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.0.xsd<br />
                           http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-3.0.xsd&quot;&gt;</p>
<p>    &lt;aop:config proxy-target-class=&quot;true&quot;&gt;<br />
        &lt;aop:advisor advice-ref=&quot;experimentalMethodSecurityInterceptor&quot;<br />
                     pointcut=&quot;execution(@(@org.springframework.security.access.prepost.PreAuthorize *) * *.* (..))&quot;/&gt;<br />
        &lt;aop:advisor advice-ref=&quot;experimentalMethodSecurityInterceptor&quot;<br />
                     pointcut=&quot;execution(@(@org.springframework.security.access.prepost.PreFilter *) * *.* (..))&quot;/&gt;<br />
        &lt;aop:advisor advice-ref=&quot;experimentalMethodSecurityInterceptor&quot;<br />
                     pointcut=&quot;execution(@(@org.springframework.security.access.prepost.PostAuthorize *) * *.* (..))&quot;/&gt;<br />
        &lt;aop:advisor advice-ref=&quot;experimentalMethodSecurityInterceptor&quot;<br />
                     pointcut=&quot;execution(@(@org.springframework.security.access.prepost.PostFilter *) * *.* (..))&quot;/&gt;<br />
    &lt;/aop:config&gt;</p>
<p>    &lt;!-- Configure custom security interceptor --&gt;<br />
    &lt;bean id=&quot;experimentalMethodSecurityInterceptor&quot;<br />
          class=&quot;org.springframework.security.access.intercept.aopalliance.MethodSecurityInterceptor&quot;&gt;<br />
        &lt;property name=&quot;securityMetadataSource&quot;&gt;<br />
            &lt;bean class=&quot;cz.novoj.spring.security.aop.ExperimentalPrePostAnnotationSecurityMetadataSource&quot;&gt;<br />
                &lt;constructor-arg&gt;<br />
                    &lt;bean class=&quot;org.springframework.security.access.expression.method.ExpressionBasedAnnotationAttributeFactory&quot;&gt;<br />
                        &lt;constructor-arg ref=&quot;expressionHandler&quot;/&gt;<br />
                    &lt;/bean&gt;<br />
                &lt;/constructor-arg&gt;<br />
            &lt;/bean&gt;<br />
        &lt;/property&gt;<br />
        &lt;property name=&quot;authenticationManager&quot; ref=&quot;authenticationManager&quot;/&gt;<br />
        &lt;property name=&quot;validateConfigAttributes&quot; value=&quot;false&quot;/&gt;<br />
        &lt;property name=&quot;accessDecisionManager&quot;&gt;<br />
            &lt;bean class=&quot;org.springframework.security.access.vote.AffirmativeBased&quot;&gt;<br />
                &lt;constructor-arg&gt;<br />
                    &lt;list&gt;<br />
                        &lt;bean class=&quot;org.springframework.security.access.prepost.PreInvocationAuthorizationAdviceVoter&quot;&gt;<br />
                            &lt;constructor-arg&gt;<br />
                                &lt;bean class=&quot;org.springframework.security.access.expression.method.ExpressionBasedPreInvocationAdvice&quot;&gt;<br />
                                    &lt;property name=&quot;expressionHandler&quot; ref=&quot;expressionHandler&quot;/&gt;<br />
                                &lt;/bean&gt;<br />
                            &lt;/constructor-arg&gt;<br />
                        &lt;/bean&gt;<br />
                    &lt;/list&gt;<br />
                &lt;/constructor-arg&gt;<br />
            &lt;/bean&gt;<br />
        &lt;/property&gt;<br />
    &lt;/bean&gt;</p>
<p>    &lt;bean id=&quot;expressionHandler&quot;<br />
          class=&quot;org.springframework.security.access.expression.method.DefaultMethodSecurityExpressionHandler&quot;/&gt;</p>
<p>&lt;/beans&gt;<br />
[/source]</p>
<p><em><strong>Note:</strong>you need to declare AspectJ pointcuts as follows if you want to find not only methods annotated directly with certain annotation type but also methods annotated with annotations annotated with such annotation type:</em></p>
<p>[source lang="xml"]<br />
execution(@(@org.springframework.security.access.prepost.PreAuthorize *) * *.* (..))<br />
[/source]</p>
<p>As you can see - all classes except one are taken from Spring codebase. The single exception is class <b>ExperimentalPrePostAnnotationSecurityMetadataSource</b> that is meant to be used instead of original <b>PrePostAnnotationSecurityMetadataSource</b> that looks up for annotations of @PreAuthorize, @PreFilter, @PostAuthorize and @PostFilter. My experimental version finds all annotations that represents above mentioned security annotations or are annotated with them. It retrieves all SPeL security rules that these annotations contain and combine them into a single one in context initialization time. Principles of the rules combinations are stated in the beginning of the previous chapter.</p>
<p>Source code of all used extension classes are available in form of GIST (implementation details are not so important for this article as the main idea is): <a href="https://gist.github.com/2081353">https://gist.github.com/2081353</a></p>
<p>If you find this idea useful - please vote or comment Spring Security issue I've created for this idea: <a href="https://jira.springsource.org/browse/SEC-1945" target="_blank"><b>Spring Security issue documenting this idea</b></a></p>
