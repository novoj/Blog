---
status: publish
published: true
title: Import velkých dat do MySQL
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Ještě něž jsem zahájil svou dovolenou, jsme při dokončování projektu narazili
  na výkonnostní problém při velkém importu dat do MySQL databáze. V našem případě
  se jednalo o cca 30 tisíc záznamů do tří tabulek navzájem provázaných cizími klíči.
  Úvodní verze importního algoritmu trvala cirka 50 minut, po dvou dnech jsme se dostali
  na jednotky minut. Nedalo mi to, a udělal jsem pár testů, které snaží tento problém
  rozkrýt do většího detailu, tak abych pro příště věděl, co a především jak významně
  ovlivňuje rychlost importu takto rozsáhlých dat.\r\n\r\n"
wordpress_id: 614
wordpress_url: http://blog.novoj.net/?p=614
date: '2009-10-06 13:14:48 +0200'
date_gmt: '2009-10-06 12:14:48 +0200'
categories:
- Programování
- Databáze
tags: []
comments: []
---
<p>Ještě něž jsem zahájil svou dovolenou, jsme při dokončování projektu narazili na výkonnostní problém při velkém importu dat do MySQL databáze. V našem případě se jednalo o cca 30 tisíc záznamů do tří tabulek navzájem provázaných cizími klíči. Úvodní verze importního algoritmu trvala cirka 50 minut, po dvou dnech jsme se dostali na jednotky minut. Nedalo mi to, a udělal jsem pár testů, které snaží tento problém rozkrýt do většího detailu, tak abych pro příště věděl, co a především jak významně ovlivňuje rychlost importu takto rozsáhlých dat.</p>
<p><a id="more"></a><a id="more-614"></a></p>
<p>Pro svůj test jsem použil pouze dvě tabulky provázané přes cizí klíč, první tabulka má navíc jeden unikátní index. V tabulkách je pouze minimum sloupců. Tyto dvě tabulky jsou vytvořeny jednou pro InnoDB a jednou pro MyISAM engine (pro MyISAM cizí klíč chybí, jelikož tento engine cizí klíče nepodporuje). Zde je jejich deklarace:</p>
<p>[source:sql]<br />
CREATE TABLE T_RECIPIENT_INNO(<br />
id INTEGER NOT NULL AUTO_INCREMENT,<br />
email VARCHAR(255) NOT NULL,<br />
created DATETIME NOT NULL,<br />
PRIMARY KEY (id),<br />
UNIQUE UQ_RECIPIENT_EMAIL_INNO(email)<br />
) ENGINE=InnoDB DEFAULT CHARSET=utf8;</p>
<p>CREATE TABLE T_RECIPIENT_PROPS_INNO(<br />
idProp INTEGER NOT NULL AUTO_INCREMENT,<br />
idRcpt INTEGER NOT NULL,<br />
name VARCHAR(255) NOT NULL,<br />
PRIMARY KEY (idProp),<br />
KEY (idRcpt)<br />
) ENGINE=InnoDB DEFAULT CHARSET=utf8;</p>
<p>ALTER TABLE T_RECIPIENT_PROPS_INNO ADD CONSTRAINT FK_T_RECIPIENT_PROPS_INNO<br />
FOREIGN KEY (idRcpt) REFERENCES T_RECIPIENT_INNO (id)<br />
ON DELETE CASCADE ON UPDATE CASCADE;</p>
<p>CREATE TABLE T_RECIPIENT_ISAM(<br />
id INTEGER NOT NULL AUTO_INCREMENT,<br />
email VARCHAR(255) NOT NULL,<br />
created DATETIME NOT NULL,<br />
PRIMARY KEY (id),<br />
UNIQUE UQ_RECIPIENT_EMAIL_ISAM(email)<br />
) ENGINE=MyISAM DEFAULT CHARSET=utf8;</p>
<p>CREATE TABLE T_RECIPIENT_PROPS_ISAM(<br />
idProp INTEGER NOT NULL AUTO_INCREMENT,<br />
idRcpt INTEGER NOT NULL,<br />
name VARCHAR(255) NOT NULL,<br />
PRIMARY KEY (idProp),<br />
KEY (idRcpt)<br />
) ENGINE=MyISAM DEFAULT CHARSET=utf8;<br />
[/source]</p>
<p>Před každým testem se provede drop všech tabulek a jejich znovu vytvoření. Každý test se jinou strategií snaží vložit 100 tisíc provázaných řádků do obou tabulek (tj. 200 tisíc řádků celkem). Všechny testy používají jedinou konekci (JDBC session, která se nikdy nezavírá).</p>
<ol>
<li><strong>testNaiveInnoImport:</strong> provádí insert jednoho řádku po druhém bez použití transakcí (tj. autocommit = true)</li>
<li><strong>testMultiRowInnoImportLongChunks:</strong> použití vícenásobného insertu (specialita MySQL) ve větších dávkách (po 10tisících záznamech v insertu) bez zakrytí transakcí</li>
<li><strong>testMultiRowInnoImportShortChunks:</strong> použití vícenásobného insertu (specialita MySQL) v menších dávkách (po 2tisících záznamech v insertu) bez zakrytí transakcí</li>
<li><strong>testMultiRowInnoImportLongChunksUnderTransaction:</strong> použití vícenásobného insertu (specialita MySQL) ve větších dávkách (po 10tisících záznamech v insertu) s použitím transakcí</li>
<li><strong>testMultiRowInnoImportShortChunksUnderTransaction:</strong> použití vícenásobného insertu (specialita MySQL) v menších dávkách (po 2tisících záznamech v insertu) s použitím transakcí</li>
<li><strong>testInnoImportUnderTransaction:</strong> zakrytí všech 200 tisíc insertů jedinou transakcí</li>
<li><strong>testInnoImportUnderTransactionLongChunks:</strong> zakrytí větší dávky insertů (po 20tisících záznamech) transakcí</li>
<li><strong>testInnoImportUnderTransactionSmallChunks:</strong> zakrytí menší dávky insertů (po 4tisících záznamech) transakcí</li>
</ol>
<p>Dále jsem ještě vytvořil klony těchto testů s následujícími modifikacemi:</p>
<ol>
<li><strong>Locking testy:</strong> před zavoláním každého testu provede zamčení používaných tabulek pro WRITE a na konci testů je opět odemkne</li>
<li><strong>Disable foreign key testy:</strong> před zavoláním každého testu nastaví proměnnou MySQL, která řídí kontrolu referenční integrity na false a na konci testů ji opět zapne</li>
<li><strong>Disable unique key testy:</strong> před zavoláním každého testu nastaví proměnnou MySQL, která řídí kontrolu unique indexů na false a na konci testů ji opět zapne</li>
<li><strong>Combied testy:</strong> kombinují všechny tři výše uvedené operace</li>
</ol>
<p>Všechny tyto kombinace se volají zvlášť pro InnoDB a zvlášť pro MyISAM tabulky.</p>
<h3>Výsledky testů</h3>
<p>A nyní se již podívejme na statistiky výkonnosti jednotlivých testů:</p>
<p>[caption id="attachment_632" align="aligncenter" width="461" caption="Výsledky testů"]<a href="http://blog.novoj.net/binary/2009/10/Statistics1.png"><img src="http://blog.novoj.net/binary//2009/10/Statistics1.png" alt="Výsledky testů" title="Výsledky testů" width="461" height="1799" class="size-full wp-image-632" /></a>[/caption]</p>
<p><strong>Update k 7/10/09</strong> V tabulce ještě není znázorněn poslední test, který jsem dopracoval na námět Lukáše Drbala (viz. komentáře), který testuje další funkci MySQL <a href="http://dev.mysql.com/doc/refman/5.0/en/load-data.html" target="_blank">Load data infile</a>. Import dat s využitím této funkce, trval:</p>
<ul>
<li>MyIsam: 8.55s</li>
<li>InnoDB: 6.46s</li>
</ul>
<p>Zdrojové kódy jsem aktualizoval, takže si funkci můžete vyzkoušet sami.</p>
<h3>Závěry</h3>
<ul>
<li>MyISAM je v daném případě srovnatelně rychlý jak InnoDB pod transakcí</li>
<li>multi-row inserty zaznamenaly v případě MyISAM engine cca. 2.5x zrychlení, v případě InnoDB engine cca. 15x zrychlení oproti autocommit přístupu a 2x zrychlení oproti transakčnímu přístupu</li>
<li>uzamčení tabulek pro zápis znamenalo v případě MyISAM cca 20-25% zrychlení, v případě InnoDB nemělo prakticky vliv</li>
<li>vypnutí kontroly cizích a unikátních klíčů nemělo na rychlost importu v podstatě vliv pro oba enginy</li>
<li>zakrytí importu transakcí v případě InnoDB enginu znamenalo 8x zrychlení importu</li>
<li>využití funkce LOAD DATA INFILE je pro tyto účely nejoptimálnější - znamenalo v případě MyISAM zrychlední cca. 5.5x a v případě InnoDB cca. 42x zrychlení oproti autocommit přístupu a 5.5x zrychlení oproti transakčnímu přístupu</li>
</ul>
<p>Z výše uvedeného vyplývají následující doporučení:</p>
<ul>
<li>pokud je to možné použijte LOAD DATA INFILE funkci - zde můžete narazit na problém provázání cizích klíčů - nicméně kombinace s dodatečným selectem by stále mohla být poměrně efektivní</li>
<li>v libovolném případě preferujte multi-row inserty po pravidelných segmentech (velikost segmentu nehraje zase až tak velikou roli)</li>
<li>v případě, že nechcete použít multi-row inserty:
<ul>
<li>v případě MyISAM si zkuste zamknout tabulky pro zápis</li>
<li>v případě InnoDB vždy používejte transakce a segmentujte</li>
</ul>
</li>
</ul>
<h3>Out of memory při dotazování rozsáhlého resultsetu</h3>
<p>V kombinaci s rozsáhlými daty mi také docházelo k OutOfMemoryError. Prováděl jsem stránkování na úrovni ResultSetů - tj. skip řádků na první pozici požadované stránky, přečtení požadovaného počtu záznamů a uzavření result setu. Nicméně, zdá se, že MySQL JDBC ovladač se defaultně chová tak, že vždy načítá kompletní obsah result setů do paměti. Viz. výňatek z oficiální dokumentace:</p>
<p><cite>By default, ResultSets are completely retrieved and stored in memory. In most cases this is the most efficient way to operate, and due to the design of the MySQL network protocol is easier to implement. If you are working with ResultSets that have a large number of rows or large values, and can not allocate heap space in your JVM for the memory required, you can tell the driver to stream the results back one row at a time.</cite></p>
<p>Tím pádem jsem se už někde kolem 20 tisíc záznamech v tabulce dostával při 256MB paměti na Javu k OutOfMemoryError.</p>
<p>V dokumentaci je uvedeno i řešení tohoto problému na úrovni JDBC. Já jsem se dal jednodušší cestou - uvedením specifické MySQL klauzule LIMIT ve vlastním SQL příkazu.</p>
<p>Svět je plný překvapení.</p>
<h3>Odkazy na webu</h3>
<ul>
<li><a href="http://dev.mysql.com/doc/refman/5.0/en/insert-speed.html" target="_blank">Dokumentace MySQL hovořící o strategiích pro import rozsáhlých dat</a></li>
<li><a href="http://dev.mysql.com/doc/refman/5.1/en/innodb-foreign-key-constraints.html" target="_blank">MySQL dokumentace - vypnutí kontroly cizích klíčů</a></li>
<li><a href="http://www.mysqlperformanceblog.com/files/presentations/UC2005-Advanced-Innodb-Optimization.pdf" target="_blank">Tipy pro optimalizaci práce s InnoDB tabulkamy v MySQL</a></li>
<li><a href="http://benjchristensen.com/2008/05/27/mysql-jdbc-memory-usage-on-large-resultset/" target="_blank">Zdrojový článek, který mě navedl na řešení OOM v případě rozsáhlých ResultSetů</a></li>
<li><a href="http://dev.mysql.com/doc/refman/5.0/en/connector-j-reference-implementation-notes.html" target="_blank">Oficiální dokumentace MySQL JDBC ovladače</a></li>
</ul>
<h2>Zdrojové kódy ke stažení</h2>
<p><a href="http://blog.novoj.net/binary/2009/10/HugeImport.zip"><img style="margin-right: 10px" title="Zdrojové soubory" src="http://files.novoj.net/button_zip.gif" alt="Zdrojové soubory" align="left" /> IntelliJ Idea projekt se zdrojovými soubory</a></p>
<p><strong>Poznámka na závěr: </strong> Nepovažuji se za žádného MySQL databázového specialistu, takže vám budu vděčný, pokud moje závěry něčím doplníte, dovysvětlíte nebo nečím vyvrátíte.</p>
