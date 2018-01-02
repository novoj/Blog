---
status: publish
published: true
title: MySQL nebezpečí průtokových tabulek, zamyšlení nad insert into ... select from
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Je to asi rok co jsem psal <a href=\"http://blog.novoj.net/2008/08/23/mysql-temporary-tables-inside-transaction-and-the-magic-of-implicit-commit/\"
  target=\"_blank\">článek o implicitních commitech při provádění DDL příkazů</a>.
  Řešil jsem tehdy problém velmi složitého selectu, který se výrazně zjednodušil,
  pokud jsem jej rozdělil na dvě části s uložením mezivýsledků. Jelikož jsem potřeboval
  zachovat transakčnost, nemohl jsem využít temporárních tabulek a šel jsem cestou
  stálé tabulky s aplikačním hashem rozlišující mezivýsledky jednotlivých transakcí
  mezi sebou. To jsem ještě netušil, jaké mi to přinese komplikace ...\r\n\r\n"
wordpress_id: 778
wordpress_url: http://blog.novoj.net/?p=778
date: '2010-02-02 20:45:31 +0100'
date_gmt: '2010-02-02 19:45:31 +0100'
categories:
- Programování
- Databáze
tags:
- mysql
comments:
- id: 17777
  author: milos
  author_email: mmmiloss@seznam.cz
  author_url: ''
  date: '2010-02-03 08:37:38 +0100'
  date_gmt: '2010-02-03 07:37:38 +0100'
  content: "Resili jsme podobne problemy. Dost casto se zpracovani zrychlilo, kdyz
    jsme selecty (i updaty) rozdelili a ukladali mezivysledky.\r\n\r\nZda se ale,
    ze vsechny enginy musi resit stejne problemy a reseni se lisi jen v detailech.
    Takze zpusob ukladani na stranky a politika zamku bude podobna. Delam na Sybase
    a tzv. Deleted rows (ale i Forwarded rows - radky, ktere se nevesly po update
    a nachazeji se na jine strance, nez by mely byt) se nam objevuji take. U kmenovych
    tabulek jsme provedli po jedne reorganizaci, to je ale narocne na misto. \r\n\r\nNejlepsi
    asi bude mit casovou ulohu, ktera v klidove dobe provozu udela truncate. Ten je
    navic vyhodny i z hlediska indexu.\r\n\r\nINSERT .. SELECT se navic v Sybase chova
    jeste lepe, nez SELECT.... INTO tabulka (nevim, zda to v MySQL jde)."
- id: 17787
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-02-03 10:03:09 +0100'
  date_gmt: '2010-02-03 09:03:09 +0100'
  content: "Nepodporuje - má alternativní zápisy, ale takhle to přímo použít nejde:\r\n\r\nhttp://dev.mysql.com/doc/refman/5.0/en/ansi-diff-select-into-table.html\r\n\r\nMě
    se to celé naštěstí podařilo předělat na vnořené selecty, které zdá se jsou i
    výkonnější než původní řešení - hádám právě pro to, že se to celé dokáže odehrát
    v paměti a nemusí se to fyzicky dostat do té odkládací tabulky, což by zahrnovalo
    IO operace."
- id: 36374
  author: lzap
  author_email: lzap@seznam.cz
  author_url: http://lukas.zapletalovi.com/
  date: '2011-03-16 09:56:41 +0100'
  date_gmt: '2011-03-16 08:56:41 +0100'
  content: "\"Jelikož jsem potřeboval zachovat transakčnost, nemohl jsem využít temporárních
    tabulek...\"\r\n\r\nCopak to nejde vytvořit záznam v temp tabulce v rámci jedné
    transakce? V Oracle i na Postgresu lze tedy vytvořit temp tabulku v rámci transakce
    (ona se dokonce na konci transakce smaže).\r\n\r\nZajímavé každopádně. Je to dobré
    vědět."
- id: 36380
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-03-16 10:52:09 +0100'
  date_gmt: '2011-03-16 09:52:09 +0100'
  content: Na MySql je vytvoření temporární tabulky považované za DDL příkaz, který
    přeruší aktuální transakci (commitne ji).
- id: 36481
  author: Maaartin
  author_email: grajcar1@seznam.cz
  author_url: ''
  date: '2011-03-17 17:45:10 +0100'
  date_gmt: '2011-03-17 16:45:10 +0100'
  content: "Samozrejme vytvoreni temp tabulky je DDL a dela commit, ale me se vzdy
    podarilo posunout to pred zacatek transakce. Netusim v jakym pripade by to nemelo
    jit. Takze si ji vytvoris, v ramci transakce naplnis a na konci vyprazdnis. Pokud
    ji potrebujes opakovane, pak musis jen dat pozor, abys ji nepouzil vickrat soucasne,
    ale to by se stat nemelo. Tez je treba dat pozor aby dva kusy kody od ruznych
    lidi - ci od jednoho - nepouzily omylem stejny nazev, ale to lze lehce resit vhodnou
    konvenci a pro jistotu grep-em. Pri poolovani pripojeni je treba zacit necim jako
    \"DROP TEMPORARY TABLE IF EXISTS\", coz se hodi i tehdy kdyz si chces kus kodu
    opakovane vyzkouset.\r\n\r\nCelkove mam pocit, ze temporalni tabulky jsou v MySql
    naprosta nutnost. Hodne prikazu jinak proste nejde napsat efektivne, protoze vnoreny
    dotazy jsou nekdy neskutecne pomaly (a to z toho duvodu, ze MySql to neumi udelat
    poradne). Databazisti se na temporalni tabulky mraci, ale me prijde ze je to obdoba
    lokalnich promennych - zvysuje citelnost a zprehlednuje kod. Samozrejme kdyby
    DB doopravdy umely lokalni promenne, tj. vcetne typu TABLE, tak by to bylo mnohem
    lepsi."
- id: 36631
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-03-19 20:16:15 +0100'
  date_gmt: '2011-03-19 19:16:15 +0100'
  content: No tahle moje část kódu si sice řídila vlastní transakce, ale pokud existovala
    nějaká širší transakce, tak se do ní jen zapojila (<a href="http://static.springsource.org/spring/docs/2.0.x/api/org/springframework/transaction/TransactionDefinition.html#PROPAGATION_REQUIRED"
    target="_blank" rel="nofollow">PROPAGATION_REQUIRED</a>) - tj. nemohl jsem zaručit
    vytvoření tabulky před transakcí :( .
---
<p>Je to asi rok co jsem psal <a href="http://blog.novoj.net/2008/08/23/mysql-temporary-tables-inside-transaction-and-the-magic-of-implicit-commit/" target="_blank">článek o implicitních commitech při provádění DDL příkazů</a>. Řešil jsem tehdy problém velmi složitého selectu, který se výrazně zjednodušil, pokud jsem jej rozdělil na dvě části s uložením mezivýsledků. Jelikož jsem potřeboval zachovat transakčnost, nemohl jsem využít temporárních tabulek a šel jsem cestou stálé tabulky s aplikačním hashem rozlišující mezivýsledky jednotlivých transakcí mezi sebou. To jsem ještě netušil, jaké mi to přinese komplikace ...</p>
<p><a id="more"></a><a id="more-778"></a></p>
<p>Jak jsem nedávno zjistil není ukládání mezivýsledků to odkládací tabulky vůbec dobrý nápad. Zvlášť, když se počty záznamů v mezivýsledcích pohybují v řádech tisíců. Jednak tento mechanismus vyžaduje I/O operace na disku a jednak velikost tabulky neustále roste, přestože se správně čistí a reálně v ní nejsou žádné záznamy. Zní to zvláštně, ale tabulka, která pro <cite>select count(*) from TABULKA</cite> vrátí výsledek 0 záznamů může představovat několik giga místa na disku.</p>
<p>To co teď píšu je spíš empirická zkušenost, než reálná znalost toho jak to v InnoDB skutečně uvnitř chodí. Obraz jsme si skládal ze střípků v různých článcích a dokumentaci, co jsem našel. InnoDB má alokovaný prostor pro tabulku, ve kterém se pohybuje. Při insertech si doalokovává nový potřebný prostor, nicméně při deletech prostor automaticky neuvolňuje. Vzniká tak fragmentace tabulky - stejná jako známe v případě fragmentace souborů v souborovém systému. InnoDB by se mělo snažit díry s novými inserty zaplňovat, nicméně v některých případech se tak neděje moc efektivně.</p>
<p>Rychlost odezev SQL dotazů je přímo úměrná reálné velikosti tabulky a jeji fragmentaci. Tj. příkaz <cite>select count(*) from TABULKA</cite> bude trvat znatelně pomaleji na prázdné tabulce zabírající 1GB oproti prázdné tabulce zabírající pouhý 1kB. A v tom je celé jádro pudla.</p>
<p>V mém případě proudilo skrz odkládací tabulku velké množství dat (pomocí insert into ... select from ... příkazu), které (přestože ve finally bloku odmazávaly) neustále nafukovaly objem této odkládací tabulky a postupně degradovaly výkon systému.</p>
<p>Čištění zaneřáděné tabulky je možné - buď příkazem DROP + CREATE TABLE (respektive <a href="http://dev.mysql.com/doc/refman/5.0/en/truncate-table.html" target="_blank">TRUNCATE TABLE, které v konkrétním případě dělá totéž</a>) nebo <a href="http://dev.mysql.com/doc/refman/5.1/en/optimize-table.html" target="_blank">příkazem OPTIMIZE TABLE</a>. Oba dva způsoby však vyřadí tabulku na nějakou dobu z provozu (díky uzamčení celé tabulky) a tudíž jsou pro pravidelné používání v rámci práce nějaké knihovny dost diskutabilní.</p>
<p>Z výše uvedného vyplývá, že použití principu průtokové tabulky na MySQL InnoDB při větší zátěži nepoužitelné. Osobně jsem algoritmus přepsal tak, abych si vystačil s jedním SQL dotazem s dalšími subselecty a problém jsem za cenu drsnější aplikační logiky obešel.</p>
<p>Zvláštní na tom celém je to, že když jsem si dělal odděleně testy s cílem navodit fragmentaci tabulky, tak se mi to na lokálním systému vůbec nepodařilo (a to i v případě, že jsem v paralelních threadech současně vkládal i vymazával řádky z tabulky s průtokem 1 mil. řádků v tabulce). Tedy velikost tabulky se zmenšovala s počtem záznamů v ní. Z toho vyvozuji, že problém tkvěl právě v použití insert into ... select from ..., který zároveň vkládal a odmazával celé bloky řádků. Popřípadě odlišnému chování MySQL na Windows a Linuxu.</p>
<p>Insert into ... select from ... má ještě další nevýhody. Není to na první pohled vidět, ale tento příkaz vytváří celou řadu zámků - jednak write zámky v tabulce, do které zapisuje a jednak read zámky v tabulce, ze které čte. V případě, že v selectu nemůže využít indexů, ale jedná se o fulltable scan, tak to při standardní isolaci transakce (REPEATABLE READ) v podstatě uzamkne zdrojovou tabulku proti změnám (opět mne neberte 100% za slovo, tohle už bylo na mě trošku husté čtení a třeba jsem něco z dokumentace vyčetl špatně). Výsledkem bylo, že při konkurentním přístupu mě z kódu, který tyto statementy používá začaly vybíhat deadlock vyjímky, v některých případech timeout vyjímky při čekání na zámek.</p>
<p>Pokud mám mezi čtenáři nějakého MySQL experta budu velmi rád, když do komentářů napíše svůj názor na celou věc, nebo ještě lépe - víc odkryje pozadí toho všeho.</p>
<p>Tyto informace samozřejmě nejsou přenositelné na jiné DB enginy - každý pracuje se zámky trochu odlišně. Tohle jsou prostě jen empirické zkušenosti z MySQL 5.1 + InnoDB.</p>
