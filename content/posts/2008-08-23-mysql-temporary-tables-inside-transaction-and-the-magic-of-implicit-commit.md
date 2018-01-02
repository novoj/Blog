---
status: publish
published: true
title: MySQL temporary tables inside Transaction <br> and the magic of implicit commit
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "I've run into interesting and very strange problem. I was writing transactional
  <a href=\"http://www.mysql.com\" target=\"_new\"><img src=\"http://www.mysql.com/common/logos/logo_mysql_sun.gif\"
  align=\"right\" width=\"180px\" height=\"53px\" style=\"margin: 5px 0px 5px 5px;\"></a>
  Spring test that opens transaction at the beginning of it, and rollbacks at the
  end. First part of my test performed bunch of INSERT and UPDATE SQL commands and
  after that I was checking persisted changes by loading data back from the database.
  Suddenly my tests started to fail. And I was searching for the reason ...\r\n\r\n"
wordpress_id: 109
wordpress_url: http://blog.novoj.net/2008/08/23/mysql-temporary-tables-inside-transaction-and-the-magic-of-implicit-commit/
date: '2008-08-23 12:35:08 +0200'
date_gmt: '2008-08-23 11:35:08 +0200'
categories:
- Java
- English
tags:
- mysql
comments:
- id: 33485
  author: znani celebryci
  author_email: Luis@g-mail.com
  author_url: http://www.piotr-rubik.pl
  date: '2011-02-08 19:05:28 +0100'
  date_gmt: '2011-02-08 18:05:28 +0100'
  content: I have read through your article and i was satisfied of the good information
    that you have contributed in your article! Thanks a lot for that beneficial article!
---
<p>I've run into interesting and very strange problem. I was writing transactional <a href="http://www.mysql.com" target="_new"><img src="http://www.mysql.com/common/logos/logo_mysql_sun.gif" align="right" width="180px" height="53px" style="margin: 5px 0px 5px 5px;"></a> Spring test that opens transaction at the beginning of it, and rollbacks at the end. First part of my test performed bunch of INSERT and UPDATE SQL commands and after that I was checking persisted changes by loading data back from the database. Suddenly my tests started to fail. And I was searching for the reason ...</p>
<p><a id="more"></a><a id="more-109"></a></p>
<p>The reason was that the data created by the first part of test was not cleared by rollback at the end of the test. I examined the log and verified, that Spring really opened and rollbacked the transaction during the test. So I started to suspect myself, that I setup Spring wrong test and that they are using different DataSource than application logic. But after several minutes I realized that suspicion probably wasn't right (if you look at the Spring transaction logic, you will understand why I couldn't say it for sure). </p>
<p>I started to be quite annoyed, so I continued with removing piece after piece of the test code and realized, that when I remove verification part (that loaded data back from the database), the transaction was successfuly rollbacked and stored data vanished after test. So where was the problem? </p>
<p>Loading logic took advantage of another part of library I was programming and this logic involved creating and dropping temporary table while fetching data. And this caused rollback to be ignored by MySQL server, moreover instead of rollback data was commited. I found <a href="http://bugs.mysql.com/bug.php?id=37011" target="_new">one bug in MySQL issue tracker</a>, that describes this problem more in detail. Following statement was the key:</p>
<p><cite>"According to <a href="http://dev.mysql.com/doc/refman/5.1/en/implicit-commit.html" target="_new">http://dev.mysql.com/doc/refman/5.1/en/implicit-commit.html</a>: CREATE TABLE and DROP TABLE do not commit a transaction if the TEMPORARY keyword is used. (This does not apply to other operations on temporary tables such as CREATE INDEX, which do cause a commit.) However, although no implicit commit occurs, neither can the statement be rolled back. Therefore, use of such statements will violate transaction atomicity: For example, if you use CREATE TEMPORARY TABLE and then roll back the transaction, the table remains in existence."</cite></p>
<p>Though the statement says, that creating temporary table doesn't caus an implicit commit - test behaved like that. Data stayed at the database after rollback. One way or another, it was something I didn't want to happen and what I hadn't idea of. Another day, another surprise. I had to rewrite loading logic to get along without temporary table and tests started to work again.</p>
<p>I wish you'll find it more quickly than I did.</p>
