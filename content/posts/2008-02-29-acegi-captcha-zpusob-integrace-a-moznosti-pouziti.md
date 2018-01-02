---
status: publish
published: true
title: Acegi Captcha způsob integrace a možnosti použití
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "V tomto příspěvku se nechci věnovat popisu zprovoznění jCaptchy v bezpečnostní
  frameworku Acegi Security, jelikož toto je velmi dobře popsáno již v <a href=\"http://weblog.morosystems.cz/spring/Spring-Acegi-JCaptcha-integration\"
  target=\"_new\">existujícím článku na MoroSystems weblogu</a>. Spíš se chci zaobírat
  způsobem, jakým se k integraci do Acegi frameworku autoři postavili. Tento způsob
  mi přijde totiž přinejmenším neobvyklý. Zachovává sice zavedené principy Acegi,
  ale ten neodpovídá mým (ale řekl bych vcelku přirozeným) představám o tom, jak by
  měla captcha ve web strákách fungovat.\r\n\r\nPrincip práce s captchou v Acegi je
  podobný principu standardního přihlašování. Acegi při přístupu na \"chráněné url\"
  kontroluje ověření uživatele v SecurityContextu a pokud uživatel není ověřen, přesměruje
  tok aplikace na přihlašovací formulář nebo v případě captchy na  formulář obsahující
  obrázek a textové pole pro vepsání rozpoznané captchy. Pokud řešíme přihlašování,
  je tento způsob přirozený - v případě captchy však očekávám, že captcha bude rovnou
  součástí formuláře, který je \"hlídán\". Tak ale integrace jCaptchy v Acegi ve svém
  základu nefunguje.\r\n\r\nPokud Vám tento způsob připadne taky trochu podivný a
  zajímá Vás, jak si s tím poradit, čtěte dál.\r\n\r\n"
wordpress_id: 54
wordpress_url: http://blog.novoj.net/2008/02/29/acegi-captcha-zpusob-integrace-a-moznosti-pouziti/
date: '2008-02-29 07:39:49 +0100'
date_gmt: '2008-02-29 06:39:49 +0100'
categories:
- Java
- Bezpečnost
- Web
tags: []
comments: []
---
<p>V tomto příspěvku se nechci věnovat popisu zprovoznění jCaptchy v bezpečnostní frameworku Acegi Security, jelikož toto je velmi dobře popsáno již v <a href="http://weblog.morosystems.cz/spring/Spring-Acegi-JCaptcha-integration" target="_new">existujícím článku na MoroSystems weblogu</a>. Spíš se chci zaobírat způsobem, jakým se k integraci do Acegi frameworku autoři postavili. Tento způsob mi přijde totiž přinejmenším neobvyklý. Zachovává sice zavedené principy Acegi, ale ten neodpovídá mým (ale řekl bych vcelku přirozeným) představám o tom, jak by měla captcha ve web strákách fungovat.</p>
<p>Princip práce s captchou v Acegi je podobný principu standardního přihlašování. Acegi při přístupu na "chráněné url" kontroluje ověření uživatele v SecurityContextu a pokud uživatel není ověřen, přesměruje tok aplikace na přihlašovací formulář nebo v případě captchy na  formulář obsahující obrázek a textové pole pro vepsání rozpoznané captchy. Pokud řešíme přihlašování, je tento způsob přirozený - v případě captchy však očekávám, že captcha bude rovnou součástí formuláře, který je "hlídán". Tak ale integrace jCaptchy v Acegi ve svém základu nefunguje.</p>
<p>Pokud Vám tento způsob připadne taky trochu podivný a zajímá Vás, jak si s tím poradit, čtěte dál.</p>
<p><a id="more"></a><a id="more-54"></a></p>
<p>Současná integrace Captchy do Acegi umožňuje vývojářům nezabývat se v jednotlivých formulářích captchou, ale ve chvíli kdy je již aplikace hotová určit URL, které mohou být zneužitelná boty a nastavit pravidla pro rozpoznávání chování robotů. Acegi v tomto směru poskytuje několik strategií:</p>
<ul>
<li><b><a href="http://www.jdocs.com/acegi/1.0.0/org/acegisecurity/captcha/AlwaysTestAfterMaxRequestsCaptchaChannelProcessor.html" target="_new">AlwaysTestAfterMaxRequestsCaptchaChannelProcessor</a></b> - vyžádá ověření captchy vždy po určitém počtu přístupů na chráněné url</li>
<li><b><a href="http://www.jdocs.com/acegi/1.0.0/org/acegisecurity/captcha/AlwaysTestAfterTimeInMillisCaptchaChannelProcessor.html" target="_new">AlwaysTestAfterTimeInMillisCaptchaChannelProcessor</a></b> - vyžádá ověření captchy pokud je přístup na chráněné url po definovaném časovém intervalu od posledního úspěšného prověření captchou</li>
<li><b><a href="http://www.jdocs.com/acegi/1.0.0/org/acegisecurity/captcha/AlwaysTestBelowAverageTimeInMillisBetweenRequestsChannelProcessor.html" target="_new">AlwaysTestBelowAverageTimeInMillisBetweenRequestsChannelProcessor</a></b> - vyžádá ověření captchy, pokud jdou requesty na chráněná url v kratších časových intervalech než je povolené</li>
<li><b><a href="http://www.jdocs.com/acegi/1.0.0/org/acegisecurity/captcha/TestOnceAfterMaxRequestsCaptchaChannelProcessor.html" target="_new">TestOnceAfterMaxRequestsCaptchaChannelProcessor</a></b> - vyžádá ověření captchy vždy po určitém počtu přístupů na chráněné url - ověření captchy se ovšem provede pouze jednou</li>
</ul>
<p>Po krátké úvaze mě však přišel použitelný jediný a to je TestOnceAfterMaxRequestsCaptchaChannelProcessor s nastavením Threshold na hodnotu 0. To znamená, že při prvním přístupu na formulář chráněný captchou se má provést ověření "humanity" uživatele a po správném ověření už považovat uživatele s danou session za ověřeného a neobtěžovat ho dalšími captcha obrázky.</p>
<h3>Captcha servlet filter</h3>
<p>Vzhledem k nemožnosti cokoliv rozumného provést s existujícím filtrem <a href="http://www.jdocs.com/acegi/1.0.0/org/acegisecurity/captcha/CaptchaValidationProcessingFilter.html" target="_new">org.acegisecurity.captcha.CaptchaValidationProcessingFilter</a>, byl jsem nucen napsat si na základě části jeho funkcionality filtr vlastní (bohužel řada tříd z Acegi má jednu nepříjemnou vlastnost a to tu, že je velmi obtížné je extendovat či jinak modifikovat, jelikož mají řadu private metod / fieldů nebo občas i mnoho funkcionality v jedné metodě, kde by člověk potřeboval změnit jen jednu její část).</p>
<p>Nuže v následujícím kódu je implementace filtru, který provádí validaci captchy a zároveň poskytuje vygenerovaný captcha obrázek. Jelikož je filtr součástí Acegi delegating filtru je obvykle posazen na url-pattern "/*", což nám umožňuje jednoduše se navěsit na libovolné volání serveru v daném kontextu. Toho filtr využívá k tomu, aby mohl při dotazu na konkrétní url (např.: http://server/context/generatedCaptchaImage.jpg) online vygenerovat captcha obrázek a okamžitě jej vložit do response.</p>
<p>Ten stejný filtr provádí validaci jím vygenerovaných captcha obrázků v případě, že v parametrech requestu objeví parametr s názvem "captcha" (nebo kterýkoliv jiný, který uvedeme v konfiguraci), pokusí se zvalidovat jeho hodnotu vůči naposledy poskytnuté captche. V případě, že validace neprojde je do requestu uložen atribut signalizující neplatný pokus o validaci captchy - v opačném případě je do CaptchaSecurityContext nastaven příznak human na true.</p>
<p>[source lang="java"]<br />
/**<br />
 * Filter for web integration of the {@link org.acegisecurity.captcha.CaptchaServiceProxy}. <br><br />
 * It basically intercept calls containing the specific validation parameter, use the {@link org.acegisecurity.captcha.CaptchaServiceProxy} to<br />
 * validate the request, and update the {@link org.acegisecurity.captcha.CaptchaSecurityContext} if the request passed the validation. <br><br />
 * This Filter should be placed after the ContextIntegration filter and before the {@link<br />
 * org.acegisecurity.captcha.CaptchaChannelProcessorTemplate} filter in the filter stack in order to update the {@link org.acegisecurity.captcha.CaptchaSecurityContext}<br />
 * before the humanity verification routine occurs. <br><br />
 * This filter should only be used in conjunction with the {@link org.acegisecurity.captcha.CaptchaSecurityContext}<br><br />
 *
<p/>
 * Filter extends the original one with adding functionality to return binary image when url end with<br />
 * particular string.<br />
 */<br />
public class CaptchaGenerationValidationProcessingFilter implements InitializingBean, Filter, ApplicationEventPublisherAware {<br />
	private static Log log = LogFactory.getLog(CaptchaGenerationValidationProcessingFilter.class);<br />
	private CaptchaServiceProxy captchaService;<br />
	private String captchaImgUrl = "generatedCaptchaImage.jpg";<br />
	private String captchaValidationParameter = "captcha";<br />
	private CaptchaService jcaptchaService;<br />
	private ApplicationEventPublisher publisher;<br />
	public static final String REQUEST_CAPTCHA_RECOGNITION_FAILURE_FLAG = "_acegi_captcha_recognition_failure_flag";</p>
<p>	public String getCaptchaImgUrl() {<br />
		return captchaImgUrl;<br />
	}</p>
<p>	public void setCaptchaImgUrl(String captchaImgUrl) {<br />
		this.captchaImgUrl = captchaImgUrl;<br />
	}</p>
<p>	public void setCaptchaValidationParameter(String captchaValidationParameter) {<br />
		this.captchaValidationParameter = captchaValidationParameter;<br />
	}</p>
<p>	public String getCaptchaValidationParameter() {<br />
		return captchaValidationParameter;<br />
	}</p>
<p>	public void setCaptchaService(CaptchaServiceProxy captchaService) {<br />
		this.captchaService = captchaService;<br />
	}</p>
<p>	public void setCaptchaServiceProvider(CaptchaServiceProvider captchaServiceProvider) {<br />
		this.jcaptchaService = captchaServiceProvider.getCaptchaService();<br />
	}</p>
<p>	//~ Methods ========================================================================================================</p>
<p>	public void afterPropertiesSet() throws Exception {<br />
		if(this.captchaService == null) {<br />
			throw new IllegalArgumentException("CaptchaServiceProxy must be defined ");<br />
		}</p>
<p>		if((this.captchaValidationParameter == null) || "".equals(captchaValidationParameter)) {<br />
			throw new IllegalArgumentException("captchaValidationParameter must not be empty or null");<br />
		}<br />
	}</p>
<p>	public void setApplicationEventPublisher(ApplicationEventPublisher applicationEventPublisher) {<br />
		this.publisher = applicationEventPublisher;<br />
	}</p>
<p>	public void init(FilterConfig filterConfig) throws ServletException {<br />
		//no implementation - we do everything in Spring lifecycle<br />
	}</p>
<p>	public void destroy() {<br />
		//no implementation - we do everything in Spring lifecycle<br />
	}</p>
<p>	public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain chain) throws IOException, ServletException {<br />
		if((servletRequest != null) && servletRequest instanceof HttpServletRequest) {<br />
			HttpServletRequest request = ((HttpServletRequest)servletRequest);<br />
			HttpServletResponse response = ((HttpServletResponse)servletResponse);</p>
<p>			if(((HttpServletRequest)servletRequest).getRequestURI().endsWith(captchaImgUrl)) {<br />
				generateImageOutputAndSkipProcessing(request, response);<br />
			}<br />
			else {<br />
				String captchaResponse = request.getParameter(captchaValidationParameter);<br />
				boolean continueWithChainProcessing = true;</p>
<p>				if(captchaResponse != null) {<br />
					continueWithChainProcessing =<br />
							validateCaptchaResponse(request, response, captchaResponse);<br />
				} else {<br />
					log.debug("Captcha validation parameter not found, do nothing");<br />
				}</p>
<p>				if (continueWithChainProcessing) {<br />
					if(log.isDebugEnabled()) {<br />
						log.debug("Continuing with chain processing ...");<br />
					}</p>
<p>					chain.doFilter(request, response);<br />
				}<br />
			}<br />
		}<br />
		else {<br />
			chain.doFilter(servletRequest, servletResponse);<br />
		}<br />
	}</p>
<p>	/**<br />
	 * Method validates captcha response and fires appropriate events.<br />
	 * @param request<br />
	 * @param response<br />
	 * @param captchaResponse<br />
	 *<br />
	 * @return true if filter processing should continue, false when redirect was made<br />
	 */<br />
	private boolean validateCaptchaResponse(HttpServletRequest request, HttpServletResponse response, String captchaResponse) throws IOException {<br />
		log.debug("Captcha validation parameter found, trying to validate");<br />
		// validate the request against CaptchaServiceProxy<br />
		HttpSession session = request.getSession();</p>
<p>		if(session != null) {<br />
			String id = session.getId();<br />
			boolean valid = false;<br />
			try {<br />
				valid = this.captchaService.validateReponseForId(id, captchaResponse);<br />
			} catch(CaptchaServiceException ex) {<br />
				if(log.isWarnEnabled()) {<br />
					log.warn("Captcha already used. Returning false for recognition result!");<br />
				}<br />
			}<br />
			log.debug("CaptchaServiceProxy says : request is valid = " + valid);</p>
<p>			if(valid) {<br />
				log.debug("Captcha response accepted - updating context");<br />
				((CaptchaSecurityContext)SecurityContextHolder.getContext()).setHuman();</p>
<p>				publisher.publishEvent(<br />
						new CaptchaChallengePassedEvent(this, captchaResponse)<br />
				);</p>
<p>				//if there is saved request redirect to it<br />
				SavedRequest savedRequest = (SavedRequest)request.getSession()<br />
						.getAttribute(SelfAwareCaptchaEntryPoint.CAPTCHA_ENTRY_POINT_SAVED_REQUEST_ATTRIBUTE);<br />
				if (savedRequest != null) {<br />
					String url = savedRequest.getFullRequestUrl();</p>
<p>					if(log.isDebugEnabled()) {<br />
						log.debug("Original captcha requested url (" + url + ") found. Redirecting back because captcha was accepted.");<br />
					}</p>
<p>					response.sendRedirect(url);<br />
					return false;<br />
				}</p>
<p>			}<br />
			else {<br />
				log.debug("Captcha response rejected - wrong answer");<br />
				request.setAttribute(REQUEST_CAPTCHA_RECOGNITION_FAILURE_FLAG, Boolean.TRUE);</p>
<p>				publisher.publishEvent(<br />
						new CaptchaChallengeFailedEvent(this, captchaResponse)<br />
				);<br />
			}<br />
		}<br />
		else {<br />
			log.debug("No session found, user didn't even ask a captcha challenge");<br />
		}</p>
<p>		return true;<br />
	}</p>
<p>	/**<br />
	 * This method just generates captcha image and skips request processing.<br />
	 *<br />
	 * @param request<br />
	 * @param response<br />
	 * @throws IOException<br />
	 */<br />
	private void generateImageOutputAndSkipProcessing(HttpServletRequest request, HttpServletResponse response) throws IOException {<br />
		//we skip processing and return generated captcha image<br />
		response.setHeader("Cache-Control", "no-store");<br />
		response.setHeader("Pragma", "no-cache");<br />
		response.setDateHeader("Expires", 0);<br />
		response.setContentType("image/jpeg");<br />
		// get the session id that will identify the generated captcha.<br />
		//the same id must be used to validate the response, the session id is a good candidate!<br />
		//generated image we stream directly onto output<br />
		generateCaptcha(request.getSession().getId(), request.getLocale(), response.getOutputStream());<br />
	}</p>
<p>	/**<br />
	 * Generates the captcha image;<br />
	 *<br />
	 * @param captchaId<br />
	 * @param locale<br />
	 * @param os<br />
	 * @throws IOException<br />
	 */<br />
	private void generateCaptcha(String captchaId, Locale locale, OutputStream os) throws IOException {<br />
		if (jcaptchaService instanceof ImageCaptchaService) {<br />
			BufferedImage challenge = ((ImageCaptchaService)jcaptchaService)<br />
					.getImageChallengeForID(captchaId, locale);<br />
			JPEGImageEncoder jpegEncoder = JPEGCodec.createJPEGEncoder(os);<br />
			jpegEncoder.encode(challenge);<br />
			// flush it in the response<br />
			os.flush();<br />
			os.close();<br />
		} else {<br />
			String msg = "CaptchaService does not implement ImageCaptchaService. Cannot generate image captcha.";<br />
			log.error(msg);<br />
		}<br />
	}</p>
<p>}<br />
[/source]</p>
<p>Tento přístup se liší od standardní implementace tím, že vůbec nepracuje s patterny chráněných url. Pouze jednoduše pro určité url (/generatedCaptchaImage.jpg) vrací vygenerovanou captchu a při konkrétním parametru v requestu se naopak pokouší validovat captchu. Ve každém případě však propouští zpracování requestu dál, tzn. vlastní url formuláře není tímto filtrem nijak chráněno.</p>
<h3>Zaznamenání chyby při validaci formuláře</h3>
<p>Filtr není závislý na žádném web frameworku, jediný jeho výstup je nastavení příznaku v SecurityContextu nebo specifického atributu v requestu. Vlastní ochranu formuláře musíme tedy řešit až o krok dále - na úrovni validačního rámce konkrétního použitého frameworku. V některých bude tato  ochrana velmi triviální, někde se můžeme při implementaci ochrany docela nadřít. Nejlepším způsobem je se vetřít do standardní validace konkrétního validačního rámce a využít jej i k propagaci chybového hlášení, zpracování flow při chybě, obarvení chybových polí atp. - tím si ušetříme spoustu práce.</p>
<p>V mém případě se jednalo o integraci do frameworku Stripes a tam je tato záležitost zcela přímočará. Spočívá v implementaci Interceptoru, který se spouští ve fázi BindingAndValidation a který pouze prověří přítomnost atributu signalizujícího špatně rozeznanou captchu. V takovém případě automaticky přidá do seznamu chyb nový záznam, což způsobí, že zpracování requestu skončí ve fázi validace dat a vrátí se zpět na původní formulář.</p>
<p>Obdobně by bylo asi velmi jednoduché implementovat tento způsob validace i v JSF frameworcích. Obtížně si jeho realizaci naopak umím představit ve Strutsech (minimálně v 1.2.X verzi).</p>
<p>[source lang="java"]<br />
@Intercepts(LifecycleStage.BindingAndValidation)<br />
public class CaptchaValidationInterceptor implements Interceptor {</p>
<p>	/**<br />
	 * Invoked when intercepting the flow of execution.<br />
	 *<br />
	 * @param context the ExecutionContext of the request currently being processed<br />
	 * @return the result of calling context.proceed(), or if the interceptor wishes to change<br />
	 *         the flow of execution, a Resolution<br />
	 * @throws Exception if any non-recoverable errors occur<br />
	 */<br />
	public Resolution intercept(ExecutionContext context) throws Exception {<br />
		Boolean captchaRecognitionFailed = (Boolean)context.getActionBeanContext()<br />
				.getRequest().getAttribute(<br />
				CaptchaGenerationValidationProcessingFilter.REQUEST_CAPTCHA_RECOGNITION_FAILURE_FLAG<br />
		);<br />
		if (captchaRecognitionFailed != null && captchaRecognitionFailed.booleanValue()) {<br />
			context.getActionBeanContext().getValidationErrors().add(<br />
					"captcha", new SimpleError("Chybně rozpoznaná captcha.")<br />
			);<br />
		}<br />
		return context.proceed();<br />
	}</p>
<p>}<br />
[/source]</p>
<h3>Webová vrstva - formulář a zobrazení captchy</h3>
<p>V JSP stránce přidáme do formuláře IMG tag, který se odkazuje na "virtuální url", na které bude reagovat CaptchaGenerationValidationProcessingFilter vrácením nového Captcha obrázku. Ve formuláři bude taktéž k dispozici textové políčko pro zapsání odpovědi opět s názvem, který daný filtr očekává. Celá tato část je uzavřená do IF klauzule, která prověřuje, zda již test "humanity" pro aktuálního uživatele (session) náhodou nebyl v minulosti proveden. Pokud ano, zmizí captcha z formuláře. Pokud tedy uživatel bude ve vaší aplikaci vyplňovat více formulářů chráněných captchou, bude muset tuto captchu vyplnit pouze v prvním formuláři, a když jej aplikace úspěšně prověří, v dalších formulářích již nebude uživatel obtěžován.</p>
<p>[source lang="xml"]<br />
<stripes:form action="/url.x" class="in" focus=""></p>
<h3>Odeslat dotaz:</h3>
<p>	<c:if test="<%=!((CaptchaSecurityContext)SecurityContextHolder.getContext()).isHuman()%>"><br />
		<span id="captchaArea"><br />
			<img id="captchaImage" src="/srv/www/generatedCaptchaImage.jpg" width="208" height="44"></p>
<p>			<span><br />
				<label for="captcha">Opište prosím text z obrázku:</label><br />
				<stripes:text id="captcha" name="captcha" class="text"/><br />
			</span><br />
		</span><br />
	</c:if><br />
	<stripes:submit name="createItem"/><br />
</stripes:form><br />
[/source]</p>
<h3>Závěrem</h3>
<p>Jak jsem již v článku uvedl, integrace captchy v Acegi frameworku se mi zdá prapodivná. Na stranu druhou jsem si vědom, že přímá integrace do formulářů s sebou nese dodatečné problémy - není možné přímo v Acegi implementovat dostatečnou podporu, jelikož zobrazování chyb se musí provádět na úrovni konkrétního použitého web frameworku. Taktéž toto řešení vyžaduje, aby se v každém formuláři vložila část obsahující captchu a kontrolní pole. Toto si museli autoři zcela jistě uvědomovat - bohužel už o tom ale nikde nenajdete zmínku a musíte nad tím přemýšlet sami.</p>
<p>Na úplný závěr si ještě neodpustím jeden povzdech. Z několika přednášek o tvorbě API jsem si odnesl pravidla: </p>
<ul>
<li>nedělejte API širší než je nezbytně nutné,</li>
<li>příliš neotvírejte třídy k dědičnosti a nebojte se použít final,</li>
<li>omezte viditelnost metod na maximální možnou míru</li>
</ul>
<p>Z pohledu vývojáře API dávají pravidla smysl. Má daleko větší kontrolu nad svým API a především má daleko větší možnosti refaktoringu a změn v něm.</p>
<p>Z pohledu uživatele API to však vede místy k naprostému zoufalství. V Acegi je většina tříd poměrně slušně připravená k rozšiřování, ovšem najdete tam i takové kousky, kdy je veškerá logika třídy v jedné metodě, nebo naopak jsou důležité metody jako friendly nebo private (aniž by to dávalo zjevný smysl). Na obdobné potíže jsme narazili i v knihovně jCaptcha a častokrát na místech, kde jsme to naprosto nečekali a kde nám to ani nedává smysl.</p>
<p>Jediným výsledkem je bohužel to, že buď to přímo zkopírujete kusy zdrojáku z originálu, nebo použijete reflection ke znásilnění původního kódu. Prostě není jiná možnost - výsledkem je, že tvůrci API svoji kompatibilitu neochránili, pouze si udělali alibi, že při vydání nové verze neručí za to, když "vám to přestane fungovat".</p>
