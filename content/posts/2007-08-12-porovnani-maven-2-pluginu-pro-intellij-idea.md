---
status: publish
published: true
title: Porovnání Maven 2 pluginů pro IntelliJ Idea
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Integrace build systému do IDE je věc pro mne nepostradatelná. Není ovšem
  integrace jako integrace. Pokud používáte Maven 2 a IntelliJ Idea jako my zjistíte,
  že pluginů je řada, ale velmi rozdílné kvality a velmi rozdílné aktuálnosti.\r\n\r\nNavíc
  osobně si velmi cením možnosti buildovat projekt přímo z IDE - toto buildování je
  totiž řádově rychlejší než kterýkoli ant / maven build, jelikož IDE ví přesně, které
  třídy se změnily a zda je třeba překompilovat závislé třídy a když, tak jaké. Ant
  a Maven při vší své dokonalosti dokáží rozeznat a překompilovat jen třídy se změněným
  timestamp, ale závislé třídy nezkompilují. Dále mi to umožňuje jednoduše používat
  HOT replace funkcionalitu, pouštět testy přímo z IDE atd. Důvodů je prostě řada.
  Proto jsem chtěl, aby mi plugin pomohl zůstat ve svém IDE, ale pro správu dependencí
  a produkčních buildů využít daleko lepších možností Maven 2. Chvíli to trvalo, ale
  našel jsem.\r\n\r\n"
wordpress_id: 29
wordpress_url: http://blog.novoj.net/2007/08/12/porovnani-maven-2-pluginu-pro-intellij-idea/
date: '2007-08-12 06:09:43 +0200'
date_gmt: '2007-08-12 05:09:43 +0200'
categories:
- Softwarové nástroje
- Maven
tags: []
comments: []
---
<p>Integrace build systému do IDE je věc pro mne nepostradatelná. Není ovšem integrace jako integrace. Pokud používáte Maven 2 a IntelliJ Idea jako my zjistíte, že pluginů je řada, ale velmi rozdílné kvality a velmi rozdílné aktuálnosti.</p>
<p>Navíc osobně si velmi cením možnosti buildovat projekt přímo z IDE - toto buildování je totiž řádově rychlejší než kterýkoli ant / maven build, jelikož IDE ví přesně, které třídy se změnily a zda je třeba překompilovat závislé třídy a když, tak jaké. Ant a Maven při vší své dokonalosti dokáží rozeznat a překompilovat jen třídy se změněným timestamp, ale závislé třídy nezkompilují. Dále mi to umožňuje jednoduše používat HOT replace funkcionalitu, pouštět testy přímo z IDE atd. Důvodů je prostě řada. Proto jsem chtěl, aby mi plugin pomohl zůstat ve svém IDE, ale pro správu dependencí a produkčních buildů využít daleko lepších možností Maven 2. Chvíli to trvalo, ale našel jsem.</p>
<p><a id="more"></a><a id="more-29"></a></p>
<p>Pokud se podíváte do repositáře Maven 2 pluginů pro Ideu, naleznete tam následujicí:</p>
<ul>
<li><strong><a href="http://quebbemann.kicks-ass.net/idea-maven-plugin/">MAIDEA - Maven 2 Integration</a></strong><br />Relativně aktuální plugin s poslední aktualizací na jaře 2007. Bohužel dokáže pouze to, že vám vypíše jen seznam použitelných Maven goalů a umí je spustit. V dolním části vám potom v konzoli vypíše standardní log Maven buildu. To není to co jsem hledal.</li>
<li><strong><a href="http://www.intellij.org/twiki/bin/view/Main/MavenPlugin">MavenPlugin</a></strong><br />Poslední aktualizace v květnu 2005. Nedokáže o moc víc jak MAIDEA.</li>
<li><strong><a href="http://mevenide.codehaus.org/mevenide-idea/">Mevenide od Codehaus</a></strong><br />Byť jsem dlouho používal jejich Maven 2 plugin do Netbeans, který byl opravdu velmi dobrý, pro IntelliJ Idea je to dost bída. Poslední aktualizace květen 2005 a opět se drží jen zavedného schematu - mít možnost pustit Maven z prostředí IDE - nic víc.</li>
<li><strong><a href="http://bryankate.googlepages.com/mavenreloaded">Maven Reloaded</a></strong><br />Už jsem ztrácel naději, když jsem narazil na tento plugin. Poslední aktualizace na jaře 2007 a především vlastnosti, které hledám.</li>
</ul>
<p>Vyzkoušel jsem tedy MAIDEA i Maven Reloaded a druhý jmenovaný vyšel zakrátko z klání jako vítěz. Po několika měsíčním používání na něj mohu pět jen chválu. O jeho vlastnostech se můžete dočíst <a href="http://bryankate.googlepages.com/mavenreloaded">na homepage</a>, přesto však některé z nich uvedu:</p>
<ol>
<li>automaticky vyhledá pom.xml v projektu a do definice modulu v IDE doplní závislosti (včetně tranzitivních) z pom.xml</li>
<li>při dotahování závislých knihoven umí volitelně dotáhnout a přilinkovat i zdrojáky a javadoc (pokud jsou tyto dostupné v repositáři)</li>
<li>pokud máte multimodule projekt a více pomů, které mají dependence navzájem, dokáže tyto vztahy převést do IDE a transparentně propojí moduly i tam (tzn. skutečně tak, jak byste to provedli vy sami)</li>
<li>při aktualizaci závislostí respektuje vaše ruční změny, které jste případně provedli (např. jste ke knihovně ručně namapovali zdrojové soubory či javadoc, popř. nechá netknuté ty dependence, které jste např. ručně vložili a nemají svou reprezentaci v pom.xml - i když toto chování bych označil přinejmenším za nerozumné)</li>
<li>závislosti dokáže setřídit dle abecedy, takže i při větším množství knihoven se docela dobře orientujete</li>
<li>synchronizuje také nastavení resource adresářů - respektive adresářů, které jsou v Idea označeny jako “sources”, “test sources” a “excluded” - v Maven 2 buildu potom jako resources a testResources s jejich nastavením includes a excludes</li>
<li>dokáže spustit libovolný maven goal přímo z IDE - což je ovšem vlastnost, kterou mají i všechny ostatní pluginy a pro mě je nejméně významná</li>
<li>všechny synchronizace probíhají “on the fly”, tzn. po zaktualizování POMu, vidíte, jak se do Idey naládují (dostáhnou) nové knihovny a oindexují připojené zdrojáky nebo javadoc</li>
</ol>
<p>Ze zkušeností by uvedl jen asi dvě věci, na které jsem si musel přijít. Jednak si dejte pozor, že plugin je nutné <strong>pro každý projekt (IPR) zapnout - defaultně je vypnutý</strong> - viz. následující obrazovka (zaškrtávátko vpravo nahoře):</p>
<div><img alt="" src="http://bryankate.googlepages.com/plugin_config.png/plugin_config-full.jpg" /></div>
<p>A dále, že plugin se vám může zdát velmi pomalý - zláště pokud jste si ve výše uvedném dialogu zaškrtli dotahování zdrojáků a javadoců ke knihovnám. Například při startu IntelliJ Idea tento plugin vždy synchronizuje váš projekt a v některých případech mi start Idey protáhl z obvyklých 2-3 minut i na 5 minut. Řešení je velmi prosté - vždy jej nechávejte pouze v offline režimu - plugin se v takovém případě nebude dotazovat remote repository ale pouze se podívá do vaší lokální na disku. Synchronizace potom proběhnou do pár sekund.</p>
<p>Pouze v případech, kdy potřebujete do pom.xml dodat novou knihovnu nebo zvednout verzi existující knihovny, kterou nemáte ve svém lokálním repositáři potřebujete tyto balíky dotáhnout z remote repository. To řeším tak, že si vedle otevřu příkazovou řádku a ve složce, kde je pom.xml napíšu:</p>
<p>[source lang="java"]<br />
mvn dependency:go-offline dependency:sources<br />
[/source]</p>
<p>Tento plugin mi do lokální repository dotáhne všechny chybějící knihovny včetně jejich zdrojových kódů pokud je zapotřebí. Jakmile jsou v lokální repository, už je dokáže Maven Reloaded v offline režimu nasypat do konfigurace modulů během pár vteřin. Tato praktika možná není tak úplně user friendly, nicméně velmi radikálně šetří váš čas.</p>
<p>Poslední doporučení, které mám, je nenechat Maven Reloaded sám si zjišťovat změny pom.xml, ale udělat si na to klávesovou zkratku a pouštět si synchronizaci ručně. Osobně mám při tomto způsobu pocit lepší kontroly nad celým aktualizačním procesem - zkrátka, že vím co se děje.</p>
<p><strong>Rozloučím se heslem: Maven Reloaded Rocks!!! :D</strong></p>
