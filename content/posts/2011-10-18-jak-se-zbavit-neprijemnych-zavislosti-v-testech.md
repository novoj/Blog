---
status: publish
published: true
title: Jak se zbavit nepříjemných závislostí v testech
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img src=\"http://blog.novoj.net/binary/2011/10/mockito-300x139.jpg\" alt=\"\"
  title=\"Mockito\" width=\"150\" height=\"69\" class=\"alignleft size-medium wp-image-1662\"
  /> Dnešní příspěvek bude velmi krátký. Je dost pravděpodobné, že podobné řešení
  už dávno máte ve svých tetovacích utilitkách, ale mě tato kombinace napadla relativně
  nedávno a jsem nadšený z toho, o jak elegantní řešení se pro testy jedná.\r\n\r\nV
  některých testech potřebuji vytvořit část Spring aplikačního kontextu, jehož některé
  beany mají závislost na nějaké další beaně, kterou je pro mne obtížné do testu zahrnout.
  Buď z důvodu, že její samotné vytvoření s vyžaduje další komplexní infrastrukturu
  okolo ní nebo třeba proto, že její zařazení do testovacího kontextu způsobuje při
  běhu testu vedlejší efekty (např. odeslání e-mailu).\r\n\r\n"
wordpress_id: 1661
wordpress_url: http://blog.novoj.net/?p=1661
date: '2011-10-18 01:00:44 +0200'
date_gmt: '2011-10-18 00:00:44 +0200'
categories:
- Programování
- Java
- Testování
- Spring Framework
tags: []
comments:
- id: 52862
  author: Lukas
  author_email: Lukas.Rypl@atlas.cz
  author_url: http://twitter.com/#!/LukasRypl
  date: '2011-10-18 08:53:20 +0200'
  date_gmt: '2011-10-18 07:53:20 +0200'
  content: "K unit testingu a mockum jsem v posledni dobe narazil na dva dobre pluginy
    do eclipse\r\n1. eclemma  pro test coverage http://www.eclemma.org/installation.html\r\n2.
    MoreUnit ulehcuje generovani testu a nabizi i generovani skeletonu pro Mockito
    a EasyMock http://moreunit.sourceforge.net/"
- id: 53861
  author: Arnost
  author_email: arnost.valicek@gmail.com
  author_url: ''
  date: '2011-11-02 11:12:26 +0100'
  date_gmt: '2011-11-02 10:12:26 +0100'
  content: "Myslim zo do kodu by bylo dobre doplnit co dela metoda mock pouzivat v
    getObject.\r\n\r\nPredpokladam ze metoda je staticky importovana z org.mockito.Mockito...\r\n\r\n\r\n
    \   public Object getObject() throws Exception {  \r\n        return mock(mockClass);
    \ \r\n    }"
- id: 53871
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-11-02 14:42:24 +0100'
  date_gmt: '2011-11-02 13:42:24 +0100'
  content: Ano je to tak ... kvůli přehlednosti jsem odebral importy a tím jsem to
    naopak znesrozumitelnil. Omlouvám se, situaci napravím.
- id: 58271
  author: "&raquo; Pátý rok Myšlenek Otce Fura Myšlenky dne otce Fura"
  author_email: ''
  author_url: http://blog.novoj.net/2012/01/01/paty-rok-myslenek-otce-fura/
  date: '2012-01-01 14:43:53 +0100'
  date_gmt: '2012-01-01 13:43:53 +0100'
  content: "[...] Jak se zbavit nepříjemných závislostí v testech [...]"
- id: 78921
  author: banter
  author_email: lubos.racansky@gmail.com
  author_url: http://blog.zvestov.cz
  date: '2012-07-11 12:41:47 +0200'
  date_gmt: '2012-07-11 11:41:47 +0200'
  content: "Jsem zvyklý na EasyMock a ve srovnání s ním mi Mockito přijde nešikovné
    v tom, že se opakuje stejný kód v klauzuli when a verify.\r\n\r\nTřeba\r\n<code>\r\nMockito.when(mailService.sendMail(Mockito.anyObject())).thenReturn(Boolean.TRUE);\r\n...\r\nMockito.verify(mailService).sendMail(Mockito.anyObject());\r\n</code>\r\n\r\nbych
    napsal jako\r\n<code>\r\nEasyMock.expect(mailService.sendMail(EasyMock.anyObject())).andReturn(Boolean.TRUE);\r\n...\r\nEasyMock.verify(mailService);\r\n</code>\r\n\r\nNebo
    jsem něco pochopil špatně?"
- id: 81609
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-07-23 08:20:59 +0200'
  date_gmt: '2012-07-23 07:20:59 +0200'
  content: "Pokud by tě nezajímalo, co sendMail vrací, tak by stačilo pouze:\r\n\r\n<code>\r\nimport
    static Mockito.*;\r\nverify(mailService, times(1)).sendMail(anyObject());\r\n</code>\r\n\r\nMockito
    provádí automatickou capture všech volání aniž by bylo potřeba nějak instruovat.
    Co je docela hezké je toto:\r\n\r\n<code>\r\nimport static Mockito.*;\r\nArgumentCaptor<Person>
    argument = ArgumentCaptor.forClass(Person.class);\r\nverify(mailService, atLeastOnce()).sendMail(argument.capture());\r\nassertEquals(5,
    argument.getAllValues().size());\r\nassertEquals(\"John\", argument.getLastValue().getName());\r\n</code>\r\n\r\nAle
    zase jsem už dlouho nepoužil EasyMock, takže nemůžu srovnávat. Mockito mi přišlo
    na použití hodně příjemné. Koneckonců autoři Mockita přímo na HP píšou, že hlavní
    inspirací byl pro ně EasyMock a že v podstatě staví na základech, které položil
    on."
- id: 84271
  author: "&raquo; Springockito &#8211; výroba mocků snadno a rychle Myšlenky dne
    otce Fura"
  author_email: ''
  author_url: http://blog.novoj.net/2012/07/31/springockito-vyroba-mocku-snadno-a-rychle/
  date: '2012-07-31 21:57:43 +0200'
  date_gmt: '2012-07-31 20:57:43 +0200'
  content: "[...] Jednu z nich, která se mi zdála poměrně jednoduchá jsem popisoval
    v dřívějším článku Jak se zbavit nepříjemných závislostí v testech, nicméně tento
    přístup dotáhl Jakub Janczak o kus dál (jo na světě jsou milóny lidí [...]"
---
<p><img src="http://blog.novoj.net/binary/2011/10/mockito-300x139.jpg" alt="" title="Mockito" width="150" height="69" class="alignleft size-medium wp-image-1662" /> Dnešní příspěvek bude velmi krátký. Je dost pravděpodobné, že podobné řešení už dávno máte ve svých tetovacích utilitkách, ale mě tato kombinace napadla relativně nedávno a jsem nadšený z toho, o jak elegantní řešení se pro testy jedná.</p>
<p>V některých testech potřebuji vytvořit část Spring aplikačního kontextu, jehož některé beany mají závislost na nějaké další beaně, kterou je pro mne obtížné do testu zahrnout. Buď z důvodu, že její samotné vytvoření s vyžaduje další komplexní infrastrukturu okolo ní nebo třeba proto, že její zařazení do testovacího kontextu způsobuje při běhu testu vedlejší efekty (např. odeslání e-mailu).</p>
<p><a id="more"></a><a id="more-1661"></a></p>
<p>Pro tyto případy jsem si vytvořil jednoduchou Spring FactoryBean, která používá mockovací knihovnu <a href="http://code.google.com/p/mockito/" target="_blank">Mockito</a> a která vytvoří místo zmíněné obtížné beany, na kterou mám v kontextu závislosti, dynamickou proxy imitující její chování:</p>
<p>[source lang="java"]<br />
import org.springframework.beans.factory.FactoryBean;<br />
import static org.mockito.Mockito.mock;</p>
<p>/**<br />
 * Simple factory bean creating mock object for specified class.<br />
 * Mock object is a prototype that means it is created<br />
 * everytime Spring bean retrieval occurs. In practice it means<br />
 * that each test method has its own new and pretty mock<br />
 * object created before it starts.<br />
 */<br />
public class MockitoFactoryBean implements FactoryBean {<br />
	private Class mockClass;</p>
<p>	public void setMockClass(Class mockClass) {<br />
		this.mockClass = mockClass;<br />
	}</p>
<p>	public Object getObject() throws Exception {<br />
		return mock(mockClass);<br />
	}</p>
<p>	public Class getObjectType() {<br />
		return mockClass;<br />
	}</p>
<p>	public boolean isSingleton() {<br />
		return false;<br />
	}</p>
<p>}<br />
[/source]</p>
<p>V úplně nejjednodušším případě mi potom stačí v kontextu místo původní beany definovat beanu zástupnou - díky níž umožním naběhnutí celého kontextu aniž bych musel nějak výrazněji šachovat se Spring konfiguráky:</p>
<p>[source lang="xml"]<br />
<bean id="mailService" class="com.fg.support.test.MockitoFactoryBean"></p>
<property name="mockClass" value="cz.novoj.mail.MailService"/>
</bean><br />
[/source]</p>
<p>Druhé hezké použití tohoto přístupu je ve chvíli, kdy potřebujeme pro test nainstruovat chování konkrétní mockované beany. Díky tomu, že MockitoBeanFactory vytváří beany typu "prototype" (tj. vždy, když požádáme kontext o referenci na danou beanu, vznikne nová instance konkrétní třídy), má každá testovací metoda na začátku svou vlastní "čistou" instanci tohoto mocku, který už stačí jen naskriptovat:</p>
<p>[source lang="java"]<br />
@RunWith(SpringJUnit4ClassRunner.class)<br />
@ContextConfiguration(locations = {<br />
		"classpath:/META-INF/spring/business.xml",<br />
		"classpath:/META-INF/spring/mocks.xml"<br />
})<br />
public class BusinessObjectTest {<br />
	@Autowired private BusinessObject businessObject;<br />
	@Autowired private MailService mailService;</p>
<p>	@Test<br />
	@DirtiesContext<br />
	public void testBusinessMethod() {<br />
		Mockito.when(mailService.sendMail(Mockito.anyObject())).thenReturn(Boolean.TRUE);<br />
		businessObject.setMailService(mailService);<br />
		assertTrue(businessObject.doWork());<br />
		Mockito.verify(mailService).sendMail(Mockito.anyObject());<br />
	}</p>
<p>	@Test<br />
	@DirtiesContext<br />
	public void testBusinessMethodMailFail() {<br />
		Mockito.when(mailService.sendMail(Mockito.anyObject())).thenThrow(new MailSendException("test"));<br />
		businessObject.setMailService(mailService);<br />
		assertFalse(businessObject.doWork());<br />
	}<br />
}<br />
[/source]</p>
<p>Jak jsem psal už zkraje - není to nic zázračného, ale použití je skutečně velmi elegantní. Nechápu, že mi něco podobného nedoteklo daleko dřív. Alternativně by se dala použít ještě <a href="http://static.springsource.org/spring/docs/2.5.x/api/org/springframework/aop/framework/ProxyFactoryBean.html" target="_blank">ProxyFactoryBean</a>, jenže ta je spíš určena na hrátky s AOP než jako podpora testů. Mockito (respektive libovolná jiná mock knihovna) se pro tyto účely hodí výrazně lépe.</p>
