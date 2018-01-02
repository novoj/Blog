---
status: publish
published: true
title: Automatické testování odeslání emailu
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<p>Jistě jste také už mnohokrát, stejně jako já, řešili problém, jak spolehlivě
  automaticky otestovat, že vaše aplikace správně odeslala email s konkrétním obsahem
  na konkrétní emailovou adresu. Problém je to zapeklitý a dosud jsem ho dokázal řešit
  jen těmito způsoby:</p>\r\n<ul>\r\n   <li>udáním testovací schránky a automatickým
  výběrem této schránky (např. přes protokol POP3)</li>\r\n   <li>vytvořením mock
  objektu, který mi zastoupil třídu starající se o odeslání emailu (tzn. k žádnému
  emailu fyzicky v testu nedošlo)</li>\r\n</ul>\r\n<p>Oba dva přístupy mají svá úskalí.
  Ten první velmi komplikuje běh testu - musíme naprogramovat další funkcionalitu,
  která nám vybere emaily jiným protokolem, musíme řešit možnost, že se email někde
  pozdrží, musíme fyzicky nějakou schránku mít, musíme vyřešit to, jak při opakovaném
  spouštění testů rozeznáme, že do schránky přišel právě ten mail, na kterém v testu
  čekáme. Fakticky se potom často stane, že v testu samotném je víc chyb, jak v tom
  jednoduchém kódu, který se snažíme otestovat.</p>\r\n<p>Druhý přístup je jednodušší
  a test s ním obvykle po vyladění spolehlivě prochází. Nicméně tento přístup nezaručuje,
  že v reálném nasazení,kdy místo mock objektu, bude skutečný objekt zajišťujicí odeslání
  emailu nedojde k chybě (např. díky tomu, že náš mock objekt nedostatečně dobře imituje
  chování reálného objektu).</p>\r\n<p>Do této doby jsem tedy odesílání emailů ověřoval
  \"ručně\". Automatické testy sice odesílaly emaily, ale ty šly na moji schránku
  a v ní jsem zkontroloval, jestli očekávaný email v očekávané době došel. Skvělá
  věc, když spouštíte testy ručně, ovšem horší v případě, že vám testy spouští integrační
  server. To se vaše schránka pěkně plní a vy stejně nemáte šanci vyhodnotit, zda
  je vše jak má.</p>\r\n"
wordpress_id: 17
wordpress_url: http://blog.novoj.net/2007/05/31/automaticke-testovani-odeslani-emailu/
date: '2007-05-31 19:46:30 +0200'
date_gmt: '2007-05-31 18:46:30 +0200'
categories:
- Java
- Testování
tags: []
comments:
- id: 117
  author: Petr Ferschmann
  author_email: pferschmann@softeu.com
  author_url: http://blog.softeu.cz/
  date: '2007-06-01 07:39:24 +0200'
  date_gmt: '2007-06-01 06:39:24 +0200'
  content: Díky za tip. Tohle je jedna z těch věcí, které kdyby člověka napadly, že
    jdou takto dělat, už to dávno používá. Díky za otevření očí :-)
- id: 118
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-06-01 08:03:21 +0200'
  date_gmt: '2007-06-01 07:03:21 +0200'
  content: JJ, měl jsem úplně stejný pocit, když jsem to na OnJava objevil ;).
- id: 119
  author: Roman Dagi Pichlik
  author_email: pichlik@seznam.cz
  author_url: http://www.sweb.cz/pichlik/
  date: '2007-06-01 09:16:36 +0200'
  date_gmt: '2007-06-01 08:16:36 +0200'
  content: Presne tenhle pristup ukazuje, ze kdyz vyvojar chce, tak muze automaticky
    testovat prakitcky jakoukoliv cast sveho kodu a to i v pripade integracniho scenare
    s posilanim mailu. Skoda,ze ochota vyvojaru hledat reseni pro automatcike testy,
    jako je treba tento, je mala.  Kazdopadne diky, az mi zase nekdo bude tvrdit,
    jak je tezke neco podobneho testovat, tak mu tenhle clanek omplatim o hlavu ;-).
- id: 120
  author: Jety
  author_email: pavel.jetensky@seznam.cz
  author_url: http://jetensky.net
  date: '2007-06-01 09:28:15 +0200'
  date_gmt: '2007-06-01 08:28:15 +0200'
  content: Díky za užitečnou věcičku. Škoda, že zrovna teď nepotřebuju žádné odesílání
    otestovat, hned bych si to vyzkoušel. Však to časem určitě příjde :).
- id: 121
  author: Lukas
  author_email: lukas.vlcek@gmail.com
  author_url: http://blog.lukas-vlcek.com/
  date: '2007-06-01 14:23:39 +0200'
  date_gmt: '2007-06-01 13:23:39 +0200'
  content: Testovat odesilani emailu je krehkou zalezitosti, jako kazda jina komunikace
    se singletonem. Ten samy problem muze nasta pri komunikaci pres FTP napr.
- id: 122
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-06-01 14:44:45 +0200'
  date_gmt: '2007-06-01 13:44:45 +0200'
  content: Ano je to tak. Nicméně tento způsob se mi zdá poměrně stabilní a přesto
    vypovídající. Otázka je, jestli neexistuje v Javě také nějaká lightweight in memory
    implementace pro FTP stejně jako SubEthaSMTP Server pro maily. Pak by i pro FTP
    existovala rozumná cesta pro testování.
- id: 124
  author: Roman Dagi Pichlik
  author_email: pichlik@seznam.cz
  author_url: http://www.sweb.cz/pichlik/
  date: '2007-06-02 08:42:35 +0200'
  date_gmt: '2007-06-02 07:42:35 +0200'
  content: to Lukas&gt; urcite mi to prijde lepsi nez vyuziti mocku ci stubu, protoze
    ty mohou zvalidovat ciste jenom operaci, ale ne spravnost vysledku.
- id: 132
  author: benzin
  author_email: benzin@centrum.cz
  author_url: http://live.jabbim.cz/benzin
  date: '2007-06-05 16:03:52 +0200'
  date_gmt: '2007-06-05 15:03:52 +0200'
  content: "Coz jaksi nepomuze, protoze v realnem nasazeni muze napriklad dojit k
    tomu, ze nastavite SMTP server u ktereho druhy den spravce omezi pristum jenom
    na urcite IP adresy. Nebo Vas zkusebni SMTP server nevyvolava nektere vyjimky,
    ktere pak realny server vyvolat muze. Atp. atd.\r\n\r\nA cim se vlastne podstatne
    lisi tento vas SMTP server od Mock objektu? Nejedna se vlastne jenom o sofistifikovany
    Mock objekt?\r\n\r\nTim nechci rict, ze by tento clanek nebyl prinosny. Urcite
    je super, ze jste informoval o teto moznosti, jenom chci upozornit ze se jedna
    o sofistifikovany Mock objekt a v realnem nasazeni, muze vyvstat spousta dalsich
    problemu.\r\n\r\nBtw. ja takoveto problemy resim pouzitim prislusneho API, otestovani
    API a spoelhnutim na spravnost API. Tudiz napriklad na E-mail pouzivam springframwork,
    na to mam udelane testy. V aplikaci pak mockuju objekty tohoto api, ktere jsou
    vyrazne jednodussi.\r\n\r\nProtoze pouzite API sprigframeworku pozivam v stale
    stejne verzi, nejsem nucen delat testy na neho automatizovane, tak jak je tomu
    v aplikaci."
- id: 133
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-06-05 16:20:07 +0200'
  date_gmt: '2007-06-05 15:20:07 +0200'
  content: "No především SubEthaMail reálně implementuje SMTP protokol - tudíž pokud
    vám test projde, znamená to, že vaše aplikace odesílá emaily validně podle SMTP
    protokolu. Nastavení serveru je stejně věc, kterou v testovacím provozu odchytit
    nemůžete.\r\n\r\nWiser je defakto mock objekt - takže se od mock objektu nijak
    neliší. Na Wiseru vidím dvě základní výhody:\r\n\r\na) je to mock, který nemusíte
    psát - protože je už dobře napsán\r\nb) testuje druhou stranu rozhraní - tzn.
    otestuje vám, že jste skutečně správně odeslali email SMTP protokolem\r\nc) je
    to mock, který není závislý na implementaci odesílací strany rozhraní\r\n\r\nTaky
    používám SpringFramework, ale než si psát své mocky, radši použiji tenhle."
---
<p>Jistě jste také už mnohokrát, stejně jako já, řešili problém, jak spolehlivě automaticky otestovat, že vaše aplikace správně odeslala email s konkrétním obsahem na konkrétní emailovou adresu. Problém je to zapeklitý a dosud jsem ho dokázal řešit jen těmito způsoby:</p>
<ul>
<li>udáním testovací schránky a automatickým výběrem této schránky (např. přes protokol POP3)</li>
<li>vytvořením mock objektu, který mi zastoupil třídu starající se o odeslání emailu (tzn. k žádnému emailu fyzicky v testu nedošlo)</li>
</ul>
<p>Oba dva přístupy mají svá úskalí. Ten první velmi komplikuje běh testu - musíme naprogramovat další funkcionalitu, která nám vybere emaily jiným protokolem, musíme řešit možnost, že se email někde pozdrží, musíme fyzicky nějakou schránku mít, musíme vyřešit to, jak při opakovaném spouštění testů rozeznáme, že do schránky přišel právě ten mail, na kterém v testu čekáme. Fakticky se potom často stane, že v testu samotném je víc chyb, jak v tom jednoduchém kódu, který se snažíme otestovat.</p>
<p>Druhý přístup je jednodušší a test s ním obvykle po vyladění spolehlivě prochází. Nicméně tento přístup nezaručuje, že v reálném nasazení,kdy místo mock objektu, bude skutečný objekt zajišťujicí odeslání emailu nedojde k chybě (např. díky tomu, že náš mock objekt nedostatečně dobře imituje chování reálného objektu).</p>
<p>Do této doby jsem tedy odesílání emailů ověřoval "ručně". Automatické testy sice odesílaly emaily, ale ty šly na moji schránku a v ní jsem zkontroloval, jestli očekávaný email v očekávané době došel. Skvělá věc, když spouštíte testy ručně, ovšem horší v případě, že vám testy spouští integrační server. To se vaše schránka pěkně plní a vy stejně nemáte šanci vyhodnotit, zda je vše jak má.</p>
<p><a id="more"></a><a id="more-17"></a></p>
<h3>SubEthaSMTP Server</h3>
<p>A nyní přichází rozřešení mého dlouholetého problému. SubEthaSMTP Server je SMTP server napsaný v Javě, který má integrovanou podporu pro jednoduché testování a ten můj problém vyřešil.</p>
<p>V celém řešení není žádná záhada, fígl nebo vychytávka. V rámci svého testu si normálně spustíte vlastní instanci SMTP Serveru, která se bindne na konkrétní port a chová se jako klasický SMTP Server. Váš kód tedy fakticky email odešle - jen máte SMTP Server pod svojí kontrolou. Z instance SMTP Serveru si maily můžete jednoduše vyzvednout a nějak je zpracovat. V testech obvykle stačí jen ověřit, že nějaké došly a případně proklepnout jejich obsah.</p>
<p>Krásné na tom celém je to, že nasazení je naprosto směšně jednoduché. Stačí vám k tomu jen tyto věci:</p>
<ul>
<li>k projektu přilinkovat Wiser z projektu SubEthaMail - pro Maven 2 projekty stačí přidat dependency:<br><br />
   [source lang="xml"]<br />
   <dependency><br />
      <groupId>org.subethamail</groupId><br />
      <artifactId>subethasmtp-wiser</artifactId><br />
      <version>1.0.3</version><br />
      <scope>test</scope><br />
   </dependency><br />
   [/source]
   </li>
<li>pak už stačí jen napsat test:<br><br />
   [source lang="java"]<br />
   public void testResendActivationEmail() throws Exception {<br />
         Wiser wiser = new Wiser();<br />
         wiser.setPort(2500); // výchozí port je 25<br />
         wiser.start();<br />
         //tady spusťte metodu, která vyvolá odeslání emailu<br />
         //důležité je zajistit odesílání emailů přes SMTP server localhost:2500<br />
         wiser.stop()<br />
         //ověřte, že byl odeslán právě jeden mail<br />
         assertTrue("No messages arrived! No of messages = " + wiser.getMessages().size(), wiser.getMessages().size() == 1);<br />
         MimeMessage message = wiser.getMessages().get(0).getMimeMessage();<br />
         //ověříme třebas recipienta<br />
         assertEquals("pop@fg.cz", message.getRecipients(MimeMessage.RecipientType.TO)[0].toString());<br />
         //nebo předmět emailu<br />
         assertEquals("Aktivační email", message.getSubject());<br />
         //vyčístíme server od zpráv (další test může klidně recyklovat stejný objekt Wiseru)<br />
         wiser.getMessages().clear();<br />
   }<br />
   [/source]
   </li>
</ul>
<p>Prosté a funkční. Na tento způsob jsem narazil v článku <a href="http://www.onjava.com/pub/a/onjava/2007/03/23/using-groovy-to-send-emails.html" target="_new">Using Groovy to send email na OnJava</a> - možná jej řada z vás k testování této funkcionality používá, ale pro mne to byla cenná novinka.</p>
