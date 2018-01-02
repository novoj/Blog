---
status: publish
published: true
title: Recreate MySQL views without definer, one-liner solution (Linux)
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft size-full wp-image-1365\" alt=\"MySQL\" src=\"http://blog.novoj.net/binary/2011/02/mysql.png\"
  width=\"120\" height=\"121\" />Rather cryptic headline describes a pain many of
  us have to go through when restoring MySQL database backup from different machine.
  If you have ever done this on database with DB views - you'd probably run at this
  problem too.\r\n\r\nSource of the problem is that MySQL dump exports CREATE VIEW
  DLL with DEFINER attribute and there is no way how to instruct it to exclude this
  attribute (as far as I know). When you take such export and import it for example
  on developer machine you'd probably not have the same user or user with same privileges
  on this machine. Each and every select to the views with invalid definer fails with
  error - for example:\r\n<pre>Error Code: 1449. The user specified as a definer ('xxxx'@'localhost')
  does not exist</pre>\r\n"
wordpress_id: 2872
wordpress_url: http://blog.novoj.net/?p=2872
date: '2014-05-16 17:37:12 +0200'
date_gmt: '2014-05-16 16:37:12 +0200'
categories:
- Programování
- English
- Databáze
tags:
- mysql
comments: []
---
<p><img class="alignleft size-full wp-image-1365" alt="MySQL" src="http://blog.novoj.net/binary/2011/02/mysql.png" width="120" height="121" />Rather cryptic headline describes a pain many of us have to go through when restoring MySQL database backup from different machine. If you have ever done this on database with DB views - you'd probably run at this problem too.</p>
<p>Source of the problem is that MySQL dump exports CREATE VIEW DLL with DEFINER attribute and there is no way how to instruct it to exclude this attribute (as far as I know). When you take such export and import it for example on developer machine you'd probably not have the same user or user with same privileges on this machine. Each and every select to the views with invalid definer fails with error - for example:</p>
<pre>Error Code: 1449. The user specified as a definer ('xxxx'@'localhost') does not exist</pre>
<p><a id="more"></a><a id="more-2872"></a></p>
<h3>One-liner</h3>
<p>If you're so lucky that you run Linux as your operating system - you can use this one-liner solution, that will drop all views in your database and will recreate them without definer, so that they become defined by current user and will start to work again:</p>
<pre>mysql -u<strong>user</strong> -p<strong>pwd</strong> -A --skip-column-names -e"SELECT CONCAT('SHOW CREATE VIEW ',table_schema,'.',table_name,';') FROM information_schema.tables WHERE engine IS NULL and table_schema like '<strong>mydb%</strong>'" | mysql -u<strong>user</strong> -p<strong>pwd</strong> -A --skip-column-names | sed -rn 's/.*?VIEW ([^\s]+?) (AS .*?)\s([^\s]+?)\s([^\s]+?)/DROP VIEW ;\nCREATE VIEW  ;/p' | mysql -u<strong>user</strong> -p<strong>pwd</strong> -A --skip-column-names</pre>
<p><em><strong>Note:</strong> You have only to replace strings in bold with your DB user credentials and database name / like pattern.</em></p>
<h4>What the script does?</h4>
<ol>
<li>connects to the database and selects all tables without engine - ie. views from information schema of MySQL</li>
<li>constructs SHOW CREATE VIEW for each returned view name</li>
<li>runs that newly created script against MySQL database again</li>
<li>returned create statements runs through <a href="http://en.wikipedia.org/wiki/Sed" target="_blank">sed</a> with regular expression that converts them into DROP VIEW + CREATE VIEW without definer</li>
<li>generated scripts runs again in MySQL database</li>
</ol>
<h3>Don't repeat yourself</h3>
<p>If you happen to use this one-liner often you might want to create ALIAS to your bash profile that will let you to use it as a short command:</p>
<pre>recreate-views mydb% user pwd</pre>
<p>Just add to your <strong>~/.bash_aliases</strong> following lines:</p>
<pre>function recreate-views-fct() {
   mysql -u$2 -p$3 -A --skip-column-names -e"SELECT CONCAT('SHOW CREATE VIEW ',table_schema,'.',table_name,';') FROM information_schema.tables WHERE engine IS NULL and table_schema like '$1'" | mysql -u$2 -p$3 -A --skip-column-names | sed -rn 's/.*?VIEW ([^\s]+?) (AS .*?)\s([^\s]+?)\s([^\s]+?)/DROP VIEW ;\nCREATE VIEW  ;/p' | mysql -u$2 -p$3 -A --skip-column-names
}
alias recreate-views=recreate-views-fct</pre>
<h3>Sources</h3>
<ul>
<li><a href="http://dba.stackexchange.com/questions/4129/modify-definer-on-many-views" target="_blank">http://dba.stackexchange.com/questions/4129/modify-definer-on-many-views</a></li>
<li><a href="http://www.palominodb.com/blog/2011/10/05/change-views-definer-without-alter-view-how-fix-thousands-views" target="_blank">http://www.palominodb.com/blog/2011/10/05/change-views-definer-without-alter-view-how-fix-thousands-views</a></li>
<li><a href="http://dbperf.wordpress.com/2010/04/12/removing-definer-from-mysql-dump/" target="_blank">http://dbperf.wordpress.com/2010/04/12/removing-definer-from-mysql-dump/</a></li>
</ul>
