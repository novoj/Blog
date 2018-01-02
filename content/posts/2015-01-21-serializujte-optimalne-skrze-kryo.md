---
status: publish
published: true
title: Serializujte optimálně skrze Kryo
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft  wp-image-2971\" alt=\"kryo\" src=\"http://blog.novoj.net/binary/2015/01/kryo.jpg\"
  width=\"237\" height=\"101\" />Je zajímavé, že tak základní věc, jako serializace
  objektů do binárního streamu je v Javě implementovaná neoptimálně - a to jak z hlediska
  velikosti výsledné binární podoby, tak i rychlosti s jakou je vytvořena. Míst, kde
  se serializace objektů hodí je celá řada, a proto je určitě v zájmu každého kvalitního
  vývojáře zamyslet se, jestli to nejde dělat líp.\r\n\r\nOno totiž jde :)\r\n\r\n"
wordpress_id: 2970
wordpress_url: http://blog.novoj.net/?p=2970
date: '2015-01-21 10:00:13 +0100'
date_gmt: '2015-01-21 09:00:13 +0100'
categories:
- Programování
- Java
tags: []
comments:
- id: 154888
  author: Zdenek Henek
  author_email: vrablik@gmail.com
  author_url: ''
  date: '2015-01-21 10:27:23 +0100'
  date_gmt: '2015-01-21 09:27:23 +0100'
  content: "Ahoj,\r\nKryo ma i nejaky ten problem. Ve Tvem use case je to asi ok.\r\nvice
    https://www.mail-archive.com/infinispan-dev@lists.jboss.org/msg07388.html"
- id: 154889
  author: Jara Hamala
  author_email: jaromir.hamala@gmail.com
  author_url: http://gravatar.com/jerrinot
  date: '2015-01-21 11:32:21 +0100'
  date_gmt: '2015-01-21 10:32:21 +0100'
  content: "Bylo byla zajimave zkusit upravit domain tridy a mit fieldy jako public.
    \r\nJen pro test, zajimal by me rozdil. Kryo pouziva https://github.com/EsotericSoftware/reflectasm
    a to se neumi dostat k private fieldum jinak nez pres reflection. Pro public fieldy
    vygeneruje vlastni bytecode (GETFIELD).\r\n\r\nPozor pokud to provozujete na platforme,
    ktere vyzaduje \"aligned\" pristup do pameti (Sparc?). Kryo na to kasle (kaslalo?)
    a shazuje to celou JVM."
- id: 154890
  author: Jety
  author_email: pavel.jetensky@seznam.cz
  author_url: http://jetensky.net/blog
  date: '2015-01-21 12:20:38 +0100'
  date_gmt: '2015-01-21 11:20:38 +0100'
  content: To zní dobře, oproti Google protocol buffers. které jsem v podobném usecase
    používal já, to nevyžaduje speciální formát (jako je .proto) a tím pádem odpadá
    i nutnost vygenerování domain objektů, což je super výhoda.
- id: 154892
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2015-01-22 08:52:57 +0100'
  date_gmt: '2015-01-22 07:52:57 +0100'
  content: "Úpravu tříd na public fieldy zkusit můžu - není to složité. Pak jsem postnu
    naměřené výsledky. Jen se k tomu dostanu asi až o víkendu.\r\n\r\nDíky moc za
    příspěvky - o reflectasm jsem neměl ani páru. Každopádně to Kryo má embednuté,
    protože pokud vím tak ve WARu se vysktuje jen to kryo.jar."
- id: 154898
  author: Jara Hamala
  author_email: jaromir.hamala@gmail.com
  author_url: ''
  date: '2015-01-23 09:30:35 +0100'
  date_gmt: '2015-01-23 08:30:35 +0100'
  content: "Jestli te zaujal reflactasm tak si nemuzu neprihrat vlastni polivcicku
    - https://github.com/jerrinot/FieldMagic\r\n\r\nVysoce experimentalni, funkcne
    neuplne, neotestovane, ale dostane se to bez puziti reflection i k private fieldum.
    Za zneuziti implementacniho detailu HotSpotu."
- id: 154973
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2015-01-31 15:12:17 +0100'
  date_gmt: '2015-01-31 14:12:17 +0100'
  content: Tak jsem to vyzkoušel a bylo tam jen drobné zrychlení (cca 5%) ale to mohla
    být stejně tak dobře chyba měření (je to jen microbenchmark). Charakteristiky
    (poměry) výkonnosti zůstaly u všech způsobů víceméně stejné.
---
<p><img class="alignleft  wp-image-2971" alt="kryo" src="http://blog.novoj.net/binary/2015/01/kryo.jpg" width="237" height="101" />Je zajímavé, že tak základní věc, jako serializace objektů do binárního streamu je v Javě implementovaná neoptimálně - a to jak z hlediska velikosti výsledné binární podoby, tak i rychlosti s jakou je vytvořena. Míst, kde se serializace objektů hodí je celá řada, a proto je určitě v zájmu každého kvalitního vývojáře zamyslet se, jestli to nejde dělat líp.</p>
<p>Ono totiž jde :)</p>
<p><a id="more"></a><a id="more-2970"></a>Pokusů o reimplementaci Java serializace je na webu mnoho, ale mezi ty nejlepší zcela jistě patří knihovna <a href="https://github.com/EsotericSoftware/kryo" target="_blank">Kryo</a>. Dá se použít jako plnohodnotná náhrada Java serializace, je jednoduchá na konfiguraci a má klony pro alternativní jazyky nad JVM (<a href="https://github.com/EsotericSoftware/kryo#scala" target="_blank">Scala</a>, <a href="https://github.com/EsotericSoftware/kryo#clojure" target="_blank">Clojure</a>) ale má také port pro <a href="https://github.com/EsotericSoftware/kryo#objective-c" target="_blank">Objective-C</a>.</p>
<h2>Kdy byste měli Kryo použít místo běžné Java Serializace?</h2>
<p>Vždy, když serializujete velké množství objektů a tudíž vám záleží na výkonnosti a velikosti výsledného pole. Že rozdíly nejsou malé, se můžete přesvědčit na následujícím grafu (zdroj: <a href="https://github.com/eishay/jvm-serializers/wiki" target="_blank">Java Serializers Benchmark Group</a>):</p>
<div style="text-align: center;"><img alt="" src="https://camo.githubusercontent.com/829809b59ac2efe1ec62ac2f2cfbb29606a02a44/68747470733a2f2f63686172742e676f6f676c65617069732e636f6d2f63686172743f636874743d746f74616c2b2532386e616e6f73253239266368663d637c7c6c677c7c307c7c4646464646467c7c317c7c3736413446427c7c307c62677c7c737c7c454645464546266368733d35303078343330266368643d743a313232362c313439322c313536382c323230302c323436352c323933392c333530312c333635392c333637302c343439352c383531362c31303035372c31303437372c31323138372c31333130392c31353632382c31393938302c32383534382c33363034362c343438333826636864733d302c34393332322e313530333526636878743d79266368786c3d303a7c6a736f6e253246666c65786a736f6e2532466461746162696e647c6a6176612d6275696c742d696e7c6a626f73732d6d61727368616c6c696e672d72697665727c786d6c2532467873747265616d253242637c6a736f6e2532467376656e736f6e2d6461746162696e647c6a626f73732d73657269616c697a6174696f6e7c62736f6e2532466a61636b736f6e2532466461746162696e647c6a736f6e253246676f6f676c652d67736f6e2532466461746162696e647c6865737369616e7c786d6c2532466a61636b736f6e2532466461746162696e642d61616c746f7c6a736f6e2532466a61636b736f6e2532466461746162696e647c6a736f6e25324670726f746f73747566662d72756e74696d657c736d696c652532466a61636b736f6e2532466461746162696e647c6a736f6e2532466a61636b736f6e25324664622d61667465726275726e65727c736d696c652532466a61636b736f6e25324664622d61667465726275726e65727c6a736f6e253246666173746a736f6e2532466461746162696e647c6d73677061636b2d6461746162696e647c666173742d73657269616c697a6174696f6e7c6b72796f7c70726f746f73747566662663686d3d4e2532302a662a2c3030303030302c302c2d312c3130266c6b6c6b266368646c703d74266368636f3d3636303030307c3636303033337c3636303036367c3636303039397c3636303043437c3636303046467c3636333330307c3636333333337c3636333336367c3636333339397c3636333343437c3636333346467c3636363630307c3636363633337c363636363636266368743d62686726636862683d31302c302c3130266e6f6e73656e73653d6161612e706e67" align="center" /></div>
<p>V grafu je kombinován čas na serializaci a deserializaci <a href="https://github.com/eishay/jvm-serializers/wiki/TestValue" target="_blank">běžných POJO objektů</a> a jak je vidět, oproti standardní Java serializaci je zde 95% časová úspora.</p>
<p>Když se podíváme na velikost vygenerovaného binárního pole docházíme k podobně zásadní (76%) úspoře místa:</p>
<div style="text-align: center;"><img alt="" src="https://camo.githubusercontent.com/e211bb86df70ee47e5c77b34fcc42878025211b7/68747470733a2f2f63686172742e676f6f676c65617069732e636f6d2f63686172743f636874743d73697a652b2532386279746573253239266368663d637c7c6c677c7c307c7c4646464646467c7c317c7c3736413446427c7c307c62677c7c737c7c454645464546266368733d35303078343330266368643d743a3231322c3233332c3233392c3235322c3333382c3335322c3436392c3438352c3438352c3438362c3438362c3438372c3439352c3530312c3530332c3530362c3638332c3639342c3838392c39333226636864733d302c313032352e3226636878743d79266368786c3d303a7c6a626f73732d73657269616c697a6174696f6e7c6a6176612d6275696c742d696e7c6a626f73732d6d61727368616c6c696e672d72697665727c786d6c2532466a61636b736f6e2532466461746162696e642d61616c746f7c62736f6e2532466a61636b736f6e2532466461746162696e647c6a736f6e253246666c65786a736f6e2532466461746162696e647c6865737369616e7c6a736f6e2532467376656e736f6e2d6461746162696e647c786d6c2532467873747265616d253242637c6a736f6e253246666173746a736f6e2532466461746162696e647c6a736f6e253246676f6f676c652d67736f6e2532466461746162696e647c6a736f6e2532466a61636b736f6e25324664622d61667465726275726e65727c6a736f6e2532466a61636b736f6e2532466461746162696e647c6a736f6e25324670726f746f73747566662d72756e74696d657c736d696c652532466a61636b736f6e25324664622d61667465726275726e65727c736d696c652532466a61636b736f6e2532466461746162696e647c666173742d73657269616c697a6174696f6e7c70726f746f73747566667c6d73677061636b2d6461746162696e647c6b72796f2663686d3d4e2532302a662a2c3030303030302c302c2d312c3130266c6b6c6b266368646c703d74266368636f3d3636303030307c3636303033337c3636303036367c3636303039397c3636303043437c3636303046467c3636333330307c3636333333337c3636333336367c3636333339397c3636333343437c3636333346467c3636363630307c3636363633337c363636363636266368743d62686726636862683d31302c302c3130266e6f6e73656e73653d6161612e706e67" /></div>
<h2>Jak složitá je náhrada za standardní serializaci?</h2>
<p>Vcelku jednoduchá - nevyžaduje aby objekty implementovaly rozhranní ani umístění speciálních anotací nad vlastnosti třídy. Do svého existujícího doménového modelu tak nemusíte, pokud nepotřebujete nějaké speciality, nijak zásadně zasahovat (což považuji za další velkou výhodu).</p>
<p>Ukázka serializace:</p>
<p>[source lang="java"]Kryo kryo = new Kryo();<br />
kryo.addDefaultSerializer(Trida.class, new TridaSerializer()));<br />
final ByteArrayOutputStream bos = new ByteArrayOutputStream(32768);<br />
try (Output output = new Output(bos)) {<br />
   kryo.writeObject(output, clusteredResult);<br />
}<br />
return bos.toByteArray();[/source]</p>
<p>Ukázka deserializace:</p>
<p>[source lang="java"]Kryo kryo = new Kryo();<br />
kryo.addDefaultSerializer(Trida.class, new TridaSerializer()));<br />
try (Input input = new Input(stream)) {<br />
   return kryo.readObject(input, resultType);<br />
}[/source]</p>
<p>Pokud budete chtít navíc nad výsledným streamem provést kompresi stačí stream obalit do <a href="https://github.com/EsotericSoftware/kryo#compression-and-encryption" target="_blank">DeflaterStreamu</a>.</p>
<h2>Kde jsem Kryo použil já a s jakým úspěchem?</h2>
<p>Kryo jsem použil v souvislosti se službou <a href="http://www.monkeytracker.cz" target="_blank">MonkeyTracker</a> pro serializaci map s objekty reprezentující kliknutí na konkrétní souřadnici před uložením do <a href="mongodb.org" target="_blank">MongoDB</a> databáze. Mongo je totiž poměrně dost známé tím, že (díky neexistenci schématu) ke každému záznamu opakovaně ukládá jak hodnoty, tak i názvy polí (problém platí ještě i pro současnou GA verzi 2.6). V rozsáhlém objektu může být pak místo pro uložení názvů polí klidně stejně tak veliké, jako místo pro hodnoty.</p>
<p>Základní představu o tom, jak vypadá můj dokument si můžete udělat <a href="https://gist.github.com/novoj/bc2fe47783bc971b61f9" target="_blank">z tohoto Gistu</a>.</p>
<p>Vzhledem k tomu, že data kliknutí neslouží k dotazování a potřebuji je vždy nahrát / uložit jako celek, mohu s nimi v I/O na úrovni MongoDB klidně nakládat jako s binárními daty a opustit "drahý" JSON formát. V hostingu využíváme drahé SSD disky a proto má úspora místa přímé finanční úspory.</p>
<h3>Výsledky testů na datech</h3>
<p>Abych si hypotézu ověřil (podle úsloví - nikdy nevěř statistikám, které si nezfalšuješ sám) vytvořil jsem jednoduchý test. Vzal jsem reálná data z měření domény <a href="http://www.stava.cz" target="_blank">www.stava.cz</a> za poslední rok a dávkově jsem nad nimi provedl serializaci a deserializaci v následujících formátech:</p>
<ol>
<li>v plném JSON formátu (použil jsem <a href="https://github.com/FasterXML/jackson" target="_blank">Jackson</a>)</li>
<li>v BSON formátu, který pro ukládání používá MongoDB (použil jsem knihovnu <a href="http://www.michel-kraemer.com/binary-json-with-bson4jackson" target="_blank">Bson4Jackson</a>)</li>
<li>jako binární data přes Java serializaci (standardní ObjectStream)</li>
<li>jako binární data přes Kryo serializaci</li>
<li>jako komprimovaná (deflater) data přes Kryo serializaci</li>
</ol>
<p>Jednalo se celkem o <strong>176 tisíc záznamů</strong> podobných tomu, který je uveden <a href="https://gist.github.com/novoj/bc2fe47783bc971b61f9" target="_blank">v Gistu</a>. Výsledky mého měření jsou zde:</p>
<div align="center"><iframe width="600" height="390" frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/1b6Qf6G1wA9Zm2JNV67WVch8zXLNR0pxuNeb3emD9TZc/pubchart?oid=1479274396&amp;format=interactive"></iframe><br/><a href="https://docs.google.com/spreadsheets/d/1b6Qf6G1wA9Zm2JNV67WVch8zXLNR0pxuNeb3emD9TZc/pubchart?oid=1479274396&amp;format=interactive" target="_blank">zobrazit graf v novém okně</a></div>
<p>Rychlost serializace pomocí Kryo (bez komprimace) je více než 3x rychlejší oproti nativní Java serializaci, rychlost deserializace dokonce 40x rychlejší! I v případě, že zapojíme komprimaci dat dosáhneme v součtu lepších výsledků (serializace je sice pomalejší, ale deserializace je i tak 9x rychlejší oproti Java deserializaci).</p>
<p>Když se potom podívám na velikost výstupního streamu, Kryo je v případě použití komprimovaného formátu šetří 11x úspornější a v případě nekomprimovaného 5x úspornější než Java serializace. Pokud porovnám velikost BSON formátku, který používá Mongo - ušetří mi komprimované Kryo přes 70% místa na disku.</p>
<div align="center"><iframe width="600" height="330" frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/1b6Qf6G1wA9Zm2JNV67WVch8zXLNR0pxuNeb3emD9TZc/pubchart?oid=1735027071&amp;format=interactive"></iframe><br/><a href="https://docs.google.com/spreadsheets/d/1b6Qf6G1wA9Zm2JNV67WVch8zXLNR0pxuNeb3emD9TZc/pubchart?oid=1735027071&amp;format=interactive" target="_blank">zobrazit graf v novém okně</a></div>
<p>Použití Kryo knihovny má v mém případě jednoznačně smysl.</p>
