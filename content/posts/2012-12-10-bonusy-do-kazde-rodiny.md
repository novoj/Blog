---
status: publish
published: true
title: Bonusy do každé rodiny
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<a href=\"http://blog.novoj.net/binary/2012/07/logo.png\"><img class=\"size-full
  wp-image-2120 alignleft\" title=\"Ok bonus\" src=\"http://blog.novoj.net/binary/2012/07/logo.png\"
  alt=\"\" width=\"202\" height=\"68\" /></a>O radosti z releasů jsem tady <a href=\"http://blog.novoj.net/2008/10/09/release-day/\">na
  blogu psal už dříve</a> a teď budu psát znovu, ale z jiného úhlu pohledu. Téměř
  po roce od začátku analytických prací jde do produkce jeden z mých největších dosavadních
  projektů - <strong><a href=\"https://www.okbonus.sk\" target=\"_blank\">Ok Bonus</a></strong> portál
  pro slovenskou společnost <a href=\"http://www.doxx.sk/\" target=\"_blank\">DOXX</a>.
  Podstatou projektu je poskytnout technické řešení maloobchodům a jednotlivcům pro
  tvorbu věrnostních (bonusových) programů, které si dokáží ušít samy sobě na míru.\r\n\r\nŘešení
  je složeno z několika částí: desktopové aplikace postavené nad <a href=\"http://netbeans.org/features/platform/\"
  target=\"_blank\">NetBeans RCP</a> - tzv. terminálu, který bude provozován vedle
  pokladního systému a bude umožňovat zápis informací o nákupech a také čerpání odměn.
  Nákupy a bonusy se evidují na libovolnou <a href=\"http://www.mobilmania.cz/clanky/google-nfc-neni-jen-nahrada-kreditni-karty/sc-3-a-1316282/default.aspx\"
  target=\"_blank\">NFC kartu</a>, kterých v současné době po světě běhá více než
  dost (samozřejmě bude možné získat u provozovatelů systému i brandované Ok Bonus
  NFC karty). Druhou část představuje tzv. \"platební brána\", která zpracovává transakce
  ze všech desktopových klientů a spravuje zákaznické účty. Třetí část je potom webový
  portál <a href=\"https://www.okbonus.sk\" target=\"_blank\">Ok Bonus</a>, který
  představuje prostředníka mezi zákazníky, obchodníky a platební branou. Na portále
  jsou k dispozici výpisy z účtů (tj. evidence nákupů, přidělování bonusů atd.), pro
  obchodníky potom rozhraní pro tvorbu bonusových programů, správu autorizovaných
  karet a terminálů, statistiky, e-shop a vyúčtování.\r\n\r\n"
wordpress_id: 2089
wordpress_url: http://blog.novoj.net/?p=2089
date: '2012-12-10 04:00:20 +0100'
date_gmt: '2012-12-10 03:00:20 +0100'
categories:
- Programování
- Úvahy
tags: []
comments:
- id: 120835
  author: Guido
  author_email: vit.kotacka@gmail.com
  author_url: http://www.sw-samuraj.cz/
  date: '2012-12-11 11:05:57 +0100'
  date_gmt: '2012-12-11 10:05:57 +0100'
  content: "Gratuluji k releasu :-)  Portál vypadá moc pěkně.\r\n\r\nK tomu pokrytí
    testy. Osvědčilo se mi vydefinovat si pouze určité package, které obsahují business
    logiku apod. A u nich mít pokrytí co nejvyšší (klidně +90 %). Věci, které se blbě
    testují a bylo by to spíš na integrační/funkční testy pokrývám mock objekty.\r\n\r\nTestování
    čistých POJO nemá samozřejmě smysl. Pokud ovšem neobsahují nějaké gettery se speciální
    logikou. Někdy zákazník požaduje pokrytí celé aplikace. To pak u POJO řeším jedním
    testem, který přes reflexi prosviští všechny zaregistrované třídy."
- id: 124227
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-12-13 15:51:20 +0100'
  date_gmt: '2012-12-13 14:51:20 +0100'
  content: "Díky za komentář. Já jsem si právě říkal, že mě zajímá komplexní pohled
    a tak jsem package nevylučoval, abych zjistil, kde máme mezery, ale z výše uvedeného
    rozboru vyplývá, že to smysl má - nicméně šel bych spíš cestou vylučování packagí,
    než jejich vyjmenováváním. V rámci dalšího rozvoje systému se mi to zdá jako spolehlivější
    postup.\r\n\r\nMock objekty samozřejmě taky používáme, ale jak říkám - v případě
    statistických výstupů nebo exportu do PDF jsem nepřišel na rozumný způsob jak
    účinně testovat."
---
<p><a href="http://blog.novoj.net/binary/2012/07/logo.png"><img class="size-full wp-image-2120 alignleft" title="Ok bonus" src="http://blog.novoj.net/binary/2012/07/logo.png" alt="" width="202" height="68" /></a>O radosti z releasů jsem tady <a href="http://blog.novoj.net/2008/10/09/release-day/">na blogu psal už dříve</a> a teď budu psát znovu, ale z jiného úhlu pohledu. Téměř po roce od začátku analytických prací jde do produkce jeden z mých největších dosavadních projektů - <strong><a href="https://www.okbonus.sk" target="_blank">Ok Bonus</a></strong> portál pro slovenskou společnost <a href="http://www.doxx.sk/" target="_blank">DOXX</a>. Podstatou projektu je poskytnout technické řešení maloobchodům a jednotlivcům pro tvorbu věrnostních (bonusových) programů, které si dokáží ušít samy sobě na míru.</p>
<p>Řešení je složeno z několika částí: desktopové aplikace postavené nad <a href="http://netbeans.org/features/platform/" target="_blank">NetBeans RCP</a> - tzv. terminálu, který bude provozován vedle pokladního systému a bude umožňovat zápis informací o nákupech a také čerpání odměn. Nákupy a bonusy se evidují na libovolnou <a href="http://www.mobilmania.cz/clanky/google-nfc-neni-jen-nahrada-kreditni-karty/sc-3-a-1316282/default.aspx" target="_blank">NFC kartu</a>, kterých v současné době po světě běhá více než dost (samozřejmě bude možné získat u provozovatelů systému i brandované Ok Bonus NFC karty). Druhou část představuje tzv. "platební brána", která zpracovává transakce ze všech desktopových klientů a spravuje zákaznické účty. Třetí část je potom webový portál <a href="https://www.okbonus.sk" target="_blank">Ok Bonus</a>, který představuje prostředníka mezi zákazníky, obchodníky a platební branou. Na portále jsou k dispozici výpisy z účtů (tj. evidence nákupů, přidělování bonusů atd.), pro obchodníky potom rozhraní pro tvorbu bonusových programů, správu autorizovaných karet a terminálů, statistiky, e-shop a vyúčtování.</p>
<p><a id="more"></a><a id="more-2089"></a></p>
<h2>Fungování věrnostního systému</h2>
<p>Princip fungování by měl být velmi prostý. Majitel obchodu se zaregistruje na<a href="http://www.okbonus.sk" target="_blank"> www.okbonus.sk</a> a pro své provozovny si vytvoří bonusové akce. V rámci bonus editoru je možné nastavit celou škálu akcí. Všechny akce pracují přímo s reálnými produkty - tj. útratou v EUR, konkrétním typem zboží nebo služby (např. každé 10 pivo zdarma apod.). Zvažovali jsme jednodušší variantu - zavést bodový systém, kde by se vše převádělo přes konverzní poměr na nějaké virtuální body, za které by se daly odměny "nakupovat". Nakonec jsme však tuto variantu po diskusi zamítli, protože jsou virtuální body velmi odosobněné a my jsme chtěli, aby akce byly co nejčitelnější pro koncové spotřebitele.</p>
<p>Po publikaci akce se na terminálech (instalovaných na počítačích s pokladním systémem) zobrazí sbíraný produkt a obsluha pokladny (číšník, prodavač) může začít klientům zapisovat na jejich NFC karty jejich nákupy / platby. Nevýhodou je aktuálně absence integrací do pokladních systémů - tj. při platbě je nutné zaevidovat daný produkt 2krát.</p>
<p>Z pohledu spotřebitele stačí na místě, kde akce probíhá zakoupit Ok bonus kartu nebo si zaregistrovat u prodavače na terminálu libovolnou jinou NFC kartu, kterou již zákazník vlastní. V dnešní době je velmi pravděpodobné, že takovou kartu už má - použitelné NFC karty kupříkladu jsou In-karty ČD, městké karty (pražská Opencard, pardubická / hradecká městská karta), novější typy Android telefonů (Nexus S, Galaxy II atd.), nové typy kreditních karet atd. Registrace vyžaduje pouze sdělení své e-mailové adresy a od té chvíle je již je možné sbírat produkty na všech provozovnách provozujících své varianty Ok bonus akcí. Zákazník tím automaticky získává přístup do portálu, kde vidí všechny své nákupy, zůstatky a odměny.</p>
<p>Obchodníci mohou přes systém vypisovat i poukázkové akce, jak je známe třeba ze <a href="http://slevomat.cz" target="_blank">Slevomat.cz</a> a stovky dalších. V této oblasti však existuje taková konkurence, že nemá smysl se je snažit porazit právě v tomto segmentu. Výhodou může být jen to, že obchodník neplatí za vypsání každé jednotlivé akce, ale formou předplatného a v předplaceném období si bude moci vypsat libovolné množství poukázkových akcí, jaké uzná za vhodné.</p>
<h2>Pár dat ze zákulisí vývoje</h2>
<p>Na konci projektu je čas pro retrospektivu a tak jsem si vyjel pár informací, které mě zajímaly. Zdrojové kódy čítají aktuálně <strong>80 tisíc ručně psaných řádků</strong> kódu a dalších 82 tisíc řádků generovaného kódu (web servicy). Na třídu připadá <strong>průměrně 90 řádek</strong> kódu s tím, že na portále je největším mackem třída o 1138 řádcích a na platební bráně o 567 řádcích. Při vydělení časem vynaloženým na vývoj nám vychází produktivita <strong>31 řádků za hodinu </strong>(ne že by to číslo něco znamenalo).</p>
<p>Problémem vidím v některých případech s cyklomatickou komplexitou (cca u 30 metod někde okolo 13) a komplexitou některých tříd (cca 11 tříd okolo 130). Tedy nějaký ten refaktoring nás ještě čeká.</p>
<p>Z celkového počtu připadá <strong>30% řádků na  celkově 930 automatických testů</strong>. Valná většina testů jsou integrační testy (Spring+db). V průběhu vývoje jsme se nijak nesnažili sledovat ani cílit na nějaké metriky pokrytí kódu testy a tak jsem analýzu provedl až v závěru. <strong>Pokrytí kódů testy</strong> nám vychází na portále na žalostných <strong>36% </strong>a na platební bráně <strong>70%</strong>. Nízké číslo pokrytí na portále mi samozřejmě nedalo spát a proto jsem se pustil do hlubšího průzkumu, proč tomu tak je.</p>
<p>Jednou z příčin jsou velmi rozsáhlé modelové třídy (tj. plain POJO), kde je celá řada atributů (gettery/settery) pouze nositelem dat z DB (ceklově 3800 řádek a z toho jen 1500 je volaných v rámci testů) a druhou neexistence testů pro view vrstvu. Pokrytí vlastní <strong>business vrstvy</strong>, která je nejdůležitější, je<strong> 61%</strong>. Chybějící testy na business vrstvě se týkají většinou generování PDF, přípravy dat pro e-mailing a získávání statistických údajů, u kterých je automatizace testů sporná (tj. testovat obsah lze jen velmi obtížně - lze jen testovat, že metoda proběhla bez chyby). Z toho také vyplývá, proč máme na platební bráně úplně jiné výsledky - ta totiž představuje pouze business vrstvu s exportem do web servis.</p>
<p><em><strong>Poznámka na okraj:</strong> Ještě se na chvilku zastavím u webové vrstvy, abych trochu elaboroval na téma 0% pokrytí testy. Webovou vrstvu naší architektuře tvoří jen velmi jednoduché implementace rozhraní pro získávání dat do datové vrstvy nebo akce. Ty pouze získají uživatelská data z komponent na stránce a převolají business vrstvu, výsledek případně zkonvertují a předají dál. Akce vypíší informační respektive chybové hlášky a to je vše. </em></p>
<p><em>Jsou to tedy jen velmi tenké implementace, které jsou úzce spojeny s konfiguračními XML soubory, které definují komponentovou strukturu stránek, a také s připojenými Freemarker šablonami. Testovat je samostatně mi nepřipadá vhodné - aby to mělo nějaký efekt musely by se testovat integračně - pravděpodobně pomocí Selenium testů. Jenže Selenium testy u zakázkového projektu, jehož supportní fáze je teprve před námi je velmi drahá záležitost. Výsledkem je tedy 0% pokrytí testy s nutností ručního přetestování případných změn na webové vrstvě.</em></p>
<p>Z hlediska zastoupení formátů - kromě Java souborů je v projektu <strong>7 tisíc řádků ve Freemarkerových šablonách</strong> (průměrně 42 řádků na soubor, maximálně 1046), <strong>15 tisíc řádků v CSS souborech</strong> (průměrně 240 a maximálně 4797 řádků v souboru), <strong>26 tisíc řádků v JavaScript souborech</strong> (průměrně 221 a maximálně 4781 řádků v souboru), <strong>37 tisíc řádků v XML souborech</strong> (průměrně 105 a maximálně 1597 řádků na soubor). Jinými slovy <strong>v doprovodných souborech tvořících webovou vrstvu a konfigurace</strong> (Spring soubory, XSD, naše vlastní konfigurace komponentového GUI a nastavení modulů) <strong>je stejný počet řádek jako v Java kódu</strong>.</p>
<p>Pro ilustraci - aplikaci tvoří <strong>165 typově různých obrazovek</strong> na frontendu a něco kolem 100 obrazovek v administraci. Zdojem dat je <strong>75 specifických aplikačních tabulek</strong> a dalších 75 tabulek víceúčelových modulů v databázi <a href="http://www.percona.com/" target="_blank">Percona</a>.</p>
<p>Technologicky tvoří systém náš více méně odzkoušený stack - <a href="http://www.springsource.org/spring-framework/" target="_blank">Spring Framework</a>, <a href="http://www.springsource.org/spring-security/" target="_blank">Spring Security</a>, <a href="http://static.springsource.org/spring-ws/site/" target="_blank">Spring WebServices</a>, <a href="http://www.mybatis.org/core/index.html" target="_blank">MyBatis</a>, RamJet, <a href="http://www.oracle.com/technetwork/articles/javase/index-140168.html" target="_blank">JaxB</a>, <a href="http://itextpdf.com/" target="_blank">iText</a> a <a href="http://www.edee-cms.cz/" target="_blank">Edee CMS</a>.</p>
<h2>Koukněte se sami ...</h2>
<p>Doufám, že se projekt na trhu uchytí a my budeme mít šanci se na jeho rozvoji dále podílet. Přestože jsme se snažili odvést tu nejlepší práci co umíme, myslím, že je celá řada míst, kde by se mohlo zlepšovat (slovy našeho grafika - "tak teď když vidím, jak to má celé fungovat, tak bych plno věcí navrhl jinak"). Bohužel některé věci jsou vidět až tehdy, když je systém hotový a jsem si jistý, že na leccos po pár měsících provozu ještě přijdeme.</p>
<p>Dost řečí - sami si můžete proklepnout alespoň část projektu na adrese <a href="http://www.okbonus.sk" target="_blank">www.okbonus.sk</a> a přikládám také pár fotek z míst, která nejsou na první pohled vidět (jsou přístupná až po registraci a jenom někomu):</p>
<p>[gallery link="file" columns="4" orderby="title" exclude="2120"]</p>
