---
status: publish
published: true
title: Vyhodnocení iBatis 3 Workshopu
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Tento týden proběhl workshop na téma iBatis 3 v Národní technické knihovně.
  Na workshopu jsem vyhlásil soutěž o licenci vývojového prostředí IntelliJ Idea 9
  - Ultimate Edition a v tomto příspěvku najdou soutěžící jak moji verzi řešení příkladů,
  tak i výsledné vyhodnocení. Kompletní řešení všech testů, které jsme v průběhu workshopu
  probírali najdete v GitHub repository na stejném místě jako původně (stačí si \"pullnout\"
  novou verzi zdrojových kódů):\r\n\r\n<div align=\"right\"><b>Sponzor přednášky:</b><br><a
  href=\"http://blog.novoj.net/binary/2010/03/logo_jetbrains1.png\"><img src=\"http://blog.novoj.net/binary/2010/03/logo_jetbrains1.png\"
  alt=\"\" title=\"logo_jetbrains\" width=\"120\" height=\"46\" class=\"alignright
  size-full wp-image-839\" /></a></div>\r\n\r\n<ul>\r\n   <li>GIT klient: git://github.com/novoj/iBatisWorkShop.git</li>\r\n
  \  <li>HTTP: <a href=\"http://github.com/novoj/iBatisWorkShop/tree/master\" target=\"_blank\">http://github.com/novoj/iBatisWorkShop/tree/master</a><br>(v
  menu odkaz Download sources)</li>\r\n</ul>\r\n\r\nDěkuji ještě jednou všem, kdo
  si našli cestu na seminář a kdo se i po něm za mnou zastavili a řekli mi svůj názor
  na jeho formu a průběh (speciální díky patří <a href=\"http://vsadnajavu.cz/2010-03/databaze/ibatis-3-workshop/\"
  target=\"_blank\">chlapcům z MoroSystems za jejich příspěvek na blogu</a>). Není
  totiž horší pocit než, když se jako přednášející dobu potíte vedle projektoru, pak
  se publikum potichu rozuteče a vy odcházíte z rozpačitým pocitem a otázkou, jestli
  to nakonec mělo smysl. Jsem rád, že, pokud nic jiného, tenhle workshop nějaké emoce
  vyvolal a ke konci za mnou zašlo hodně lidí, a měl jsem šanci si udělat obrázek
  o tom, jestli jsem to vzal za ten správný konec.\r\n\r\n"
wordpress_id: 819
wordpress_url: http://blog.novoj.net/?p=819
date: '2010-03-05 22:00:48 +0100'
date_gmt: '2010-03-05 21:00:48 +0100'
categories:
- Programování
- Java
- Reportáže
- iBatis
tags: []
comments:
- id: 20696
  author: Radek Teichmann
  author_email: radek.teichmann@morosystems.cz
  author_url: http://www.vsadnajavu.cz
  date: '2010-03-05 23:41:58 +0100'
  date_gmt: '2010-03-05 22:41:58 +0100'
  content: Tak to je velmi hezké a opravdu velké překvapení. Moc díky jak za licenci
    tak za kvalitní workshop. Už se těším až někdě iBatis 3 použijeme :)
- id: 20775
  author: Tomáš Procházka
  author_email: atom@atomsoft.cz
  author_url: ''
  date: '2010-03-07 15:58:43 +0100'
  date_gmt: '2010-03-07 14:58:43 +0100'
  content: Bohužel jsem se na workshop nedostal, s iBatisem si už ale nějakou dobu
    hraju. Určitě by bylo super, kdyby se někde zveřejnili zdrojové kódy ukázkových
    úloh, ale to asi až poté, co proběhne přednáška v Ostravě a v Hradci.
- id: 20786
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-03-07 20:23:39 +0100'
  date_gmt: '2010-03-07 19:23:39 +0100'
  content: Zdrojové kódy jsou již zveřejněny - viz. začátek tohoto článku. Stačí si
    je stáhnout z GitHubu.
- id: 20787
  author: Tomáš Procházka
  author_email: atom@atomsoft.cz
  author_url: ''
  date: '2010-03-07 21:51:04 +0100'
  date_gmt: '2010-03-07 20:51:04 +0100'
  content: ":-) To bude tím, jak mě dnes celý den bolí hlava, asi z přepracování,
    než jsem to dočetl do konce, zapomněl jsem, že na začátku byla zmínka o řešení
    všech úloh :-)"
- id: 21727
  author: Martin Bednář
  author_email: xxbedy@gmail.com
  author_url: ''
  date: '2010-04-08 14:18:02 +0200'
  date_gmt: '2010-04-08 13:18:02 +0200'
  content: "Pochopil jsem z diskuse správně, že tuto přednášku chystáte i v Ostravě
    ?\r\nKdy a kde bude ?\r\nDiky"
- id: 21739
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-04-09 07:32:50 +0200'
  date_gmt: '2010-04-09 06:32:50 +0200'
  content: "Bohužel v Ostravě se nic nechystá. Přednáška ještě jednou proběhla v Praze
    na ČVUT a potom v Hradci Králové na UHK. Nikdo další mě prozatím neoslovil ...\r\n\r\nMinimálně
    jsou tedy k dispozici zdrojové kódy s řešeními."
---
<p>Tento týden proběhl workshop na téma iBatis 3 v Národní technické knihovně. Na workshopu jsem vyhlásil soutěž o licenci vývojového prostředí IntelliJ Idea 9 - Ultimate Edition a v tomto příspěvku najdou soutěžící jak moji verzi řešení příkladů, tak i výsledné vyhodnocení. Kompletní řešení všech testů, které jsme v průběhu workshopu probírali najdete v GitHub repository na stejném místě jako původně (stačí si "pullnout" novou verzi zdrojových kódů):</p>
<div align="right"><b>Sponzor přednášky:</b><br><a href="http://blog.novoj.net/binary/2010/03/logo_jetbrains1.png"><img src="http://blog.novoj.net/binary/2010/03/logo_jetbrains1.png" alt="" title="logo_jetbrains" width="120" height="46" class="alignright size-full wp-image-839" /></a></div>
<ul>
<li>GIT klient: git://github.com/novoj/iBatisWorkShop.git</li>
<li>HTTP: <a href="http://github.com/novoj/iBatisWorkShop/tree/master" target="_blank">http://github.com/novoj/iBatisWorkShop/tree/master</a><br>(v menu odkaz Download sources)</li>
</ul>
<p>Děkuji ještě jednou všem, kdo si našli cestu na seminář a kdo se i po něm za mnou zastavili a řekli mi svůj názor na jeho formu a průběh (speciální díky patří <a href="http://vsadnajavu.cz/2010-03/databaze/ibatis-3-workshop/" target="_blank">chlapcům z MoroSystems za jejich příspěvek na blogu</a>). Není totiž horší pocit než, když se jako přednášející dobu potíte vedle projektoru, pak se publikum potichu rozuteče a vy odcházíte z rozpačitým pocitem a otázkou, jestli to nakonec mělo smysl. Jsem rád, že, pokud nic jiného, tenhle workshop nějaké emoce vyvolal a ke konci za mnou zašlo hodně lidí, a měl jsem šanci si udělat obrázek o tom, jestli jsem to vzal za ten správný konec.</p>
<p><a id="more"></a><a id="more-819"></a></p>
<p>Když si to zpětně promítám, přiznávám, že jsem postupoval poměrně svižně - nenechal jsem moc prostoru na zotavení, v podstatě to byl takový 1.5 hodinový maratón v kódování. Jak říkal Dagi, pro někoho to mohlo být trošku moc rychlé, zvlášť, když se třeba v některé části zasekl. Nicméně lidé, kteří se u mě stavovali po přednášce shodně říkali, že více méně stíhali, takže jsem to snad moc nepřestřelil. Osobně nemám moc rád přednášky, kde přednášející postupuje příliš pomalu a já mám čas se nudit. Z toho důvodu se svoje přednášky snažím dělat takové, aby člověk, kterého téma zajímá, čas na nudu neměl.</p>
<div align="center">
<a href="http://blog.novoj.net/binary/2010/03/prednaska-ibatis.jpg"><img src="http://blog.novoj.net/binary/2010/03/prednaska-ibatis-300x225.jpg" alt="" title="prednaska-ibatis" width="300" height="225" class="aligncenter size-medium wp-image-820" /></a><br><br />
Foto: http://vsadnajavu.cz/
</div>
<p>Nuže, přikročme k vyhodnocení soutěže. Ve stanoveném termínu došlo 7 řešení (v pořadí, jak došly):</p>
<ol>
<li>Tomáš Záluský - řešení ok</li>
<li>Radek Teichmann - řešení ok</li>
<li>Jaromír Vajgert - řešení ok</li>
<li>Petr Masopust - řešení ok (možná až trošku extrémní minimalizace ZIPu, trošku mě to potrápilo, než jsem to dal do kupy ;-) )</li>
<li>Jiri Samek - řešení ok (TypeHandlery možno registrovat centrálně v MapperConfig.xml)</li>
<li>Vojtěch Krása - řešení ok</li>
</ol>
<p>Vyřazeno:</p>
<ol>
<li>Tomas Bublik - vyřazuji ze soutěže z důvodu neimplementování UserMapper.xml logiky pro test F_UserMapperTest</li>
</ol>
<p>Ze sedmi soutěžících nám tedy zůstalo pouze šest. Přemýšlel jsem, jak provést prokazatelně objektivní hlasování, ale žádný jednoduchý způsob mě nenapadl. Proto, doufám, budete věřit mé nestrannosti a objektivnímu vylosování výherce. Použil jsem veřejný generátor náhodných čísel (<a href="http://www.random.org/" target="_blank">http://www.random.org/</a>), který mi vylosoval číslo <b>2</b> a licenci IntelliJ Idey vyhrává </p>
<div align="center">
<b>Radek Teichmann</b>
</div>
<p>Ještě dnes odesílám email Romanovi Štroblovi a Václavu Pechovi z JetBrains, aby ti, Radku, poslali tvoje licenční číslo pro Ideu.</p>
<p>Pokud jste se někdo nedostal na tento workshop a měli zájem se přeci jen o iBatisu něco dozvědět, budu jej opakovat ještě na konci března na ČVUT v předmětu <a href="http://service.felk.cvut.cz/courses/X36SWT/prednasky.html" target="_blank">Softwarové technologie</a> a v prozatím neupřesněném termínu na Univerzitě Hradec Králové. Kdyžtak mi tedy napište na email a já bych se pokusil dohodnout nějaké to místo navíc.</p>
