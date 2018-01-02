---
status: publish
published: true
title: Kafemlejnek.TV 16. - Local Session Poisoning
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft wp-image-3223\" src=\"http://blog.novoj.net/binary/2016/08/DSC_0203-e1471330654655-300x287.jpg\"
  alt=\"Roman Kümmel\" width=\"156\" height=\"150\" />Je až s podivem, že tato zranitelnost
  i několik let po svém objevení není běžně známá a že jí stále trpí všechny PHP aplikace,
  které se spolehnou na výchozí nastavení PHP. Principielně se zranitelnost týká i
  dalších platforem, ale tam není riziko tak vysoké jako právě v PHP.\r\n\r\n"
wordpress_id: 3251
wordpress_url: http://blog.novoj.net/?p=3251
date: '2016-10-24 23:03:08 +0200'
date_gmt: '2016-10-24 22:03:08 +0200'
categories:
- Podcast
tags: []
comments: []
---
<p><img class="alignleft wp-image-3223" src="http://blog.novoj.net/binary/2016/08/DSC_0203-e1471330654655-300x287.jpg" alt="Roman Kümmel" width="156" height="150" />Je až s podivem, že tato zranitelnost i několik let po svém objevení není běžně známá a že jí stále trpí všechny PHP aplikace, které se spolehnou na výchozí nastavení PHP. Principielně se zranitelnost týká i dalších platforem, ale tam není riziko tak vysoké jako právě v PHP.</p>
<p><a id="more"></a><a id="more-3251"></a></p>
<p>Local session poisoning objevil Roman Kümmel na konci roku 2015 a snažil se informovat postižené majitele webů, které byly touto technikou zranitelné. Jak dopadl si sami můžete přečíst v článku <a href="http://www.soom.cz/clanky/1171--Bezpecnostni-tragikomedie" target="_blank">Bezpečnostní tragikomedie</a>. Zranitelnost byla pravděpodobně poprvé zdokumentována na webu <a href="http://ha.xxor.se/2011/09/local-session-poisoning-in-php-part-1.html" target="_blank">Haxxor Security</a> v září 2011, nicméně nijak světem neotřásla a dosud na internetu najdete jen několik dalších článků o této zranitelnosti.</p>
<p>To však neznamená, že se nejedná o závažný problém nebo o problém, který by byl od té doby již vyřešen. Zranitelnost je tu stále s námi a jak si Roman empiricky ověřil, je poměrně rozšířená.</p>
<p>S využitím této zranitelnosti máte poměrně velkou šanci dostat se neoprávněně do administrací ostatních webů, které běží na stejném webovém serveru, jako ten Váš. Riziko platí pro všechny defaultní PHP instalace na serverech, které hostují několik webů. U Java platformy by toto riziko připadalo v úvahu pouze tehdy, pokud by jedna aplikace (WAR) hostovala více různých klientských webů a neošetřila si spojení session s konkrétním webem.</p>
<p>Detaily o této zranitelnosti si ale radši poslechněte rovnou od Romana. A nezapomeňte na demo v druhé polovině dílu.</p>
<p><strong>Poděkování</strong></p>
<p>Děkujeme firmě <a href="http://www.fg.cz/">FG Forrest</a> za kanceláře a firmě <a href="http://www.flamesite.cz/">Flamesite</a> za profesionální natočení a sestříhání dílu.</p>
<p>Kompletní obsah zde: <a href="https://kafemlejnek.tv/dil-16-local-session-poisoning/" target="_blank">https://kafemlejnek.tv/dil-16-local-session-poisoning/</a></p>
<h4><strong>Zdroje</strong></h4>
<p>Jak šel čas v přednáškách:</p>
<ul>
<li><a href="http://ha.xxor.se/2011/09/local-session-poisoning-in-php-part-1.html" target="_blank">Local Session Poisoning in PHP</a></li>
</ul>
<h4>Obsah</h4>
<ol>
<li><a href="https://www.youtube.com/watch?v=wDGDv6I56b8&amp;t=1m14s" target="_blank">představení zranitelnosti</a> 1:14</li>
<li><a href="https://www.youtube.com/watch?v=wDGDv6I56b8&amp;t=12m10s" target="_blank">zamyšlení nad tím, které aplikace jsou zranitelné</a> 12:10</li>
<li><a href="https://www.youtube.com/watch?v=wDGDv6I56b8&amp;t=16m20s" target="_blank">zrychlení hackingu nad všemi subdoménami</a> 16:20</li>
<li><a href="https://www.youtube.com/watch?v=wDGDv6I56b8&amp;t=20m1s" target="_blank">zranitelnost Wordpressu</a> 20:11</li>
<li><a href="https://www.youtube.com/watch?v=wDGDv6I56b8&amp;t=22m09s" target="_blank">jak reagovali majitelé hostingů a majitelů webů při oznámení zranitelnosti</a> 22:09</li>
<li><a href="https://www.youtube.com/watch?v=wDGDv6I56b8&amp;t=29m19s" target="_blank">přiznání autorství</a> 29:19</li>
<li><a href="https://www.youtube.com/watch?v=wDGDv6I56b8&amp;t=31m23s" target="_blank">co udělat pro opravu?</a> 31:23</li>
<li><a href="https://www.youtube.com/watch?v=wDGDv6I56b8&amp;t=34m06s" target="_blank">demo s ukázkou zranitelnosti v praxi</a> 34:06</li>
</ol>
