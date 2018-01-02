---
status: publish
published: true
title: Maven Release Plugin releases SNAPSHOT instead of STABLE version
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft  wp-image-2843\" alt=\"maven\" src=\"http://blog.novoj.net/binary/2014/01/maven.jpg\"
  width=\"140\" height=\"140\" />There has been a lot of fuss around this issue and
  it seems there are already fixes in place. But in certain use-cases problems persist
  even if you apply fix mentioned in <a href=\"http://jira.codehaus.org/browse/MRELEASE-812\"
  target=\"_blank\">MRELEASE-812</a> issue or this <a href=\"http://www.shredzone.de/cilla/page/373/maven-release-plugin-and-git-fix.html\"
  target=\"_blank\">ShredZone article</a>. So if you experience the behaviour described
  in the title of this article keep on reading I may have a fix for you or at least
  I can help you debug the problem.\r\n\r\n"
wordpress_id: 2840
wordpress_url: http://blog.novoj.net/?p=2840
date: '2014-01-24 10:45:08 +0100'
date_gmt: '2014-01-24 09:45:08 +0100'
categories:
- Java
- Softwarové nástroje
- Maven
tags: []
comments: []
---
<p><img class="alignleft  wp-image-2843" alt="maven" src="http://blog.novoj.net/binary/2014/01/maven.jpg" width="140" height="140" />There has been a lot of fuss around this issue and it seems there are already fixes in place. But in certain use-cases problems persist even if you apply fix mentioned in <a href="http://jira.codehaus.org/browse/MRELEASE-812" target="_blank">MRELEASE-812</a> issue or this <a href="http://www.shredzone.de/cilla/page/373/maven-release-plugin-and-git-fix.html" target="_blank">ShredZone article</a>. So if you experience the behaviour described in the title of this article keep on reading I may have a fix for you or at least I can help you debug the problem.</p>
<p><a id="more"></a><a id="more-2840"></a></p>
<h2>Fix for complex folder structures</h2>
<p>If you have following project structure:</p>
<ul>
<li>superproject [Git repository root]
<ul>
<li>projectA [release target]</li>
<li>projectB [release target]</li>
</ul>
</li>
</ul>
<p>in other words you release subproject of a larger Git repository separately, you probably run at the same issue as we did. No recipe from above mentioned sources solves your problems and during release:prepare phase still no commit of stable pom.xml occurs. There is another bug in <strong>GitStatusConsumer</strong> class that checks output of the <em>git status --porcelain</em> command and verifies existency of the mentioned files on local filesystem. Regretfully it uses working directory instead of git repository root (that was previously retrieved by <em>git rev-parse --show-toplevel</em>) as the base folder and thus it constructs invalid path to the file where project folder directory is duplicated.</p>
<p><strong>Reported bug is here:</strong> <a href="http://jira.codehaus.org/browse/MRELEASE-864" target="_blank">http://jira.codehaus.org/browse/MRELEASE-864</a></p>
<p>Till the proper fix is released by Apache you can upload fixed plugin JAR into your internal repository. You can downloaded patched wars here:</p>
<p>Plugin POM: <a href="http://files.novoj.net/MavenGitPlugin/pom.xml" target="_blank">download</a><br />
Plugin JAR: <a href="http://files.novoj.net/MavenGitPlugin/maven-scm-provider-gitexe-1.9.jar" target="_blank">download</a><br />
Plugin Source JAR: <a href="http://files.novoj.net/MavenGitPlugin/maven-scm-provider-gitexe-1.9-sources.jar" target="_blank">download</a></p>
<h2>Recipe for debugging similar type of problems</h2>
<p>If you ever run into the similar issue in the future you can easily debug such problem if you do following steps:</p>
<ol>
<li>checkout maven-scm-providers repository from git:<br />
<code><span style="line-height: 1.5em;">git clone https://git-wip-us.apache.org/re</span><span style="line-height: 1.5em;">pos/asf/maven-scm.git maven-scm-git</span></code></li>
<li>open project in your IDE and place breakpoint into the class<br />
<code>org.apache.maven.scm.provider.git.gitexe.command.status.GitStatusConsumer</code></li>
<li>run maven release:prepare goal in following way<br />
<code>mvnDebug release:prepare</code></li>
<li>Attach debugger on a port 8000 (maven will wait for it) - you should use something similar to<br />
<code>-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=8000</code></li>
<li>Debug the problem in the class :)</li>
</ol>
<p>This one took me several hours but next time I will be faster ... I hope there will be no next time :)</p>
