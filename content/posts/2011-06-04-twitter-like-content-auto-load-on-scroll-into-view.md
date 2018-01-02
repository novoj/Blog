---
status: publish
published: true
title: Twitter like content auto load on scroll into view
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img src=\"http://blog.novoj.net/binary/2011/06/jquery-logo_0.png\" alt=\"\"
  title=\"jquery-logo_0\" width=\"150\" height=\"150\" class=\"alignleft size-full
  wp-image-1507\" />I guess everyone of you already know content loading mechanism
  used on the <a href=\"http://www.twitter.com\" target=\"_blank\">Twitter</a> site.
  When you scroll down at the bottom of current page another content is loaded immediatelly
  without you clicking on any UI element. It's a very nice idea for AJAX powered listings
  and you'd probably take advantage of it on your own site too. I came to the same
  conclusion also but it seems there is no single jQuery plugin enveloping this kind
  of mechanism. Searching Google you could find several articles describing how to
  implement similar funcionality with jQuery but you wouldn't find any jQuery plugin
  ready to use. So I decided to make one for this purpose - it's called <a href=\"http://jquery.novoj.net/triggerOnView\"
  target=\"_blank\">TriggerOnView plugin</a>.\r\n\r\n"
wordpress_id: 1504
wordpress_url: http://blog.novoj.net/?p=1504
date: '2011-06-04 21:27:06 +0200'
date_gmt: '2011-06-04 20:27:06 +0200'
categories:
- English
- JavaScript
tags: []
comments: []
---
<p><img src="http://blog.novoj.net/binary/2011/06/jquery-logo_0.png" alt="" title="jquery-logo_0" width="150" height="150" class="alignleft size-full wp-image-1507" />I guess everyone of you already know content loading mechanism used on the <a href="http://www.twitter.com" target="_blank">Twitter</a> site. When you scroll down at the bottom of current page another content is loaded immediatelly without you clicking on any UI element. It's a very nice idea for AJAX powered listings and you'd probably take advantage of it on your own site too. I came to the same conclusion also but it seems there is no single jQuery plugin enveloping this kind of mechanism. Searching Google you could find several articles describing how to implement similar funcionality with jQuery but you wouldn't find any jQuery plugin ready to use. So I decided to make one for this purpose - it's called <a href="http://jquery.novoj.net/triggerOnView" target="_blank">TriggerOnView plugin</a>.</p>
<p><a id="more"></a><a id="more-1504"></a></p>
<p>Plugin itself is very subtle. Let say you have a control element somewhere that loads more content to the page when user clicks on it (imagine link named "Older records" loading another page of records at the bottom of the page). You already have loading and appending mechanism ready and working for your page - but what about not forcing user to click on the link? What about letting the "click" event happen automatically at the time user scrolls down to the bottom of the page and see this link?</p>
<p>You can enrich your site with this functionality very easily using triggerOnView jQuery plugin. All you need to do is:</p>
<p><strong>1. embed plugin to the page</strong></p>
<p>[source:xhtml]<br />
<script type="text/javascript" src="https://github.com/novoj/jQuery-triggerOnView-plugin/raw/master/src/jquery.triggeronview.js"></script><br />
[/source]</p>
<p><strong>2. alter desired link with this call</strong></p>
<p>[source:js]<br />
$("#loadContentLink").triggerOnView();<br />
[/source]</p>
<p>And that's all. When the link gets displayed to the user, click event is automatically triggered by this plugin. Ofcourse, this is example of the main use-case but you can use this for any kind of element and trigger any kind of event on it. You can also further customize triggerOnView plugin with following ...</p>
<h2>Options</h2>
<dl>
<dt>eventType (default "click")</dt>
<dd>defines the event, that should be triggered</dd>
<dt>verticalRange (default 0)</dt>
<dd>vertical offset to expand reaction area (you may need to trigger event even before element gets into the view, but user is in the vicinity of it)</dd>
<dt>horizontalRange (default 0)</dt>
<dd>horizontal offset to expand reaction area (you may need to trigger event even before element gets into the view, but user is in the vicinity of it)</dd>
<dt>singleShotOnly (default true)</dt>
<dd>if set to true triggerOnView handler is removed after event has been triggered and will trigger any event no more</dd>
<dt>callback</dt>
<dd>function that should be invoked just before event triggering, if the function returns false, triggering is stopped<br><br />
           function signature: function(domElement, settings)
   </dd>
</dl>
<h2>Download information</h2>
<p>Plugin is licensed under the MIT License.</p>
<ul>
<li><a href="http://novoj.net/jquery/triggerOnView/index.html" target="_blank">Homepage of the plugin</a></li>
<li><a href="http://novoj.net/jquery/triggerOnView/demo/demo.html" target="_blank">Live demo</a></li>
<li><a href="https://github.com/novoj/jQuery-triggerOnView-plugin/raw/master/src/jquery.triggeronview.js">Download plugin</a> (<a href="https://github.com/novoj/jQuery-triggerOnView-plugin/raw/master/src/jquery.triggeronview.min.js">minified version</a>)</li>
</ul>
<h2>Further information (based on readers' reactions)</h2>
<p>Similar mechanism is covered also by the <a href="http://www.infinite-scroll.com/" target="_blank">Infinite Scroll jQuery plugin</a> that has much longer development history (since 2008). Infinite Scroll plugin provides much more complex functionality for your paginated data but on the other hand is quite heavy weight. So when you need only triggering mechanism (having loading logic already on place) you still might recognize this plugin as a better solution for you. You should probably give a shot to the infinite scroll plugin and other articles connected to it and make well-informed decision yourself. I want to point out at least one referenced article - <a href="http://tumbledry.org/2011/05/12/screw_hashbangs_building" target="_blank">FOR GOD’S SAKE, DON’T BREAK THE BACK BUTTON</a> that brings up several interesting issues you should take into account.</p>
