---
status: publish
published: true
title: How do YOU test access control of your application?
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft  wp-image-2071\" title=\"Security testing\" src=\"http://blog.novoj.net/binary/2012/06/Security-Testing-300x225.jpg\"
  alt=\"\" width=\"168\" height=\"126\" /> Many of complex applications put on top
  of their complexity access control logic for securing data and to limit access to
  certain functions. No matter if you have fully configurable ACL settings based on
  rights or role based access you'd probably want to test this part of application
  too. In order to have proper test coverage you should make it easy for you and your
  colleagues to test this. I have no doubts that if you ever needed to test this you
  already have some kind of such test support, but this article describes what kind
  of it I've created for myself. It might be interesting for you to compare it with
  your solution or inspire you to create one if you haven't done it already.\r\n\r\n"
wordpress_id: 2069
wordpress_url: http://blog.novoj.net/?p=2069
date: '2012-06-14 23:10:59 +0200'
date_gmt: '2012-06-14 22:10:59 +0200'
categories:
- Programování
- Java
- Testování
- Bezpečnost
- English
tags: []
comments:
- id: 73834
  author: dkl
  author_email: daniel@kolman.cz
  author_url: http://blog.kolman.cz/
  date: '2012-06-15 07:27:56 +0200'
  date_gmt: '2012-06-15 06:27:56 +0200'
  content: 'Just a comment: You are setting access rights per role, but test users.
    IMHO it would be better to test roles. I mean that if your method has attribute
    @AllowedForAdministrator, I would expect to see something like this in the test:
    @RunAsRole(UserRoles.ADMINISTRATOR). Let the test runner figure out which user
    it needs to run the test.'
- id: 73842
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-06-15 09:07:18 +0200'
  date_gmt: '2012-06-15 08:07:18 +0200'
  content: Yes, you're right. I usually have test user accounts named appropriatelly
    that represent those roles. So I use such accounts - but you are right it could
    be based directly on roles and it might make it a little more understandable.
- id: 73901
  author: banter
  author_email: lubos.racansky@gmail.com
  author_url: http://blog.zvestov.cz
  date: '2012-06-15 12:32:17 +0200'
  date_gmt: '2012-06-15 11:32:17 +0200'
  content: Thanks, the test listeners are pretty good concept, but I have never use
    them yet. I will keep them in mind.
- id: 73957
  author: Marian Schubert
  author_email: marian.schubert@gmail.com
  author_url: http://blog.think-forth.com/
  date: '2012-06-15 22:09:02 +0200'
  date_gmt: '2012-06-15 21:09:02 +0200'
  content: Had I nice annotations which you mention in your post I would consider
    not to write integration tests like these at all (assuming that each annotation
    is tested on its own) as they would not help me write production code or prevent
    future bugs. Only way to introduce bug is to miss to add annotation or delete
    one that's already there - which is unlikely.
- id: 74398
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-06-17 22:57:36 +0200'
  date_gmt: '2012-06-17 21:57:36 +0200'
  content: "Yes, I don't write so thorought tests for all secured methods - I thoroughly
    test all variants only once or twice per annotation type. Behind annotations there
    is string SpEL expression that needs to be tested (for example: principal.userObject.isOwnerOf(#organization.id)
    ... more here http://blog.novoj.net/2012/03/27/combining-custom-annotations-for-securing-methods-with-spring-security/)
    - and because of that I have like 10 - 15 annotation types which I test by the
    way described in this post.\r\n\r\nSo I think we are on the same page here."
- id: 77654
  author: Tomek Kaczanowski
  author_email: tkaczano@poczta.onet.pl
  author_url: http://practicalunittesting.com
  date: '2012-07-02 10:34:13 +0200'
  date_gmt: '2012-07-02 09:34:13 +0200'
  content: Thanks for this very interesting post. Nice idea of using a custom TestExecutionListener!
- id: 148465
  author: "&raquo; Šestý rok Myšlenek dne otce Fura Myšlenky dne otce Fura"
  author_email: ''
  author_url: http://blog.novoj.net/2013/01/01/sesty-rok-myslenek-dne-otce-fura/
  date: '2013-01-01 00:01:55 +0100'
  date_gmt: '2012-12-31 23:01:55 +0100'
  content: "[...] Po většinu tohoto roku jsem se věnoval vývoji bonusového systému
    s využitím NFC karet pro slovenskou společnost DOXX. Možnosti NFC technologie
    jsou velmi zajímavé a myslím, že nás do budoucna čeká ještě hodně velký rozmach
    v této oblasti. Pro mě byl tento projekt velkým posunem vpřed především díky poměrně
    masivnímu nasazení Spring Security, o kterém jsem psal i několik článků. [...]"
---
<p><img class="alignleft  wp-image-2071" title="Security testing" src="http://blog.novoj.net/binary/2012/06/Security-Testing-300x225.jpg" alt="" width="168" height="126" /> Many of complex applications put on top of their complexity access control logic for securing data and to limit access to certain functions. No matter if you have fully configurable ACL settings based on rights or role based access you'd probably want to test this part of application too. In order to have proper test coverage you should make it easy for you and your colleagues to test this. I have no doubts that if you ever needed to test this you already have some kind of such test support, but this article describes what kind of it I've created for myself. It might be interesting for you to compare it with your solution or inspire you to create one if you haven't done it already.</p>
<p><a id="more"></a><a id="more-2069"></a>Let's state some starting points. We use <a href="http://static.springsource.org/spring/docs/2.5.x/reference/testing.html" target="_blank">Spring Framework test framework</a> in combination with <a href="http://www.junit.org/" target="_blank">JUnit 4</a> and <a href="http://static.springsource.org/spring-security/site/docs/3.0.x/reference/el-access.html" target="_blank">Spring Security method level EL based security rules</a>. Our business methods look like this:</p>
<p>[source lang="java"]<br />
@AllowedForAdministrator<br />
@AllowedForTerminalOrganizationOwner<br />
@DeniedForMerchant<br />
public void blockTerminal(Terminal terminal) {<br />
   //business logic<br />
}<br />
[/source]</p>
<p><em><strong>Note:</strong> If you wonder what @Allowed* annotations mean you might want to read another my article <a href="http://blog.novoj.net/2012/03/27/combining-custom-annotations-for-securing-methods-with-spring-security/">Custom annotations for Spring Security</a> - but in short you can imagine them as multiple <a href="http://static.springsource.org/spring-security/site/docs/3.0.x/reference/el-access.html#el-pre-post-annotations" target="_blank">@PreAuthorize</a> annotations with some SpEL in them.</em></p>
<p>In order to test upper mentioned method properly you should test at least following scenarios:</p>
<ul>
<li>call method as administrator - should be allowed</li>
<li>call method as organization owner - should be allowed</li>
<li>call method as merchant - should throw AccessDeniedException</li>
<li>call method as unauthorized user - should throw AccessDeniedException</li>
</ul>
<p>You need to login proper user before test run and log him out on tear down. This could look very ugly because for each of such test you need different user to be logged in so you cannot take advantage of @Before or @BeforeClass annotations.</p>
<h2>Extend your test execution lifecycle</h2>
<p>In Spring test support you can use so called <a href="http://static.springsource.org/spring/docs/3.0.x/javadoc-api/org/springframework/test/context/TestExecutionListener.html" target="_blank">TestExecutionListener</a> that will be called by framework before / after executing each of the test method. Each callback you can override has access to the <a href="http://static.springsource.org/spring/docs/3.0.x/javadoc-api/org/springframework/test/context/TestContext.html" target="_blank">TestContext</a> object with reference to the reflection object of the test method and other useful things. Having known that, we could create our own listener that would examine annotations on test method and will take care of logging in a new user and safely cleaning after the test. See example of the test:</p>
<p>[source lang="java"]<br />
@Test<br />
@RunAsUser(&quot;owner@fg.cz&quot;)<br />
public void shouldBlockTerminalAsOrganizationOwner() throws Exception {<br />
   Terminal terminal = terminalManager.getTerminalById(100);<br />
   assertNull(terminal.getDateBlocked());</p>
<p>   terminalManager.blockTerminal(terminal);<br />
   terminal = terminalManager.getTerminalById(100);<br />
   assertNotNull(terminal.getDateBlocked());<br />
}</p>
<p>@Test<br />
@RunAsUser(&quot;administrator@fg.cz&quot;)<br />
public void shouldBlockTerminalAsAdministrator() throws Exception {<br />
   Terminal terminal = terminalManager.getTerminalById(100);<br />
   terminalManager.blockTerminal(terminal);<br />
}</p>
<p>@Test(expected = AccessDeniedException.class)<br />
@RunAsUser(&quot;merchant@fg.cz&quot;)<br />
public void shouldFailToBlockTerminalAsMerchant() throws Exception {<br />
   Terminal terminal = terminalManager.getTerminalById(100);<br />
   terminalManager.blockTerminal(terminal);<br />
}</p>
<p>@Test(expected = AccessDeniedException.class)<br />
public void shouldFailToBlockTerminalAsUnauthorized() throws Exception {<br />
   Terminal terminal = terminalManager.getTerminalById(100);<br />
   terminalManager.blockTerminal(terminal);<br />
}<br />
[/source]</p>
<p>Now you got the point - as you can see testing access rights in such way is really easy so you can provide sufficient security coverage. I've tried this approach on a year long project consisting of 60k+ lines of code and have had really great experience with it. Now how you to achieve this test behaviour:</p>
<h3>Define custom annotation ...</h3>
<p>... that you'd place on test methods and would mark them to be enveloped by the "logging in" logic:</p>
<p>[source lang="java"]<br />
/**<br />
 * Allows to run test in the context of logged in frontend user.<br />
 */<br />
@Target({ElementType.METHOD})<br />
@Retention(RetentionPolicy.RUNTIME)<br />
@Documented<br />
public @interface RunAsUser {<br />
   /**<br />
     * Method returns login of logged in user.<br />
     * @return<br />
     */<br />
    String value();<br />
}<br />
[/source]</p>
<h3>Write custom TestExecutionListener ...</h3>
<p>... that would process aforementioned annotation. You'd probably want to extend existing AbstractTestExecutionListener that allows you to implement only those callback you really want to override.</p>
<p>[source lang="java"]<br />
/**<br />
 * Supports annotations {@link RunAsUser}.<br />
 */<br />
public class RunAsSupportTestExecutionListener extends AbstractTestExecutionListener {<br />
    private static final ThreadLocal&lt;Authentication&gt; savedAuthentication = new ThreadLocal&lt;Authentication&gt;();<br />
    private static final ThreadLocal&lt;User&gt; savedAdmin = new ThreadLocal&lt;User&gt;();</p>
<p>    @Override<br />
    public void beforeTestMethod(TestContext testContext) throws Exception {<br />
        super.beforeTestMethod(testContext);<br />
        final RunAsUser runAsUser = testContext.getTestMethod()<br />
                                      .getAnnotation(RunAsUser.class);<br />
        if (runAsUser != null) {<br />
            final String userName = runAsUser.value();<br />
            loginAsUser(<br />
               userName, testContext.getApplicationContext()<br />
            );<br />
        }<br />
    }</p>
<p>    @Override<br />
    public void afterTestMethod(TestContext testContext) throws Exception {<br />
        super.afterTestMethod(testContext);<br />
        final RunAsUser runAsUser = testContext.getTestMethod()<br />
                                     .getAnnotation(RunAsUser.class);<br />
        if (runAsUser != null) {<br />
            logoutUser();<br />
        }<br />
    }</p>
<p>    public static void loginAsUser(String userName, ApplicationContext appCtx) {<br />
        UserDetailsService userDetailsService = getDaoAuthenticationProvider(appCtx);<br />
        final UserDetails userDetails = userDetailsService.loadUserByUsername(userName);<br />
        SecurityContextHolder.getContext().setAuthentication(<br />
            new UsernamePasswordAuthenticationToken(<br />
                userDetails, userDetails.getPassword(),<br />
                new ArrayList&lt;GrantedAuthority&gt;(<br />
                    userDetails.getAuthorities()<br />
                )<br />
            )<br />
        );<br />
    }</p>
<p>    private static void logoutUser() {<br />
        SecurityContextHolder.getContext().setAuthentication(null);<br />
    }</p>
<p>    private static UserDetailsService getDaoAuthenticationProvider(ApplicationContext appCtx) {<br />
        UserDetailsService userDetailsService;<br />
        final Map&lt;String,UserDetailsService&gt; userDetailsServiceIndex = appCtx.getBeansOfType(<br />
            UserDetailsService.class<br />
        );<br />
        if (userDetailsServiceIndex.size() == 1) {<br />
            userDetailsService = userDetailsServiceIndex.values()<br />
                                      .iterator().next();<br />
        } else {<br />
            throw new IllegalStateException(<br />
                &quot;Cannot determine user detail service - there is &quot; +<br />
                userDetailsServiceIndex.size()<br />
                + &quot; beans of class UserDetailsService!&quot;<br />
            );<br />
        }<br />
        return userDetailsService;<br />
    }</p>
<p>}<br />
[/source]</p>
<h3>Initialize Test (or better TestAncestor) class with listener ...</h3>
<p>... to setup your test class to use newly created test execution listener. You probably already have some test class ancestor - so this is the best place to place this:</p>
<p>[source lang="java"]<br />
@ContextConfiguration(<br />
   locations = {<br />
      &quot;classpath:/META-INF/spring/some-spring-config.xml&quot;,<br />
      ... and others ...<br />
   }<br />
)<br />
@TestExecutionListeners( {<br />
   DependencyInjectionTestExecutionListener.class,<br />
   DirtiesContextTestExecutionListener.class,<br />
   RunAsSupportTestExecutionListener.class<br />
})<br />
public abstract class AbstractTest {<br />
   //whatever<br />
}<br />
[/source]</p>
<h3>Finally</h3>
<p>Do you like it? Give it +1! I hope it will ease your life when testing access rights - it worked for me it might work for you also. Happy coding!</p>
