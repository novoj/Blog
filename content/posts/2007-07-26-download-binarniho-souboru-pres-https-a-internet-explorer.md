---
status: publish
published: true
title: Download binárního souboru přes HTTPS a Internet Explorer
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Jsou chyby malé, velké, závažné i triviální, úsměvné, spletité i velmi hloupé.
  Z celého pokolení chyb je tahle velmi, velmi stará a také dost hloupá. A vypadá
  to, že z úcty k jejímu věku, ji nechá M$ už pokojně dožít spolu s chatrčí zvanou
  Internet Explorer.\r\n\r\nNa chybu narazíte tehdy, když coby Java programátor napíšete
  servlet, který vrací binární data přes protokol HTTPS (např. vygenerovaný MS Excel
  jako já, nebo třeba PDF atd.). Aniž byste to explicitně nastavili do HttpResponse,
  bude vrácená odpověď (pravděpodobně) obsahovat v hlavičce tyto údaje:\r\n\r\n[source
  lang=\"java\"]\r\nPragma: no-cache\r\nCache-Control: no-cache\r\n[/source]\r\n\r\nO
  to se vám postará váš web server (v mém případě Tomcat i Apache zároveň). Internet
  Explorer se však k vrácené binární odpovědi s těmito hlavičkami obrátí zády a lakonicky
  vás informuje: \"Aplikace Internet Explorer nemůže otevřít tento server v síti Internet.
  Požadovaný server není k dispozici nebo jej nelze najít. Akci zopakujte později.\"\r\n\r\nTato
  chybka je dle některých zdrojů v Exploreru už od verze 4.0 (byť záznam v knowledge
  base Microsoftu tvrdí, je reportovaná až u IE 6.0 SP1) a přetrvává až do současné
  verze 7.0, což jsem si měl bohužel možnost vyzkoušet na vlastní kůži.\r\n\r\n"
wordpress_id: 23
wordpress_url: http://blog.novoj.net/2007/07/26/download-binarniho-souboru-pres-https-a-internet-explorer/
date: '2007-07-26 14:08:03 +0200'
date_gmt: '2007-07-26 13:08:03 +0200'
categories:
- Java
- Web
tags: []
comments:
- id: 24017
  author: tomas kutin
  author_email: tomas.kutin@gmail.com
  author_url: ''
  date: '2010-07-20 14:17:39 +0200'
  date_gmt: '2010-07-20 13:17:39 +0200'
  content: 'ahoj, diky za clanek ktery mi zachrani snad zivot, je to az neuveritelna
    nahoda ze sme se dnes potkali po tak dlouhe dobe a ze ve stejny den budu potrebovat
    tento prispevek, ktery sem cirou nahodou vygooglil : )'
- id: 24030
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-07-21 17:31:34 +0200'
  date_gmt: '2010-07-21 16:31:34 +0200'
  content: ":-) rádo se stalo, tohle mě taky pěkně potrápilo"
- id: 27685
  author: Zdeněk
  author_email: mail.zdenka.maleho@email.cz
  author_url: ''
  date: '2010-11-03 16:04:10 +0100'
  date_gmt: '2010-11-03 15:04:10 +0100'
  content: Taky jsem na tenhle problém narazil. Nejvtipnější na celé věci je neuvěřitelný
    alibismus Microsoftu, když na svém support webu tvrdí, že "Toto chování je záměrné."
    Proč ne, to není chyba - ta aplikace nám nefunguje záměrně!
---
<p>Jsou chyby malé, velké, závažné i triviální, úsměvné, spletité i velmi hloupé. Z celého pokolení chyb je tahle velmi, velmi stará a také dost hloupá. A vypadá to, že z úcty k jejímu věku, ji nechá M$ už pokojně dožít spolu s chatrčí zvanou Internet Explorer.</p>
<p>Na chybu narazíte tehdy, když coby Java programátor napíšete servlet, který vrací binární data přes protokol HTTPS (např. vygenerovaný MS Excel jako já, nebo třeba PDF atd.). Aniž byste to explicitně nastavili do HttpResponse, bude vrácená odpověď (pravděpodobně) obsahovat v hlavičce tyto údaje:</p>
<p>[source lang="java"]<br />
Pragma: no-cache<br />
Cache-Control: no-cache<br />
[/source]</p>
<p>O to se vám postará váš web server (v mém případě Tomcat i Apache zároveň). Internet Explorer se však k vrácené binární odpovědi s těmito hlavičkami obrátí zády a lakonicky vás informuje: "Aplikace Internet Explorer nemůže otevřít tento server v síti Internet. Požadovaný server není k dispozici nebo jej nelze najít. Akci zopakujte později."</p>
<p>Tato chybka je dle některých zdrojů v Exploreru už od verze 4.0 (byť záznam v knowledge base Microsoftu tvrdí, je reportovaná až u IE 6.0 SP1) a přetrvává až do současné verze 7.0, což jsem si měl bohužel možnost vyzkoušet na vlastní kůži.</p>
<p><a id="more"></a><a id="more-23"></a></p>
<p style="text-align: center"><a href="http://blog.novoj.net/binary//2007/07/downloadhttpsie.png" title="Zobrazená chyba v Internet Exploreru"><img src="http://blog.novoj.net/binary//2007/07/downloadhttpsie.thumbnail.png" alt="Zobrazená chyba v Internet Exploreru" /></a></p>
<p>Naštěstí za ta léta již existují střípky rad, jak tuto chybku překonat. V mém případě bylo řešení složitější, jelikož v používáme dva web servery v kombinaci - Apache a Tomcat komunikující spolu protokolem AJP13. V mém případě totiž ony "no-cache" informace přidávaly do hlaviček oba dva tyto servery.</p>
<h3>Řešením v mém případě tedy bylo:</h3>
<h4>1. v servletu definovat pouze tyto hlavičky:</h4>
<p>[source lang="java"]<br />
public class XlsExportServlet extends HttpServlet {</p>
<p>	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {<br />
		try {<br />
			response.setContentType("application/vnd.ms-excel");<br />
			response.setHeader("Content-Disposition", "attachment; filename=callMeExport.xls" );						</p>
<p>			//writeBinaryOutput(response.getOutputStream());<br />
			}<br />
		}<br />
		catch(Exception e) {<br />
			if(log.isFatalEnabled()) {<br />
				log.fatal("Error during processing request!", e);<br />
			}<br />
			response.sendError(HttpServletResponse.SC_INTERNAL_SERVER_ERROR);<br />
		}<br />
		finally {<br />
			response.flushBuffer();<br />
			response.getOutputStream().close();<br />
		}<br />
	}</p>
<p>}<br />
[/source]</p>
<h4>2. v Contextu v Tomcatu vypnout proxy, která dodává "no-cache" informaci:</h4>
<p>Dle všech informací by no-cache do hlavičky měl Tomcat přidávat pouze v okamžiku, kdy máte na dané url nakonfigurovanou autentizaci přes webový kontejner. V mém případě jsem měl v Tomcatu nakonfigurovanou exploded aplikaci přímo v server.xml:</p>
<p>[source lang="xml"]<br />
<Host name="www.nesmysl.cz" appBase="/www/test-secure/" unpackWARs="false"><br />
	<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs" prefix="www_access_log." suffix=".txt" pattern="common"/><br />
	<Context path="/srv/www" docBase="_deploy/webapp"><br />
		<Valve className="org.apache.catalina.authenticator.BasicAuthenticator"  disableProxyCaching="false" /><br />
		<Realm className="org.apache.catalina.realm.MemoryRealm" pathname="/www/test-secure/etc/tomcat-users.xml"/><br />
	</Context><br />
	<Context path="/srv/manager" privileged="true" docBase="/usr/local/tomcat/server/webapps/manager"/><br />
</Host><br />
[/source]</p>
<p>Nicméně v případě waru by mělo postačovat vložení následující konfigurace do souboru <strong>/META-INF/context.xml</strong> :</p>
<p>[source lang="xml"]<br />
<Context><br />
	<Valve className="org.apache.catalina.authenticator.BasicAuthenticator"  disableProxyCaching="false" /><br />
</Context><br />
[/source]</p>
<p>Použijte samozřejmě správnou implementaci Authenticatoru, kterou vaše aplikace používá - na výběr máte:</p>
<p>[source lang="java"]<br />
BasicAuthenticator, DigestAuthenticator, FormAuthenticator, NonLoginAuthenticator, SSLAuthenticator<br />
[/source]</p>
<h4>3. v Apachi předefinovat makro pro konkrétní URL, které nastaví hlavičky jak je třeba:</h4>
<p>[source lang="java"]<br />
<Location /srv/www/adm/xlsExport><br />
     Header set Pragma public<br />
     Header set Cache-control max-age=0<br />
</Location><br />
[/source]</p>
<h3>Závěrem</h3>
<p>Po restartu Tomcatu a Apache se mi podařilo stahovat a otevírat binární soubor i v Internet Exploreru. Toto řešení fungovalo v mém případě - to že to pomůže i Vám samozřejmě nemůžu zaručit. Nicméně dalo to docela práci tenhle problém rozlousknout, takže si myslím, že stojí jen na blogu zaznamenat pro příští generace :). Jen ještě jednu radu na závěr - pokud si nejste jistí, co vám server posílá za hlavičky, zkuste využít funkcí pluginu Firebug pro Firefox - ten hlavičky přehledně zobrazí:</p>
<p align="center"><a href='http://blog.novoj.net/binary//2007/07/firebug.png' title='Firebug snapshot'><img src='http://blog.novoj.net/binary//2007/07/firebug.thumbnail.png' alt='Firebug snapshot' /></a></p>
<p>Bez něj bych nikdy nepřišel na to, že přestože můj servlet do hlaviček zapisuje do hlaviček informace o cachování, Tomcat s Apachem je vesele přenastavují po svém.</p>
<h3>Související odkazy</h3>
<ul>
<li><a href="http://support.microsoft.com/default.aspx?scid=kb;en-us;812935&Product=ie600" target="_new">záznam o chybě v KB Microsoftu</a></li>
<li><a href="http://forum.java.sun.com/thread.jspa?forumID=45&threadID=233446" target="_new">záznam v KB Sunu</a></li>
<li><a href="http://www.symphonious.net/2007/06/19/caching-in-tomcat/" target="_new">článek o tom, jak vypnout automatické nastavování "no-cache" v Tomcatu</a></li>
<li><a href="http://vanrees.org/weblog/archive/2007/02/22/ie-https-download-problem" target="_new">blog popisující stejný problém</a></li>
<li><a href="http://downside.ch/blog/?p=26" target="_new">další záznam na blogu o tomto problému - tentokrát rozkrývá něco z pozadí této chyby</a></li>
</ul>
