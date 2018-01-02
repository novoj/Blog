---
status: publish
published: true
title: 'Teamcity & CVS & Maven: release on server'
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "If you use Maven 2 and Teamcity integration server, you might want to perform
  releases on server. Although it's not so complicated, some things must fit one into
  another and you might spend a lot of time till you find out how to configure pom.xml
  and build configuration. For those of you, who need to setup it, this article could
  come quite handy.\r\n\r\n"
wordpress_id: 77
wordpress_url: http://blog.novoj.net/2008/06/28/teamcity-cvs-maven-release-on-server/
date: '2008-06-28 20:12:07 +0200'
date_gmt: '2008-06-28 19:12:07 +0200'
categories:
- Softwarové nástroje
- Maven
- English
- TeamCity
tags: []
comments:
- id: 6915
  author: Paweł Zubkiewicz
  author_email: pan.zupa@gmail.com
  author_url: http://pawelzubkiewicz.blogspot.com/
  date: '2009-03-16 10:31:09 +0100'
  date_gmt: '2009-03-16 09:31:09 +0100'
  content: Hi, very nice post. Indeed it's not rocket science &amp; setting up release
    plugin is much harder then TeamCity. I appreciate your effort. Thanks a lot.
- id: 6926
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-03-17 05:34:36 +0100'
  date_gmt: '2009-03-17 04:34:36 +0100'
  content: I completely agree. I setuped relase proces two times in different companies
    with diferrent infrastructure settings and it took me always at least a whole
    day (involving tracing inside Maven sources to find out what's wrong). But it's
    hard to live without release process, so it had to be done.
- id: 23371
  author: Dennis
  author_email: sinapieper@gmx.de
  author_url: ''
  date: '2010-06-21 12:13:36 +0200'
  date_gmt: '2010-06-21 11:13:36 +0200'
  content: Thank you for this excellent instruction. It really helped me to set up
    the build configuration within a short time.
- id: 23922
  author: Jay
  author_email: jperry@brightcove.com
  author_url: ''
  date: '2010-07-16 14:47:48 +0200'
  date_gmt: '2010-07-16 13:47:48 +0200'
  content: "Are any of you using perforce as your SCM?  I am having issues where it
    doesn't know what the clientspec is?  \r\n\r\nGetting this message:  [ERROR] CommandLineException
    Exit code: 1 - Client 'my-mac' unknown - use 'client' command to create it.\r\n\r\nTIA"
- id: 23929
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-07-17 09:16:24 +0200'
  date_gmt: '2010-07-17 08:16:24 +0200'
  content: Sorry Jay - I've never seen such a message.
- id: 24003
  author: Jay
  author_email: jperry@brightcove.com
  author_url: ''
  date: '2010-07-19 04:57:18 +0200'
  date_gmt: '2010-07-19 03:57:18 +0200'
  content: Have you tried using the release plugin with Perforce?  I was able to get
    it to work when I was set into a clientspec.  The problem I'm having is I'm using
    TeamCity and wanted to use it to do releases.  I thought the release plugin creates
    temporary client specs for the release:prepare then throws them away.  If you
    got this working can you tell me your setup and what you run on the command line?  Thanks.
- id: 24029
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-07-21 17:30:43 +0200'
  date_gmt: '2010-07-21 16:30:43 +0200'
  content: "And I forgot to mention, that we use CVS as our SCM - so I have no experience
    with Perforce at all. I remember that when I tried to get release plugin working
    with SVN in my previous job, I run at different bunch of problems, but finally
    made it running.\r\n\r\nSo sorry, again - no hint from me :-("
---
<p>If you use Maven 2 and Teamcity integration server, you might want to perform releases on server. Although it's not so complicated, some things must fit one into another and you might spend a lot of time till you find out how to configure pom.xml and build configuration. For those of you, who need to setup it, this article could come quite handy.</p>
<p><a id="more"></a><a id="more-77"></a></p>
<p>Let's assume that you have maven release process setuped up for your localhost. If you do not, you can look at following articles, to get it running (this is the most difficult part, that I want to avoid analyzing in this post):</p>
<ul>
<li><a href="http://blog.novoj.net/2007/11/02/maven2-release-plugin-a-pristup-do-cvs-pres-ssh-s-privatnim-klicem/">Maven 2 release plugin and access to CVS over SSH with private key (only in Czech)</a></li>
<li><a href="http://wiki.petals.objectweb.org/xwiki/bin/view/Developers/ReleasePetals" target="_new">Simple HOWTO for Maven release process</a></li>
<li><a href="http://maven.apache.org/plugins/maven-release-plugin/plugin-info.html" target="_new">Maven release plugin documentation</a></li>
</ul>
<p>So let's concentrate on what's needed to setup in Teamcity. Create new configuration according to these steps:</p>
<ol>
<li>
<h4>General Settings Tab</h4>
<p>   Fill basic data but focus on <b>Artifact paths</b>. Relative paths where built artifacts will be placed should be inserted in this field. You can find it out if you run "mvn release:prepare release:perform" on you localhost. Then, when everything goes well, newly created artifacts should end up somewhere in target/checkout directory.</p>
<div align="center">
      <a href='http://blog.novoj.net/binary//2008/06/generalsettings.png' title='General Settings'><img src='http://blog.novoj.net/binary//2008/06/generalsettings.png' alt='General Settings' width="100%"/></a>
   </div>
<p>   This will enable you quick download of built artifacts from Overview page.
   </li>
<li>
<h4>VCS Settings Tab</h4>
<p>   Some settings in this tab are important to be set right. At first you need to select <b>VCS checkout mode</b> to <b>Automatically on agent (if supported by VCS roots)</b> option. It means, that agent running this build will perform checkout (not export) so Maven will be able to create a tag from it. You can verify that by going to teamcity agent intallation directory, work subdirectory and finding checkout directory for this build (of course you must to run this build config at least once) - you'll see VCS subdirectiores among project files and folders (in case of CVS you'll find CVS directory there). Maven is extensively working with VCS during release process, so it is vital to have it like that.</p>
<div align="center">
      <a href='http://blog.novoj.net/binary//2008/06/vcssettings.png' title='VCS Settings Tab'><img src='http://blog.novoj.net/binary//2008/06/vcssettings.png' alt='VCS Settings Tab' width="100%"/></a>
   </div>
<p>   Click on the <b>Edit</b> link in VCS Root or <b>Create and attach new VCS Root</b>.
   </li>
<li>
<h4>VCS Root Tab</h4>
<p>      There are two places you should concentrate on. The first one is <b>CVS Root</b> where you should insert the same CVS Root as you have in your pom.xml. String should be exactly the same including protocol type (ssh, ext or so). For example if you have in pom.xml this declaration:</p>
<p>       [source lang="xml"]<br />
<scm><br />
	<connection>scm:cvs:ext:anonymous@mycvsserver:/CVSRoot/groupFolder:projectX</connection><br />
</scm><br />
       [/source]</p>
<p>       You should have "cvs:ext:anonymous@mycvsserver:/CVSRoot/groupFolder" in <b>CVS Root</b> (to tell the truth, username could differ, but process is sensible to other values difference). Field <b>Module name </b> could differ as well - so you can have "projectX" in pom.xml (as in example above) and fill subfolder "projectX/subProjectY" in Teamcity.</p>
<p>      If you setup CVS Root wrong, you'll be rewarded with this exception:</p>
<p>      [source:html]<br />
java.lang.IllegalArgumentException: Unrecognized CVS Root: :ssh:anonymous@mycvsserver:/CVSRoot/groupFolder<br />
        at org.netbeans.lib.cvsclient.connection.ConnectionFactory.getConnection(ConnectionFactory.java:88)<br />
        at org.apache.maven.scm.provider.cvslib.cvsjava.util.CvsConnection.connect(CvsConnection.java:158)<br />
        at org.apache.maven.scm.provider.cvslib.cvsjava.util.CvsConnection.processCommand(CvsConnection.java:475)<br />
        at org.apache.maven.scm.provider.cvslib.cvsjava.command.checkin.CvsJavaCheckInCommand.executeCvsCommand(CvsJavaCheckInCommand.java:55)<br />
        at org.apache.maven.scm.provider.cvslib.command.checkin.AbstractCvsCheckInCommand.executeCheckInCommand(AbstractCvsCheckInCommand.java:89)<br />
        at org.apache.maven.scm.command.checkin.AbstractCheckInCommand.executeCommand(AbstractCheckInCommand.java:53)<br />
        at org.apache.maven.scm.command.AbstractCommand.execute(AbstractCommand.java:58)<br />
        at org.apache.maven.scm.provider.cvslib.AbstractCvsScmProvider.executeCommand(AbstractCvsScmProvider.java:521)<br />
        at org.apache.maven.scm.provider.cvslib.AbstractCvsScmProvider.checkin(AbstractCvsScmProvider.java:585)<br />
        at org.apache.maven.scm.provider.AbstractScmProvider.checkIn(AbstractScmProvider.java:365)<br />
        at org.apache.maven.shared.release.phase.ScmCommitPhase.checkin(ScmCommitPhase.java:124)<br />
        at org.apache.maven.shared.release.phase.ScmCommitPhase.execute(ScmCommitPhase.java:109)<br />
        at org.apache.maven.shared.release.DefaultReleaseManager.prepare(DefaultReleaseManager.java:194)<br />
        at org.apache.maven.shared.release.DefaultReleaseManager.prepare(DefaultReleaseManager.java:131)<br />
        at org.apache.maven.shared.release.DefaultReleaseManager.prepare(DefaultReleaseManager.java:94)<br />
        at org.apache.maven.plugins.release.PrepareReleaseMojo.execute(PrepareReleaseMojo.java:136)<br />
        at org.apache.maven.plugin.DefaultPluginManager.executeMojo(DefaultPluginManager.java:451)<br />
        at org.apache.maven.lifecycle.DefaultLifecycleExecutor.executeGoals(DefaultLifecycleExecutor.java:558)<br />
        at org.apache.maven.lifecycle.DefaultLifecycleExecutor.executeStandaloneGoal(DefaultLifecycleExecutor.java:512)<br />
        at org.apache.maven.lifecycle.DefaultLifecycleExecutor.executeGoal(DefaultLifecycleExecutor.java:482)<br />
        at org.apache.maven.lifecycle.DefaultLifecycleExecutor.executeGoalAndHandleFailures(DefaultLifecycleExecutor.java:330)<br />
        at org.apache.maven.lifecycle.DefaultLifecycleExecutor.executeTaskSegments(DefaultLifecycleExecutor.java:227)<br />
        at org.apache.maven.lifecycle.DefaultLifecycleExecutor.execute(DefaultLifecycleExecutor.java:142)<br />
      [/source]</p>
<p>   Last thing is to select <b>Checkout HEAD revision</b> in <b>Checkout option</b>. Maven makes tag and checkout by tag inside release process, so we need to select checkout of newest source files from HEAD (or alternatively from some branch if you need).</p>
<div align="center">
      <a href='http://blog.novoj.net/binary//2008/06/vcsroot.png' title='VCS Root'><img src='http://blog.novoj.net/binary//2008/06/vcsroot.png' alt='VCS Root'  width="100%"/></a>
   </div>
</li>
<li>
<h4>Build Runner Tab</h4>
<p>   This is the last important tab. There you should fill "clean install release:prepare release:perform" in <b>Goals</b> field. I found out, that sometimes in multiproject environment release:prepare fails to run because it doesn't find SNAPSHOT artifacts in repository when building dependent subprojects that has them defined in parent declaration. Specifying "clean install" in this field will prevent failure of this type.</p>
<p>   Next you should fill <b>--batch-mode</b> in <b>Additional Maven command line parameters</b>. This means, that maven will not ask you to enter or confirm release version number, next SNAPSHOT number and tag name. It will use computed defaults without asking (TeamCity does not offer any means to interact with the build process after it has been started). The only way how to affect on these vaules is to set proper SNAPSHOT version in pom.xml an commit it before starting release build in TeamCity.</p>
<p>   Finally you might want to enter Java memory extension for Maven build. Default memory limit is 64MB and when uploading created artifacts to remote repository it could be easily reached (it seems that maven holds entire artifact in memory while uploading).</p>
<p>  If you rely on performRelease property, you should be aware, that this property is set by Maven only for release:perform stage - not for release:prepare. So when you have profile activated by this property, that defines "modules" inclusion in build, Maven will activate this profile only for the last goal. Pom.xml's versions are renumbered in release:prepare stage, so in this case you'd have some projects skipped from renumbering. Setting -DperformRelease property in <b>JVM command line parameters</b> will ensure, that profiles will be activated consistently thorough whole build process.</p>
<div align="center">
      <a href='http://blog.novoj.net/binary//2008/06/maven.png' title='Maven Tab'><img src='http://blog.novoj.net/binary//2008/06/maven.png' alt='Maven Tab' width="100%"/></a>
   </div>
</li>
<li>
<h4>Build Runner Tab</h4>
<p>   When everything goes well, your release build should end with success and you should see menu with built artifacts on the overview screen of TeamCity (artifacts are of course also in your company repository).</p>
<div align="center">
      <a href='http://blog.novoj.net/binary//2008/06/overview.png' title='Overview'><img src='http://blog.novoj.net/binary//2008/06/overview.png' alt='Overview' width="100%"/></a>
   </div>
</li>
</ol>
<p>Although it's not a rocket science, it takes some time to get all this running. I've spent six hours to tune this, so if my advices could save some of your time, purpose of this article would be fulfilled.</p>
