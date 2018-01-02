---
status: publish
published: true
title: Prospěšná Captcha
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Kamarád mi poslal odkaz na <a href=\"http://news.bbc.co.uk/1/hi/technology/7023627.stm\"
  target=\"_new\">zajímavý článek</a>. Jistě všichni znáte ochranu zneužití veřejně
  dostupných formulářů pomocí CAPTCHA. Koneckonců je většina z nás má na svých blozích
  po tom, co nám začaly chodit spamové komentáře k článkům. Pánové z Carnegie Mellon
  University však našli způsob, jak tento otravný fenomén převést na něco, co je užitečné.\r\n\r\n"
wordpress_id: 40
wordpress_url: http://blog.novoj.net/2007/10/04/prospesna-captcha/
date: '2007-10-04 15:19:43 +0200'
date_gmt: '2007-10-04 14:19:43 +0200'
categories:
- Web
tags: []
comments: []
---
<p>Kamarád mi poslal odkaz na <a href="http://news.bbc.co.uk/1/hi/technology/7023627.stm" target="_new">zajímavý článek</a>. Jistě všichni znáte ochranu zneužití veřejně dostupných formulářů pomocí CAPTCHA. Koneckonců je většina z nás má na svých blozích po tom, co nám začaly chodit spamové komentáře k článkům. Pánové z Carnegie Mellon University však našli způsob, jak tento otravný fenomén převést na něco, co je užitečné.</p>
<p><a id="more"></a><a id="more-40"></a></p>
<p>Na světě existuje ohromné množství tištěné literatury, které se snaží archiváři digitalizovat, aby se zachovaly pro budoucí generace. Při digitalizaci se používá OCR pro rozeznávání textového obsahu. OCR však není v řadě případů úspěšné - prostě nedokáže rozeznat napsané slovo (podle statistiky 1 z 10). Výsledkem je tedy text, který je více či méně znehodnocený a je nutný lidský zásah, aby byl původní text zkompletován.</p>
<p>Právě k rozeznávání špatně čitelných slov, se kterými si nedokáže AI poradit se dají využít Captchi. Princip je geniálně jednoduchý - slova, která se nepodařilo OCR identifikovat jsou jako obrázky distribuovány na web servery, které je použijí jako Captchi. V každé Captcha budou vždy dvě slova - jedno, které se OCR nepodařilo identifikovat a druhé, které se podařilo. Na slovo, které se podařilo OCR identifikovat jsou aplikovány filtry pro zhoršení  rozeznání slova (aby bylo ostatním AI stíženo čtení tohoto slova). Uživatelský vstup je potom porovnáván pouze s tím správně identifikovaným slovem - znění druhého slova je po rozluštění člověkem naopak posláno zpět na CMU k doplnění do původního textu. Aby bylo možné považovat rozluštění za důvěryhodné - minimálně dva lidé se musí shodnout na stejném znění tohoto slova. Pokud se neshodnou, je automaticky podstrčeno dalším lidem, dokud není dostatečná shoda na jeho znění.</p>
<p>Tahle myšlenka ve mě utvrzuje pocit, že geniální věci jsou často tak prosté. Zajímalo by mne, jestli si články na BBC čtou i naši archiváři ...</p>
<p><strong>Zdroj:</strong> <a href="http://news.bbc.co.uk/2/hi/technology/7023627.stm" target="_new">BBC NEWS</a><br />
<strong>Carnegie Mellon University</strong> <a href="http://www.cmu.edu/news/archive/2007/May/may24_recaptcha.shtml" target="_new">zpráva CMU</a></p>
<p><strong>Aktualizace k 13.1.2008:</strong> Na blogu jsem nasadil <a href="http://recaptcha.net" target="_new">plugin reCaptcha</a>, který je reálnou ukázkou tohoto principu. Více o tom, jak plugin funguje se dočtete <a href="http://recaptcha.net/learnmore.html" target="_new">na stránkách autorů</a>.</p>
