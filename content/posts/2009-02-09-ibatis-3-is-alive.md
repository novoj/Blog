---
status: publish
published: true
title: iBatis 3 is alive!
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "I had a discussion with <a href=\"http://jirablog.blogspot.com/2009/01/orm-mych-snu-ibatis-3.html\"
  target=\"_blank\">Jira</a> recently, whether we could be still looking forward to
  iBatis 3. It has been  long time since <a href=\"http://opensource.atlassian.com/confluence/oss/display/IBATIS/iBATIS+3.0+Whiteboard\"
  target=\"_blank\">iBatis 3 Whiteboard</a> was seriously touched and I haven't found
  any other clue when or whether there is going to be iBatis 3. There is very small
  activity for 3.x version in Jira, though <a href=\"http://www.mail-archive.com/commits@ibatis.apache.org/\"
  target=\"_blank\">there were some commits into iBatis 3 core</a>. As I am going
  to have <a href=\"http://blog.novoj.net/2009/02/08/pozvanka-na-prednasku-na-uhk-ibatis-sqlmaps/\"
  target=\"_blank\">a speech in University Hradec Králové on iBatis</a>, I have decided
  to ask directly its authors about this issue.\r\n\r\n"
wordpress_id: 391
wordpress_url: http://blog.novoj.net/?p=391
date: '2009-02-09 18:31:03 +0100'
date_gmt: '2009-02-09 17:31:03 +0100'
categories:
- Java
- English
- iBatis
tags: []
comments:
- id: 6274
  author: Jira
  author_email: Jiramares@gmail.com
  author_url: http://jirablog.blogspot.com/
  date: '2009-02-09 20:37:05 +0100'
  date_gmt: '2009-02-09 19:37:05 +0100'
  content: Really great to hear such a great news... I think I'm not the only one
    looking forward to.
- id: 6524
  author: Lubor
  author_email: lubor.gajda@gmail.com
  author_url: ''
  date: '2009-02-18 02:23:14 +0100'
  date_gmt: '2009-02-18 01:23:14 +0100'
  content: Does anybody know if iBatis 3 will support dirty checking and cascading
    by any chance? IMHO usability of any persistence tool without dirty checking is
    quite limited.
- id: 6531
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-02-18 08:01:53 +0100'
  date_gmt: '2009-02-18 07:01:53 +0100'
  content: I don't want to talk for authors but I don't think so. Judging from the
    iBatis philosophy, where you are the author of SQL queries, framework is not eligible
    to modify / generate your SQL updates (that would be necessary to provide dirty
    checking). I think, that if you need such functionality JPA is the way you should
    follow. iBatis is more valuable when you want to keep full control over your SQL
    communication mechanism than when you want to minimize your work. Full control,
    reliability and simplicity are the values we appreciate.
- id: 6540
  author: Lubor
  author_email: lubor.gajda@gmail.com
  author_url: ''
  date: '2009-02-18 12:49:29 +0100'
  date_gmt: '2009-02-18 11:49:29 +0100'
  content: But what about performance impacts then? If iBatis doesn't support dirty
    checking, during update operations it's not able to detect what part of object
    tree has been modified and therefore full update has to be used (what can be significant
    performance overhead). Is iBatis meant to be used for simple flat domain object
    models only? Or are there any techniques that can be used to optimize database
    communication in case that your application requires complex domain object models?
- id: 6542
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-02-18 13:26:11 +0100'
  date_gmt: '2009-02-18 12:26:11 +0100'
  content: "iBatis unit of work is single SQL statement. If you want to store object
    tree, you have to decide yourself what needs to be stored and what does not and
    call iBatis function appropriately. Even transaction demarcation is done \"manually\"
    - iBatis won't decide what will run in transaction and what does not (of course
    in combination with Spring we use declarative transaction management).\r\n\r\nFor
    the purposes of our web presentation is the functionality of iBatis sufficient.
    We don't need to modify complex object trees on several places at once and store
    them from the top. When we have complex object tree, we usualy work with its decomposed
    parts, so the objects we work with are quite simple. So why bother?\r\n\r\nYes,
    there is some overhead in the sense, that we always update whole record and not
    only columns with modified data - but I think that this is not a major problem.
    When there is huge data involved there we usualy define two update statements
    so that we can avoid unnecessary tranfer of such data.\r\n\r\nAs I said earlier
    - iBatis is not magic almighty super duper engine as for example Hibernate is.
    It is simple - saves you a lot of work, but leaves all important decisions up
    to you. On the other hand, there is a little what could go wrong comparing to
    Hibernate."
- id: 6558
  author: Lubor
  author_email: lubor.gajda@gmail.com
  author_url: ''
  date: '2009-02-19 17:50:06 +0100'
  date_gmt: '2009-02-19 16:50:06 +0100'
  content: "Imagine for instance that we have object tree that consists of five objects
    mapped to five different database tables. This object tree is used during user
    interaction and user can modify properties of any of these objects. At the end
    of the user interaction we need to update that object tree to persist all changes
    made by the user. But without dirty checking we don't know which of those five
    objects has been modified and which hasn't so we always have to send five updates
    to database. Maybe there wasn't any modification at all, but we still have to
    hit database five times. With more complex domain object models this problem can
    be even more obvious.\r\n\r\nI understand that IBatis has better learning curve
    and can save you some effort, but it sounds to me that it can bring you a lot
    of headaches during performance tuning when you discover that your application
    doesn't scale very well.\r\n\r\nOf course that you don't have care about all these
    details if your application is using very simple flat domain object model because
    performance impact won't be significant in that circumstances. But who will guarantee
    that application requirements won't change in the future and that your application
    won't have to support much complex object model? Will you then rewrite your persistence
    layer or mix two different persistence tolls?"
- id: 6559
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-02-19 20:56:44 +0100'
  date_gmt: '2009-02-19 19:56:44 +0100'
  content: "I understand what you try to explain to me. iBatis is not the right tool
    when you need such things. On the other hand look around the web and tell me how
    many web applications focusing on broad public require editing complex object
    trees in single transaction? Even if I look at the Facebook that is pretty complex
    application I don't see much use cases of such type. So the final thought of mine
    is, that in certain domains we could be more or less sure, that we wouldn't get
    into a situation you describe at the end. Partly it's also matter of UI design
    - whether complex editation is allowed or not. Look at websites that we make:\r\n\r\nhttp://www.g2.cz\r\nhttp://www.trotina.cz\r\nhttp://www.cez.cz\r\nhttp://www.frekvence1.cz\r\nhttp://www.cilichili.cz/\r\nhttps://secure.plobergerhotels.com/maximilian/reservation.html\r\n\r\nNo
    complex object trees were needed. Some of those applications we have supported
    and extended for several years and technology still suffices.\r\n\r\nOn the other
    hand if I had to make an accounting application or company information system,
    I would probably go the JPA way. Because the task is diametrically different."
- id: 6560
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2009-02-19 21:35:30 +0100'
  date_gmt: '2009-02-19 20:35:30 +0100'
  content: "Maybe this mail thread could save us a lot of discussing:\r\n\r\nhttp://www.mail-archive.com/ibatis-user-java@incubator.apache.org/msg01239.html\r\n\r\nThose
    two posts from the thread I'd like to point out the most (they directly connect
    to our discussion):\r\n\r\nhttp://www.mail-archive.com/ibatis-user-java@incubator.apache.org/msg01241.html\r\nhttp://www.mail-archive.com/ibatis-user-java@incubator.apache.org/msg01251.html\r\n\r\nI
    couln't say it better, especially when having only little experience with Hibernate."
---
<p>I had a discussion with <a href="http://jirablog.blogspot.com/2009/01/orm-mych-snu-ibatis-3.html" target="_blank">Jira</a> recently, whether we could be still looking forward to iBatis 3. It has been  long time since <a href="http://opensource.atlassian.com/confluence/oss/display/IBATIS/iBATIS+3.0+Whiteboard" target="_blank">iBatis 3 Whiteboard</a> was seriously touched and I haven't found any other clue when or whether there is going to be iBatis 3. There is very small activity for 3.x version in Jira, though <a href="http://www.mail-archive.com/commits@ibatis.apache.org/" target="_blank">there were some commits into iBatis 3 core</a>. As I am going to have <a href="http://blog.novoj.net/2009/02/08/pozvanka-na-prednasku-na-uhk-ibatis-sqlmaps/" target="_blank">a speech in University Hradec Králové on iBatis</a>, I have decided to ask directly its authors about this issue.</p>
<p><a id="more"></a><a id="more-391"></a></p>
<p>The answer I've received and considered very delighting I quote on following lines:</p>
<div style="border: 1px solid white; background-color: #cccccc; color: black; font-style: italic; font-size: 90%; padding: 10px;">
Hi Jan,</p>
<p>Let me address a few of your assertions, and then I can give you an update:</p>
<ul>
<li>First, Kai is right, iBATIS 2 has reached it's "feature completeness" -- we won't add any new significant features to it.  We'll maintain it and fix bugs. </li>
<li>As far as Java 5 goes, iBATIS 2 supports Enums and Generics as well as iBATIS 3 ever will (with the exception of interface binding, which will benefit from generics and annotations).</li>
<li>The iBATIS 3 Whiteboard hasn't been touched because it too is complete.  It's purpose was to gather thoughts and provide a forum for debate.</li>
<li>What I guess hasn't been communicated is that development of iBATIS 3 is well under way, and nearing a Beta release.  We should put up a blog for this... long overdue.</li>
<li>You can find the iBATIS 3 source here:  <a href="http://svn.apache.org/repos/asf/ibatis/trunk/java/ibatis-3/" target="_blank">http://svn.apache.org/repos/asf/ibatis/trunk/java/ibatis-3/</a></li>
</ul>
<p>The core of iBATIS 3 is complete and in fact it runs the full suite of iBATIS 2 and JPetStore 5 unit tests, as well as its own comprehensive suite of tests. The new XML structure has been implemented and is far less verbose than the current one.  Many improvements have been made to the core implementation of mappings, auto mappings, join mapping, caching, transaction management, batching, autocommit (real autocommit) and many other areas of the framework have been greatly improved and modernized.</p>
<p>The features remaining to be implemented at this time are:</p>
<ul>
<li>Interface Binding</li>
<li>Annotation based configuration</li>
<li>New Dynamic SQL</li>
</ul>
<p>Beyond that it will need some volunteers for Q/A and performance testing. It's a complete rewrite and one would be hard pressed to find a single method shared between the two.</p>
<p>I don't have an ETA, as I'm very busy.  But we should see significant new progress made by the end of February. </p>
<p>I'll see if we can get a team blog up, possibly to replace the homepage so that we can report more regularly on the status. </p>
<p>Cheers,<br />
Clinton
</p></div>
<p>Finally, there is no doubt what situation is around iBatis. I hope that you are as glad as I am.</p>
<p>And it there are any volunteers among you to provide Q/A and performance testing, just subscribe to iBatis mailing list and contact Clinton Begin.</p>
