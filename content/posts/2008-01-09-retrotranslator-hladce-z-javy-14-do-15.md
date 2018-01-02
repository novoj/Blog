---
status: publish
published: true
title: Retrotranslator - hladce z Javy 1.5 do 1.4
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "Řada z vás si určitě řekne, co to ten Fura vytahuje za prehistorická témata.
  V době, kdy se už živě diskutuje o tom, co bude v Javě 1.7, rozebírá přechod z verze
  1.4 na verzi 1.5. Možná vás to překvapí, ale v našem prostředí (server web aplikace),
  provozujeme ještě řadu instalací na verzi 1.4 a možnosti upgradu v nedohlednu. Proto
  je pro nás stále aktuální udržovat / vytvářet sdílené knihovny i pro 1.4 verzi Javy.
  Hledali jsme a zkoušeli tedy nějakou co nejméně bolestivou cestu, jak využít možností
  vyšších verzí se zachováním zpětné přenositelnosti. A naším (mým :-) ) favoritem
  se stal <a href=\"http://retrotranslator.sourceforge.net/\" target=\"_new\">Retrotranslator</a>.
  Více o jeho použití se dočtete v tomto článku.\r\n\r\n"
wordpress_id: 49
wordpress_url: http://blog.novoj.net/2008/01/09/retrotranslator-hladce-z-javy-14-do-15/
date: '2008-01-09 22:41:57 +0100'
date_gmt: '2008-01-09 21:41:57 +0100'
categories:
- Java
- Softwarové nástroje
tags: []
comments: []
---
<p>Řada z vás si určitě řekne, co to ten Fura vytahuje za prehistorická témata. V době, kdy se už živě diskutuje o tom, co bude v Javě 1.7, rozebírá přechod z verze 1.4 na verzi 1.5. Možná vás to překvapí, ale v našem prostředí (server web aplikace), provozujeme ještě řadu instalací na verzi 1.4 a možnosti upgradu v nedohlednu. Proto je pro nás stále aktuální udržovat / vytvářet sdílené knihovny i pro 1.4 verzi Javy. Hledali jsme a zkoušeli tedy nějakou co nejméně bolestivou cestu, jak využít možností vyšších verzí se zachováním zpětné přenositelnosti. A naším (mým :-) ) favoritem se stal <a href="http://retrotranslator.sourceforge.net/" target="_new">Retrotranslator</a>. Více o jeho použití se dočtete v tomto článku.</p>
<p><a id="more"></a><a id="more-49"></a></p>
<h3>Použití</h3>
<p>Retrotranslator umožňuje konvertovat knihovny zkompilované v Javě 1.5 a 1.6 pro běh v Javě 1.4. Konverze si poradí s generikami, anotacemi, reflexí nad anotacemi, enumy, autoboxingem, novými for-each deklaracemi, varargs, kovariantními návratovými typy, statickými importy, novými funkcemi v kolekcích a dalšími fíčurkami. Retrotranslator dokáže navíc správně zkonvertovat i použití určité <a href="http://retrotranslator.sourceforge.net/#supported" target="_new">omezené části Java 1.5 / 1.6 API</a>.</p>
<p>Pro konverzi nepotřebujete mít k dispozici zdrojové kódy, celý převod probíhá na úrovni zkompilovaného kódu (class, jar). Úplně nejjednodušší způsob konverze je přes příkazový řádek:</p>
<p>[source lang="java"]<br />
java -jar retrotranslator-transformer-n.n.n.jar -srcjar stripes-1.4.3.jar -destjar stripes-1.4.3-jdk14.jar<br />
[/source]</p>
<p>Vyrobený jar již je možné vložit na classpath aplikace běžící pod Javou 1.4. K tomuto jaru (popř. více takto zkonvertovaným jarům) je nutné na classpath dostat ještě retrotranslator-runtime-n.n.n.jar, který obsahuje pomocné třídy, které zastupují funkcionalitu vyšší verze Javy.</p>
<p>Při použití maven pro buildování vám bude stačit snippet:</p>
<p>[source lang="xml"]<br />
<dependency><br />
    <groupId>net.sf.retrotranslator</groupId><br />
    <artifactId>retrotranslator-runtime</artifactId><br />
    <version>1.2.1</version><br />
</dependency><br />
[/source]</p>
<p>Také je možné potřebné classy (tzn. ty co jsou součástí balíku retrotranslator-runtime) zakompilovat přímo do konvertované knihovny do vámi určené package (k tomu slouží parametr -embed
<package>).</p>
<h3>Podpora</h3>
<p>Výhodu retrotranslatoru vidím v dalších doprovodných nástrojích. Jednak existuje <a href="http://plugins.intellij.net/plugin/?id=145" target="_new">plugin do IntelliJ Idea</a>, avšak důležité je hlavně jednoduché <a href="http://retrotranslator.sourceforge.net/#ant" target="_new">použití v buildovacích nástrojích jako je Ant nebo Maven</a>.</p>
<p>V našem případě je integrace do buildovacího procesu směšně jednoduchá a zajistí ji následující snippet:</p>
<p>[source lang="xml"]</p>
<plugins>
<plugin>
		<groupId>org.codehaus.mojo</groupId><br />
		<artifactId>retrotranslator-maven-plugin</artifactId><br />
		<executions><br />
			<execution><br />
				<goals><br />
					<goal>translate-project</goal><br />
				</goals><br />
				<configuration><br />
					<attach>true</attach><br />
				</configuration><br />
			</execution><br />
		</executions>
	</plugin>
</plugins>
[/source]</p>
<p>Bohužel plugin v současné verzi ještě neumí includovat runtime classy do výsledného artefaktu. V dokumentaci je sice deklarováno, že by to plugin měl umět, ale po krátkém průzkumu Groovy kódu pluginu jsem došel k závěru, že realita je jiná. Doufejme, že při vydání stabilní verze už tato funkce bude doplněna.</p>
<p>Parametr attach = true zajistí, že se retranslated jar dostane spolu s původním jarem do remotní repository.</p>
<h3>Zkušenosti</h3>
<p>Dosavadní zkušenosti s Retrotranslatorem máme dobré. S jeho pomocí jsme převedli více jak desítku externích knihoven (SubEthaMail kupříkladu) a také udržujeme JDK 1.4 verze několika vlastních knihoven a zatím jsme nenarazili na žádný problém (všechny testy svítí zelenou ;-) ). Doporučení Retrotranslatoru také najdete v <a href="http://stripes.mc4j.org/confluence/display/stripes/Java+1.4+and+Stripes" target="_new">dokumentaci Stripes Frameworku</a>, který je také JDK 1.5 only.</p>
<p>Pokud máte nějaké zkušenosti vy - budu rád, když se o ně podělíte v komentářích.</p>
<h3>Zdroje</h3>
<ul>
<li><a href="http://retrotranslator.sourceforge.net/" target="_new">Homepage Retrotranslatoru</a></li>
<li><a href="http://mojo.codehaus.org/retrotranslator-maven-plugin/" target="_new">Retrotranslator Maven Plugin - dokumentace a použití</a></li>
<li><a href="http://www.oreillynet.com/onjava/blog/2006/11/retrotranslator.html" target="_new">Blognutí o retrotranslatoru na www.onjava.com</a></li>
</ul>
<h3>Alternativy</h3>
<ul>
<li><a href="http://retroweaver.sourceforge.net/" target="_new">Retroweaver - pozor neplést, toto je úplně jiný produkt jen s podobným názvem</a></li>
<li><a href="https://glazedlists.dev.java.net/servlets/ProjectDocumentList?folderID=4541&expandFolder=4541&folderID=4540" target="_new">Declawer</a></li>
<li><a href="http://wiki.jboss.org/wiki/Wiki.jsp?page=JBossRetro" target="_new">JBossRetro</a></li>
</ul>
