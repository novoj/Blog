---
status: publish
published: true
title: Jabber Shell
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img src=\"http://blog.novoj.net/binary/2011/04/jabber-e1304104507350.png\"
  alt=\"\" title=\"Jabber\" width=\"100\" height=\"150\" class=\"alignleft size-full
  wp-image-1410\" style=\"margin-left: 20px; margin-right: 20px;\" />Nápad použít
  <a href=\"http://cs.wikipedia.org/wiki/Extensible_Messaging_and_Presence_Protocol\"
  target=\"_blank\">jabber</a> jako příkazovou řádku k živému systému nás napadl asi
  před dvěma lety. Přestože se nám naše idea zdála velmi originální, jak se později
  zjistilo, nebyli jsme sami, koho podobná věc napadla. Existuje například implementace
  použití SSH přes Jabber protokol (<a href=\"http://sourceforge.net/projects/jabsh/\"
  target=\"_blank\">JabSh</a>) a možná by bylo možné při detailnějším hledání najít
  další. \r\n\r\n<b>Co nás vůbec motivovalo o nějaké takové věci vůbec přemýšlet?</b>
  \r\n\r\nPředně jsme vývojáři, kterým je příkazová řádka často bližší než sebelepší
  klikátka. Navíc klikátka umí milion věcí, které běžně nepotřebujeme - nám stačí
  jen pár základních úloh, které ovšem chceme provést velmi rychle a odkudkoliv. Ve
  firmě máme zprovozněný interní Jabber server (<a href=\"http://www.igniterealtime.org/projects/openfire/index.jsp\"
  target=\"_blank\">Openfire Jabber Server</a>) integrovaný s naším LDAP (s odpovídající
  politikou hesel), který je provozován přes SSL protokol a tudíž splňuje všechny
  bezpečnostní požadavky definované naším TA oddělením pro přístup zvenčí. Svůj jabber
  účet má každý <a href=\"http://www.fg.cz\" target=\"_blank\">zaměstnanec Forresta</a>,
  a mají ho také všichni po ruce (jeden klik nebo klávesová zkratka obvykle stačí)
  a to nejen ve firmě, ale i z domova. Klientů pro jabber protokoly je <a href=\"http://xmpp.org/xmpp-software/clients/\"
  target=\"_blank\">nepřeberné množství pro všechny platformy</a>, a to i dokonce
  pro platformy mobilní (Android, iPhone, Symbian). XMPP má řadu použitelných knihoven
  v Javě - konkrétně autoři Openfire Jabber Serveru dodávají i velmi kvalitní klientskou
  knihovnu <a href=\"http://www.igniterealtime.org/downloads/source.jsp\" target=\"_blank\">Smack</a>,
  kterou jsme si pro naše účely vybrali. Všechno tedy hrálo do karet nápadu použít
  jabber protokol jako bránu k našim interním systémům.\r\n\r\n"
wordpress_id: 1409
wordpress_url: http://blog.novoj.net/?p=1409
date: '2011-05-03 12:21:47 +0200'
date_gmt: '2011-05-03 11:21:47 +0200'
categories:
- Programování
- Java
- Softwarové nástroje
tags: []
comments:
- id: 39783
  author: NkD
  author_email: michal.nikodim@gmail.com
  author_url: ''
  date: '2011-05-03 13:37:27 +0200'
  date_gmt: '2011-05-03 12:37:27 +0200'
  content: Mazec, tohle musi byt fakt paradni.
- id: 39789
  author: lzap
  author_email: lzap@seznam.cz
  author_url: http://lukas.zapletalovi.com/
  date: '2011-05-03 14:54:00 +0200'
  date_gmt: '2011-05-03 13:54:00 +0200'
  content: "No jestli nebylo lepší udělat to VYKAZOVANI poradne, tj. pres Kerberos
    a nejake AJAX GUI pro rychlé jedno kliknutí. Ale ruku na srdce - ještě jsem nikdy
    neviděl, že by byli programátoři spokojeni s jakýmkoliv vykazovacím systémem :-)))\r\n\r\nJabber
    SSH je zajímavá myšlenka."
- id: 39800
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-05-03 21:19:51 +0200'
  date_gmt: '2011-05-03 20:19:51 +0200'
  content: "@Izap - hmm Kerberos ... myslíš použití autologinu pomocí NTLM? No je
    v případě heterogeního prostředí prohlížečů a OS (FFox, Chrome, Opera, IE + Windows
    / Linux / Mac) řekl bych nepoužitelné ... ale nerad bych tady fabuloval.\r\n\r\nNavíc
    nám Jabber přinesl celou mobilní platformu mimo interní síť a to by Kerberox s
    AJAX GUI stejně nepořešil.\r\n\r\nAle máš pravdu v tom, že vykazovací systém je
    vždycky zlo - jen je dost nutné :-D."
- id: 39853
  author: benzin
  author_email: benzin@centrum.cz
  author_url: ''
  date: '2011-05-04 07:59:52 +0200'
  date_gmt: '2011-05-04 06:59:52 +0200'
  content: Mohu se zeptat, co to prineslo oproti trivialni text array v prohlizeci?
    Jestli to dobre chapu tak u vaseho vykazovaciho systemu je hlavnim problemem prilisna
    uzivatelska privetivost. Aby clovek nemusel vedet jak napsat vetu sestavi mu ji
    klikatko samo, coz je zdlouhavejsi ne zkdyz clovek vi jak tu vetu napsat. Nebylo
    by tedy jednodussi umoznit zpis stejne vety, kterou posilate pres jabber, do text
    array ve webove aplikaci? A nebyla by pak takovai mplemetnace spise otazkou minut,
    nez tydnu?
- id: 39854
  author: benzin
  author_email: benzin@centrum.cz
  author_url: ''
  date: '2011-05-04 08:05:12 +0200'
  date_gmt: '2011-05-04 07:05:12 +0200'
  content: 'P.S.: Kdybyste to umoznili zadavat vykaz jako vetu (stejne jako to delate
    v jabberu), a pololi jste metodu GET, stacilo by pak pro zadani vykazu mit nastavenou
    webovou skratru. Vykazovalo by se pak jenom zadani treba nasledujiciho textu do
    adresniho radku "vykaz 15h task 188810 delal sem na tom fakt usilovne". A prohlizec
    by se pak treba jeste zeptatl na uzivatelske heslo, v pripade ze by uzivatel uz
    nebyl prihlasen. Dokopy by to bylo velmi obdobne snadno pouzitelne i z mobilniho
    telefonu, ale urcite by byla implementace rychlejsi.'
- id: 39857
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-05-04 08:16:12 +0200'
  date_gmt: '2011-05-04 07:16:12 +0200'
  content: "@benzin odpověď je jednoduchá - z různých důvodů (které osobně chápu)
    nechce naše TA (security) otevřít webové rozhranní směrem ven\r\n\r\nParadoxně
    nejsložitější na celém vehementu bylo právě to napojení na Legacy IS spíš než
    napojení na XMPP."
- id: 39869
  author: benzin
  author_email: benzin@centrum.cz
  author_url: ''
  date: '2011-05-04 11:21:49 +0200'
  date_gmt: '2011-05-04 10:21:49 +0200'
  content: "4Otec: to sem si myslel :-D . Takze radsi se otevrou daleko mene otestovanemu
    reseni pres XMPP :-D\r\n\r\nAle jinak se mi to libi, obecne se mi libi reseni
    postavene na jabberu."
- id: 39940
  author: "@LadaDvorak"
  author_email: lada.dvorak@email.cz
  author_url: ''
  date: '2011-05-05 12:46:03 +0200'
  date_gmt: '2011-05-05 11:46:03 +0200'
  content: Neuvazujete o tom, ze byste ten _twitter publikovali? Apropo - mame tu
    ve firme system postavenej na jabberu, skenuje to produkcni logi a pres cislo
    radku ve stack trace to zpetne dohledava v CVS/GIT autora radku a nasledne mu
    zasila pres jabber zpravu o drkopadu aplikace.... rikame tomu _robonzak
- id: 40139
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-05-08 07:58:25 +0200'
  date_gmt: '2011-05-08 06:58:25 +0200'
  content: "@LadaDvorak ... no už nějakou dobu zvažujeme publikování víc věcí, ale
    nějak jsme zatím nenašli čas rozmyslet si, co open-sourcování vlastně představuje
    za práci a jak se k tomu nejlépe postavit - a samozřejmě kde najít čas na support\r\n\r\nJeště
    k tomu _roboznaku ... nemáte problém s tím, že by vás až moc spamoval? Když si
    uvědomím, kolik vyjímek z různých důvodů nám na produkci vzniká, tak nevím, jestli
    by to škálovalo. My máme pro tyto účely zavedený agregátor výjimečných událostí
    na projektu, který tyto informce z logu sbírá a v přehledné tabulce zobrazuje
    ... tj. agreguje výjimky podle společného hashcode (podle stacktrace) a dává nám
    informace jaké výjimky, kde a s jakou četností vznikají. Navíc na konkrétní typy
    vyjímek máme nastavené detekční automaty, které nás okamžitě notifikují. Ne všechny
    výjimky ale řešíme okamžitě a některé se prostě ani nevyplatí řešit (v poměru
    přínos / náklady).\r\n\r\nUvítal bych, kdyby ses podělila o vaše zkušenosti. Díky."
- id: 40192
  author: "@LadaDvorak"
  author_email: lada.dvorak@email.cz
  author_url: ''
  date: '2011-05-09 13:17:45 +0200'
  date_gmt: '2011-05-09 12:17:45 +0200'
  content: Ja jsem ON:) Jinak delame to podobne, jen neukladame do DB. Vyjimky se
    klasifikuji podle tridy a radku, kde k nim doslo. Autorovi se posila pouze 1 hlaska,
    ostatni se zapisi do statistiky, ale neposilaji se, Urcite typy vyjimek filtrujeme
    a neposilame. Dale je zde moznost odfiltrovat urcitou cast stacku ve tracu a registrovat
    kod ve kterem je skutecna chyba. Typicky nevalidni parametry atd... Vystup na
    WEB jsem uvazoval, ale kluci tady v teamu by nebyli moc radi, kdyby se hodnotila
    jejich prace podle poctu chyb... Navic mame problem, ze pokud nekdo upravi spacing
    v kodu, tak to jde samozrejme na nej =&gt; kluci brblaj na lidi, co spatne odsazujou
    kod. S prechodem na GIT tenhle problem mozna odpadne,  Jinak na to slouzi k ciste
    rychlemu odhalovani a reakci na chyby. I ten pripadny spam vice hlaseni po jabberu
    neni uplne k zahozeni - cloveka to donuti skutecne neco s tim delat. Pamatuju
    se, ze v dobe, kdy jsem toho bota psal, tak nam system generoval denne nekolika
    MB soubory z nich valna cast byl balast casto se opakujicich vyjimek, ktere nezpusobovaly
    v aplikaci vazne problemy, ale ten zbytek byl kritickej. V tom mnozstvi dat se
    to nedalo dohledat. Po nasazeni bota, jsme odstranili nepotrebnej balast vyjimek.
    Dale jsme schopni velice pruzne reagovat na problemy v aplikaci,bez toho aniz
    by sme neustale sledovali logy.  Tak to jsou me zkusenosti. Co se tyka twitter
    botu - uvazoval o tom, ze bych na to zalozil open source projekt. vase myslenka
    se me veice libi - v nasi firme pouzivame ruzne skype msg, jabber konference,
    ale to je strasne roztristeny. Vzhledem k tomu, ze obcas mam i volny cas a programovani
    me bavi, tak by to nemusel byt uplne ztracenej cas a jakekoli spolupraci na pripadnem
    projektu se nebranim - naopak uvitam, s pozdravem Vladimir Dvorak
- id: 40200
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-05-09 14:49:48 +0200'
  date_gmt: '2011-05-09 13:49:48 +0200'
  content: "Jé sorry, tak to je teda přehmat :-D ... já mám kolegyni, co se jmenuje
    Lada a ten nick mě svedl na scestí.\r\n\r\nSkoro to vypadá, že rozumné notifikace
    přes Jabber mají svůj smysl. V podstatě jsme, jak tak koukám, došli k podobným
    závěrům, jen jsme každý použili jinou technologii pro jejich řešení (a taky bych
    řekl podle popisu, že jste o kus dál než my).\r\n\r\nCo se týká toho open-sourcování
    - proberu to s autory a vedením, co by na to říkali (já tomu jednoznačně nakloněný
    jsem) a mohli bychom to nějak dát do kupy. Osobně bych měl zase velký zájem kouknout
    se na to vaše řešení s agregací chyb + rozesíláním notifikací přes jabber.\r\n\r\nPošlu
    nějaký e-mail s mojí přestavou ok?\r\n\r\nMmch. pořádáme pravidelné hackathony,
    kde by nám mohli další pomoct dotáhnout nějaké věci na OS do konce. Mohl bych
    to zkusit nadhodit i tam ..."
- id: 40201
  author: "@LadaDvorak"
  author_email: lada.dvorak@email.cz
  author_url: ''
  date: '2011-05-09 15:10:12 +0200'
  date_gmt: '2011-05-09 14:10:12 +0200'
  content: OK. Tesim se..
- id: 40313
  author: kolega z prace
  author_email: nedam@nikomu--nic.cz
  author_url: http://www.fg.cz
  date: '2011-05-11 08:19:20 +0200'
  date_gmt: '2011-05-11 07:19:20 +0200'
  content: "1. Pokud najdes *neco*, co umi historii prikazu jako napr prikazova radka,
    tak to velmi uvitam. Nejsem totiz schopen si zapamatovat (asi postizeni mozku)
    klicova slova pro jednotlive prikazy ani jedne z nasich Jabber aplikaci.\r\n2.
    A asi bych chtel moc, kdyby to umelo Tab, jako spravny shell :)\r\nad 1. Pidgin
    umi Ctrl+Shit+sipka nahoru v Chat window umi posledni zadavane texty. Ale pokud
    chat window zavru tak si nic nepamatuje. Nicmene ve FG prostredi Pidgin neni vhodny,
    kvuli vlastnim ruznym kesovacim zalezitostem (komunikovany na cool intranetu)
    - napr. pri fluktuaci zamestnancu, odchozivsi zustavaji u Pidgin klientu v rosteru
    (kdesi v xml souboru). Napr. Psi s timto problem nema.\r\nad 2. Kdy to bude?"
- id: 40893
  author: hnidopich obecny
  author_email: nic@neni.dokonale
  author_url: ''
  date: '2011-05-18 12:25:08 +0200'
  date_gmt: '2011-05-18 11:25:08 +0200'
  content: Knihovna od Igniterealtime se nejmenuje Smash (co kouris?), ale Smack.
    Pred par dny vysla po dvou letech nova verze.
- id: 40895
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-05-18 13:34:20 +0200'
  date_gmt: '2011-05-18 12:34:20 +0200'
  content: Špatný název jsem v článku opravil, díky za upozornění. Btw. už jsme upgradovali.
- id: 42125
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-06-02 08:00:13 +0200'
  date_gmt: '2011-06-02 07:00:13 +0200'
  content: Poznámka na okraj - komentáře bez rozumného obsahu od lidí, kteří se neumějí
    podepsat budu mazat ...
- id: 48566
  author: ady
  author_email: ady@nasracky.cz
  author_url: http://ady.nasracky.cz
  date: '2011-08-12 10:35:11 +0200'
  date_gmt: '2011-08-12 09:35:11 +0200'
  content: "1) zkuste yammer na ten twitter messaging (a dev do toho muzou porad busit
    jabberem)\r\n2) parsovani chyb jsem moc nepochopil - neni na tohle continous integration
    (treba jenkins)"
- id: 48568
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-08-12 10:41:31 +0200'
  date_gmt: '2011-08-12 09:41:31 +0200'
  content: "Yammer jsme testovali. Tím, že jsme ale už měli hotové _VYKAZOVANI nebylo
    moc pracné si udělat něco podobného doma, kde to máme stoprocentně pod kontrolou.\r\n\r\nAd
    2) tím asi myslíš to co se pak odehrálo v komentářích pod článkem? Tím je myšlena
    notifikace zalogovaných chyb z produkce přímo na jabber konto autora kódu, kde
    zalogovaná chyba vylítla. To s CI nemá nic společného."
- id: 48635
  author: ady
  author_email: ady@nasracky.cz
  author_url: http://ady.nasracky.cz
  date: '2011-08-13 04:23:01 +0200'
  date_gmt: '2011-08-13 03:23:01 +0200'
  content: Aha posilat chyby z produkce autorovi radku jsem nikdy nepotreboval , za
    me to vzdy schytal nekdo z maintenance. Pokud bych to potreboval tak bych asi
    vyuzil jabber implementaci na google app enginu (a ten zrejme rovnou i napojil
    na GIT) a posilal to opet pres yammer (a filtrovani delal nekde tam na grupe).
    Diky za vysvetleni - nekdy mi prijde ze lidi zbytecne implementuji veci na ktere
    existuji nejake tooly, popriade delaji veci zbytecne slozite - tim samozrejme
    nerikam ze tohle je ten pripad :)
- id: 48763
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2011-08-14 19:52:44 +0200'
  date_gmt: '2011-08-14 18:52:44 +0200'
  content: "@Ady - myslím, že vždy je nejdůležitější zvážit kontext, ve kterém se
    člověk právě pohybuje. Osobně mám také poměrně špatnou zkušenost z kombinace příliš
    mnoho externích technologií, které spolu ne vždy dobře hrají dohromady. Zvlášť
    pokud je chci navíc úzce integrovat na interní systémy. V obecné rovině máš, ale
    samozřejmě pravdu."
---
<p><img src="http://blog.novoj.net/binary/2011/04/jabber-e1304104507350.png" alt="" title="Jabber" width="100" height="150" class="alignleft size-full wp-image-1410" style="margin-left: 20px; margin-right: 20px;" />Nápad použít <a href="http://cs.wikipedia.org/wiki/Extensible_Messaging_and_Presence_Protocol" target="_blank">jabber</a> jako příkazovou řádku k živému systému nás napadl asi před dvěma lety. Přestože se nám naše idea zdála velmi originální, jak se později zjistilo, nebyli jsme sami, koho podobná věc napadla. Existuje například implementace použití SSH přes Jabber protokol (<a href="http://sourceforge.net/projects/jabsh/" target="_blank">JabSh</a>) a možná by bylo možné při detailnějším hledání najít další. </p>
<p><b>Co nás vůbec motivovalo o nějaké takové věci vůbec přemýšlet?</b> </p>
<p>Předně jsme vývojáři, kterým je příkazová řádka často bližší než sebelepší klikátka. Navíc klikátka umí milion věcí, které běžně nepotřebujeme - nám stačí jen pár základních úloh, které ovšem chceme provést velmi rychle a odkudkoliv. Ve firmě máme zprovozněný interní Jabber server (<a href="http://www.igniterealtime.org/projects/openfire/index.jsp" target="_blank">Openfire Jabber Server</a>) integrovaný s naším LDAP (s odpovídající politikou hesel), který je provozován přes SSL protokol a tudíž splňuje všechny bezpečnostní požadavky definované naším TA oddělením pro přístup zvenčí. Svůj jabber účet má každý <a href="http://www.fg.cz" target="_blank">zaměstnanec Forresta</a>, a mají ho také všichni po ruce (jeden klik nebo klávesová zkratka obvykle stačí) a to nejen ve firmě, ale i z domova. Klientů pro jabber protokoly je <a href="http://xmpp.org/xmpp-software/clients/" target="_blank">nepřeberné množství pro všechny platformy</a>, a to i dokonce pro platformy mobilní (Android, iPhone, Symbian). XMPP má řadu použitelných knihoven v Javě - konkrétně autoři Openfire Jabber Serveru dodávají i velmi kvalitní klientskou knihovnu <a href="http://www.igniterealtime.org/downloads/source.jsp" target="_blank">Smack</a>, kterou jsme si pro naše účely vybrali. Všechno tedy hrálo do karet nápadu použít jabber protokol jako bránu k našim interním systémům.</p>
<p><a id="more"></a><a id="more-1409"></a></p>
<h2>Náš přítel _VYKAZOVANI</h2>
<p>První implementací bylo naše vykazování práce, které se přímo promítá do fakturace klientům. Pro vykázání práce bylo nutné v prohlížeči otevřít stránku našeho IS, přihlásit se, kliknout v menu na záložku vykázání práce a následně pomocí standardního formulářového dialogu vykazovat. Odezvy IS nebyly nejrychlejší a proto nám denní vykazování zabíralo víc času než většina z nás chtěla (morna to byla především pro mě, který si na vykazování vzpomenu vždy až ve chvíli, kdy už bych měl pomalu vyrážet na autobus).</p>
<p>Proto jsme si vytvořili jednoduchý protokol pro vykazování práce právě přes jabber. Mezi naše firemní kontakty jsme zařadili nový systémový účet _VYKAZOVÁNÍ, na kterém naslouchá Java aplikace zpracovávající vstupní příkazy. Pro vykázání stačí navázat kontakt s _VYKAZOVANIm a napsat mu:</p>
<pre>
[JNO 29/04/2011 at 19:42:58 says]: vloz 0.5 VDF18 APP "Implementace správy Android aplikací." 29780

[_VYKAZOVANI 29/04/2011 at 19:42:58 says]: Příkaz byl úspěšně proveden: vloz 0.5 VDF18 APP "Implementace správy Android aplikací." 29780
Celkem za 29.05.2011 odpracováno: 4,50 hodin (4 h 30 m)
Bylo úspěšně provedeno 1 příkaz(ů), neúspěšně 0 příkaz(ů)
</pre>
<p>Což představuje jednoduchý příkaz, ve kterém systému předáme žádost o zaznamenání nové činnosti na projektu VDF18 v délce trvání 1/2 hodiny, programování úkolu číslo 29780 s konkrétním komentářem. Automat nám pošle odpověď zda naši žádost zpracoval, nebo jsme se někde uklepli. Výkaz mé dnešní práce si vypíšu také jednoduše:</p>
<pre>
[JNO 29/04/2011 at 19:42:58 says]: vypis bm

[_VYKAZOVANI 29/04/2011 at 09:42:58 says]: Výpis vykázané práce ze systému Bílý Motýl:
8,00 FG OSZ " " Darování krve.                          
0,50 KB191 POR "Status JSL, JPR, LSU."                                         
4,00 BDI57 APP "Implementace šablon."                                         
Celkem za 29.04.2011 odpracováno: 12,50 hodin (12 h 30 m)
</pre>
<p>Díky tomuto přístupu dokáže většina z nás vykázat celodenní práci během minuty nebo dvou. Jediné čeho lituji je, že Jabber klienti nemají funkci podobnou Linuxovému shellu, kde přes klávesu šipka nahoru vyvolám poslední provedené příkazy v něm.</p>
<p>Je jasné, že tento způsob vykazování není pro každého a po nějakém roce a půl provozu máme poměr lidí používající původní "klikací" způsob oproti vykazování přes jabber asi 3:2. Nicméně poměr se stále hýbe dál ve směru k jabber protokolu (spolu s tím, jak se rozrůstá jeho funkcionalita).</p>
<p>V současné době se náš protokol rozrostl o řadu dalších "příkazů". Ve firmě velmi bedlivě udržujeme informace o tom, kdy je kdo na dovolené / schůzce / na jiné pobočce atd., aby vás mohli ostatní kolegové rychle lokalizovat a přizpůsobit vaší aktuální dostupnosti. Sem tam se mi ovšem stane, že zapomenu informaci o tom, že daný den budu třeba pracovat na pobočce v Praze zapsat do systému včas a vzpomenu si na to až cestou do Prahy. Aktuálně nemám problém tuto informaci pomocí příkazu v jabberu vykázat ve vlaku za pár vteřin (někteří kolegové taky často píší záznam o nepřítomnosti až na schůzce u zákazníka):</p>
<pre>
[JNO29/04/2011 at 06:24:25 says]: nepritomnost mimo "Na prazske pobocce" 29.4.2011

[_VYKAZOVANI 29/04/2011 at 06:24:25 says]: Záznam o Vaší plánované nepřítomnosti byl vložen do BM.
</pre>
<p>Aktuálně si, kromě výše uvedeného, dokážeme přes jabber velmi rychle vyhledat, na kterém serveru sídlí aplikace pro konkrétního zákazníka (dle domény, kódu projektu, kódu zákazníka), najít ten správný tomcat a apache, který aplikaci obsluhuje, najít konkrétní lidi, kteří jsou za různá oddělení za projekt odpovědní a kdo je jeho PM nebo zjistit telefonní číslo kolegy na jiné pobočce. S rostoucími možnosti stoupá i počet uživatelů a naše "závislost" na kamarádu se jménem _VYKAZOVANI pomalu roste.</p>
<h3>Kolik to stojí</h3>
<p>Díky tomu, jak je infrastruktura lehce dostupná (většinu toho skutečně získáte zdarma), jde jen o implementaci vlastní business logiky nad XMPP protokolem. V našem případě zabrala implementace napojení na IS v úvodní fázi cca 7 dní a společně s dalšími rozšířeními jsme se vyšplhali cca na 15 dní práce. Čas ušetřený 20 zaměstnanci (2/5 firmy), kteří denodenně protokol využívají, vynaložené náklady rychle nahradil.</p>
<h2>Naše tetka švitořilka _TWITTER</h2>
<p>Přestože máme cool vymakaný intranet, chyběla nám určitá forma krátké hromadné komunikace. Na intranet se obvykle píší články přinášející větší souvislejší sadu informací a napsání takového článku na intranet pár desítek minut trvá. E-mail ani hromadné zprávy v twitteru se k podobné věci nehodí, protože časem zapadnou.</p>
<p>V týmu existuje plno informací, které se dají říci jedinou (důležitou) větu a které se nikde hromadně nekomunikují / neukládají. Tento druh informací se obvykle předává na chodbách u kafe nebo na balkónech u cigarety a zřídkakdy opouští místnost, kde se na ně někdo vyptal. Přesto mohou být některé z nich pro ostatní kolegy na jiných pobočkách důležité.</p>
<p>Proto jsme si vyrobili nového kamaráda _TWITTERa, který nám umožňuje tento druh informací sdílet, aniž by opustily brány firmy. Princip je v podstatě kopie toho, na co jsme zvyklí v Twitteru - tj. základem je používání tagů, které umožňují slinkovávat podobné věci dohromady. Nerozeznáváme mezi uživatelem a tagem, tj. zkratka každého z nás je zároveň tagem, pod kterým je možné vyhledat tweety od daného člověka. A zapsání nového tweetu je opravdu jednoduché:</p>
<pre>
[JNO 20/04/2011 at 10:17:03 says]: @ #Patch #MailModule verze 4.7.2 opravuje problém nenaběhnutí modulu při touchování sitemap. První naběhnutí je ok, po touchích už nenabíhal. #fix
[JNO 25/04/2011 at 16:10:43 says]: @ #JNO #Release #Adam v. 2.9.0 ADaM - oprava Blobů na Oracle, další vylepšení (viz. release notes)
[JNO 29/04/2011 at 09:52:19 says]: @ #JNO nově umí #RamJet jednoduše duplikovat celé oblasti s vstupními polemi pro zadávání 1:N dat
</pre>
<p>Zprávy jsou rozeslány do stejné skupiny, do které patří autor zprávy (tj. od vývojáře dalším vývojářům), ale je možné sadu příjemců rozšířit zadáním tagů dalších oddělení firmy. Příjemci dostanou zprávu na svůj jabber klient. Zároveň je zpráva uložena do databáze a zobrazí se na firemním intranetu, kde je zaindexována. Informace je možné zpětně dohledat přes fulltextové vyhledávání a je zde také dostupná jednoduchá prohlížečka zpráv podle použitých tagů. Tj. na jedno kliknutí je možné si nechat vypsat zprávy od konkrétního autora, zprávy týkající se konkrétní knihovny, seznam releasů, fixy atp.</p>
<p>Implementace interního twitteru zabrala celkově asi 5 dní práce, což považuji za přiměřené náklady, jejichž návratnost je sice těžko měřitelná ale kterých ani v nejmenším nelitujeme.</p>
<h2>Pár obrazovek na závěr</h2>
<p>Aby nebylo povídání příliš suché přikládám pár obrazovek nasnímaných z různých klientů a našeho intranetu. Seznamte se s našimi "kovovými" přáteli _VYKAZOVANI a _TWITTER ...</p>
<div style="height: 500px;"/>
[gallery link="file" orderby="ID" exclude="1410"]
</div>
