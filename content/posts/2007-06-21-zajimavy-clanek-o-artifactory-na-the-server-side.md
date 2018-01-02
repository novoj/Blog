---
status: publish
published: true
title: Zajímavý článek o Artifactory na The Server Side
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
wordpress_id: 19
wordpress_url: http://blog.novoj.net/2007/06/21/zajimavy-clanek-o-artifactory-na-the-server-side/
date: '2007-06-21 14:19:04 +0200'
date_gmt: '2007-06-21 13:19:04 +0200'
categories:
- Maven
tags: []
comments: []
---
<p>Na serveru <a href="http://www.theserverside.com" target="_blank">The Server Side</a> vyšel <a href="http://www.theserverside.com/tt/articles/article.tss?l=SettingUpMavenRepository" target="_blank">zajímavý článek o Artifactory</a>. Pro ty kdož chtějí Artifactory nasadit pro vnitrofiremní použití se jistě jedná o velmi užitečný článek. Faktem je, že Artifactory se dá velmi jednoduše nasadit i bez větších znalostí - jedná se o velmi user friendly aplikaci.</p>
<p>Jediný problém, na který jsem narazil (a který je tedy relativně dost nepříjemný) byl ve verzi 1.2.1-rc0, kdy při deployi do repository se náhodně vracel HTTP 500 - Internal Server Error, díky problematické práci se zámky v JackRabbitu. Více <a href="http://www.jfrog.org/jira/browse/RTFACT-122" target="_new">zde</a>. Problém je ale v pozdějších verzích již opraven</p>
