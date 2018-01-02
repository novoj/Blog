---
status: publish
published: true
title: Monitoring Declarative Transactions in Spring, <br>bod pro Otce Fura
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
wordpress_id: 214
wordpress_url: http://blog.novoj.net/?p=214
date: '2008-12-09 06:50:33 +0100'
date_gmt: '2008-12-09 05:50:33 +0100'
categories:
- Java
tags: []
comments: []
---
<p>Nevím jak vy, ale já mám vždy radost, když někdo jiný nezávisle dojde ke stejným závěrům, jako jsem došel já sám. Osobně to považuji za jisté potvrzení smysluplnosti mých vlastních úvah a toho, že nejsem tak úplně "mimo mísu".</p>
<p>Dnes vyšel na java.DZone.com <a href="http://java.dzone.com/articles/monitoring-declarative-transac" target="_new">článek s názvem Monitoring Declarative Transactions in Spring</a> od Toma Celluciho, který se zabývá jednoduchým otestováním správného nastavení pointcutů při používání deklarativního nastavení transakcí ve Springu. Pokud si pamatujete, sám jsem tuto problematiku řešil před pár měsíci a publikoval <a href="http://blog.novoj.net/2008/09/20/testing-aspect-pointcuts-is-there-an-easy-way/">vlastní řešení</a> (a tak trochu mě zviklal Dagi, když se na něj na jOpenSpace moc netvářil).</p>
<p>Tom Celluci dochází ke stejnému závěru jako já a to je použití logovací funkcionality k otestování přítomnosti transakcí při volání metod v runtime. Bod v kterém se rozcházíme je ten, jak ověřit přítomnost advice. On se dotazuje API Springu na přítomnost aktivní transakce, kdežto já zůstávám pasivní - pouze monitorující logovací výstup advice. V mém případě je nevýhoda navěšení na interní funkcionalitu advicy a naopak výhoda v tom, že stejný způsob můžu použít i na vlastní advicy, které řeší např. zabezpečení aniž bych musel rozšiřovat jejich API. Jeho způob je možná čistší, ale použitelný zase pouze na ověření správnosti transakční logiky v kombinaci se Springem.</p>
<p>Nicméně, evidentní je, že to je problém, který pálí víc vývojářů než jen Otce Fura v Čechách. A to mi dnes ráno udělalo opravdu radost ...</p>
