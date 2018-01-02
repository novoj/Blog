---
status: publish
published: true
title: Ubuntu 13.04 and IntelliJ Idea shortcut binding
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft  wp-image-2654\" title=\"Ubuntu-Unity-Logo\" src=\"http://blog.novoj.net/binary/2013/07/Ubuntu-Unity-Logo.png\"
  alt=\"\" width=\"140\" height=\"140\" />I had a <a href=\"https://twitter.com/sw_samuraj/status/351720440068177920\"
  target=\"_blank\">conversation</a> about IntelliJ Idea shortcut bindings conflicting
  with default shortcuts of Ubuntu/Unity OS. Well, it's a real problem, your muscle
  memory can be a tough beast. You can re-lean a shortcut or two but it's hard to
  change your habits completely after years of coding in IntelliJ Idea. And I want
  to concentrate on different things than to learn again shortcuts I am used to use.
  Because I am developer my IDE is more important for me than the OS and that means
  that shortcuts of the OS must go away or be changed. There is no other way possible.\r\n\r\n"
wordpress_id: 2639
wordpress_url: http://blog.novoj.net/?p=2639
date: '2013-07-12 22:36:45 +0200'
date_gmt: '2013-07-12 21:36:45 +0200'
categories:
- English
- Linux
tags: []
comments:
- id: 152058
  author: koubel
  author_email: koubel@volny.cz
  author_url: http://www.mirin.cz
  date: '2013-08-02 15:52:04 +0200'
  date_gmt: '2013-08-02 14:52:04 +0200'
  content: Simple solution without any change to Ubuntu key mapping - utilize ideavim,
    vim plugin for typing in IntelliJ - It works very good and supports so complicated
    things like text objects
- id: 152243
  author: Shervin
  author_email: shervin@mailinator.com
  author_url: ''
  date: '2013-11-05 21:46:17 +0100'
  date_gmt: '2013-11-05 20:46:17 +0100'
  content: Thanks. I have the same problem. I will have to change all the ubuntu key
    bindings. Really a pain in the ass!
---
<p><img class="alignleft  wp-image-2654" title="Ubuntu-Unity-Logo" src="http://blog.novoj.net/binary/2013/07/Ubuntu-Unity-Logo.png" alt="" width="140" height="140" />I had a <a href="https://twitter.com/sw_samuraj/status/351720440068177920" target="_blank">conversation</a> about IntelliJ Idea shortcut bindings conflicting with default shortcuts of Ubuntu/Unity OS. Well, it's a real problem, your muscle memory can be a tough beast. You can re-lean a shortcut or two but it's hard to change your habits completely after years of coding in IntelliJ Idea. And I want to concentrate on different things than to learn again shortcuts I am used to use. Because I am developer my IDE is more important for me than the OS and that means that shortcuts of the OS must go away or be changed. There is no other way possible.</p>
<p><a id="more"></a><a id="more-2639"></a></p>
<p>Luckily Ubuntu/Unity allows you to change  a lot of shortcuts and those you can't change by default tools you can change by <a href="http://www.noobslab.com/2013/04/latest-unity-tweak-tool-for-ubuntu-1304.html" target="_blank">Unity Tweak Tool</a>. It's a pity Unity doesn't take advantage of Win(Super) key as much as it could. For me the solution was to go through all OS shortcut combinations and change each use of Ctrl key with Windows key (&lt;Super&gt;) and disable a lot of default bindings entirely (I wouldn't use them anyway). There is also a thread in <a href="http://youtrack.jetbrains.com/issue/IDEA-55796" target="_blank">IntelliJ Idea YouTrack</a> that suggests to create compatible shortcut bindings for IntelliJ Idea but I think that it's the OS that should go aside in this case.</p>
<p>If anyone wants to be inspired here are my OS bindings that don't conflict with IDE (and sorry for Czech key names - I use native localization of Ubuntu and I was lazy to change it because of these few screenshots):</p>
<h2>Unity Tweak Tool</h2>
<h3>Unity settings</h3>
<p><a href="http://blog.novoj.net/binary/2013/07/unity-switcher.png" target="_screenshot"><img class="size-medium wp-image-2658" style="display: inline; margin: 5px;" title="unity-switcher" src="http://blog.novoj.net/binary/2013/07/unity-switcher-300x267.png" alt="" width="300" /></a><a href="http://blog.novoj.net/binary/2013/07/unity-additional.png" target="_screenshot"><img class="size-medium wp-image-2657" style="display: inline; margin: 5px;" title="unity-additional" src="http://blog.novoj.net/binary/2013/07/unity-additional-300x267.png" alt="" width="300" /></a></p>
<h3>Window manager settings</h3>
<p>I was suprised that Unity allows you to easily use magnifier glass as I was seeing on Apple guys presentations before. See the first image settings.</p>
<p><a href="http://blog.novoj.net/binary/2013/07/window-manager-general.png" target="_screenshot"><img class="alignnone size-medium wp-image-2659" style="display: inline; margin: 5px;" title="window-manager-general" src="http://blog.novoj.net/binary/2013/07/window-manager-general-300x267.png" alt="" width="300" height="267" /></a><a href="http://blog.novoj.net/binary/2013/07/window-manager-spread.png" target="_screenshot"><img class="alignnone size-medium wp-image-2660" style="display: inline; margin: 5px;" title="window-manager-spread" src="http://blog.novoj.net/binary/2013/07/window-manager-spread-300x267.png" alt="" width="300" height="267" /></a><a href="http://blog.novoj.net/binary/2013/07/window-manager-workspace.png" target="_screenshot"><img class="alignnone size-medium wp-image-2661" style="display: inline; margin: 5px;" title="window-manager-workspace" src="http://blog.novoj.net/binary/2013/07/window-manager-workspace-300x267.png" alt="" width="300" height="267" /></a></p>
<h2>Unity Ubuntu Settings</h2>
<p>The single thing a wasn't able to get rid of is to open Nautilus with Trash folder by combination of+T. I used this for opening terminal, but unfortunately I will have to re-learn this single shortcut. What I really like though is new mechanism of changing windows - by Alt-Tabbing I change windows of distinct applications, but by Alt+; (my shortcut) I change windows of the same application. That really comes handy.</p>
<p><a href="http://blog.novoj.net/binary/2013/07/settings-navigation.png" target="_screenshot"><img class="alignnone size-medium wp-image-2673" style="display: inline; margin: 5px;" title="settings-navigation" src="http://blog.novoj.net/binary/2013/07/settings-navigation-262x300.png" alt="" width="262" height="300" /></a><a href="http://blog.novoj.net/binary/2013/07/settings-window.png" target="_screenshot"><img class="alignnone size-medium wp-image-2677" style="display: inline; margin: 5px;" title="settings-window" src="http://blog.novoj.net/binary/2013/07/settings-window-300x253.png" alt="" width="300" height="253" /></a><a href="http://blog.novoj.net/binary/2013/07/settings-screenshots.png" target="_screenshot"><img class="alignnone size-medium wp-image-2676" style="display: inline; margin: 5px;" title="settings-screenshots" src="http://blog.novoj.net/binary/2013/07/settings-screenshots-300x159.png" alt="" width="300" height="159" /></a><a href="http://blog.novoj.net/binary/2013/07/settings-runners.png" target="_screenshot"><img class="alignnone size-medium wp-image-2675" style="display: inline; margin: 5px;" title="settings-runners" src="http://blog.novoj.net/binary/2013/07/settings-runners-300x159.png" alt="" width="300" height="159" /></a><a href="http://blog.novoj.net/binary/2013/07/settings-system.png" target="_screenshot"><img class="alignnone size-medium wp-image-2679" style="display: inline; margin: 5px;" title="settings-system" src="http://blog.novoj.net/binary/2013/07/settings-system-300x169.png" alt="" width="300" height="169" /></a><a href="http://blog.novoj.net/binary/2013/07/settings-access.png" target="_screenshot"><img class="alignnone size-medium wp-image-2674" style="display: inline; margin: 5px;" title="settings-access" src="http://blog.novoj.net/binary/2013/07/settings-access-300x169.png" alt="" width="300" height="169" /></a><a href="http://blog.novoj.net/binary/2013/07/settings-media.png" target="_screenshot"><img class="alignnone size-medium wp-image-2678" style="display: inline; margin: 5px;" title="settings-media" src="http://blog.novoj.net/binary/2013/07/settings-media-300x169.png" alt="" width="300" height="169" /></a></p>
<h2>Overall experience of upgrading from 11.10 to 13.04</h2>
<p>I haven't run at any blocking issue with Raring Ringtail so far and system seems relatively stable. I was able to copy most of my configuration from 11.10 so that the installation process was really quick. It seems that most of the installation tips from my <a href="http://blog.novoj.net/poznamky-k-instalaci-ubuntu/" target="_blank">original article</a> are still applicable and those that don't I've updated in the process of upgrading. You may also find interesting bits there ...</p>
