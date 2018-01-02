---
status: publish
published: true
title: Fail-fast nebo Fail-tolerant?
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img src=\"http://blog.novoj.net/binary/2010/12/fail-tolerant.png\" alt=\"\"
  title=\"fail-tolerant\" width=\"136\" height=\"192\" class=\"alignleft size-full
  wp-image-1250\" /> Zdá se mi (soudě dle mne samotného), že heslo \"fail-fast\" bylo
  a je po léta základní mantrou všech (Java?) vývojářů. Tento přístup má pro programátora
  pří vývoji aplikace řadu nesporných výhod:\r\n\r\n<ul style=\"padding-left: 15em;\">\r\n
  \ <li>chyby jsou detekovány rychle a je levnější je opravit</li>\r\n  <li>příčina
  selhání je jasně viditelná a zdroj pádu většinou přestavuje zdroj vlastní chyby</li>\r\n
  \ <li>chyby nejsou zanedbávány - každá musí být opravena aby systém fungoval</li>\r\n</ul>\r\n\r\nDíky
  těmto výhodám se tahle technika velmi oblíbenou a intuitivně ji nasazujeme a používáme
  všude. Stejně tak i všichni okolo nás - od autorů aplikačních serverů, webových
  frameworků, až po tvůrce jednoúčelových knihoven.\r\n\r\nOdvrácenou stránkou této
  techniky je, že se jí těžko zbavuje ve chvílích, kdy o ni nestojíme. Nikdy si totiž
  nemůžeme být jisti odkud nám co vyskočí a v jakém stavu daná věc po vyvolání chyby
  zůstane. Na první pohled by se mohlo zdát, že toto bude pouze problém vývojářů fail-tolerant
  SW, ale já si myslím, že to je problém nás všech, který více-méně ignorujeme.\r\n\r\n"
wordpress_id: 1245
wordpress_url: http://blog.novoj.net/?p=1245
date: '2010-12-21 19:29:52 +0100'
date_gmt: '2010-12-21 18:29:52 +0100'
categories:
- Programování
tags: []
comments:
- id: 30553
  author: v6ak
  author_email: reknu@nic.cz
  author_url: ''
  date: '2010-12-21 19:52:31 +0100'
  date_gmt: '2010-12-21 18:52:31 +0100'
  content: "\"V takovém případě, by bylo dané chování opět ke škodě\"\r\nPatří tam
    ta čárka?"
- id: 30555
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-12-21 20:29:31 +0100'
  date_gmt: '2010-12-21 19:29:31 +0100'
  content: Ne, díky. Opraveno.
- id: 30595
  author: Kolisko
  author_email: kolisko@matfyz.cz
  author_url: ''
  date: '2010-12-22 10:16:53 +0100'
  date_gmt: '2010-12-22 09:16:53 +0100'
  content: Pokud uvažujeme produkční servery, tak bych ještě odlišil běh a start aplikace.
    Při běhu může být žádoucí tolerance k chybám, jak popisuješ v článku. Při startu
    je naproti tomu velice žádaná fail-fast strategie -- pokud i část systému nenaběhne,
    je lepší udělat rollback.
- id: 30608
  author: PN
  author_email: nedela.petr@email.cz
  author_url: ''
  date: '2010-12-22 16:34:56 +0100'
  date_gmt: '2010-12-22 15:34:56 +0100'
  content: 'Zajímavý článek. Jedna drobnost vyjímka se správně píše takto: výjimka.'
- id: 30761
  author: jehovista
  author_email: nedam.vam@mail.cz
  author_url: ''
  date: '2010-12-24 17:47:37 +0100'
  date_gmt: '2010-12-24 16:47:37 +0100'
  content: "=(naštěstí tato politika lze ve Freemarkeru oproti JSP)\r\nnechybi tam
    sloveso?\r\n@PN Osobne jsem slovo \"výjimka\" asi nikdy neslysel(zni mi to dost
    blbe) a konzervy z ustavu pro jazyk cesky mi muzou polibit sos."
- id: 30784
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2010-12-25 06:33:37 +0100'
  date_gmt: '2010-12-25 05:33:37 +0100'
  content: Uff, koukám, že jsem češtinu v tomto článku poměrně hezky zmasakroval.
    @Kolisko máš samozřejmě pravdu. V našem případě optimalizujeme CMS tak aby bylo
    fail-tolerant i v této startovací fázi. Problém je většinou totiž záležitostí
    špatné konfigurace, kterou mohou webaři spravit sami po naběhnutí systému (tj.
    musíme jim zajistit, aby to vůbec nějak naskočilo).
- id: 31393
  author: Tomáš Homola
  author_email: tomas.homola@gmail.com
  author_url: ''
  date: '2011-01-03 17:09:03 +0100'
  date_gmt: '2011-01-03 16:09:03 +0100'
  content: Zrovna se jsem objevil pěkný přiklad jak píše  Kolisko:"Při startu je naproti
    tomu velice žádaná fail-fast strategie", ale třeba když se provádí deploy Jaxws
    webových služeb, tak deploy jednotlivých se provádí ze souboru sun-jaxws.xml a
    když se nepodaří deploy jedné služby neprovede se start aplikace. Což když máte
    několik webových služeb na sobě nezávyslích. Tady by si myslím neuškodilo fail-tolerant.
    Argument proti a z vlastní zkušenosti, nikdo by si toho nevšiml, až do té doby
    než by volal rozlobený zákazník.
---
<p><img src="http://blog.novoj.net/binary/2010/12/fail-tolerant.png" alt="" title="fail-tolerant" width="136" height="192" class="alignleft size-full wp-image-1250" /> Zdá se mi (soudě dle mne samotného), že heslo "fail-fast" bylo a je po léta základní mantrou všech (Java?) vývojářů. Tento přístup má pro programátora pří vývoji aplikace řadu nesporných výhod:</p>
<ul style="padding-left: 15em;">
<li>chyby jsou detekovány rychle a je levnější je opravit</li>
<li>příčina selhání je jasně viditelná a zdroj pádu většinou přestavuje zdroj vlastní chyby</li>
<li>chyby nejsou zanedbávány - každá musí být opravena aby systém fungoval</li>
</ul>
<p>Díky těmto výhodám se tahle technika velmi oblíbenou a intuitivně ji nasazujeme a používáme všude. Stejně tak i všichni okolo nás - od autorů aplikačních serverů, webových frameworků, až po tvůrce jednoúčelových knihoven.</p>
<p>Odvrácenou stránkou této techniky je, že se jí těžko zbavuje ve chvílích, kdy o ni nestojíme. Nikdy si totiž nemůžeme být jisti odkud nám co vyskočí a v jakém stavu daná věc po vyvolání chyby zůstane. Na první pohled by se mohlo zdát, že toto bude pouze problém vývojářů fail-tolerant SW, ale já si myslím, že to je problém nás všech, který více-méně ignorujeme.</p>
<p><a id="more"></a><a id="more-1245"></a></p>
<p>Jak jsem již psal v <a href="http://blog.novoj.net/2009/08/07/odlisujete-v-aplikaci-vyvojove-testovaci-a-produkcni-prostredi/">článku o rozlišování běhových prostředí</a>, sami bychom měli chtít od SW odlišné chování v závislosti s jakým cílem aktuálně běží. Ve vývojovém a testovacím prostředí jednoznačně preferujeme fail-fast variantu, v produkci bude naopak naším cílem fail-tolerant chování. Nemusím jít daleko do historie, abych jako příklad dal totální selhání webu České Spořitelny, ze kterého po několik hodin lítaly pouze vyjímky WebLogic serveru. Otázka je, zda prvotní příčina byla natolik fatální, aby to vyřadilo 100% funkcionality webu. Co už otázkou není je výstup stacktrace přímo uživateli - v produkčním prostředí se zcela jednoznačně musí chovat aplikace tak, aby se k uživateli podobné věci nedostaly (např. nahradit chybu rozumnou hláškou nebo prázdným místem tam, kde měla být původní data - v řadě případů by si uživatel třeba ani chyby nevšimnul, pokud by po těchto datech přímo nešel).</p>
<p>Pokud vyvíjíme jednoúčelovou aplikaci, se kterou pracujeme jen my jako Java vývojáři a po jejím nasazení už jen koncový uživatel není tlak na fail-tolerant tak velký (i tak bych ale prvky fail-tolerant systému doporučoval), jako v případě aplikace, která je platformou pro další práci někoho jiného. Jako příklad bych uvedl třeba námi vyvíjené CMS, které je nástrojem pro webdevelopery pro tvorbu webů. Z mé profesní minulosti bych si ale vzpomněl i na Workflow engine, který byl přes XPDL editor plně konfigurovatelný power uživateli zákazníka (tj. ti mohli vytvářet procesní pravidla, podle kterých se workflow odehrávalo).</p>
<p>V těchto případech se mi osvědčilo adaptovat systém tak, aby absorboval určitou míru ne-fatálních chyb a dokázal s nimi fungovat dál. Také je vhodné rozdělit systém na relativně izolované části tak, aby chyba jedné části systému nezpůsobila zhroucení systému jako celku. Zní to velmi jednoduše, ale cesta je velmi trnitá - naprosto vše je totiž psáno v duchu fail-fast a dá poměrně hodně práce vnutit systému chování odlišné.</p>
<p>Namátkou uvedu pár příkladů:</p>
<ol>
<li><b>inicializace rozhranní Servlet specifikace (listenery, filtry, servlety):</b>
<p>Pokud v inicializační fázi vylítne nekontrolovaná vyjímka selže inicializace kompletní webové aplikace. Pokud tedy chcete, aby aplikace ožila i v případě že není 100% funkční, musíte ošetřit naprosto všechny servlety, filtry a listenery (i ty z knihoven 3tích stran) tak, aby nebyla propuštěna jediná Exception. Proč byste něco takového mohli chtít? Například kvůli diagnostice - pokud systém alespoň nějak naběhne, jste schopni i bez přístupu na cílové prostředí analyzovat a případně opravit problém. Podobně je problém schopný lépe opravit i technik / webdeveloper, který nemá zkušenosti s Javou jako takovou, ale dokáže analyzovat stavové informace vaší aplikace.</p>
</li>
<li><b>výchozí politika zpracování chyb v knihovnách 3-tích stran je obvykle "propusť je výš":</b>
<p>Většina knihoven, se kterými jsem se setkal, vyhazují při chybách vyjímky výš. Chyba kdekoliv v JSP způsobí HTTP 500 (respektive, pokud na to myslíme, můžeme dodat vlastní ExceptionHandler, nicméně přijdeme o výstup celé původní JSP stránky). Ve Freemarkeru je exception handling defaultně nastaven na DEBUG, což znamená, že web aplikace do výstupu vypíše stacktrace, což na produkci není ideální chování (naštěstí tato politika lze ve Freemarkeru oproti JSP velmi jednoduše změnit). V JSON-lib pokud dojde k cyklickému zanoření objektů (na což nemusíte při vývoji dlouho přijít), končí problém opět vyjímkou, pokud chceme být fail-tolerant, musíme nastavit LENIENT nebo NOPROP strategii. Ve webových frameworcích typu MVC, obvykle libovolná chyba při zpracování requestu způsobí selhání zpracování requestu jako celku (a to i přesto, že pro většinu vykreslované stránky by data k vykreslení byla k dispozici).</p>
</li>
<li><b>inicializace Springových kontextů:</b>
<p>V případě libovolné chyby při inicializaci bean ve Spring kontextu je zastavena inicializace kontextu a nic se nevytvoří (respektive aplikační kontext není funkční). Opět se jedná o vše nebo nic. Přestože v případě aplikační logiky je tento stav poměrně pochopitelný, pokud si vezmeme v potaz 2 výsledné varianty produkční instalace: a) nefunguje nic b) více méně systém funguje, ale jeho konkrétní části (jednoznačně identifikovatelné) vykazují selhání. Mohli bychom v některých případech spíš hlasovat pro variantu b).</p>
</li>
<li><b>iBatis:</b>
<p>Ten nám taktéž naběhne buď úplně nebo vůbec. Naštěstí zde se téměř vždy jedná o chybu programátora a tudíž, mi tu není tohle chování tak trnem v oku jako v jiných případech. Neumím si ovšem představit použití iBatisu v rukou administrátora, který on-line edituje SQL dotazy v XML konfiguračních souborech. V takovém případě by bylo dané chování opět ke škodě - opět bych radši preferoval variantu, kdy je možné provádět všechny SQL dotazy, krom toho, který daný admin právě zprznil.</p>
</li>
<li><b>a dalo by se pokračovat dál a dál ...</b></li>
</ol>
<p>Tento článek nenabízí a ani nemůže nabízet konkrétní praktické rady - vše je odvislé od knihoven a technologií, které používáte. Osobně si můžu snad jen povzdychnout, že v některých případech, kdy je fail-fast přístup hluboce zakořeněn v konkrétní knihovně / technologii, není práce se změnou chování vůbec jednoduchá. Zajímaly by mne ovšem vaše názory a zkušenosti s touto problematikou. Uvažovali jste nad negativy fail-fast přístupu někdy? K jakým jste, vy, dospěli závěrům? Jak k tomu přistupují autoři jiných jazyků (.NET, Ruby, PHP ...)?</p>
