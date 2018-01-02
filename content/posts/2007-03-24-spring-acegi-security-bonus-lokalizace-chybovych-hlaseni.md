---
status: publish
published: true
title: Spring Acegi Security (bonus  - lokalizace chybových hlášení)
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "V poslední době jsem řešil problematiku zabezpečení webových projektů spolu
  se správou uživatelů a oprávnění. Původně se zdálo, že neexistuje open-source projekt,
  který by pokrýval naše potřeby. Po čase jsem však narazil na Acegi Security projekt,
  který je určený přímo pro Spring. Ještě před třemi dny jsem měl úplně jiné představy
  o tom, co Acegi řeší - myslel jsem, že to je jen sada providerů pro napojení na
  externí zdroje dat o uživatelích (LDAP, Active Directory a pod.). To jsem se ovšem
  hluboce mýlil.\r\n\r\n"
wordpress_id: 12
wordpress_url: http://blog.novoj.net/2007/03/24/spring-acegi-security-bonus-lokalizace-chybovych-hlaseni/
date: '2007-03-24 16:19:57 +0100'
date_gmt: '2007-03-24 15:19:57 +0100'
categories:
- Java
tags: []
comments: []
---
<p>V poslední době jsem řešil problematiku zabezpečení webových projektů spolu se správou uživatelů a oprávnění. Původně se zdálo, že neexistuje open-source projekt, který by pokrýval naše potřeby. Po čase jsem však narazil na Acegi Security projekt, který je určený přímo pro Spring. Ještě před třemi dny jsem měl úplně jiné představy o tom, co Acegi řeší - myslel jsem, že to je jen sada providerů pro napojení na externí zdroje dat o uživatelích (LDAP, Active Directory a pod.). To jsem se ovšem hluboce mýlil.</p>
<p><a id="more"></a><a id="more-12"></a></p>
<p>Acegi pokrývá v podstatě veškeré aspekty, které je nutné řešit v souvislosti se zabezpečením webových aplikací a jde ještě mnohem dál (není fixně vázaný jen na web oriented aplikace a neřeší pouze přihlašování, ale umí i vyhodnocovat oprávnění). Nenarazil jsem na mnoho míst, které by bylo potřeba nějak rozšiřovat - v podstatě většina toho, co člověk potřebuje tam už je k dispozici. Jedinou hlavní částí, kterou je potřeba si obvykle implementovat je DAO nad databází uživatelů a oprávnění (typicky potřebujete CRUD operace nad databází uživatelů, které Acegi neimplementuje - logicky toto jde mimo její zájmy a také typicky potřebujete k uživatelům rozdílné údaje a někdy i vlastní workflow).</p>
<p>Navíc mě opravdu překvapila "návrhová čistota" kódu, ze kterého se Acegi skládá. Brouzdáním po třídách a porozumění jejich kódu jsem se opravdu mnoho naučil. Doporučuji všem, kdo řeší podobné problémy jako já, kouknout se právě na tuto knihovnu.</p>
<p><strong>Slíbený bonus článku:</strong></p>
<p><a title="Lokalizace chybových hlášení Acegi je ke stažení zde." href="http://files.novoj.net/Acegi/messages_cs_CZ.properties">Lokalizace chybových hlášení Acegi je ke stažení zde.</a></p>
<p>Do aplikace se jednoduše lokalizace zavede vložením následující deklarace do <em>applicationContext.xml</em> (nebo do jiného Spring konfiguráku).</p>
<p>[source lang="xml"]<br />
   <bean id="messageSource" class="org.springframework.context.support.ReloadableResourceBundleMessageSource"></p>
<property name="basename" value="classpath:cesta/na/classpath/k/souboru"/>
   </bean><br />
[/source]</p>
<p>Ještě je dobré dát si pozor, aby bylo v <em>LocaleContextHolder</em>, nastaveno správné locale. Tato třída ukládá informace o aktuálním locale v ThreadLocal proměnné a je tedy platná pouze pro aktuální vlákno (a také je vhodné ji před odevzdáním vlákna do poolu čistit). Pokud nepoužíváte zároveň Spring MVC, musíte si toto implementovat sami.</p>
<p>Já jsem vyřešil nastavování locale následujícím filtrem (který jsem přidal do řetězce filtrů v <em>FilterChainProxy</em>:</p>
<p>[source lang="java"]<br />
/**<br />
 * Sets locale according to locale supplied in request.<br />
 */<br />
public class RequestLocaleFilter extends OncePerRequestFilter implements Filter {</p>
<p>	/**<br />
	 * Same contract as for doFilter, but guaranteed to be just invoked once per<br />
	 * request. Provides HttpServletRequest and HttpServletResponse arguments<br />
	 * instead of the default ServletRequest and ServletResponse ones.<br />
	 */<br />
	protected void doFilterInternal(<br />
                HttpServletRequest request, HttpServletResponse response, FilterChain filterChain)<br />
                throws ServletException, IOException {<br />
		try {<br />
			LocaleContextHolder.setLocale(request.getLocale());<br />
			doFilter(request, response, filterChain);<br />
		} finally {<br />
			LocaleContextHolder.resetLocaleContext();<br />
		}<br />
	}<br />
}<br />
[/source]</p>
