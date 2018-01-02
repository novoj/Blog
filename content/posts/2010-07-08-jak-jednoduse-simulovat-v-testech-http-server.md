---
status: publish
published: true
title: Jak jednoduše simulovat v testech HTTP server
author:
  display_name: Jety
  login: jetik
  email: mail@jetensky.net
  url: http://jetensky.net
author_login: jetik
author_email: mail@jetensky.net
author_url: http://jetensky.net
excerpt: "<div style=\"border: 1px solid white; background-color: #333333; font-size:
  90%; margin-top: 20px;\">\r\n\r\n<a title=\"Pavel Jetensky\" href=\"http://jetensky.net/download/files/Selenium%20testovani%20-%20zaklady.mp3\"><img
  style=\"margin-left: 10px; margin-right: 10px;\" src=\"http://blog.novoj.net/binary/2008/09/pavel.jpg\"
  alt=\"Pavel Jetensky\" width=\"49\" height=\"62\" align=\"left\" /></a>\r\n\r\n<strong>O
  autorovi: </strong><a href=\"http://jetensky.net/blog\">Jetyho blog</a> | <a href=\"http://www.linkedin.com/in/paveljetensky\">LinkedIn</a>\r\n<p
  style=\"margin: 10px;\">Pavel Jetenský se věnuje Java/J2EE vývoji již od roku 2003,
  z toho několik let v Irsku. Zajímají ho techniky automatického testování. V současné
  době pracuje jako metodický vedoucí Java/J2EE v Deltax Systems a.s.</p>\r\n</div>\r\n\r\nObčas
  při tvorbě automatických testů potřebujeme otestovat funkcionalitu, která stahuje
  nějaká data z Internetu. V mém případě to byla funkce na stahování seznamu zneplatněných
  certifikátů (CRL). Původně jsem měl automatický test napsaný tak, že se seznam skutečně
  stahoval. To bylo nevýhodné ze dvou důvodů:\r\n\r\n<ul>\r\n\t<li>test nefungoval
  bez připojení k internetu</li>\r\n\t<li>těžko šlo ovlivnit v rámci testu stahovaná
  data</li>\r\n</ul>\r\n\r\nNapsal jsem si tedy jednoduchou implementaci HTTP serveru,
  která publikuje soubory z classpath pod stejnou relativní cestou na localhost adrese.
  Např. soubor s CRL umístěný v src\\test\\resources\\crl\\emptyCrl.crl je po spuštění
  serveru ke stažení na:\r\n\r\n<a href=\"#\">http://localhost:8001/ResourcePublishServer/crl/emptyCrl.crl</a>\r\n\r\n"
wordpress_id: 947
wordpress_url: http://blog.novoj.net/?p=947
date: '2010-07-08 06:06:52 +0200'
date_gmt: '2010-07-08 05:06:52 +0200'
categories:
- Programování
- Testování
- Web
tags:
- HttpServer
- mock
- simulate
- download
- JDK 1.6
- unit testing
- jUnit
comments:
- id: 23864
  author: Petr
  author_email: hanys.petr@gmail.com
  author_url: ''
  date: '2010-07-12 14:04:42 +0200'
  date_gmt: '2010-07-12 13:04:42 +0200'
  content: Možná hloupý dotaz - proč bylo potřeba psát vlastní HTTP server a nepoužít
    pro testování např. Jetty?
- id: 23865
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-07-12 14:22:51 +0200'
  date_gmt: '2010-07-12 13:22:51 +0200'
  content: "Odpovím za Jetyho - žádný HTTP Server se v daném řešení nepíše. Jen se
    využívá existující třídy HttpServer, která je v JDK 6. Přiložené třídy jsou jen
    supportní obal pro jednoduché použití v automatických testech.\r\n\r\nToto řešení
    je v podstatě ekvivalentní použití např. Jetty kontejneru - jen je daleko lehčí
    a zároveň není nutné k projektu linkovat další dependency."
- id: 48974
  author: Myšlenky dne otce Fura &raquo; Blog Archive &raquo; jOpenSpace 2011 &#8211;
    audio z bleskových přednášek
  author_email: ''
  author_url: http://blog.novoj.net/2011/08/16/jopenspace-2011-audio-z-bleskovych-prednasek/
  date: '2011-08-16 20:38:18 +0200'
  date_gmt: '2011-08-16 19:38:18 +0200'
  content: "[...] Remote Skype Notifications, Josef CacekKaždá akce si vyžádá adekvátní
    protiakci a tak zakázání Skype ve vašem firemním prostředí povede pouze k tomu,
    že si šikovní lidé vymyslí šikovné nástroje, jak zákaz s grácií obejít. V tomto
    podcastu se dozvíte o možnosti jak jednoduše tunelovat komunikaci z virtualizovaného
    prostředí do vašeho primárního systému &#8211; a bude stačit pouze Java 6 a HttpServer,
    o kterém jsme tu již kdysi hovořili. [...]"
---
<div style="border: 1px solid white; background-color: #333333; font-size: 90%; margin-top: 20px;">
<p><a title="Pavel Jetensky" href="http://jetensky.net/download/files/Selenium%20testovani%20-%20zaklady.mp3"><img style="margin-left: 10px; margin-right: 10px;" src="http://blog.novoj.net/binary/2008/09/pavel.jpg" alt="Pavel Jetensky" width="49" height="62" align="left" /></a></p>
<p><strong>O autorovi: </strong><a href="http://jetensky.net/blog">Jetyho blog</a> | <a href="http://www.linkedin.com/in/paveljetensky">LinkedIn</a></p>
<p style="margin: 10px;">Pavel Jetenský se věnuje Java/J2EE vývoji již od roku 2003, z toho několik let v Irsku. Zajímají ho techniky automatického testování. V současné době pracuje jako metodický vedoucí Java/J2EE v Deltax Systems a.s.</p>
</div>
<p>Občas při tvorbě automatických testů potřebujeme otestovat funkcionalitu, která stahuje nějaká data z Internetu. V mém případě to byla funkce na stahování seznamu zneplatněných certifikátů (CRL). Původně jsem měl automatický test napsaný tak, že se seznam skutečně stahoval. To bylo nevýhodné ze dvou důvodů:</p>
<ul>
<li>test nefungoval bez připojení k internetu</li>
<li>těžko šlo ovlivnit v rámci testu stahovaná data</li>
</ul>
<p>Napsal jsem si tedy jednoduchou implementaci HTTP serveru, která publikuje soubory z classpath pod stejnou relativní cestou na localhost adrese. Např. soubor s CRL umístěný v src\test\resources\crl\emptyCrl.crl je po spuštění serveru ke stažení na:</p>
<p><a href="#">http://localhost:8001/ResourcePublishServer/crl/emptyCrl.crl</a></p>
<p><a id="more"></a><a id="more-947"></a></p>
<p>Moje řešení obsahuje dvě třídy: <i>ResourcePublishServer.java</i> a <i>ResourceToResponseHandler.java</i> a využívá HTTP server, který se nově objevil v JDK 1.6 (viz. <a href="http://download.oracle.com/docs/cd/E17409_01/javase/6/docs/jre/api/net/httpserver/spec/com/sun/net/httpserver/HttpsServer.html" target="_blank">JavaDoc k HttpServer.create</a>).</p>
<p><a title="2 ResourcePublishServer třídy v ZIP souboru" href="http://jetensky.net/download/files/ResourcePublishServer.zip">Třídy ke stažení</a> (ZIP)</p>
<p><strong>Pozn.: </strong>Třídy jsou nyní závislé na Spring aplikačním kontextu, ale drobnou úpravou (nahrazením volání applicationContext.getResources za getClass().getResourceAsStream) by je šlo použít i tam, kde Spring není.</p>
<h2>Ukázka použití serveru v testu</h2>
<p>Pozn.: Stažené CRL, které se použije v testu, je uložené v CVS (tj. není přiloženo k ukázkovým třídám) ve složce <i>src\test\resources\crl\kcanbusr3.crl</i>.</p>
<p>[source lang="java"]<br />
import ResourcePublishServer server;</p>
<p>public class ExampleTest extends TestCase {<br />
   private CrlJob crlJob = new CrlJob();</p>
<p>   @Override<br />
   protected void onSetUp() throws Exception {<br />
    server = new ResourcePublishServer(applicationContext);<br />
    server.start();<br />
    super.onSetUp();<br />
   }</p>
<p>   @Override<br />
   protected void onTearDown() throws Exception {<br />
    server.stop();<br />
    super.onTearDown();<br />
   }   </p>
<p>   public void testDownloadCrl() throws Exception {<br />
    String crlAsResourceUrl = server.calculateUrl("/crl/kcanbusr3.crl");</p>
<p>    // Vytvorime si certifikacni autoritu s CRL adresou ukazujici na testovaci HTTP server<br />
    IAuthorityBo auth = authorityTestData.createWithCrlUrl(crlAsResourceUrl);<br />
    crlJob.executeInternal();<br />
    assertEquals(1, crlDao.find(auth).size());<br />
   }<br />
}<br />
[/source]</p>
