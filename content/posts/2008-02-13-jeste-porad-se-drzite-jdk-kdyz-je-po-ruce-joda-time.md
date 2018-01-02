---
status: publish
published: true
title: Ještě pořád se držíte JDK, když je po ruce Joda Time?
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Po delší době jsem měl zase čas podívat se na zoubek v mém TODO listu. Tentokrát
  jsem si vzal na paškál poměrně malou knihovnu s názvem <a href=\"http://joda-time.sourceforge.net/\"
  target=\"_new\">Joda Time</a>. Cílem této knihovny je reimplementace Java API pro
  práci s datumy a časem. Každý z nás, kdo pracuje s Javou nějaký ten čas, se tu a
  tam potýká s tímto těžkopádným API. Joda Time přinesl poměrně hodně nových myšlenek
  a stal se základem pro <a href=\"https://jsr-310.dev.java.net/\" target=\"_new\">JSR
  310</a>, které by mělo být součástí nové Javy 7. Často na toto téma naráží i pánové
  z Java Posse. Co je tedy na knihovně tak úžasného? Čtěte dál ...\r\n\r\n"
wordpress_id: 52
wordpress_url: http://blog.novoj.net/2008/02/13/jeste-porad-se-drzite-jdk-kdyz-je-po-ruce-joda-time/
date: '2008-02-13 11:18:58 +0100'
date_gmt: '2008-02-13 10:18:58 +0100'
categories:
- Programování
- Java
- Testování
tags: []
comments:
- id: 1541
  author: Jakub Doležal
  author_email: dolezj8@fel.cvut.cz
  author_url: ''
  date: '2008-02-13 15:48:14 +0100'
  date_gmt: '2008-02-13 14:48:14 +0100'
  content: Diky za pekny clanek o zajimavem frameworku. Stavajici podpora Date &amp;
    Time API v Jave je opravdu hrozna. Skoda, ze jsem o nicem takovem necetl pred
    ctyrmi mesici. Byvalo by mi to usetrilo dost prace :-)))
- id: 1542
  author: Ladislav Thon
  author_email: ladicek@gmail.com
  author_url: ''
  date: '2008-02-13 20:26:06 +0100'
  date_gmt: '2008-02-13 19:26:06 +0100'
  content: Stoprocentní souhlas, JodaTime je konečně rozumné API pro datum a čas.
    _Tohle_ mělo být ve standardní knihovně už dávno, ne ten běs, co je tam už drahně
    let a nad kterým je postaveno takového kódu, až to hezké není.
- id: 1543
  author: Novoj
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2008-02-13 20:31:11 +0100'
  date_gmt: '2008-02-13 19:31:11 +0100'
  content: Je to tak - v kritice na datumové Java API jsem vyčetl, že jeho nedokonalost
    (jen nevím v jakém směru) donutila autory JDBC vytvořit klony datumových tříd
    java.sql.Date a java.sql.Timestamp - jen jsem nějak už nevyčetl, jaké důvody to
    byly. Každopádně to rozhraní je skutečně více C++ než Java like.
- id: 1565
  author: winsik
  author_email: winsik@centrum.cz
  author_url: http://winsik.blogspot.com
  date: '2008-02-18 11:40:22 +0100'
  date_gmt: '2008-02-18 10:40:22 +0100'
  content: "Diky moc za clanek. Vypada to opravdu dobre\r\n\r\nCalendar. get(Calendar…..
    mi opravdu pilo krev.\r\n\r\nJestli bude opravdu i soucasti 7 tak to asi povede
    i k predelani starsich veci v ramci zlepseni citelnosti kodu."
- id: 1568
  author: Jety
  author_email: itconsulting@jetensky.net
  author_url: http://jetensky.net/blog
  date: '2008-02-20 09:32:47 +0100'
  date_gmt: '2008-02-20 08:32:47 +0100'
  content: Hezký článek, děkuji, tohle se mi určitě bude někdy hodit...
- id: 38565
  author: marek
  author_email: marek.duciuc@gmail.com
  author_url: ''
  date: '2011-04-18 14:05:22 +0200'
  date_gmt: '2011-04-18 13:05:22 +0200'
  content: Nevite nkdo jak tohle api pouzit s hibernate?
- id: 38577
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-04-18 20:02:39 +0200'
  date_gmt: '2011-04-18 19:02:39 +0200'
  content: 'Google: http://joda-time.sourceforge.net/contrib/hibernate/index.html'
---
<p>Po delší době jsem měl zase čas podívat se na zoubek v mém TODO listu. Tentokrát jsem si vzal na paškál poměrně malou knihovnu s názvem <a href="http://joda-time.sourceforge.net/" target="_new">Joda Time</a>. Cílem této knihovny je reimplementace Java API pro práci s datumy a časem. Každý z nás, kdo pracuje s Javou nějaký ten čas, se tu a tam potýká s tímto těžkopádným API. Joda Time přinesl poměrně hodně nových myšlenek a stal se základem pro <a href="https://jsr-310.dev.java.net/" target="_new">JSR 310</a>, které by mělo být součástí nové Javy 7. Často na toto téma naráží i pánové z Java Posse. Co je tedy na knihovně tak úžasného? Čtěte dál ...</p>
<p><a id="more"></a><a id="more-52"></a></p>
<div align="center">...</div>
<p>Joda Time se snaží práci s časem přiblížit co nejvíce přirozenému způsobu zacházení s časem v běžném životě. Tak například leden v Joda Time je první měsíc roku a ne nultý jako v Java API - když si vzpomenu kolikrát jen mě tahle hloupost vypekla. Dokáže pracovat s přirozenými entitami jako je čas bez datumu, datum bez času, časová perioda, časový interval a doba trvání. Odbourává netransparentní seznam konstant, který je potřeba pro práci s Java API ve třídě Calendar. Výsledkem je i pozitivní zpřehlednění našeho vlastního API - v parametrech metod nám proplouvají smysluplné objekty (např. Interval openHours místo Date open, Date close), čitelnost kódu se výrazně zvyšuje.</p>
<p>Joda Time poměrně extenzivně využívá builder patternu, který je postaven na jednoduchém principu - volání metody na objektu vrací instanci stejné třídy jako návratovou hodnotu. Výsledným efektem je, že se dá volání metod přirozeně řetězit, což značně zvyšuje čitelnost kódu a přibližuje jeho vzhled přirozené lidské mluvě.</p>
<p>Nejčastěji používané objekty jsou immutable (neměnitelné), což znamená, že je bezpečné s nimi manipulovat paralelně ve více threadech současně, aniž bychom se museli starat o synchronizaci. Knihovna poskytuje i mutable varianty objektů, které se vyplatí používat pouze v případech, kdy dochází k větší manipulaci s časem na úrovni lokální proměnné (analogie k String a StringBuffer třídám).</p>
<p>Posuďte sami na ukázkovém kódu níže:</p>
<p>[source lang="java"]<br />
/*<br />
 * Použití originálního Java API<br />
 */</p>
<p>//vytvoření datumu 12.12.2007<br />
Calendar cal = new GregorianCalendar(2007, 11, 12);<br />
Date date = cal.getTime();<br />
//nastavení hodiny v existujícím datumu<br />
//(ještě že jsme si schovali Calendar objekt)<br />
cal.set(Calendar.HOUR_OF_DAY, 5);<br />
cal.set(Calendar.MINUTE, 0);<br />
cal.set(Calendar.SECOND, 0);<br />
cal.set(Calendar.MILLISECOND, 0);<br />
date = cal.getTime();<br />
//přičtení 1 měsíce k datu (pořád s sebou vlečeme calendar)<br />
cal.add(Calendar.MONTH, 1);<br />
date = cal.getTime();<br />
//kolik minut je to od začátku roku?<br />
Calendar startOfTheYear = new GregorianCalendar(2007, 0, 1, 0, 0, 0);<br />
long minutes = (cal.getTimeInMillis() - startOfTheYear.getTimeInMillis()) / 60000;<br />
//práce s periodou, chceme vypočítat řadu<br />
//časových okamžiků s periodou 5 hodin, 5 vteřin<br />
for(int i = 0; i < 5; i++) {<br />
   cal.add(Calendar.HOUR, 5);<br />
   cal.add(Calendar.MINUTE, 50);<br />
   date = cal.getTime();<br />
}<br />
//zobrazení dne v týdnu na frontend<br />
SimpleDateFormat fmt = new SimpleDateFormat("E", new Locale("cs"));<br />
String dayOfWeek = fmt.format(date);</p>
<p>/*<br />
 * Použití Joda Time API<br />
 */</p>
<p>//vytvoření datumu 12.12.2007<br />
DateTime jodaDate = new DateTime().withDate(2007, 12, 12);<br />
//nastavení hodiny v existujícím datumu<br />
jodaDate = jodaDate.withTime(5, 0, 0, 0);<br />
//přičtení 1 měsíce k datu<br />
jodaDate = jodaDate.plusMonths(1);<br />
//kolik minut je to od začátku roku?<br />
DateTime jodaStartOfTheYear = new DateTime(2007, 1, 1, 0, 0, 0, 0);<br />
long jodaMinutes = new Duration(jodaStartOfTheYear, jodaDate).getMillis() / 60000;<br />
//práce s periodou, chceme vypočítat řadu<br />
//časových okamžiků s periodou 5 hodin, 5 vteřin<br />
Period period = new Period(5, 50, 0, 0);<br />
for(int i = 0; i < 5; i++) {<br />
   jodaDate = jodaDate.plus(period);<br />
}<br />
//zobrazení dne v týdnu na frontend<br />
String jodaDayOfWeek = jodaDate.dayOfWeek().getAsText(new Locale("cs"));<br />
[/source]</p>
<h3>Pokrytí všech MUST-HAVE</h3>
<h4>Learning curve</h4>
<p>Pročíst jednoduchý tutorial a přejít na toto API vám nedá víc jak 1 - 2 hodiny. Výsledné zpřehlednění kódu a ušetření "mentální" námahy při práci s datumy vám za to určitě stojí.</p>
<h4>Interoperabilita se standardními Date & Time objekty v JDK</h4>
<p>Základem je interoperabilita se objekty Date v základním API Javy. Konverze je jednořádková:</p>
<p>[source lang="java"]<br />
// from Joda to JDK<br />
Date jdkDate = new DateTime().toDate();</p>
<p>// from JDK to Joda<br />
DateTime dt = new DateTime(new Date());</p>
<p>// from Joda to JDK<br />
GregorianCalendar jdkGCal = new DateTime().toGregorianCalendar();</p>
<p>// from JDK to Joda<br />
DateTime dt = new DateTime(GregorianCalendar.getInstance());<br />
[/source]</p>
<h4>Převod ze Stringu a na String</h4>
<p>Podpora formátování datumů a v opačné směru parsování datumů ze Stringů. Základem je starý dobrý formát ze <a href="http://java.sun.com/j2se/1.4.2/docs/api/java/text/SimpleDateFormat.html" target="_new">SimpleDateFormat</a>, nicméně velmi zajímavá je i možnost vytváření vlastních parserů / formatterů následujícím způsobem:</p>
<p>[source lang="java"]<br />
DateTimeFormatter fmt = new DateTimeFormatterBuilder()<br />
            .appendDayOfMonth(2) //první dva znaky znamenají den v měsíci<br />
            .appendLiteral('-') //pak následuje znak pomlčky<br />
            .appendMonthOfYearShortText() //následuje název měsíce ve zkrácené formě<br />
            .appendLiteral('-') //opět následuje pomlčka<br />
            .appendTwoDigitYear(1956)  //a pak číslo roku v dvoumístném formátu<br />
            //toto konkrétně znamená povolený interval od roku 1906 do roku 2005<br />
            //př. 08 - převede na rok 1908, 03 - převede na rok 2003<br />
            .toFormatter();<br />
[/source]</p>
<p>Což dokáže převádět tam i zpět datumy ve formátu "12-Led-04".</p>
<h3>Cenné NICE-TO-HAVE</h3>
<h4>Výkonnostně předčí standardní Java API</h4>
<p>V dokumentaci se autoři Joda Time holedbají rychlostí, která má být ve všech případech větší než při použití standardního Java API. Já jsem si udělal jen jednoduchý testík, o kterém bych nechtěl absolutně tvrdit, že je průkazný, ale dal mi poměrně zajímavé výsledky. Úkázkový kód z prvního přikladu tohoto článku jsem spustil v milionu iterací a zpracování pomocí Joda Time zabralo asi jen okolo 45% času zpracování pomocí Java API. Příjemné.</p>
<h4>Podpora pro automatické testy</h4>
<p>Tento bonbónek mne velmi mile překvapil. Jedním z problémů při psaní testů pro kód operující se systémovým časem (typicky se jedná o testování metod pracujících s "aktuálními" entitami, které se odvozují od aktuálního systémového času). Při práci s klasickými datumovými objekty Java API nemáte jinou možnost (krom přenastavení systémového času, což bych jako taktiku zrovna nedoporučoval) než testovaným třídám vnutit čas zvenku tak, abyste mohli v testu zaručit "stabilní" testovací čas.</p>
<p>Joda Time umožňuje "virtuálně" přenastavit systémový čas, takže pokud v metodě pracujete s aktuálním časem přes defaultní konstruktory Joda API - tzn. new DateTime() a nikoliv new DateTime(System.currentTimeMillis()), můžete využít při testování virtuálně overridnutý čas:</p>
<p>[source lang="java"]<br />
DateTimeUtils.setCurrentMillisFixed(new DateTime(2007,12,1,12,0,0).getMillis());<br />
[/source]</p>
<p>Prostě další střípek do JUnit test enabled APIs.</p>
<h4>Easy to use with Maven 2</h4>
<p>Knihovna je buildovaná Mavenem, takže <a href="http://mvnrepository.com/artifact/joda-time/joda-time" target="_new">ve veřejné repository najdete aktuální verzi</a>. Stačí když do svého pomu přidáte:</p>
<p>[source lang="xml"]<br />
<dependency><br />
    <groupId>joda-time</groupId><br />
    <artifactId>joda-time</artifactId><br />
    <version>1.5.2</version><br />
</dependency><br />
[/source]</p>
<p>... a můžete začít experimentovat.</p>
<h3>Zdroje</h3>
<ul>
<li><a href="http://joda-time.sourceforge.net/index.html" target="_new">Joda Time homepage</a></li>
<li><a href="https://jsr-310.dev.java.net/" target="_new">JSR 310</a></li>
<li><a href="http://jirablog.blogspot.com/2008/02/jak-nas-vypek-dateformatparse.html" target="_new">Jak nás vypek DateFormat.parse() - povzdechnutí nad JDK implementací</a></li>
<li><a href="http://jroller.com/scolebourne/date/20070130" target="_new">Stephen Colebourne's blog - JSR 310</a></li>
<li><a href="http://tech.puredanger.com/2007/01/30/about-time-for-jsr-310/" target="_new"></a></li>
<li><a href="http://tech.puredanger.com/2007/01/30/about-time-for-jsr-310/" target="_new">Alex Miller - malá poznámka JSR 310</a></li>
<li><a href="http://www.theserverside.com/discussions/thread.tss?thread_id=41609" target="_new">diskuse na The server side</a></li>
<li><a href="http://www.onjava.com/pub/a/onjava/2003/06/05/java_calendar.html?page=2" target="_new">zajímavá je především diskuse na konci článku, kde se rozebírá vznik Date & Time API v Javě - paradoxně tvůrcem API má být jakási firma Taligent koupená IBM, která se profilovala především v oblasti C++</a> <a href="http://www.alphaworks.ibm.com/tech/calendars" target="_new">více také zde - přímo na stránkách IBM</a></li>
</ul>
