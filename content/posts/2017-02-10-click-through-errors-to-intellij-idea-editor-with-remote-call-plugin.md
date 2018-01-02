---
status: publish
published: true
title: Click through errors to IntelliJ Idea editor with Remote Call plugin
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft size-thumbnail wp-image-3026\" src=\"http://blog.novoj.net/binary/2015/01/connect-150x150.jpg\"
  alt=\"connect\" width=\"150\" height=\"150\" /> Every improvement of your development
  process that is performed on daily basis is worth considering and implementing.
  Even little things can save days in budgets if you multiply them by the count of
  team members and the number of operation occurrences in the year. How do you look
  up for classes or JSP/FreeMarker/whatever templates when you run at error in them
  during development or testing? In development mode you might have your logging output
  open in IntelliJ Idea and click through exception stacktraces if any happens to
  be printed there. But there are cases when it's not possible - for example errors
  in templates won't navigate you to the source template, logs in test / preprod environment
  can't be easily consumed by your IDE etc.\r\n\r\nSo what do you do in such case?
  You search through the logs, locate the error, copy the name of the target file/class,
  go to you IDE and look up for it there. This might take tens of seconds, right?
  And now multiply it for your whole team ...\r\n\r\n"
wordpress_id: 3017
wordpress_url: http://blog.novoj.net/?p=3017
date: '2017-02-10 20:16:10 +0100'
date_gmt: '2017-02-10 19:16:10 +0100'
categories:
- Programování
- Java
- Softwarové nástroje
- Web
- English
- IntelliJ Idea
tags: []
comments: []
---
<p><img class="alignleft size-thumbnail wp-image-3026" src="http://blog.novoj.net/binary/2015/01/connect-150x150.jpg" alt="connect" width="150" height="150" /> Every improvement of your development process that is performed on daily basis is worth considering and implementing. Even little things can save days in budgets if you multiply them by the count of team members and the number of operation occurrences in the year. How do you look up for classes or JSP/FreeMarker/whatever templates when you run at error in them during development or testing? In development mode you might have your logging output open in IntelliJ Idea and click through exception stacktraces if any happens to be printed there. But there are cases when it's not possible - for example errors in templates won't navigate you to the source template, logs in test / preprod environment can't be easily consumed by your IDE etc.</p>
<p>So what do you do in such case? You search through the logs, locate the error, copy the name of the target file/class, go to you IDE and look up for it there. This might take tens of seconds, right? And now multiply it for your whole team ...</p>
<p><a id="more"></a><a id="more-3017"></a></p>
<p>Luckily there is handy plugin for IntelliJ Idea that allows you integrate errors that you visualize in your browser with the IDE directly. <a href="https://plugins.jetbrains.com/idea/plugin/6027-remote-call">Remote Call</a> plugin opens up a port 8091 locally and when you render link in HTML output in the form of:</p>
<pre style="border: 1px solid black; background-color: lightgray; color: black; padding: 0.5em;">http://localhost:8091/?message=any/path/FileName.java:89</pre>
<p>You'd be navigated directly to the file in the IDE if it's part of any of opened projects. You can navigate to any file (not only Java files) and you can also navigate to the exact line in that file. So we took this plugin and use it for these use-cases:</p>
<h3>Navigation to FreeMarker templates</h3>
<p>Whenever there is error in FreeMarker template it's get visualized like this (of course this version is used only in <a href="http://blog.novoj.net/2009/08/07/odlisujete-v-aplikaci-vyvojove-testovaci-a-produkcni-prostredi/">dev &amp; test environment</a>):</p>
<div style="text-align: center;"><iframe width="640" height="360" src="https://www.youtube.com/embed/CsVuWHR0fHk?rel=0" frameborder="0" allowfullscreen="allowfullscreen"></iframe></div>
<p>Single click will take us to the exact error line in the FreeMarker template. We only needed to override default FreeMarker exception handler (ie. implement <em>freemarker.template.TemplateExceptionHandler</em>).</p>
<h3>Navigation to Java files</h3>
<p>Whenever there is error in Java sources that results in HTTP 500 in dev/test we see this:</p>
<div style="text-align: center;"><iframe width="640" height="360" src="https://www.youtube.com/embed/EoQBFS6wyRk?rel=0" frameborder="0" allowfullscreen="allowfullscreen"></iframe></div>
<h3>Navigation in documentation</h3>
<p>We also generate some documentation from Java sources and include it in our MarkDown documentation as well. Even from there you can reach particular source in your IDE with single click:</p>
<div style="text-align: center;"><iframe width="640" height="360" src="https://www.youtube.com/embed/yTHjyU09jrQ?rel=0" frameborder="0" allowfullscreen="allowfullscreen"></iframe></div>
<h3>Navigation in e-mail notifications</h3>
<p>Finally we are notified about each error in production that affects the user or stops asynchronous processing. Each failure has to be addressed and even if there is minimum problems in the production (as it should be :) ) links are there quite handy too:</p>
<div style="text-align: center;"><iframe width="640" height="360" src="https://www.youtube.com/embed/ToCornqc2m8?rel=0" frameborder="0" allowfullscreen="allowfullscreen"></iframe></div>
