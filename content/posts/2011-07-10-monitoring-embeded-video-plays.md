---
status: publish
published: true
title: Monitoring embeded video plays
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img src=\"http://blog.novoj.net/binary/2011/07/youtube-300x212.png\" alt=\"\"
  title=\"youtube\" width=\"150\" height=\"106\" class=\"alignleft size-medium wp-image-1562\"
  /> This week I got a simple request from our customer - to count plays of videos
  embeded at their site. We currently support different kinds of players - from FLVs
  interpeted by <a href=\"http://www.longtailvideo.com/players/jw-flv-player/\" target=\"_blank\">JwPlayer</a>,
  <a href=\"http://www.vimeo.com\" target=\"_blank\">Vimeo</a>, <a href=\"http://www.stream.cz\"
  target=\"_blank\">Czech Stream.cz</a> to <a href=\"http://www.youtube.com\" target=\"_blank\">YouTube</a>
  movies. The task was so simple that I (fool) made a prototype only for FireFox and
  estimated at most few hours for the implementation. I couldn't have been dumber
  ...\r\n\r\n"
wordpress_id: 1548
wordpress_url: http://blog.novoj.net/?p=1548
date: '2011-07-10 20:25:49 +0200'
date_gmt: '2011-07-10 19:25:49 +0200'
categories:
- Programování
- Web
- JavaScript
tags:
- youtube
- vimeo
- jwplayer
- measure
- count
- monitor video plays
comments: []
---
<p><img src="http://blog.novoj.net/binary/2011/07/youtube-300x212.png" alt="" title="youtube" width="150" height="106" class="alignleft size-medium wp-image-1562" /> This week I got a simple request from our customer - to count plays of videos embeded at their site. We currently support different kinds of players - from FLVs interpeted by <a href="http://www.longtailvideo.com/players/jw-flv-player/" target="_blank">JwPlayer</a>, <a href="http://www.vimeo.com" target="_blank">Vimeo</a>, <a href="http://www.stream.cz" target="_blank">Czech Stream.cz</a> to <a href="http://www.youtube.com" target="_blank">YouTube</a> movies. The task was so simple that I (fool) made a prototype only for FireFox and estimated at most few hours for the implementation. I couldn't have been dumber ...</p>
<p><a id="more"></a><a id="more-1548"></a></p>
<h2>First attempt</h2>
<p>The first and very naive attempt was to attach click handler via jQuery (but this didn't work at all): </p>
<p>[source lang="java"]<br />
$(document).ready(function() {<br />
   $("#video object").live("click", "alert('Played')");<br />
})<br />
[/source]</p>
<p>All players are embeded by the <a href="http://code.google.com/p/swfobject/" target="_blank">swfobject.js</a> library and in the latest (2.2) version it is possible to add callback when object is created. I wrote a simle interceptor that added onclick attribute to the DOM HTML object element and it worked! After clicking anywhere at flash my javascript closure was called:</p>
<p>[source lang="java"]<br />
var flashvars = {<br />
   file: "/video/myvideo.flv",<br />
   allowfullscreen: "false",<br />
   allowscriptaccess: "always",<br />
   image: "/img/thumbnail.jpg",<br />
   bufferlength: "0",<br />
   screencolor: "000000"<br />
};<br />
swfobject.embedSWF(<br />
   "/swf/u/jw-flv-player.swf", "video", "509", "382", "8.0.0",<br />
   null, flashvars, { wmode: "transparent", allowFullScreen: "true" }, null,<br />
   function (domObj) {<br />
      $(domObj.ref).attr("onclick", "alert('Played')");<br />
   });<br />
[/source]</p>
<p>And that was the time when I placed my bet on the realization time. During realization we found out that it didn't work anywhere else (IE, Chrome ...)</p>
<h2>Second attempt</h2>
<p>While Googling I run at <a href="http://blog.ricky-stevens.com/clickable-div-over-flash-movie/" target="_blank">interesting article</a> that seemed to address similar issue as I was trying to solve. The presented solution really works - in all browsers you have transparent area above the flash that consumes clicks anywhere on the flash movie - bingo! But clicks (and mouse movement too) are not propagated to the underlying Flash so that you cannot make the movie play.</p>
<p>I played with it for a while and consulted Google too. According to several sources - it's not possible to propagate clicks through the transparent object below. I threw away all my hopes after reading following articles <a href="http://www.vinylfox.com/forwarding-mouse-events-through-layers/" target="_blank">Forwading mouse events</a> or <a href="http://stackoverflow.com/questions/1444562/javascript-onclick-event-over-flash-object" target="_blank">StackOverflow</a>.</p>
<p>So after that it remained only to do the dirty work.</p>
<h2>Third and final solution</h2>
<p>By dirty work I mean to study JavaScript APIs of each and every used player and hook on their callbacks. At the time I didn't know whether all of them have suitable API or not. After several hours I made up few lines that did what I needed:</p>
<p>[source lang="java"]<br />
   <!-- JW PLAYER --> </p>
<p>    <script type="text/javascript"><br />
    //<![CDATA[<br />
        var flashvars = {<br />
           file: "/video/myvideo.flv",<br />
           allowfullscreen: "false",<br />
           allowscriptaccess: "always",<br />
           image: "/img/thumbnail.jpg",<br />
           bufferlength: "0",<br />
           screencolor: "000000"<br />
        };<br />
        swfobject.embedSWF(<br />
           "/swf/u/jw-flv-player.swf", "video",<br />
           "509", "382", "8.0.0", null, flashvars,<br />
           { wmode: "transparent", allowFullScreen: "true", allowScriptAccess: "always" },<br />
           {id: "video", name: "video"}<br />
        );<br />
    //]]><br />
    </script></p>
<p>   <!-- YOUTUBE --></p>
<p>    <script type="text/javascript"><br />
    //<![CDATA[<br />
        swfobject.embedSWF(<br />
           "http://www.youtube.com/v/${video.videoReference}?version=3&enablejsapi=1&playerapiid=video",<br />
           "video", "509", "306", "8.0.0", null, {},<br />
           { wmode: "transparent", allowFullScreen: "true", allowScriptAccess: "always" }<br />
        );<br />
    //]]><br />
    </script></p>
<p>   <!-- STREAM.CZ --></p>
<p>    <script type="text/javascript"><br />
    //<![CDATA[<br />
        swfobject.embedSWF(<br />
           "http://www.stream.cz/object/${video.videoReference}",<br />
           "video", "509", "311", "8.0.0", null, {},<br />
           { wmode: "transparent", allowFullScreen: "true", allowScriptAccess: "always" }<br />
        );<br />
    //]]><br />
    </script></p>
<p>   <!-- VIMEO --></p>
<p>    <script type="text/javascript"><br />
    //<![CDATA[<br />
        swfobject.embedSWF(<br />
           "http://vimeo.com/moogaloop.swf?clip_id=${video.videoReference}&server=vimeo.com&fullscreen=1&api=1&player_id=video",<br />
           "video", "509", "311", "8.0.0", null, {},<br />
           { wmode: "transparent", allowFullScreen: "true", allowScriptAccess: "always" }<br />
        );<br />
    //]]><br />
    </script><br />
[/source]</p>
<p>Important parts are <strong>allowScriptAccess: "always"</strong> and enabling javascript API (YouTube <strong>version=3&enablejsapi=1</strong>, Vimeo <strong>api=1</strong>, no parameters are needed for JwPlayer - it has API always enabled).</p>
<p>Then you need following javascript functions in place (all functions simply trigger click event of the parent div - there sits an onclick handler that performs AJAX call to increase play counter on the server side):</p>
<p>[source lang="java"]<br />
function playerReady(thePlayer) {<br />
    var jwPlayer = $("#" + thePlayer.id);<br />
    jwPlayer.get(0).addControllerListener("ITEM", "$('#" + thePlayer.id + "').parent('div').click()");<br />
}</p>
<p>function vimeo_player_loaded(playerId) {<br />
    var vimeoPlayer = $("#" + playerId);<br />
    vimeoPlayer.get(0).api_addEventListener("onPlay", "$('#" + playerId + "').parent('div').click()");<br />
}</p>
<p>function onYouTubePlayerReady(playerId) {<br />
  var ytplayer = $("#" + playerId);<br />
  ytplayer.get(0).addEventListener("onStateChange", "function(state) { if (state == 1) { $('#" + playerId + "').parent('div').click() } }");<br />
}<br />
[/source]</p>
<p>Luckily each player uses similar way of interaction. When JavaScript API is enabled and player initializes itself it calls some JS method with certain name (Youtube <strong>onYouTubePlayerReady</strong>, Vimeo <strong>vimeo_player_loaded</strong>, JwPlayer <strong>playerReady</strong>, Stream.cz <strong>playerReady</strong>). Then you need only to get the HTML Object reference and call method on the Flash interface to register your listener. Each player has its own method that does the same - first argument states the event type, second argument (String) denotes the JavaScript code, that is executed when event is triggered.</p>
<p>It's a pitty I was not able to make Stream.cz API to work. Though I decompiled their Flash code (API is not documented at all) and really thought I found a way how attach to it, it didn't call my listeners back. And I really have better things to do than to fiddle with this for hours.</p>
<h2>Disclaimer</h2>
<p>Feel free to use the code. Let's hope you save some time I had to spent to make all this work.</p>
