---
status: publish
published: true
title: Ochrana emailových adres před SpamBoty
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Nedávno na jednom připomínkovacím sezení mě zákazník překvapil přáním, že
  bych chtěl chránit své emailové adresy uvedené v kontaktech jako &lt;a href=\"mailto:blabla@blabla.cz\"/&gt;
  proti zneužití spamboty. Jedná se o poměrně jednoduché přání, se kterým jsem se
  ale ve své praxi setkal poprvé. Obvykle, většina z nás akceptuje toto riziko výměnou
  za to, že naši zákazníci jednoduše kliknou na odkaz a otevře se jim rovnou jejich
  mailový klient s předvyplněnou adresou. Ihned nás napadlo vyměnit mailto linky za
  emaily vepsané např. do obrázku, ale to bychom přišli o tu výhodu jednoduchého otevření
  mailového klienta s adresou. Nicméně jednání jsme ukončili s vědomím, že si klient
  bude muset vybrat jedno nebo druhé. Nakonec mi to ale stejně nedalo a zkusil jsem
  pana gůgla ...\r\n\r\n"
wordpress_id: 22
wordpress_url: http://blog.novoj.net/2007/07/19/ochrana-emailovych-adres-pred-spamboty/
date: '2007-07-19 20:40:57 +0200'
date_gmt: '2007-07-19 19:40:57 +0200'
categories:
- Web
tags: []
comments:
- id: 226
  author: Filip Jirsák
  author_email: filip@jirsak.org
  author_url: ''
  date: '2007-07-20 06:28:51 +0200'
  date_gmt: '2007-07-20 05:28:51 +0200'
  content: JavaScriptovou náhradu lze kombinovat s nahrazením částí e-mailové adresy
    jejich slovním popisem. Např. tedy uvedu e-mail "mail (at) example (dot) com"
    a následně všechny e-maily projedu JavaScriptem a ".*\(at\).*" nahradím zavináčem,
    ".*\(dot\).*" nahradím tečkou. Uživatelé bez JS to pochopí, a uživatelé s JS dostanou
    klasický e-mail.
- id: 230
  author: true.pako
  author_email: true.pako@gmail.com
  author_url: ''
  date: '2007-07-23 09:49:27 +0200'
  date_gmt: '2007-07-23 08:49:27 +0200'
  content: "Stejne tak jako vetsina spambotu ;-)\r\nPekne reseni je kontaktni formular,
    ale kdyz uz je proste potreba e-mailova adresa, tak se musi pocitat i se spamem..."
- id: 232
  author: Honza Novotný
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2007-07-23 20:34:45 +0200'
  date_gmt: '2007-07-23 19:34:45 +0200'
  content: Řekl bych, že v případě použití (at) a (dot), spamboti emaily získají -
    přeci jenom už to je dost profláklý způsob ochrany. Pokud však použijeme hezky
    česky (zavináč) a (tečka), tak si myslím, že se většina spambotů jde klouzat (i
    když si umím představit heuristický algoritmus, který dokáže najít tyhle patterny
    bez ohledu na jazyk). Je pár věcí, které mám na češtině docela rád (a vždy si
    je připomínám, když řeším problémy s kódováním ;) ) - a to jsou právě tyto - češtinu
    prostě skoro nikdo nezná.
---
<p>Nedávno na jednom připomínkovacím sezení mě zákazník překvapil přáním, že bych chtěl chránit své emailové adresy uvedené v kontaktech jako &lt;a href="mailto:blabla@blabla.cz"/&gt; proti zneužití spamboty. Jedná se o poměrně jednoduché přání, se kterým jsem se ale ve své praxi setkal poprvé. Obvykle, většina z nás akceptuje toto riziko výměnou za to, že naši zákazníci jednoduše kliknou na odkaz a otevře se jim rovnou jejich mailový klient s předvyplněnou adresou. Ihned nás napadlo vyměnit mailto linky za emaily vepsané např. do obrázku, ale to bychom přišli o tu výhodu jednoduchého otevření mailového klienta s adresou. Nicméně jednání jsme ukončili s vědomím, že si klient bude muset vybrat jedno nebo druhé. Nakonec mi to ale stejně nedalo a zkusil jsem pana gůgla ...</p>
<p><a id="more"></a><a id="more-22"></a></p>
<p>Samozřejmě jsem přišel na to, že nejsem první koho se takhle zákazník zeptal. Žádné stoprocentně účinné řešení neexistuje - každé má svá pro a proti (kromě řešení, kdy email skryjete úplně a nahradíte ho formulářem, který uživatel vyplní a odešle email prostřednictvím vašich stránek) a většina z řešení je jednoduše založena na pasivní ochraně a jednoduchém pravidlu, které v přírodě už platí staletí. Predátoři si většinou vybírají ty snadné úlovky.</p>
<p>Jedním z nejjednodušších způsobů je zakrýt důležité fragmenty emailové adresy na stránce a tím je znak @ a "mailto:" a to tak, aby při prostém zobrazení zdrojového textu se tam tento řetězec nevyskytoval, nicméně prohlížeč ho interpretoval správně. Což je možné jednoduše provést převodem řetězce do hexadecimální iterpretace. Tento způsob vyřadí asi jen ty nejhloupější spamboty.</p>
<p>Jiným způsobem je sestavení cílové emailové adresy JavaScriptem (čímž ovšem znepřístupníme emailovou adresu lidem s vypnutím JavaScriptem. Toto už je asi poměrně účinná obrana, jelikož při množství prohlížených stránek se už spambotům dost pravděpodobně nevyplatí interpretovat JavaScript. I když věřím, že i tato obrana lze překonat.</p>
<p>Souhrnně by se dalo říct, že cokoliv je lepšího jak nic. Stejné principy přeci spolehlivě zabírají např. v šíření virů - aneb jen tím, že místo Exploreru používáte třebas méně rozšířený Firefox nebo Operu, místo majoritního OS jako jsou Windows používáte třeba Ubuntu nebo MacOS se zařadíte do té minoritní skupiny, kterou se útočníkům nevyplatí napadat - mají přeci spoustu dalších jednodušších cílů.</p>
<p>Prostě, skoro bych si tipnul, že to funguje, i když je to obtížně prokazatelné. Rozhodně to bylo zajímavé čtení, které mi vyplnilo polední "obědovou" siestu. Existují totiž i aktivní obrany jako jsou např. BotTrapy - no prostě některé taktiky se čtou jako detektivka :) . Pro ty koho to zajímá nabízím pár odkazů:</p>
<ul>
<li><a href="http://labnol.blogspot.com/2006/03/hide-your-email-address-on-websites.html" target="_new">základní úvod do problematiky</a></li>
<li> <a href="http://labnol.blogspot.com/2006/03/hide-your-email-address-on-websites.html" target="_new">na této stránce už najdete poměrně slušný výčet triků</a></li>
<li> <a href="http://www.turnstep.com/Spambot/" target="_new">hezký úvod do problematiky spamování</a> zajímavá je kapitola <a href="http://www.turnstep.com/Spambot/harassment.html" target="_new">s odkazy na tzv. spambot trapy</a></li>
</ul>
