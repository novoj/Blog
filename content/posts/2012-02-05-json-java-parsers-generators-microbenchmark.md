---
status: publish
published: true
title: Json Java parsers / generators microbenchmark
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft size-full wp-image-1834\" title=\"JSON\" src=\"http://blog.novoj.net/binary/2012/02/json160.gif\"
  alt=\"\" width=\"120\" height=\"120\" /> A month ago I had an incident in production
  that was caused, as I found out later, by poor performance of used JSON parser library.
  I've optimalized the code and managed to solve it but decided to look for another
  library with better performance characteristics. I searched for some existing benchmarks
  and found two of them - one is for <a href=\"http://martinadamek.com/2011/02/01/adding-gson-to-android-json-parser-comparison/\"
  target=\"_blank\">JSON manipulation on Android</a> and the second one is <a href=\"https://github.com/eishay/jvm-serializers/wiki/\"
  target=\"_blank\">thorough serialization test focused on different use-cases</a>
  than I had. So I decided to write my own microbenchmark copying the use-case I had
  in the production.\r\n\r\nThere are many differencies among JSON libraries regarding
  their features and resulting performance. So if you want to know my findings continue
  reading ...\r\n\r\n"
wordpress_id: 1824
wordpress_url: http://blog.novoj.net/?p=1824
date: '2012-02-05 10:41:22 +0100'
date_gmt: '2012-02-05 09:41:22 +0100'
categories:
- Programování
- Java
tags: []
comments:
- id: 61139
  author: Tomek Kaczanowski
  author_email: tkaczano@poczta.onet.pl
  author_url: http://kaczanowscy.pl/tomek
  date: '2012-02-06 11:46:09 +0100'
  date_gmt: '2012-02-06 10:46:09 +0100'
  content: So you do not recommend Protostuff JSON because it is harder to use than
    the competition, right?
- id: 61144
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-02-06 12:41:11 +0100'
  date_gmt: '2012-02-06 11:41:11 +0100'
  content: "Yes, you're right - in terms of performance Protostuff seems to be one
    of the best. But as I said in the beginning of the article: \r\n\r\n\"I’ve used
    all libraries by same naive approach – grab it and use it the simpliest way possible.
    No tweaking, no optimalizing whatsoever (that’s the way they are usually used).\"\r\n\r\nThis
    library took me most time to integrate among all tested libraries, so I would
    recommend it for more serious work when you have time to study and try. For quick
    usage I wouldn't go that way because Jackson or GSon are performant enough and
    much easier to use."
- id: 61148
  author: geemang
  author_email: geemang_2000@yahoo.com
  author_url: ''
  date: '2012-02-06 14:09:43 +0100'
  date_gmt: '2012-02-06 13:09:43 +0100'
  content: It'd be interesting to see how the JSON support in Groovy 1.8 measures
    up.
- id: 61152
  author: Leo
  author_email: leo@thinkberg.com
  author_url: http://twimpact.com/
  date: '2012-02-06 15:58:36 +0100'
  date_gmt: '2012-02-06 14:58:36 +0100'
  content: "I did extensive testing of json parsers with really large json data sets
    (parsing alone) and we never use POJO because it is simply a speed bump. In my
    tests, no other parser matched the speed of smart-json which is available in maven
    in it's 1.0.9 version.\r\n\r\nOur use-case is slightly different though, we have
    to parse the json as fast as possible into managable hash maps to stay real-time."
- id: 61154
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-02-06 16:28:05 +0100'
  date_gmt: '2012-02-06 15:28:05 +0100'
  content: "Yes, I focused on POJO serialization / deserialization which is quite
    common in web space (IMHO). Though according to this stats:\r\n\r\nhttps://github.com/eishay/jvm-serializers/wiki/\r\n\r\nJson-Smart
    places itself in the middle of the performance chart. Maybe in some specific use-case
    it jumps up?\r\n\r\nIf you have your tests somewhere public it might be interesting
    to other readers to study your use-case it they give different results."
- id: 61162
  author: Steve Loughran
  author_email: steve.loughran@gmail.com
  author_url: http://steveloughran.blogspot.com/
  date: '2012-02-06 18:20:44 +0100'
  date_gmt: '2012-02-06 17:20:44 +0100'
  content: |-
    I had to rip all of jsonlib out last week as it seems to auto-parse strings beginning with "[" or "{" as json whenever you insert them into the object model, or attach a parent to another node.

    <a href="http://steveloughran.blogspot.com/2012/02/just-because-you-can-rewrite-your.html" rel="nofollow">
    http://steveloughran.blogspot.com/2012/02/just-because-you-can-rewrite-your.html
    </a>

    Try testing what the libs do with multiple entries of the same name; json-lib assumes you wanted an array of that name and aggregates them. similarly, see what rejects illegal JSON, such as unquoted keys: {illegal:true} or trailing commas. The authors think they are being helpful, but they are encouraging you to create invalid JSON.
- id: 61168
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-02-06 20:08:17 +0100'
  date_gmt: '2012-02-06 19:08:17 +0100'
  content: Oh well, that's nasty. I haven't run at this issue yet. Thanks for sharing!
- id: 61356
  author: Pratik Parikh
  author_email: pratik.p.parikh@gmail.com
  author_url: ''
  date: '2012-02-09 18:23:27 +0100'
  date_gmt: '2012-02-09 17:23:27 +0100'
  content: "Can you also put https://github.com/beckchr/staxon/ in equation to tell
    us how it performs.  It seems like you have a set test that you running against
    all the api. It would really help to see how this new api performances in compare
    to Jackson.  I am personally a fan of Jackson and their implementation but like
    the concept being staxon  and the conversion capability in place between xml and
    json.\r\n\r\n\r\nThanks for sharing"
- id: 61392
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-02-10 09:35:33 +0100'
  date_gmt: '2012-02-10 08:35:33 +0100'
  content: "Staxon is focused on SAX like reading / writing and therefore I didn’t
    include it into the test suite in the first time. Test suite measures direct POJO
    serialization / deserialization and this is not main aim of the Staxon as I get
    it.\r\n\r\nAfter reading some docs I found out, that with combination with JaxB
    tags Staxson could be used for POJO serialization / deserialization so I’ll try
    to prepare a test for it. Check updates of this article please."
- id: 61512
  author: jesse wilson
  author_email: jesse@swank.ca
  author_url: http://publicobject.com
  date: '2012-02-12 04:43:56 +0100'
  date_gmt: '2012-02-12 03:43:56 +0100'
  content: "Source code? My measurements showed a closer race between Gson and Jackson.\r\n\r\nDon't
    forget that gson's jar is way smaller than Jackson's: The gson-2.1.jar is 176
    Kib; this includes both streaming and binding. To do both \r\nwith Jackson you'll
    need 874 Kib in .jar files."
- id: 61548
  author: sreenath v
  author_email: srinathv77@gmail.com
  author_url: http://www.techiesinfo.com
  date: '2012-02-12 20:41:04 +0100'
  date_gmt: '2012-02-12 19:41:04 +0100'
  content: "Jackson for mobile device you can use minified jar which is ~134kb.\r\nJackson
    mini doesn't support annotations and which off-course is fine for mobile devices."
- id: 61757
  author: Kazuaki Maeda
  author_email: kmaeda@gmail.com
  author_url: ''
  date: '2012-02-16 07:17:30 +0100'
  date_gmt: '2012-02-16 06:17:30 +0100'
  content: "I'm very interested in your work.\r\n\r\nI tried serialization benchmark
    last year.\r\nBut the formats to serialize were XML and binary based.\r\nI would
    like to compare many approaches of object serialization from qualitative and quantitative
    aspects.\r\n\r\nCan I use your testing programs and the results in my benchmark?\r\nAfter
    finishing the experiments, I can open the results on my web site.\r\n\r\nThank
    you."
- id: 61759
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-02-16 08:20:41 +0100'
  date_gmt: '2012-02-16 07:20:41 +0100'
  content: "Some more detail benchmarks are located at https://github.com/eishay/jvm-serializers/wiki/
    (that I referenced in the article perex). But there are many approaches that could
    be tested - I took only one of them (POJO related).\r\n\r\nOf course you can use
    my source codes and use it for you own experimenting. Everything at this blog
    is Creative Commons licensed, so do with it what you will. Sources are at GitHub
    so you can fork easily if you like.\r\n\r\nSharing your results will be highly
    appreciated."
- id: 62053
  author: Kazuaki Maeda
  author_email: kmaeda@gmail.com
  author_url: ''
  date: '2012-02-22 02:36:44 +0100'
  date_gmt: '2012-02-22 01:36:44 +0100'
  content: "I have read your source code in groovy. Thank you.\r\n\r\nIn org/novoj/json/transformer/protostuff/ProtostuffIO.groovy,
    you wrote\r\n    JsonIOUtil.writeTo(out, photoAlbum, schema, true)\r\nThis statement
    serializes attribute names in numeric, for example,\r\n    {\r\n    \"1\":1,\r\n
    \   \"2\":\"John Doe\",\r\n    \"3\":\"Speed kills!\",\r\n    \"4\":1\r\n    }\r\nIf
    you changed it to\r\n    JsonIOUtil.writeTo(out, photoAlbum, schema, false)\r\n,
    the code serializes them in alphabetic,\r\n   {\r\n    \"id\":1,\r\n    \"name\":\"John
    Doe\",\r\n    \"motto\":\"Speed kills!\",\r\n    \"gender\":1\r\n    }\r\nThis
    is a small thing, but I prefer the latter(false) to the former(true).\r\n\r\nAnd
    I would like to know about your information in English.\r\nI can not read your
    mother language :-&lt;\r\nWhen I write technical documents, I would like to your
    name in acknowledgements.\r\nI wrote my contact information in my web page,\r\n
    \   http://www.rugson.org/\r\nCould you send email to me, please.\r\nThank you
    very much."
- id: 64020
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-03-18 09:36:26 +0100'
  date_gmt: '2012-03-18 08:36:26 +0100'
  content: Staxon tests were finally added. I had some issues with switching serialization/deserialization
    factory in runtime. It seems library is optimized for choosing one factory at
    the start of the application and never change it (what is rather common usage
    I suppose).
- id: 64691
  author: Cowtowncoder
  author_email: cowtowncoder@yahoo.com
  author_url: http://cowtowncoder.com/blog/blog.html
  date: '2012-03-27 23:42:38 +0200'
  date_gmt: '2012-03-27 22:42:38 +0200'
  content: "Your findings are odd, because using POJOs should be faster than HashMaps,
    not slower. HashMaps have higher overhead than basic Java objects (due to key/value
    lookups), use up more memory, so their use does not make much sense to me for
    high-performance use cases.\r\nPOJO binding is definitely faster than Maps with
    Jackson, at any rate. I have not found json-smart particularly fast -- it appears
    to be medium speed (see [https://github.com/eishay/jvm-serializers/wiki]), which
    is good enough for many use cases."
- id: 84825
  author: wenshao
  author_email: szujobs@gmail.com
  author_url: http://fastjson
  date: '2012-08-02 13:27:45 +0200'
  date_gmt: '2012-08-02 12:27:45 +0200'
  content: "why not include fastjson?\r\n\r\nhttps://github.com/eishay/jvm-serializers/wiki/Staging-Results\r\n\r\nfastjson
    faster than jackson, it's fast!"
- id: 84826
  author: wenshao
  author_email: szujobs@gmail.com
  author_url: http://fastjson
  date: '2012-08-02 13:28:39 +0200'
  date_gmt: '2012-08-02 12:28:39 +0200'
  content: "fastjson hosting in github: \r\nhttps://github.com/AlibabaTech/fastjson"
- id: 84888
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-08-02 17:06:37 +0200'
  date_gmt: '2012-08-02 16:06:37 +0200'
  content: "If it supports POJO serialization and deserialization I would add it when
    have some spare time. According to docs it is supposed to work with POJOs. \r\n\r\nOr
    you can make benchmark test on your own and create a pull request. Thanks for
    suggestion."
- id: 84992
  author: wenshao
  author_email: szujobs@gmail.com
  author_url: http://fastjson
  date: '2012-08-03 01:30:25 +0200'
  date_gmt: '2012-08-03 00:30:25 +0200'
  content: "fastjson support POJO, it's api very simple:\r\n\r\nserialize API : JSON.toJSONString(obj);\r\ndeserialize
    API : VO vo = JSON.parseObject(\"...\", VO.class);"
- id: 85471
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-08-04 20:53:45 +0200'
  date_gmt: '2012-08-04 19:53:45 +0200'
  content: 'Update 8/2012: Fastjson tests was added – it placed itself among the best
    performing libraries. Serialization is slightly worse than Jackson but in deserialization
    it is the clear winner.'
- id: 86331
  author: Cowtowncoder
  author_email: cowtowncoder@yahoo.com
  author_url: http://cowtowncoder.com/blog/blog.html
  date: '2012-08-08 01:11:09 +0200'
  date_gmt: '2012-08-08 00:11:09 +0200'
  content: "Good to see FastJSON included too -- it is definitely fast, as name implies
    (which is not always the case with new libs).\r\n\r\nOne other thing that'd be
    nice to test if you happen to have time is Jackson Afterburner module from:\r\n\r\nhttps://github.com/FasterXML/jackson-module-afterburner\r\n\r\nwhich
    speeds up Jackson serialization and deserialization a bit, by using dynamic byte
    code generation."
- id: 93320
  author: ryu
  author_email: maetee@maya-wizard.com
  author_url: ''
  date: '2012-09-20 15:40:37 +0200'
  date_gmt: '2012-09-20 14:40:37 +0200'
  content: "Try this solution in very easy way, copy and paste service or website
    URL and then click go\r\n\r\nhttp://www.maya-wizard.com/services/json2java.php"
- id: 102556
  author: JSON Parser &laquo; Peace be with you
  author_email: ''
  author_url: http://polimetla.com/2012/10/31/json-parser/
  date: '2012-10-31 23:03:37 +0100'
  date_gmt: '2012-10-31 22:03:37 +0100'
  content: "[...] http://blog.novoj.net/2012/02/05/json-java-parsers-generators-microbenchmark/
    [...]"
- id: 152046
  author: 'JSON y Java: Introducción a Gson | danielme.com'
  author_email: ''
  author_url: http://danielme.com/2013/07/11/json-y-java-introduccion-a-gson/
  date: '2013-07-11 19:12:25 +0200'
  date_gmt: '2013-07-11 18:12:25 +0200'
  content: "[...] si necesitamos optimizar al máximo los procesos que impliquen estas
    coversiones entre Java y JSON. Aquí hay un benchmark muy interesante sobre varias
    librerias de parseo en las que Gson no sale mal [...]"
- id: 154449
  author: Comment j&rsquo;ai battu CORBA | OCTO talks !
  author_email: ''
  author_url: http://blog.octo.com/comment-jai-battu-corba/
  date: '2014-12-22 19:20:37 +0100'
  date_gmt: '2014-12-22 18:20:37 +0100'
  content: "[&#8230;] une sérialisation rapide :  Faisant confiance à la communauté,
    ainsi qu&rsquo;à quelques benchmarks , je choisis de prendre Jackson comme parseur
    JSON. (Par la suite des essais avec boon ou [&#8230;]"
---
<p><img class="alignleft size-full wp-image-1834" title="JSON" src="http://blog.novoj.net/binary/2012/02/json160.gif" alt="" width="120" height="120" /> A month ago I had an incident in production that was caused, as I found out later, by poor performance of used JSON parser library. I've optimalized the code and managed to solve it but decided to look for another library with better performance characteristics. I searched for some existing benchmarks and found two of them - one is for <a href="http://martinadamek.com/2011/02/01/adding-gson-to-android-json-parser-comparison/" target="_blank">JSON manipulation on Android</a> and the second one is <a href="https://github.com/eishay/jvm-serializers/wiki/" target="_blank">thorough serialization test focused on different use-cases</a> than I had. So I decided to write my own microbenchmark copying the use-case I had in the production.</p>
<p>There are many differencies among JSON libraries regarding their features and resulting performance. So if you want to know my findings continue reading ...</p>
<p><a id="more"></a><a id="more-1824"></a></p>
<h2>Benchmarks (2012-03-18)</h2>
<p>Tested use case is a serialization of a rich POJO with collection of inner POJOs referencing another POJO (see PhotoAlbum model object). Tested JSON parser must have direct POJO to JSON serialization and deserialization support in order to get into the suite. I've used all libraries by same naive approach - grab it and use it the simpliest way possible. No tweaking, no optimalizing whatsoever (that's the way they are usually used). Average size of generated JSON data is 160KB, so it is rather big. The problem in production was caused by data of 33KB size in my case.</p>
<p><strong>Disclaimer</strong> microbenchmarking results may be misleading - if you want to be sure write your own tests, with your custom data on your hardware to be really sure.</p>
<h3>Update 2012-03-18</h3>
<p>I've added new tests for Staxon - with three different serialization factories - internal, GSon and Jackson. New section added. I've re-run all the tests and updated the numbers.</p>
<h3>Setup</h3>
<p><strong>Hardware:</strong> Intel® Core™2 Duo CPU T7500 @ 2.20GHz × 2, SSD disk (but File IO time is not counted)<br />
<strong>Software:</strong> Java(TM) SE Runtime Environment (build 1.6.0_23-b05), Java HotSpot(TM) Server VM on Ubuntu Linux 11.10 32-bit<br />
<strong>JVM options:</strong> -Xmx32m -server</p>
<p>Data value being tested: <a href="https://github.com/novoj/JavaJsonPerformanceTest/blob/master/src/main/java/org/novoj/json/model/PhotoAlbum.java" target="_blank">PhotoAlbum</a>.</p>
<h3>Methodology:</h3>
<p>Before taking measurements I warmed things up by running the task 250 times, next 3000 loops are counted. No other operations except the serialization or deserialization is measured. Finally average execution time is taken for each operation and library. I ran tests as a full suite and separately by each library - but the results didn't differ much.</p>
<p>Tested libraries and their versions:</p>
<ol>
<li>FlexJson (2.1)</li>
<li>GSon (2.1)</li>
<li>Jackson (2.0.4)</li>
<li>JsonLib (2.4)</li>
<li>JsonMarshaller (0.21)</li>
<li>JsonSmart (2.0-beta2)</li>
<li>Protostuff JSON (1.0.4)</li>
<li>XStream (1.4.2)</li>
<li>Staxon (1.0)</li>
</ol>
<p>Testing code is placed on GitHub: <a href="https://github.com/novoj/JavaJsonPerformanceTest" target="_blank">https://github.com/novoj/JavaJsonPerformanceTest</a></p>
<h2>Results and comments</h2>
<h3><a href="http://flexjson.sourceforge.net/" target="_blank">FlexJson</a></h3>
<p>There are a few catches when using this library. In order to serialize POJO right you have to exclude serialization of a class property deep-wise and include serialization of collections as they are not serialized by default. Library has neither problems with Date handling nor with using generated Groovy classes. I haven't noticed any support for resolution of circular references. Library is easily reachable in maven repos. Main advantage of this library according authors is ability to pick and choose specific properties and structures that should be converted to/from JSON.</p>
<p><strong>Serialization:</strong> 5.978ms / 1 PhotoAlbum, JSON file size 165KB<br />
<strong>Deserialization:</strong> 14.314ms / 1 PhotoAlbum</p>
<h3><a href="http://code.google.com/p/google-gson/" target="_blank">GSon</a></h3>
<p>It's very sophisticated and configurable library - it supports versioning, custom handlers and instantiation factories, exclusion of certain properties, custom naming. Library is super easy to use with good documentation. I haven't noticed any support for resolution of circular references, handling Groovy classes or Date objects. Library is easily reachable in maven repos.</p>
<p><strong>Serialization:</strong> 5.11ms / 1 PhotoAlbum, JSON file size 169KB<br />
<strong>Deserialization:</strong> 9.396667ms / 1 PhotoAlbum</p>
<h3><a href="http://jackson.codehaus.org/" target="_blank">Jackson</a></h3>
<p>It claims to be a fastest Java JSON library among all - and according to my statistics - they are quite right. Even then it has very rich feature set that exceeds what is provided by GSon (but no versioning support out of the box). It is super easy to use, it has native support for Dates (and JodaTime too!).</p>
<p><strong>Serialization:</strong> 1.291ms / 1 PhotoAlbum, JSON file size 165KB<br />
<strong>Deserialization:</strong> 1.588ms / 1 PhotoAlbum</p>
<h3><a href="http://json-lib.sourceforge.net/" target="_blank">JSON-Lib</a></h3>
<p>This library is very configurable but has some glitches - for example deserializing of Date objects doesn't work out of the box and you have to provide type handlers. It has several strategies how to cope with circular referencies. Very good documentation is provided and it has integration with Groovy. It is easily reachable from maven repos (but beware you have to provide classifier=jdk15). This library burned me at the production - as you can see it has really bad performance stats.</p>
<p><strong>Serialization:</strong> 17.592ms / 1 PhotoAlbum, JSON file size 168KB<br />
<strong>Deserialization:</strong> 92.248ms / 1 PhotoAlbum</p>
<h3><a href="http://code.google.com/p/jsonmarshaller/" target="_blank">JsonMarshaller</a></h3>
<p>It has problems with serialization / deserialization of Groovy objects (throws exception regarding ASM). It has no Date support built-in. It requires you to place annotations into your model (or DTO) classes that might be rather uncomfortable (and maybe unacceptable) in some cases. Documentation is quite poor. It is not placed in Maven repos.</p>
<p><strong>Serialization:</strong> 3.8146667ms / 1 PhotoAlbum, JSON file size 165KB<br />
<strong>Deserialization:</strong> 6.125ms / 1 PhotoAlbum</p>
<h3><a href="http://code.google.com/p/json-smart/" target="_blank">Json Smart</a></h3>
<p>This library is very simplistic and small - POJO deserialization comes first in version 2, which is currently in beta. Almost nothing is configurable, documentation is poor. Library is not reachable in Maven repos. It's not currently possible to deserialize Date objects, more than that there is no configurable option to add custom type handler, so that deserialization of object containing date is not possible at all.</p>
<p><strong>Serialization:</strong> 4.026ms / 1 PhotoAlbum, JSON file size 172KB<br />
<strong>Deserialization:</strong> -</p>
<h3><a href="http://code.google.com/p/protostuff/" target="_blank">Protostuff - JSON</a></h3>
<p>Powerful library requiring rather complicated setup when not using RuntimeSchema generator. In standard setup I believe library is used to do much more stuff than I've used it for. JSON transformations are just piece of work it can do (it can convert to YAML, XML and more). It had no problems with Date objects and Groovy classes. Library is accessible in Maven repos.</p>
<p><strong>Serialization:</strong> 1.9116666ms / 1 PhotoAlbum, JSON file size 165KB<br />
<strong>Deserialization:</strong> 1.2213334ms / 1 PhotoAlbum</p>
<h3><a href="http://xstream.codehaus.org/" target="_blank">XStream</a></h3>
<p>Library formerly used to serialize and deserialize to / from XML internally using <a href="http://jettison.codehaus.org/" target="_blank">Jettison</a> to transfrom data to / from JSON. It is easy to use, highly customizable and supports resolution of circular references. Library handles Date objects out of the box, it has no problem with Groovy classes and is placed in Maven repos.</p>
<p><strong>Serialization:</strong> 76.84967ms / 1 PhotoAlbum, JSON file size 171KB<br />
<strong>Deserialization:</strong> 26.361ms / 1 PhotoAlbum</p>
<h3><a href="https://github.com/beckchr/staxon/wiki/" target="_blank">Staxon</a></h3>
<p>Staxon aims primarily on the streaming API and presented use-case is not its primary kind of targeted usage. Nevertheless I was asked in the commentaries section to add some tests for this library so I did so. Staxon seems very easy to use, very well documented. It handles Date objects out of the box and is placed in Maven repos. It's performance is not one of the best - seems rather average for the use-case tested, but remember - when using streaming style or reading / writing results might be different.</p>
<p><strong>Staxon over GSon</strong><br />
<strong>Serialization:</strong> 7.510667ms / 1 PhotoAlbum, JSON file size 176KB<br />
<strong>Deserialization:</strong> 12.171ms / 1 PhotoAlbum</p>
<p><strong>Staxon over Jackson</strong><br />
<strong>Serialization:</strong> 4.8446665ms / 1 PhotoAlbum, JSON file size 176KB<br />
<strong>Deserialization:</strong> 11.099ms / 1 PhotoAlbum</p>
<p><strong>Staxon default implementation</strong><br />
<strong>Serialization:</strong> 6.3436666ms / 1 PhotoAlbum, JSON file size 176KB<br />
<strong>Deserialization:</strong> 15.087ms / 1 PhotoAlbum</p>
<h3><a href="https://github.com/AlibabaTech/fastjson/wiki" target="_blank">Fastjson</a></h3>
<p>Young library (since mid 2011) that performs really fast. It dynamically creates specific serializer / deserializer class using ASM for each custom POJO type. It has considerable <a href="https://github.com/AlibabaTech/fastjson/blob/master/src/main/java/com/alibaba/fastjson/serializer/SerializerFeature.java" target="_blank">amount of processing features</a> though not very well documented. Documentation as a whole is very poor but as long as it works you are safe to go. Library handles Date objects out of the box, it has no problem with Groovy classes and is placed in Maven repos.</p>
<p><strong>Serialization:</strong> 1.88ms / 1 PhotoAlbum, JSON file size 165KB<br />
<strong>Deserialization:</strong> 1.02ms / 1 PhotoAlbum</p>
<h3>Summary</h3>
<p>All stats are clearly comparable on the following graph:</p>
<p><img src="https://docs.google.com/spreadsheet/oimg?key=0AqgjPgS28rtndFo0RnpOR2Zsckg5S2xUcVFDZlFMM2c&amp;oid=1&amp;zx=rwrcgsbcamwp" alt="" /></p>
<p>My conclusion is that when you need easily serialize / deserialize Java POJOs without sacrificing performance and have some backup in terms of extensibility and configurability you should choose Jackson, Fastjson or GSon library. Jackson is my winner and I am going to migrate all of my code to this one. Any comments and thoughts are appreciated (and remember this is only microbenchmark so make tests for your own use-cases if you want to be 100% sure)!</p>
<p><strong>Update 8/2012</strong> Fastjson tests was added - it placed itself among the best performing libraries. Serialization is slightly worse than Jackson but in deserialization it is the clear winner.</p>
