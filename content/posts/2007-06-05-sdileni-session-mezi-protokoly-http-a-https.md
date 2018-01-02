---
status: publish
published: true
title: Sdílení session mezi protokoly HTTP a HTTPS
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Je možné zajistit bezpečné sdílení HTTP session mezi oběma protokoly? Z
  dostupné dokumentace se dozvídáme, že nikoliv. Tento článek se zabývá možným řešením,
  které za jistých podmínek umožňuje bezpečně sdílet společnou session. Důvod proč
  se tímto problémem zabývat je jednoduchý - SSL šifrování je výpočetně nákladná věc
  (viz. např. <a target=\"_blank\" href=\"http://iweb.tntech.edu/hexb/publications/https-STAR-03122003.pdf\">Performance
  analysis of Secure HTTP Protocol</a>). Proto je možná vhodné používat HTTPS pouze
  tam, kde je k tomu důvod (tedy např. uživatel pracuje s některými důvěrnými daty).
  Jistě se shodneme na tom, že na řadě webových aplikací je takto důvěrných míst pouze
  pár a zbytek bychom mohli hnát klidně přes protokol HTTP, čímž odlehčíme svému webovému
  serveru. Jenže tady narážíme na zásadní problém - nemůžeme nechráněným protokolem
  vyzradit identifikátor session (a naopak nesmíme akceptovat session, která vznikla
  přes protokol HTTP). Má tedy tato situace řešení, nebo nemá, jak se dočteme v řadě
  publikací?\r\n\r\nKolega <strong>Martin Veska</strong> ze společnosti <a target=\"_blank\"
  title=\"FG Forrest\" href=\"http://www.fg.cz\"><strong>FG Forrest</strong></a> přišel
  s návrhem řešení, které by umožňovalo bezpečně \"vyzradit\" identifikátor session,
  aniž bychom se vystavili riziku záměny autorizovaného uživatele. Jako každé jiné
  řešení má i toto své mínus, ale o tom až později v článku.\r\n<div align=\"center\">"
wordpress_id: 18
wordpress_url: http://blog.novoj.net/2007/06/05/sdileni-session-mezi-protokoly-http-a-https/
date: '2007-06-05 20:33:14 +0200'
date_gmt: '2007-06-05 19:33:14 +0200'
categories:
- Java
- Bezpečnost
- Web
tags: []
comments: []
---
<p>Je možné zajistit bezpečné sdílení HTTP session mezi oběma protokoly? Z dostupné dokumentace se dozvídáme, že nikoliv. Tento článek se zabývá možným řešením, které za jistých podmínek umožňuje bezpečně sdílet společnou session. Důvod proč se tímto problémem zabývat je jednoduchý - SSL šifrování je výpočetně nákladná věc (viz. např. <a target="_blank" href="http://iweb.tntech.edu/hexb/publications/https-STAR-03122003.pdf">Performance analysis of Secure HTTP Protocol</a>). Proto je možná vhodné používat HTTPS pouze tam, kde je k tomu důvod (tedy např. uživatel pracuje s některými důvěrnými daty). Jistě se shodneme na tom, že na řadě webových aplikací je takto důvěrných míst pouze pár a zbytek bychom mohli hnát klidně přes protokol HTTP, čímž odlehčíme svému webovému serveru. Jenže tady narážíme na zásadní problém - nemůžeme nechráněným protokolem vyzradit identifikátor session (a naopak nesmíme akceptovat session, která vznikla přes protokol HTTP). Má tedy tato situace řešení, nebo nemá, jak se dočteme v řadě publikací?</p>
<p>Kolega <strong>Martin Veska</strong> ze společnosti <a target="_blank" title="FG Forrest" href="http://www.fg.cz"><strong>FG Forrest</strong></a> přišel s návrhem řešení, které by umožňovalo bezpečně "vyzradit" identifikátor session, aniž bychom se vystavili riziku záměny autorizovaného uživatele. Jako každé jiné řešení má i toto své mínus, ale o tom až později v článku.</p>
<div align="center"><a id="more"></a><a id="more-18"></a></div>
<p align="center">###</p>
<p>Sdílení session mezi oběma protokoly je problémová věc. Lépe řečeno - bezpečnostní díra. Typicky totiž po autentizaci uživatele nahrajete informace o něm (často i jeho oprávnění do session) a při dalším dotazu už pracujete s těmito informacemi (po prvotní autentizaci už uživateli "věříte"). Dotazy jsou mezi sebou provázány identifikátorem, který je posílaný prohlížečem uživatele (JSESSIONID), a který zajistí, že při dalším požadavku vám web server poskytne "tu jeho" serverovou session. Identifikátor je buď posílán jako cookie (obvykle) nebo v případě, že uživatel má zakázané cookies v URL.</p>
<p>Slabé místo je právě ve fázi předávání identifikátoru od uživatele na server a zpět. V případě, že tento identifikátor putuje nešifrovaným kanálem (HTTP), existuje teoretická šance, že jej může někdo odposlechnout a vydávat se za uživatele, jehož komunikaci odposlechl (prostě vám pošle stejný identifikátor ze svého počítače a vy na straně serveru nemáte šanci jak rozeznat, že se jedná o podvrh - opomineme-li problémové ověřování IP klienta). Proto se všude uvádí, že jediná bezpečná komunikace mezi serverem a uživatelem je 100% se držet šifrovaného spojení (tedy HTTPS).</p>
<p>Dokladem je např. úryvek z dokumentace Acegi Security:</p>
<p><em>"An important issue in considering transport security is that of session hijacking. Your web container manages a         HttpSession by reference to a jsessionid that is sent to user agents either via a cookie or URL rewriting. If the jsessionid is ever sent over HTTP, there is a possibility that session identifier can be intercepted and used to impersonate the user after they complete the authentication process. This is because most web containers maintain         the same session identifier for a given user, even after they switch         from HTTP to HTTPS pages. If session hijacking is considered too significant a risk for         your particular application, the only option is to use HTTPS for every         request. This means the jsessionid is never sent         across an insecure channel. You will need to ensure your         web.xml -defined points to a HTTPS location,         and the application never directs the user to a HTTP location. Acegi         Security provides a solution to assist with the latter."</em></p>
<p>Ke ztrátě důvěryhodnosti navíc může dojít i na první pohled ne zcela viditelným způsobem. V případě, že vaše aplikace poskytuje alespoň jediný servlet dostupný protokolem HTTP, který během své činnosti nastartuje serverovou session (request.getSession(true)) - webový server tuto session vytvoří, přidělí ji identifikátor a ten odešle v odpovědi klientovi nešifrovaným kanálem jako cookie JSESSIONID. Přestože by uživatel hned dalším dotazem mířil na vaši aplikaci již přes protokol HTTPS, odešle spolu s requestem také již vytvořené JSESSIONID (jelikož se jedná o "nesecure" cookie prohlížeč ji může poslat jak kanálem HTTP, tak i HTTPS). Webový server ale tento identifikátor již akceptuje a při požadavku na session, již žádnou novou nevytváří, ale poskytne už tu vytvořenou - tzn. v takovémto případě uživatel sdílí session jak pro přístup přes HTTP tak i přes HTTPS - <strong>ale rozhodně není v bezpečí</strong>.</p>
<p>Jiný problém nastává v opačném případě, kdy uživatel jako první přistoupí na váš servlet přes HTTPS kanál. V takovém případě opět webový server při požadavku na session tuto session vytvoří, přidělí identifikátor, ale identifikátor posléze pošle klientovi ve formě tzv. "secure cookie". To znamená, že webový prohlížeč tuto cookie nesmí za <strong>žádných okolností</strong> poslat zpět serveru nešifrovaným (HTTP) kanálem. Mnohé potom překvapí, že když uživatel v dalším požadavku přistoupí opět na naši aplikaci tentokrát přes HTTP, webový server nám vytvoří úplně novou session - a tudíž nevidíme uživatelova data, které jsme si uložili v předchozím volání. To je způsobeno tím, že prohlížeč správně neodeslal identifikátor session, uložený v secure cookie nešifrovaným kanálem. Tentokrát <strong>jsme v bezpečí</strong> - ale aplikace nám nefunguje, tak jak bychom si představovali.</p>
<h3>Řešení problému</h3>
<p>K vyřešení tohoto problému postačují dvě jednoduché věci. Ty musíme ovšem provádět na straně serveru před zpracováním jakéhokoliv requestu (v našem případě jsme to vyřešili nasazením servletového filtru). Jeho kód uvádím níže:</p>
<p>[source lang="java"]<br />
package com.fg.user.web.filter;</p>
<p>import org.acegisecurity.providers.encoding.Md5PasswordEncoder;<br />
import org.apache.commons.logging.Log;<br />
import org.apache.commons.logging.LogFactory;<br />
import org.springframework.web.filter.OncePerRequestFilter;</p>
<p>import javax.servlet.FilterChain;<br />
import javax.servlet.ServletException;<br />
import javax.servlet.http.Cookie;<br />
import javax.servlet.http.HttpServletRequest;<br />
import javax.servlet.http.HttpServletResponse;<br />
import javax.servlet.http.HttpSession;<br />
import java.io.IOException;</p>
<p>/**<br />
 * Filter ensures that:<br />
 *
<p/>
 * 1) http and https shares the same session id<br />
 * - when first access via https and and no JSESSIONID is sent it stores JSESSIONID cookie<br />
 * as nonsecured into the request<br />
 * 2) when on secure channel ensures that supplied JSESSIONID cookie is not spurious<br />
 * - when first access via https it generates a new cookie SECURED_TOKEN that contains MD5 hash<br />
 * of JSESSIONID and some secret salt - this cookie is then set as secured into the response<br />
 * - every other access via https checks whether SECURED_TOKEN is set and that it corresponds<br />
 * with JSESSIONID (and so that has not been stolen) - otherwise 403 will be returned<br />
 *
<p/>
 * Filter will provide secure access to protected actions via SSL ensuring that the session belongs<br />
 * only to this client. But this means, that all important actions must be located at HTTPS (for sure<br />
 * login action).<br />
 *<br />
 * Tradeoffs:<br />
 * - clients that has not cookies allowed will receive HTTP 403 from the second SSL call on<br />
 *<br />
 * @author Martin Veska, Jan Novotný<br />
 */<br />
public class SharedSessionChannelFilter extends OncePerRequestFilter {<br />
	public static final String SESSION_COOKIE_NAME = "JSESSIONID";<br />
	public static final String NONSECURED_SESSION_COOKIE_SET = "NONSECURED_SESSION_COOKIE_SET";<br />
	public static final String SECURE_TOKEN_PROVIDED = "SECURE_TOKEN_PROVIDED";<br />
	public static final String SECURE_TOKEN_COOKIE_NAME = "SECURE_TOKEN";<br />
	private static Log log = LogFactory.getLog(SharedSessionChannelFilter.class);<br />
	private String salt;<br />
	private String serverPath;</p>
<p>	/**<br />
	 * Returns salt used for generating unique secure token for session.<br />
	 *<br />
	 * @return<br />
	 */<br />
	public String getSalt() {<br />
		return salt != null ? salt : String.valueOf(System.currentTimeMillis());<br />
	}</p>
<p>	/*<br />
	 * Sets salt used for generating unique secure token for session.<br />
	 */<br />
	public void setSalt(String salt) {<br />
		this.salt = salt;<br />
	}</p>
<p>	/**<br />
	 * Contains path for the generated secure token cookie.<br />
	 * @return<br />
	 */<br />
	public String getServerPath() {<br />
		return serverPath;<br />
	}</p>
<p>	/**<br />
	 * Contains path for the generated secure token cookie.<br />
	 * @param serverPath<br />
	 */<br />
	public void setServerPath(String serverPath) {<br />
		this.serverPath = serverPath;<br />
	}</p>
<p>	/**<br />
	 * Same contract as for <code>doFilter</code>, but guaranteed to be<br />
	 * just invoked once per request. Provides HttpServletRequest and<br />
	 * HttpServletResponse arguments instead of the default ServletRequest<br />
	 * and ServletResponse ones.<br />
	 */<br />
	protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response,<br />
									FilterChain filterChain) throws ServletException, IOException {<br />
		if(request.isSecure()) {<br />
			HttpSession session = request.getSession(true);<br />
			Boolean nonSecuredSessionCookieSet = (Boolean)session.getAttribute(NONSECURED_SESSION_COOKIE_SET);</p>
<p>			String clientSecureToken = null;<br />
			//ensures that nonsecured cookie is always the same as secured one<br />
			Cookie[] cookies = request.getCookies();<br />
			if (cookies != null) {<br />
				for(Cookie cookie : cookies) {</p>
<p>					if(cookie.getName().equals(SESSION_COOKIE_NAME)) {<br />
						//we copy nonsecured session cookie only once<br />
						if(nonSecuredSessionCookieSet == null) {<br />
							if(log.isDebugEnabled()) {<br />
								log.debug("Secured session cookie found ... generating nonsecured one.");<br />
							}<br />
							Cookie nonSecureCookie = new Cookie(SESSION_COOKIE_NAME, cookie.getValue());<br />
							nonSecureCookie.setMaxAge(-1);<br />
							if (serverPath != null) nonSecureCookie.setPath(serverPath);<br />
							nonSecureCookie.setSecure(false);<br />
							response.addCookie(nonSecureCookie);<br />
							session.setAttribute(NONSECURED_SESSION_COOKIE_SET, Boolean.TRUE);<br />
						}<br />
					}</p>
<p>					//we accept secured secured client tokens<br />
					if(cookie.getName().equals(SECURE_TOKEN_COOKIE_NAME)) {<br />
						clientSecureToken = cookie.getValue();<br />
					}<br />
				}<br />
			}<br />
			//ensure that nonsecured cookie is not spurious<br />
			String serverSecureToken = (String)session.getAttribute(SECURE_TOKEN_PROVIDED);<br />
			if(serverSecureToken != null) {<br />
				if(log.isDebugEnabled()) {<br />
					log.debug("Secured token was provided for this session, verifying validity.");<br />
				}<br />
				if(clientSecureToken == null || !clientSecureToken.equals(serverSecureToken)) {<br />
					//unauthorized access!!<br />
					//secured token for this session was generated but user client did not<br />
					//provided secured cookie with this token<br />
					if(log.isErrorEnabled()) {<br />
						log.error("Client has provided null or wrong secured token! Expecting: " + serverSecureToken + ", client provided: " + clientSecureToken);<br />
					}<br />
					response.sendError(HttpServletResponse.SC_FORBIDDEN);<br />
				}<br />
				else {<br />
					//client is authorized<br />
					if(log.isDebugEnabled()) {<br />
						log.debug("Access allowed, secured token verified.");<br />
					}<br />
					filterChain.doFilter(request, response);<br />
				}<br />
			}<br />
			else {<br />
				if(log.isDebugEnabled()) {<br />
					log.debug("Access allowed - secured token has not been gerated for this session yet. Generating new one.");<br />
				}<br />
				serverSecureToken = getSecuredToken(session, getSalt());<br />
				Cookie securedCookie = new Cookie(SECURE_TOKEN_COOKIE_NAME, serverSecureToken);<br />
				securedCookie.setSecure(true);<br />
				if (getServerPath() != null) securedCookie.setPath(getServerPath());<br />
				securedCookie.setMaxAge(-1);<br />
				response.addCookie(securedCookie);<br />
				session.setAttribute(SECURE_TOKEN_PROVIDED, serverSecureToken);<br />
				//client is authorized<br />
				filterChain.doFilter(request, response);<br />
			}<br />
		} else {<br />
			//non secured channel is always allowed<br />
			filterChain.doFilter(request, response);<br />
		}<br />
	}</p>
<p>	/**<br />
	 * Returns MD5 hash of session id plus some salt. Should be considerably unique.<br />
	 *<br />
	 * @param session<br />
	 * @param salt<br />
	 * @return<br />
	 */<br />
	private String getSecuredToken(HttpSession session, String salt) {<br />
		Md5PasswordEncoder encoder = new Md5PasswordEncoder();<br />
		return encoder.encodePassword(session.getId(), salt);<br />
	}</p>
<p>}<br />
[/source]</p>
<p>Konfigurace ve springu potom takto (puze výňatek z komplexnější Acegi konfigurace):</p>
<p>[source lang="xml"]<br />
<bean id="filterChainProxy" class="org.acegisecurity.util.FilterChainProxy"></p>
<property name="filterInvocationDefinitionSource">
		<value><br />
			CONVERT_URL_TO_LOWERCASE_BEFORE_COMPARISON<br />
			PATTERN_TYPE_APACHE_ANT<br />
			/**=channelProcessingFilter,sharedSessionChannelFilter<br />
		</value>
	</property>
</bean></p>
<p><bean id="channelProcessingFilter" class="org.acegisecurity.securechannel.ChannelProcessingFilter"></p>
<property name="channelDecisionManager">
		<ref bean="channelDecisionManager"/>
	</property>
<property name="filterInvocationDefinitionSource">
		<value><br />
			CONVERT_URL_TO_LOWERCASE_BEFORE_COMPARISON<br />
			PATTERN_TYPE_APACHE_ANT<br />
			/**/secure/**=REQUIRES_SECURE_CHANNEL<br />
			/**=REQUIRES_INSECURE_CHANNEL<br />
		</value>
	</property>
</bean></p>
<p><bean id="sharedSessionChannelFilter" class="com.fg.user.web.filter.SharedSessionChannelFilter"></p>
<property name="salt" value="nejakaSuperTajnaCastHesla"/>
<property name="serverPath" value="/webRootContext"/>
</bean><br />
[/source]</p>
<h4>Zajištění spolehlivého sdílení session</h4>
<p>První věcí je vyřešení neblahého stavu, kdy session vytvořená v HTTPS requestu není viditelná v následném HTTP požadavku. Toto je možné jednoduše vyřešit tím, že i v případě prvního přístupu přes HTTPS vynutíme odeslání JSESSIONID cookie jako ne secure.</p>
<p>Tím je sice problém vyřešen, ale otvíráme bránu k odposlechnutí této informace. Proto musíme bezpečnost zajistit nějak jinak.</p>
<h4>Zajištění bezpečného přístupu přes HTTPS</h4>
<p>Při prvním přístupu protokolem HTTPS, vytvoříme tzv. secure token - což je unikátní řetězec (vypočtený např. na základě JSESSIONID + nějakého dalšího modifikátoru) , který odešleme uživateli v odpovědi jako secure cookie. Tento token nám v podstatě nahrazuje původní důvěryhodnou JSESSIONID, kterou jsme byli nuceni vyzradit. Secure token nám prohlížeč odešle vždy, když uživatel bude přistupovat na naši aplikaci přes HTTPS a jen tehdy můžeme na straně serveru ověřit, že uživatel je skutečně stále ten stejný uživatel, kterého jsme přihlásili.</p>
<p>Z výše uvedeného tedy vyplývá následující základní pravidlo: jakékoli operace, u kterých si chceme být jisti, že je skutečně provádí uživatel, kterého jsme přihlásili (jako např. změna hesla, přihlášení, změna údajů uživatele, odeslání objednávky atp.), musíme provádět pouze přes protokol HTTPS - jelikož jen v něm je možné zkontrolovat secure token.</p>
<p>Při každém následujícím požadavku přes protokol HTTPS filtr zkontroluje zda spolu s JSESSIONID přišel také správný secure token, který byl pro tuto session na počátku vygenerován. Jakmile tento secure token nepřijde nebo se liší od vydaného tokenu pro konkrétní session, filtr nepovolí zpracování požadavku a vrátí HTTP Error 403 - Forbidden.</p>
<p><em><strong>Z toho také vyplývá omezení, že uživatelé, kteří nemají povolené cookies nebudou moci s naší aplikací (konkrétně tedy s částí přístupnou pouze přes HTTPS) pracovat. Podobná logika není možná zajistit v případě URL rewritingu.</strong></em></p>
<h3>Závěrem</h3>
<p>Výše uvedený článek má celkem dva cíle. Jednak se podělit s komunitou o naše myšlenky a druhak si ověřit, jestli přeci jen není možné najít způsob, kterým by bylo možné výše popsanou logiku obejít a přihlášení nějakým způsobem zneužít. Celou problematiku jsme analyzovali z různých stran a toto řešení nám připadá jako bezpečné. Jak se ovšem říká - "nikdy neříkej nikdy" a proto budeme vděčni za vaše názory, či myšlenky, jak by bylo možné popsané zabezpečení "prostřelit".</p>
