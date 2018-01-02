---
status: publish
published: true
title: Ruční aktualizace firmware Asus Transformer Infinity Pad
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft  wp-image-2365\" title=\"android-upgrade\" src=\"http://blog.novoj.net/binary/2012/10/android-upgrade-300x214.jpg\"
  alt=\"\" width=\"144\" height=\"102\" />Docela mě překvapilo, že ani měsíc od vydání
  aktualizace Jelly Bean pro Asus Infinity Pad se mi nenabídla aktualizace systémem
  sama. Při ručním zkontrolování aktualizací v nastavení systému se mi tvrdošíjně
  vracelo, že \"nové aktualizace pro váš systém neexistují\". Kecy ... někde byla
  nějaká chybka, která znemožňovala OTA, přestože ty už byly dávno dostupné. Sedl
  jsem k internetu a po docela dlouhé době jsem přišel na postup, jak tablet zaktualizovat
  manuálně. Abych vám ušetřil tuhle práci, zachytil jsem postup v tomto článku.\r\n\r\n"
wordpress_id: 2363
wordpress_url: http://blog.novoj.net/?p=2363
date: '2012-10-25 19:32:47 +0200'
date_gmt: '2012-10-25 18:32:47 +0200'
categories:
- Android
tags:
- jelly bean
- manual upgrade
- asus infinity pad
comments:
- id: 101423
  author: Martin
  author_email: djax@djax.cz
  author_url: ''
  date: '2012-10-25 20:21:59 +0200'
  date_gmt: '2012-10-25 19:21:59 +0200'
  content: Jsem rád, že jsem se Transformeru už dávno zbavil a něco podobného nemusím
    teď na iPadu řešit...
- id: 101433
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-10-25 21:26:39 +0200'
  date_gmt: '2012-10-25 20:26:39 +0200'
  content: |-
    Jo, jo - iPad je sice boží, ale já už jsem na Androidu moc závislej ;)

    Btw. mám ten dojem, že ještě donedávna Apple family OTA vůbec neuměla, takže opatrně s tou kritikou :) :) :)
- id: 101491
  author: k.
  author_email: kmoravec@gmail.com
  author_url: ''
  date: '2012-10-26 04:58:01 +0200'
  date_gmt: '2012-10-26 03:58:01 +0200'
  content: 'Když již předřečník načal téma bezproblémové OTA update: stejně to funguje
    na originálních Google Nexus výrobcích (v případě tabletu Nexus 7, nyní na 4.1.2).
    Výborný hw pro ty, kteří to myslí s Android OS vážně.'
- id: 101528
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-10-26 07:23:16 +0200'
  date_gmt: '2012-10-26 06:23:16 +0200'
  content: No já to s Androidem taky myslím vážně :) ... ale pravda je, že ten Infinity
    Pad je úplně o jiných penězích. V porovnání s tím je Nexus 7 na cena / výkon zcela
    nepřekonatelný ... jenže na druhou stranu 10" display je 10" display :)
- id: 101622
  author: Tomáš
  author_email: Ounil@seznam.cz
  author_url: http://
  date: '2012-10-26 17:08:04 +0200'
  date_gmt: '2012-10-26 16:08:04 +0200'
  content: Nevím proč z toho děláte takovou detektivku mě OTA také nejde dal jsem
    to vědět asusu ten mi doporučil reklamaci. Osobně jsem důvod neviděl a nedal jsem
    jej, aktualizace provádím pouze manuálně má to své výhody. A iPad a iOS má taky
    svoje mouchy.A taky stačí navštívit androidforum.cz
---
<p><img class="alignleft  wp-image-2365" title="android-upgrade" src="http://blog.novoj.net/binary/2012/10/android-upgrade-300x214.jpg" alt="" width="144" height="102" />Docela mě překvapilo, že ani měsíc od vydání aktualizace Jelly Bean pro Asus Infinity Pad se mi nenabídla aktualizace systémem sama. Při ručním zkontrolování aktualizací v nastavení systému se mi tvrdošíjně vracelo, že "nové aktualizace pro váš systém neexistují". Kecy ... někde byla nějaká chybka, která znemožňovala OTA, přestože ty už byly dávno dostupné. Sedl jsem k internetu a po docela dlouhé době jsem přišel na postup, jak tablet zaktualizovat manuálně. Abych vám ušetřil tuhle práci, zachytil jsem postup v tomto článku.</p>
<p><a id="more"></a><a id="more-2363"></a></p>
<p>Nakonec ten postup není zase tak složitý:</p>
<h3>1. zjistěte jakou verzi firmware máte</h3>
<p>Existují různé varianty firmware určené pro různé regiony - koukněte se do stavu systému (Nastavení -&gt; Informace o tabletu -&gt; Číslo sestavení) na to, jakou regionální mutaci budete mít - já mám aktuálně <em>JRO03C.<strong>WW</strong>_epad-10.4.4.18-20121012</em>. Česká verze spadá pod prefix WW.</p>
<h3>2. stáhněte aktualizace</h3>
<p>Podle <a href="http://www.technobloom.com/asus-transformer-prime-and-infinity-manual-jelly-bean-update/2217610/" target="_blank">jednoho článku</a> je doporučováno před aktualizací na novou verzi systému (tj. např. z ICS 4.0.X na Jelly Bean 4.1.X) nejdříve zaktualizovat systém na nejposlednější patch v dané verzi. V mém případě jsem měl verzi firmware 9.4.5.22, poslední patch v dané verzi byl 9.4.5.30 a JellyBean verze byla 10.4.4.18.</p>
<p>V mém případě jsem tedy <a href="http://support.asus.com/download.aspx?SLanguage=en&amp;p=20&amp;s=16&amp;m=ASUS+Transformer+Pad+Infinity+TF700T&amp;os=" target="_blank">stáhl ze supportních stránek</a> dva aktualizační balíčky:</p>
<ol>
<li>WW_epad_user_9_4_5_30_20120907_UpdateLauncher.zip</li>
<li>WW_epad_user_10_4_4_18_UpdateLauncher.zip</li>
</ol>
<h3>3. nakopírujte aktualizační balíček na root sd karty a instalujte</h3>
<ol>
<li>Stažený ZIP rozbalte a uvidíte v něm ještě jeden zip.</li>
<li>Ten vnitřní zip nakopírujte do tabletu do kořenové složky SD karty - tj. /sdcard (není třeba soubor ani přejmenovávat).</li>
<li>Vyrestartujte tablet.</li>
<li>Po naběhnutí uvidíte v notifikační liště systémovou zprávu, že byl na disku nalezen nový aktualizační balíček.</li>
<li>Klikněte na danou zprávu a v dialogu potvrďte, že jej chcete nainstalovat.</li>
</ol>
<div>Totéž proveďte s druhým balíčkem a máte zaktualizováno na Jelly Bean!</div>
<h2>Zdroje</h2>
<ul>
<li><a href="http://www.technobloom.com/asus-transformer-prime-and-infinity-manual-jelly-bean-update/2217610/" target="_blank">ASUS Transformer prime and Infinity manual Jelly Bean update</a></li>
<li><a href="http://www.ibtimes.co.uk/articles/388146/20120926/official-update-asus-transformer-pad-infinity-install.htm" target="_blank">How to Update Asus Transformer Pad Infinity TF700T Officially To Latest Firmware</a></li>
<li><a href="http://support.asus.com/download.aspx?SLanguage=en&amp;p=20&amp;s=16&amp;m=ASUS+Transformer+Pad+Infinity+TF700T&amp;os=" target="_blank">Asus Support - stažení aktualizací</a></li>
</ul>
