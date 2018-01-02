---
status: publish
published: true
title: Kafemlejnek.TV 14. - hackování web aplikací
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft size-thumbnail wp-image-3223\" src=\"http://blog.novoj.net/binary/2016/08/DSC_0203-e1471330654655-150x150.jpg\"
  alt=\"Roman Kümmel\" width=\"150\" height=\"150\" />\r\n\r\nRoman Kümmel je známá
  osoba v oblasti webové bezpečnosti. Stojí za portálem <a href=\"http://www.soom.cz\">www.soom.cz</a> a
  tuto problematiku taktéž <a href=\"https://www.gopas.cz/Kurzy/Katalog-kurzu/IT-bezpecnost-a-Hacking/IT-bezpecnost-a-Hacking/WebHacking-v-praxi-Zranitelnosti-webovych-aplikaci-GOC54.aspx\">uceleně
  školí</a>. V této oblasti se díky evangelizační činosti mj. i <a href=\"https://www.michalspacek.cz/\">Michala
  Špačka</a> hodně udělalo, ale přesto existuje řada mýtů a podceněných oblastí při
  vývoji webových aplikací, které se snažíme v tomto díle poodhalit.\r\n\r\n"
wordpress_id: 3222
wordpress_url: http://blog.novoj.net/?p=3222
date: '2016-08-16 07:58:38 +0200'
date_gmt: '2016-08-16 06:58:38 +0200'
categories:
- Podcast
tags:
- kafemlejnektv
comments: []
---
<p><img class="alignleft size-thumbnail wp-image-3223" src="http://blog.novoj.net/binary/2016/08/DSC_0203-e1471330654655-150x150.jpg" alt="Roman Kümmel" width="150" height="150" /></p>
<p>Roman Kümmel je známá osoba v oblasti webové bezpečnosti. Stojí za portálem <a href="http://www.soom.cz">www.soom.cz</a> a tuto problematiku taktéž <a href="https://www.gopas.cz/Kurzy/Katalog-kurzu/IT-bezpecnost-a-Hacking/IT-bezpecnost-a-Hacking/WebHacking-v-praxi-Zranitelnosti-webovych-aplikaci-GOC54.aspx">uceleně školí</a>. V této oblasti se díky evangelizační činosti mj. i <a href="https://www.michalspacek.cz/">Michala Špačka</a> hodně udělalo, ale přesto existuje řada mýtů a podceněných oblastí při vývoji webových aplikací, které se snažíme v tomto díle poodhalit.</p>
<p><a id="more"></a><a id="more-3222"></a></p>
<p>Za celým dílem je moje (tj. Novojova) účast na Romanově školení, která mi v řadě oblastí otevřela oči. Např. jsem se dozvěděl, že pomocí reflektovaného XSS útoku lze ukradnout login a heslo napadeného uživatele. Možná nebezpečí reflektovaného XSS překvapí i řadu z vás.</p>
<p>Stejně neznámou oblastí pro mě bylo i nebezpečí uploadovaného XML a využití známých či méně známých vlastností parserů. Útoků a jejich variant je nepřeberné množství a nové stále přibývají.</p>
<p>V tomto díle probíráme řadu dalších věcí, které byste měli vzít v potaz, pokud nechcete psát děravé aplikace. A jako bonus se dozvíte jak doopravdy fungují Rainbow tables - budete překvapeni :)</p>
<p><strong>Poděkování</strong></p>
<p>Děkujeme firmě <a href="http://www.fg.cz/">FG Forrest</a> za kanceláře a firmě <a href="http://www.flamesite.cz/">Flamesite</a> za profesionální natočení a sestříhání dílu.</p>
<p>Kompletní obsah zde: <a href="https://kafemlejnek.tv/dil-14-hackovani-web-aplikaci/">https://kafemlejnek.tv/dil-14-hackovani-web-aplikaci/</a></p>
<h4><strong>Zdroje</strong></h4>
<ul>
<li><a href="http://www.soom.cz" target="_blank">Soom.cz</a> - portál o hackování a bezpečnosti (nejen) webových aplikací</li>
<li><a href="http://www.citadelo.cz/cs/">Citadelo</a> - slovenská společnost snažící se zastřešit bug bounty programy</li>
<li><a href="http://www.devttys0.com/2013/10/reverse-engineering-a-d-link-backdoor/">backdor v D-Link routerech</a></li>
<li><a href="http://mashable.com/2014/08/06/wordpress-xml-blowup-dos/#5H.tPQ_BP5q1">zranitelnost XML expansion hack ve WorkPressu a Drupalu</a></li>
<li><a href="https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet">OWASP top threats</a></li>
<li><a href="http://security.stackexchange.com/questions/53474/is-chrome-completely-secure-against-reflected-xss">XSS filter v Chrome</a></li>
<li><a href="https://content-security-policy.com/">Content Security Policy</a></li>
<li><a href="https://blog.nic.cz/2016/03/21/dvoufaktorova-autentizace-v-mojeid-tentokrat-jeste-jednoduseji/" target="_blank">MojeID Autentikátor</a></li>
<li><a href="https://en.wikipedia.org/wiki/PBKDF2" target="_blank">PBKDF2 Hashovací funkce</a></li>
<li><a href="http://kestas.kuliukas.com/RainbowTables/">Jak fungují Rainbow tabulky</a></li>
</ul>
<h4>Obsah</h4>
<ol>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=0m34s" target="_blank">představení Romana Kümmela ze Soom.cz</a> 0:34</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=1m31s" target="_blank">čím se hacker v Čechách živí?</a> 1:31</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=2m04s" target="_blank">lze se uživit přes bug bounty programy?</a> 2:04</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=3m22s" target="_blank">co mám jako majitel firmy dělat, abychom vyvíjeli bezpečný SW?</a> 3:22</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=7m30s" target="_blank">revize kódu jako forma white-box testování</a> 7:30</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=8m19s" target="_blank">zamyšlení nad backdoory v aplikacích</a> 8:19</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=11m08s" target="_blank">humorné historky ze života</a> 11:08</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=15m35s" target="_blank">penetrační testování - black box testing</a> 15:35</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=19m04s" target="_blank">lze zpětně udělat white box testing a jak by byl drahý?</a> 19:04</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=21m02s" target="_blank">bug bounty jako pokračování penetračních testů</a> 21:02</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=24m36s" target="_blank">jak nastavovat odměny v bug bounty?</a> 24:36</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=26m12s" target="_blank">považuješ DDOS ještě za hacking?</a> 26:12</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=29m07s" target="_blank">útoky pomocí XML souborů a neznámých funkcí parserů</a> 29:07</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=32m48s" target="_blank">jak dalece jsou NoSQL databáze zranitelné k injection</a> 32:48</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=36m18s" target="_blank">jaké jsou tvoje zkušenosti v porovnání s OWASP žebříčkem zranitelností</a> 34:18</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=36m31s" target="_blank">Cross Site Scripting a jeho nebezpečí</a> 36:31</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=43m17s" target="_blank">pomoc prohlížeče při obraně proti XSS (filtry, Content Security Policy)</a> 43:17</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=49m51s" target="_blank">doporučení pro ukládání hesel</a> 49:51</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=54m53s" target="_blank">MojeID Autentikátor</a> 54:53</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=58m45s" target="_blank">jak fungují Rainbow tables a proč se používají</a> 58:45</li>
<li><a href="https://www.youtube.com/watch?v=d6m9tCp_s-Y&amp;t=1h05m30s" target="_blank">nebezpečnost trvalého přihlášení</a> 1:05:30</li>
</ol>
