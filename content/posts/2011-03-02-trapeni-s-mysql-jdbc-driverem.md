---
status: publish
published: true
title: Trápení s MySql JDBC driverem
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img src=\"http://blog.novoj.net/binary/2011/02/mysql.png\" alt=\"\" title=\"mysql\"
  width=\"120\" height=\"121\" class=\"alignleft size-full wp-image-1365\" /> MySql
  databázi používáme jako standardní řešení datové vrstvy už hodně let. Prošli jsme
  si už pěknou řádku verzí JDBC ovladačů, ale jedna věc mě dostala vážně do kolen.
  Tak se pohodlně usaďte, protože dnešní příběh bude vážně dlouhý :-)\r\n\r\nŽil byl
  v jedné firmě programátor starající se malou generickou knihovnu pracující s JDBC.
  Jednoho krásného rána se probudil s jednou nově reportovanou issue ve svém trackeru
  ... ale ne, takhle by to vyprávění trvalo opravdu hodně dlouho ... vše začalo touto
  krásnou exception:\r\n\r\n<pre>\r\njava.sql.SQLException: Generated keys not requested.
  You need to specify  \r\nStatement.RETURN_GENERATED_KEYS to Statement.executeUpdate()
  or \r\nConnection.prepareStatement(). at the execute command.\r\n</pre>\r\n\r\n"
wordpress_id: 1362
wordpress_url: http://blog.novoj.net/?p=1362
date: '2011-03-02 00:00:15 +0100'
date_gmt: '2011-03-01 23:00:15 +0100'
categories:
- Programování
- Databáze
tags:
- mysql
comments:
- id: 35209
  author: lzap
  author_email: lzap@seznam.cz
  author_url: http://lukas.zapletalovi.com/
  date: '2011-03-02 13:20:55 +0100'
  date_gmt: '2011-03-02 12:20:55 +0100'
  content: Pěkné. A nezasloužil by si ten konstatní pattern zkompilovat do statické
    konstanty? Jen výstřel od boku - nevím jak často se tohle volá. Jestli jen jednou
    za request, tak to nemá prakticky smysl. :-D
- id: 35212
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-03-02 14:22:21 +0100'
  date_gmt: '2011-03-02 13:22:21 +0100'
  content: "Volá se to jen jednou při inicializaci knihovny (spojení na DB). Tj. fakticky
    je to zbytečné, ale programátorsky by to bylo asi hezčí ;-) .\r\n\r\nDík"
- id: 35218
  author: msk
  author_email: msk.conf@gmail.com
  author_url: ''
  date: '2011-03-02 15:34:37 +0100'
  date_gmt: '2011-03-02 14:34:37 +0100'
  content: "Fuj.\r\n\r\nDokonale to odraza stav opensource jdbc driverov a pristupu
    java programatorov k verzovaniu releasov ( tzn. seru nan jak na placaty kamen
    ).\r\n\r\nSpravne by imho bolo opravit jdbc driver ( s patricnou zmenou verzie
    ) a chybny release dalej nedistribuovat."
- id: 35330
  author: Ondra
  author_email: ax@by.cz
  author_url: ''
  date: '2011-03-03 17:06:26 +0100'
  date_gmt: '2011-03-03 16:06:26 +0100'
  content: Jen by me zajimalo, proc ona firma nepouziva misto male genericke knihovny
    pracující s JDBC hibernate.
- id: 35334
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-03-03 18:42:33 +0100'
  date_gmt: '2011-03-03 17:42:33 +0100'
  content: Ze stejného důvodu proč ještě občas píše servlety i když tu máme boží standardizované
    frameworky jako jsou JSF ;-)
---
<p><img src="http://blog.novoj.net/binary/2011/02/mysql.png" alt="" title="mysql" width="120" height="121" class="alignleft size-full wp-image-1365" /> MySql databázi používáme jako standardní řešení datové vrstvy už hodně let. Prošli jsme si už pěknou řádku verzí JDBC ovladačů, ale jedna věc mě dostala vážně do kolen. Tak se pohodlně usaďte, protože dnešní příběh bude vážně dlouhý :-)</p>
<p>Žil byl v jedné firmě programátor starající se malou generickou knihovnu pracující s JDBC. Jednoho krásného rána se probudil s jednou nově reportovanou issue ve svém trackeru ... ale ne, takhle by to vyprávění trvalo opravdu hodně dlouho ... vše začalo touto krásnou exception:</p>
<pre>
java.sql.SQLException: Generated keys not requested. You need to specify  
Statement.RETURN_GENERATED_KEYS to Statement.executeUpdate() or 
Connection.prepareStatement(). at the execute command.
</pre>
<p><a id="more"></a><a id="more-1362"></a></p>
<p>Pravděpodobně díky opravě jiné chyby (<a href="http://bugs.mysql.com/bug.php?id=34185" target="_blank">Issue 34185</a>) změnil MySQL JDBC driver mezi verzemi 5.1.6 a 5.1.7 své chování při vracení hodnot GeneratedKeys (autoinkrementy) z update statementů. Ve starších verzích se hodnoty klíčů vracely i bez deklarace dodatečného flagu (<a href="http://download.oracle.com/javase/1.4.2/docs/api/java/sql/Statement.html#RETURN_GENERATED_KEYS" target="_blank">RETURN_GENERATED_KEYS</a>) při vytváření statementu, nově je tento flag vyžadován, jinak se vrací výše uvedená vyjímka. Chyba je dokumentována v <a href="http://bugs.mysql.com/bug.php?id=41448" target="_blank">Issue 41488</a>. Od verze 5.1.7 je tedy nutné, pokud chcete dostat hodnoty autoinkrementů, specifikovat statement takto:</p>
<p>[source lang="java"]<br />
PreparedStatement ps = con.prepareStatement(<br />
    "INSERT INTO `myTable` (name) VALUES (?)",<br />
   PreparedStatement.RETURN_GENERATED_KEYS<br />
);<br />
[/source]</p>
<p>Ok, podle specifikace jsme to měli dělat odjakživa (což ale jak jsem později zjistil stejně nešlo - viz. dále), jenže když to fungovalo bez flagu, tak se samozřejmě nikdo neobtěžoval to tak používat. Důležité ovšem také je, že k této zpětně nekompatibilní změně došlo mezi verzemi odlišující se jen třetím číslem (což obvykle představuje jen patche chyb), kde by to nikdo nečekal.</p>
<p>Historce ale ještě není konec - opravili jsme volání na správné a ouha, na starších ovladačích (pre 5.1.6) vracelo volání s použitím flagu NULL (dokumentováno v <a href="http://bugs.mysql.com/bug.php?id=32101" target="_blank">Issue 32101</a>). Tj. knihovnu, kterou jsme chtěli zároveň pouštět jak se starší verzí driverů i s těmi novějšími, jsme museli naučit obojí chování. Poradili jsme si trošku naivně, zato funkčně:</p>
<p>[source lang="java"]<br />
PreparedStatement ps = con.prepareStatement(<br />
   "INSERT INTO `myTable` (name) VALUES (?)",<br />
   PreparedStatement.RETURN_GENERATED_KEYS<br />
);<br />
if (ps == null) {<br />
   ps =con.prepareStatement(<br />
      "INSERT INTO `myTable` (name) VALUES (?)"<br />
      );<br />
}<br />
[/source]</p>
<p>To nám chvíli vydrželo, než jsme na aktivnějších projektech začali pozorovat memory leaky. Po analýze heapdumpu jsme přišli na to, že nejvíc paměti zabírají Connection, které držely PreparedStatementy. Od tohoto zjištění nám už netrvalo dlouho si domyslet, že, přestože MySQL driver vrací NULL hodnotu při vytváření PreparedStatementu prvním způsobem, reálně objekt vznikne a je na connection zaregistrován! </p>
<p>No a to byl už trošku těžší oříšek - museli jsme tedy chování rozlišovat podle znalosti použitého JDBC driveru a ne adaptovat se podle chování této metody. Ještě že na třídě DatabaseMetaData existují metody: getDriverMajorVersion() a getDriverMinorVersion(). Jenže! Změna se nám odehrála až na třetím verzovacím čísle, takže ve všech případech dostaneme majorVersion=5, minorVersion=1. No a teď už je to vážně zajímavé ...</p>
<p>Chytli jsme se tedy metody getDriverVersion(), která sice vrací kompletní verzi nicméně jako řetězec. A v případě MySQL je ten řetězec vážně lahůdka:</p>
<pre>
mysql-connector-java-5.1.13 ( Revision: ${bzr.revision-id} )
</pre>
<p>Co ale nezvládneme pomocí regulárních výrazů, že? Takže jsme skončili u této verze metody:</p>
<p>[source lang="java"]<br />
public VersionDescriptor getDriverVersion(Connection connection) {<br />
	try {<br />
		DatabaseMetaData metaData = connection.getMetaData();<br />
		Pattern versionPattern = Pattern.compile(".*?([0-9\\.]+).*?");<br />
		Matcher matcher = versionPattern.matcher(metaData.getDriverVersion());<br />
		if (matcher.matches()) {<br />
			return new VersionDescriptor(matcher.group(1));<br />
		} else {<br />
			return null;<br />
		}<br />
	} catch (SQLException ex) {<br />
		String msg = "Error retrieving JDBC driver version: " + ex.getLocalizedMessage();<br />
		log.error(msg, ex);<br />
		return null;<br />
	}<br />
}<br />
[/source]</p>
<p>A ve výsledném kódu nakonec používáme toto:</p>
<p>[source lang="java"]<br />
PreparedStatement ps;<br />
if (AbstractDatabaseStorage.MYSQL.equals(platform)) {<br />
	if (driverVersion != null && new VersionComparator().compare(driverVersion, MYSQL_NON_COMPATIBLE_VERSION) >= 0) {<br />
		//update required by MySQL JDBC driver 5.1.7 and newer<br />
		ps = con.prepareStatement(sqlBundle.getQuery(), PreparedStatement.RETURN_GENERATED_KEYS);<br />
	} else {<br />
		//correction of MySQL JDBC drivers older than 5.1.7 = issue #23017<br />
		ps = con.prepareStatement(sqlBundle.getQuery());<br />
	}<br />
} else {<br />
	ps = con.prepareStatement(sqlBundle.getQuery());<br />
}<br />
[/source]</p>
<p>A to je už je vážně konec dnešní programátorské pohádky. A přitom je to jenom pár drobných chybek a nedomyšleností programátorů JDBC ovladače ... :-)</p>
