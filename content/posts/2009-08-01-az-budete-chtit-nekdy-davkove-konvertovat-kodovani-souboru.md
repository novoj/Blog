---
status: publish
published: true
title: Až budete chtít někdy dávkově konvertovat kódování souborů ...
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Čas od času řeším problém jak hromadně zkonvertovat sadu souborů z kódování
  A do kódování B, popřípadě jak ze sady souboru odstranit <a href=\"http://en.wikipedia.org/wiki/Byte-order_mark\"
  target=\"_blank\">UTF-8 BOM</a>. Vždy jsem na hledání nějakého jednorázového vehementu
  strávil plno času, především proto, že to obvykle nefungovalo tak úplně jak bych
  potřeboval. Na odstranění BOMu, jsem navíc nenašel vůbec nic. Nakonec mi došla trpělivost
  a za 20 minut jsem si spíchnul utilitku, kterou jsem si problém jednou provždy (doufám)
  vyřešil. A pak že je Java na takovéhle utilitky nešikovná (vím že v Groovy bych
  to měl na polovině řádku, ale ještě nejsem úplně Groovy ready) ...\r\n\r\n"
wordpress_id: 572
wordpress_url: http://blog.novoj.net/?p=572
date: '2009-08-01 20:21:17 +0200'
date_gmt: '2009-08-01 19:21:17 +0200'
categories:
- Programování
tags: []
comments:
- id: 11189
  author: Filda
  author_email: fsubr@centrum.cz
  author_url: http://vobloz.xtr.cz
  date: '2009-08-02 12:16:07 +0200'
  date_gmt: '2009-08-02 11:16:07 +0200'
  content: na windows se mi osvědčilo tohle http://www.sisulizer.com/kaboom/index.shtml
- id: 11196
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-08-02 16:39:15 +0200'
  date_gmt: '2009-08-02 15:39:15 +0200'
  content: Tak ten vypadá rozhodně líp než většina co jsem zkoušel. No internet je
    holt moře, a tak se v něm dá lehce utopit.
- id: 11209
  author: Švarcik
  author_email: milan.schwarz@gmail.com
  author_url: ''
  date: '2009-08-03 08:03:33 +0200'
  date_gmt: '2009-08-03 07:03:33 +0200'
  content: "Ahoj, pro inspiraci jsem si chtěl stáhnout zdrojáky, ale bohužel nemám
    na to právo:-(\r\nYou don't have permission to access /EncodingConvertor/ on this
    server."
- id: 11214
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-08-03 14:24:52 +0200'
  date_gmt: '2009-08-03 13:24:52 +0200'
  content: Chybička se vloudila, odkazy opraveny, nyní možno stáhnout.
- id: 11466
  author: Bedo
  author_email: siekel@prosoft.sk
  author_url: ''
  date: '2009-08-13 07:10:50 +0200'
  date_gmt: '2009-08-13 06:10:50 +0200'
  content: "Ak už má človek nainštalovanú javu, tak má aj nástroj native2ascii. S
    ním je možné spraviť konverziu bez inštalácie akýchkoľvek knižníc tretích strán.
    Ja som používal tento BAT\r\n\r\n1 rem Windows-1250 to UTF-8.\r\n2 copy \"%1\"
    \"%1.1250\"\r\n3 %JAVA_HOME%\\bin\\native2ascii.exe -J-Xmx64M -encoding windows-1250
    \"%1.1250\" | %JAVA_HOME%\\bin\\native2ascii.exe -reverse -encoding UTF-8 &gt;
    \"%1\"\r\n4 del \"%1.1250\"\r\n\r\nRiadok 2 urobil pracovnú kópiu súboru ktorý
    chcem konvertovať.\r\nRiadok 3 urobí dve konverzie - z pôvodného formátu do java-encoding
    a z neho do požadovaného formátu, ktorý prepíše pôvodný súbor.\r\nRiadok 4 vymaže
    pracovnú verziu (v java-encoding formáte).\r\n\r\nTento baťák stačí obaliť baťákom,
    ktorý tam láduje súbory z nejakých adresárov a to je všetko."
- id: 20345
  author: niko
  author_email: niko@srnet.cz
  author_url: ''
  date: '2010-03-01 15:22:58 +0100'
  date_gmt: '2010-03-01 14:22:58 +0100'
  content: "Nevim jak s BOM, ale na prevod kodovani se mi osvedcil iconv. Lze i na
    windows (pouzivam cygwin). Trivialni priklad::\r\n\r\nmyconv.sh:\r\n#!/bin/bash\r\nmv
    $1 %1.tmp\r\niconv -f UTF-8 -t CP1250 $1.tmp &gt; $1\r\nrm $1.tmp\r\n\r\nnasledne
    se zavola na potrebne soubory napr. pres find:\r\n\r\nfind ./ -type f - name \"*.java\"
    -o - name \"*.txt\" -exec myconv.sh \\{\\} \\;"
- id: 27931
  author: Myšlenky dne otce Fura &raquo; Blog Archive &raquo; How to add your own
    dictionary to IntelliJ Idea Spellchecker
  author_email: ''
  author_url: http://blog.novoj.net/2010/11/07/how-to-add-your-own-dictionary-to-intellij-idea-spellchecker/
  date: '2010-11-07 22:47:55 +0100'
  date_gmt: '2010-11-07 21:47:55 +0100'
  content: "[...] convert 4MB txt file to the desired encoding). I was successful
    with my own transformation utility (available for download here &#8211; Google
    translated version of the [...]"
- id: 43538
  author: Myšlenky dne otce Fura &raquo; Blog Archive &raquo; Groovy namísto shell
    skriptů
  author_email: ''
  author_url: http://blog.novoj.net/2011/06/15/groovy-namisto-shell-skriptu/
  date: '2011-06-15 23:24:40 +0200'
  date_gmt: '2011-06-15 22:24:40 +0200'
  content: "[...] Pozn.: na Groovy jsem převedl i další skripty pro hromadnou konverzi
    kódování textových souborů a odstranění BOM z UTF-8 popsaných v článku Až budete
    chtít někdy dávkově konvertovat kódování souborů … [...]"
- id: 154854
  author: ptomasek
  author_email: ptomasek@me.com
  author_url: http://erstefc.wordpress.com
  date: '2015-01-16 14:46:17 +0100'
  date_gmt: '2015-01-16 13:46:17 +0100'
  content: než jsem si přečetl komentáře s návody pro iconv nebo native2ascii, tak
    jsem to stáhl, vyzkoušel a funguje, takže díky :-)
- id: 154882
  author: Ondřej Kolín
  author_email: ondrej.kolin@gmail.com
  author_url: https://plus.google.com/+OndřejKolín
  date: '2015-01-19 13:39:28 +0100'
  date_gmt: '2015-01-19 12:39:28 +0100'
  content: "Teda pouštět kvůli takový kravině JVM :D \r\nTohle se mi zdá daleko lepší
    :)\r\nhttp://awesomeprogrammer.com/blog/2013/07/25/windows-1250-to-utf-8-bash-one-liner/"
- id: 154885
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2015-01-20 13:51:19 +0100'
  date_gmt: '2015-01-20 12:51:19 +0100'
  content: "Dík za tip - nezapomeň, že jsem to psal v roce 2009, to jsem byl ještě
    na Windowsech :) ... ještě jsem hledal, jak by to bylo s BOMem a i na to existuje
    jednoduché bash based řešení:\r\n\r\nhttp://stackoverflow.com/questions/4364156/iconv-converting-from-windows-ansi-to-utf-8-with-bom"
---
<p>Čas od času řeším problém jak hromadně zkonvertovat sadu souborů z kódování A do kódování B, popřípadě jak ze sady souboru odstranit <a href="http://en.wikipedia.org/wiki/Byte-order_mark" target="_blank">UTF-8 BOM</a>. Vždy jsem na hledání nějakého jednorázového vehementu strávil plno času, především proto, že to obvykle nefungovalo tak úplně jak bych potřeboval. Na odstranění BOMu, jsem navíc nenašel vůbec nic. Nakonec mi došla trpělivost a za 20 minut jsem si spíchnul utilitku, kterou jsem si problém jednou provždy (doufám) vyřešil. A pak že je Java na takovéhle utilitky nešikovná (vím že v Groovy bych to měl na polovině řádku, ale ještě nejsem úplně Groovy ready) ...</p>
<p><a id="more"></a><a id="more-572"></a></p>
<p>Utilitka je směšně jednoduchá -  před použitím zatřepat a na příkazový řádek napsat:</p>
<p>[source lang="java"]<br />
java -jar convertor-1.0.0.jar -m convert -i utf-8 -o windows-1250 -s /www/vstupni -t /tmp/vystupni -e java,txt,properties,xml<br />
[/source]</p>
<p>Tímhle příkazem zkonvertujete všechny soubory s příponami java, txt, properties, xml z adresáře /www/vstupni z kódování UTF-8 do kódování windows-1250 a výsledek se uloží do složky /tmp/vystupni. Pro odstranění BOM stačí -m convert zaměnit za -m removeBOM.</p>
<p>Nehledejte v utilitce žádnou inženýrský přístup - jde jen o jednorázovku, která má plnit jednoduchý účel. Třeba se vám ale bude taky hodit ...</p>
<p><a href="http://files.novoj.net/EncodingConvertor/convertor-1.0.0.jar"><img src="http://files.novoj.net/button_jar.gif" width="80" height="15"> Convertor [JAR 150kB] ke stažení</a></p>
<p><a href="http://files.novoj.net/EncodingConvertor/convertor-sources.zip"><img src="http://files.novoj.net/button_zip.gif" width="80" height="15"> Zdrovové soubory [ZIP 4kB] ke stažení</a></p>
<h2>Application for batch file encoding and UTF-8 BOM removal</h2>
<p>Many times I had a need for batch file encoding conversion or UTF-8 BOM removal. I repeatedly searched for utility appliacations that would do this for me, but usually lost a lot of time trying them and finally uninstall them dissapointed. The problem is so dumb simple, that I couldn't resist and wrote my own in 20 minutes, doing the right thing I need. Feel free to use it or extend it, if you want.</p>
<p>Usage is simple - you would need Java 1.5 installed:</p>
<p>[source lang="java"]<br />
java -jar convertor-1.0.0.jar -m convert -i utf-8 -o windows-1250 -s /www/input-t /tmp/output-e java,txt,properties,xml<br />
[/source]</p>
<p>Thic command will convert all files with extension of java, txt, properties and xml from input directory /www/input into output directory /tmp/output from encoding utf-8 into windows-1250. If you need to batch remove UTF-8 BOM, just change the mode to -m removeBOM.</p>
<p><a href="http://files.novoj.net/EncodingConvertor/convertor-1.0.0.jar"><img src="http://files.novoj.net/button_jar.gif" width="80" height="15"> Download Convertor [JAR 150kB]</a></p>
<p><a href="http://files.novoj.net/EncodingConvertor/convertor-sources.zip"><img src="http://files.novoj.net/button_zip.gif" width="80" height="15"> Download source files [ZIP 4kB]</a></p>
