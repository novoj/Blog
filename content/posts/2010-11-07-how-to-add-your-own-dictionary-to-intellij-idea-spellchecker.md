---
status: publish
published: true
title: How to add your own dictionary to IntelliJ Idea Spellchecker
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img src=\"http://blog.novoj.net/binary/2010/11/dictionary1.jpg\" alt=\"\"
  title=\"dictionary\" width=\"150\" height=\"113\" class=\"alignleft size-full wp-image-1212\"
  /> Spellchecking provided by IntelliJ Idea is very handy for those who are not confident
  in written English (such as me for example ;-) ). \r\n\r\nBut for non-English speaking
  developers it's common to use (at least) two languages simultaneously - English
  for writing Javadoc, method and variable names and their native language (Czech,
  Polish ...) for strings in UI layer. Setuping Ideas' spellchecker to validate string
  in multiple languages is more than handy. This article will guide you through setuping
  your native dictionary.\r\n\r\n"
wordpress_id: 1194
wordpress_url: http://blog.novoj.net/?p=1194
date: '2010-11-07 22:47:46 +0100'
date_gmt: '2010-11-07 21:47:46 +0100'
categories:
- Softwarové nástroje
- English
- IntelliJ Idea
tags: []
comments:
- id: 28015
  author: Arno.Nyhm
  author_email: no@email.com
  author_url: ''
  date: '2010-11-09 17:13:11 +0100'
  date_gmt: '2010-11-09 16:13:11 +0100'
  content: "it would be nice if intelliJ automaticly download and convert the dictionaries.
    \r\ni remember with open office is also a dictionary available."
- id: 28182
  author: optik
  author_email: koubel@volny.cz
  author_url: http://www.mirin.cz
  date: '2010-11-13 18:32:26 +0100'
  date_gmt: '2010-11-13 17:32:26 +0100'
  content: I tried to convert huge aspell dictionary with simple bash script and use
    it in PHPStorm. File was &gt; 50MB and PHPStorm loads it a very very long so I
    put ti down.
- id: 28187
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-11-13 20:40:18 +0100'
  date_gmt: '2010-11-13 19:40:18 +0100'
  content: What language has this huge vocabulary? My Czech dictionary is about 4MB
    and I didn't noticed Idea getting slowly.
- id: 28348
  author: optik
  author_email: koubel@volny.cz
  author_url: http://www.mirin.cz
  date: '2010-11-17 00:52:11 +0100'
  date_gmt: '2010-11-16 23:52:11 +0100'
  content: Czech, I used aspell source to extact more shapes of words (some words
    in 7 shapes) and each with and without punctuation, because some of my legacy
    code base has comments in Czech without punctuation.
- id: 28673
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-11-23 09:30:06 +0100'
  date_gmt: '2010-11-23 08:30:06 +0100'
  content: I am a bit suprised that it makes such a big difference. There are some
    shapes in the 4MB dictionary I use. Doubling variants for words without punctuation
    would make 8MB file. That would mean I have 10 times less words / variants that
    you have. Where did you get your dictionary?
- id: 151921
  author: Mems
  author_email: memmie@lenglet.name
  author_url: ''
  date: '2013-06-25 13:43:17 +0200'
  date_gmt: '2013-06-25 12:43:17 +0200'
  content: 'If after adding a folder and or a dic file, IntelliJ Idea still not recognize
    your words, relaunch it by: "File &gt; Invalidate caches..."'
- id: 152055
  author: SimonSimCity
  author_email: simonsimcity@gmail.com
  author_url: http://gravatar.com/simonsimcity
  date: '2013-07-18 14:07:57 +0200'
  date_gmt: '2013-07-18 13:07:57 +0200'
  content: "If you find yourself (like me) forever searching for a page that has these
    dic-files, here's a link I found very useful: https://github.com/SublimeText/Dictionaries\r\n\r\nI
    just cloned the repo and linked the folder ;)"
- id: 152056
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2013-07-18 19:36:01 +0200'
  date_gmt: '2013-07-18 18:36:01 +0200'
  content: Thanks for the pointer!
- id: 152329
  author: Nilo César Teixeira
  author_email: nilo.teixeira@gmail.com
  author_url: https://plus.google.com/105792072003979020895
  date: '2014-03-13 19:20:44 +0100'
  date_gmt: '2014-03-13 18:20:44 +0100'
  content: "To change WinEdt.org dictionary to UTF-8:\r\n\r\nopen the file in vim,
    then issue ([Key] is notation for pressing corresponding keyboard):\r\n\r\n[ESC]
    :set fileencoding=UTF-8 [ENTER]\r\n[ESC] :w ++enc=UTF-8 [ENTER]\r\n[ESC] :q [ENTER]\r\n\r\nIt
    changed my portuguese (sp) file instantly =)"
- id: 153401
  author: Ricardo Martins
  author_email: ricardo@ricardomartins.info
  author_url: http://ricardomartins.net.br/
  date: '2014-10-02 14:54:00 +0200'
  date_gmt: '2014-10-02 13:54:00 +0200'
  content: Nice article. I converted to uft-8 using native TextEdit from mac going
    in File-&gt;Save As...
- id: 158360
  author: Michele
  author_email: gennarino86@libero.it
  author_url: ''
  date: '2016-06-10 08:23:39 +0200'
  date_gmt: '2016-06-10 07:23:39 +0200'
  content: Nice job, thank you.
---
<p><img src="http://blog.novoj.net/binary/2010/11/dictionary1.jpg" alt="" title="dictionary" width="150" height="113" class="alignleft size-full wp-image-1212" /> Spellchecking provided by IntelliJ Idea is very handy for those who are not confident in written English (such as me for example ;-) ). </p>
<p>But for non-English speaking developers it's common to use (at least) two languages simultaneously - English for writing Javadoc, method and variable names and their native language (Czech, Polish ...) for strings in UI layer. Setuping Ideas' spellchecker to validate string in multiple languages is more than handy. This article will guide you through setuping your native dictionary.</p>
<p><a id="more"></a><a id="more-1194"></a></p>
<p>In the default installation you have only English and JetBrains dictionary enabled. So when you open your localization property bundle it can look like this:</p>
<p><a href="http://blog.novoj.net/binary/2010/11/dictionary-before.png"><img src="http://blog.novoj.net/binary/2010/11/dictionary-before.png" alt="" title="dictionary-before" width="500" height="367" class="aligncenter size-full wp-image-1203" /></a></p>
<p>But you'd probably want to validate either your own native sentences - as there could be mistakes too. In order to make Idea validate these strings you have to perform these 3 steps:</p>
<h3>1. Find your language dictionary</h3>
<p>There are several sources on the web. I found our Czech dictionary on WinEdt community site - there are plenty of other languages too:</p>
<p><a href="http://www.winedt.org/Dict/" target="_blank">http://www.winedt.org/Dict/</a></p>
<p>So download your language dictionary in DIC format.</p>
<h3>2. Convert the dictionary file into UTF-8 encoding</h3>
<p>IntelliJ Idea, though its not mentioned in documentation, reads dictionary files in UTF-8 encoding. Usually your downloaded dictionary doesn't conform to this encoding. Czech dictionary on WinEdt site was stored for example in "windows-1250" codepage.</p>
<p>Because dictionary files are very large, you could have problems converting them to UTF-8 (for example Idea and Notepad++ both failed to convert 4MB txt file to the desired encoding). I was successful with my own transformation utility (<a href="http://blog.novoj.net/2009/08/01/az-budete-chtit-nekdy-davkove-konvertovat-kodovani-souboru/" target="_blank">available for download here</a> - <a href="http://translate.google.com/translate?js=n&prev=_t&hl=cs&ie=UTF-8&layout=2&eotf=1&sl=cs&tl=en&u=http://blog.novoj.net/2009/08/01/az-budete-chtit-nekdy-davkove-konvertovat-kodovani-souboru/&act=url" target="_blank">Google translated version of the article</a>).</p>
<h3>3. Configure IntelliJ Idea to use the dictionary</h3>
<p>Finally open IntelliJ Idea settings dialog, locate Spelling settings and Add custom folder at Dictionaries tab. You should create individual folder for storing DIC files, because when targeting Idea to some high level folder, it starts to recursively search for all *.DIC files and in case of huge folders it could take several minutes till it finishes (yes, I did this wrong for first time :-) ).</p>
<p><a href="http://blog.novoj.net/binary/2010/11/dictionary-settings.png"><img src="http://blog.novoj.net/binary/2010/11/dictionary-settings.png" alt="" title="dictionary-settings" width="500" height="352" class="aligncenter size-full wp-image-1204" /></a></p>
<p>After enabling custom dictionary in the bottom section of the tab your native sentences should be validated as expected. Even auto-correction should offer similar words at the places where Idea underlines invalid words.</p>
<p>The same screen should now look like this:</p>
<p><a href="http://blog.novoj.net/binary/2010/11/dictionary-after.png"><img src="http://blog.novoj.net/binary/2010/11/dictionary-after.png" alt="" title="dictionary-after" width="500" height="367" class="aligncenter size-full wp-image-1205" /></a></p>
