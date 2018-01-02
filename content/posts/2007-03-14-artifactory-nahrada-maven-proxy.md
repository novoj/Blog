---
status: publish
published: true
title: Artifactory - náhrada Maven Proxy?
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Kdo někdy nasazoval Maven2 pro vnitrofiremní použití, možná se setkal s
  aplikací <a target=\"_blank\" href=\"http://maven-proxy.codehaus.org/Home\">Maven
  Proxy od Codehausu</a>. Od vydání verze 0.2 již uběhlo přes rok a Maven Proxy neutrpěla
  žádnou aktualizaci, zato se však objevila nová konkurence v podobě <a target=\"_blank\"
  href=\"http://www.jfrog.org/sites/artifactory/latest/index.html\">Artifactory od
  JFrog</a>. Již základní sada funkcí dostupná v Maven Proxy dostatečně obhájí náklady
  s jejím zavedením, Artifactory však předbíhá Maven Proxy  vlastnostmi, které ocení
  především větší organizace. Jak sami autoři popisují, začínali sami s Maven-Proxy.
  Ve chvíli kdy její možnosti přestávaly stačit, začali si je dodělávat a došli do
  stavu, kdy jich prostě bylo tolik, že nebylo myslitelné \"propašovat\" je do původní
  Maven-Proxy.\r\n\r\n"
wordpress_id: 11
wordpress_url: http://blog.novoj.net/2007/03/14/artifactory-nahrada-maven-proxy/
date: '2007-03-14 10:18:40 +0100'
date_gmt: '2007-03-14 09:18:40 +0100'
categories:
- Maven
tags: []
comments: []
---
<p>Kdo někdy nasazoval Maven2 pro vnitrofiremní použití, možná se setkal s aplikací <a target="_blank" href="http://maven-proxy.codehaus.org/Home">Maven Proxy od Codehausu</a>. Od vydání verze 0.2 již uběhlo přes rok a Maven Proxy neutrpěla žádnou aktualizaci, zato se však objevila nová konkurence v podobě <a target="_blank" href="http://www.jfrog.org/sites/artifactory/latest/index.html">Artifactory od JFrog</a>. Již základní sada funkcí dostupná v Maven Proxy dostatečně obhájí náklady s jejím zavedením, Artifactory však předbíhá Maven Proxy  vlastnostmi, které ocení především větší organizace. Jak sami autoři popisují, začínali sami s Maven-Proxy. Ve chvíli kdy její možnosti přestávaly stačit, začali si je dodělávat a došli do stavu, kdy jich prostě bylo tolik, že nebylo myslitelné "propašovat" je do původní Maven-Proxy.</p>
<p><a id="more"></a><a id="more-11"></a> Instalace a konfigurace by měla být stejně jednoduchá jako je tomu u Maven Proxy - v podstatě jen rozbalení adresáře, který již v sobě obsahuje Jetty. Samozřejmě Artifactory lze deploynout již do existujícího aplikačního serveru. Pro ukládání artefaktů používá databázi Derby (o persistenci se stará <a target="_blank" href="http://jackrabbit.apache.org/">JackRabbit</a> - content repository dle JSR 170). Nicméně má plně funkční export / import z / do filesystem reprezentace Maven 2 repository.</p>
<p>Čím se tedy Artifactory chlubí?</p>
<ol>
<li>možností více "lokálních repository" pro rozdělení knihoven různých třetích stran i pro rozdělení vlastnoručně sestavovaných knihoven (např. na snapshot nebo ostré verze)</li>
<li>možností deploynutí nové knihovny přes web rozhraní do vybrané lokální repository</li>
<li>možností pravidelné zálohy knihoven</li>
<li>zabezpečení přístupu ke knihovnám (read / write), včetně možnosti správy skupin uživatelů atd.</li>
<li>velmi komportní webový přístup k repository využívající síly Ajaxu (<a target="_blank" href="http://www.jfrog.org/artifactory/">zkuste si demo</a> - guest/guest)</li>
<li>vyhledávání v repository ala http://mvnrepository.com/ s možností vykopírovat si rovnou kousky XML pro vložení dependency do pom.xml</li>
<li>kompletní možností administrovat obsah repository přes web - tedy odstraňování artefaktů, refresh cache u daného artefaktu atp.</li>
<li>při konfiguraci "remote repository", které tato "proxy" imituje možnost lépe nastavovat timeouty, filtry na dotahování např. jen některých knihoven (hodí se např. pro zavedení vnitrofiremní politiky zákazu používání snapshotů knihoven třetích stran)</li>
<li>a že by také větší aktivitě při zavádění nových featur a oprav chyb než je tomu u Maven-Proxy?!</li>
</ol>
<p>Sám jsem ocenil přínos původní Maven-Proxy, pokud bych však teď měl instalovat podobný nástroj, šel bych spíše cestou komfortnějšího Artifactory. Možná by stálo za úvahu zvážit i přechod z původní Maven-Proxy, díky importní funkci by to mělo být velmi jednoduché. Každopádně uvidíme, jak se budou chlapci z JFrog tužit dál.</p>
