---
status: publish
published: true
title: Springockito - výroba mocků snadno a rychle
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft  wp-image-2157\" title=\"Mockito\" src=\"http://blog.novoj.net/binary/2012/07/logo-300x139.jpg\"
  alt=\"\" width=\"210\" height=\"97\" />Na tento poklad narazil kolega <a href=\"http://www.linkedin.com/in/jakubliska\"
  target=\"_blank\">Jakub Liška</a>, když si sám chtěl napsat něco podobného. Pokud
  používáte pro automatické testy podporu Springu a na vytváření mocků <a href=\"http://code.google.com/p/mockito/\"
  target=\"_blank\">Mockito</a>, máte řadu možností jak vytvářet mock objekty. Jednu
  z nich, která se mi zdála poměrně jednoduchá jsem popisoval v dřívějším článku <a
  href=\"http://blog.novoj.net/2011/10/18/jak-se-zbavit-neprijemnych-zavislosti-v-testech/\"
  target=\"_blank\">Jak se zbavit nepříjemných závislostí v testech</a>, nicméně tento
  přístup dotáhl <a href=\"http://kubek2k.w.ds14.agh.edu.pl/wiki/doku.php\" target=\"_blank\">Jakub
  Janczak</a> o kus dál (jo na světě jsou milóny lidí chytřejších jak já :) ).\r\n\r\n"
wordpress_id: 2152
wordpress_url: http://blog.novoj.net/?p=2152
date: '2012-07-31 21:57:29 +0200'
date_gmt: '2012-07-31 20:57:29 +0200'
categories:
- Programování
- Java
- Testování
- Spring Framework
tags:
- Testování
- mock
- unit testing
comments:
- id: 84426
  author: Jiří Knesl
  author_email: jiri.knesl@gmail.com
  author_url: http://www.knesl.com
  date: '2012-08-01 08:19:39 +0200'
  date_gmt: '2012-08-01 07:19:39 +0200'
  content: Máte hezké barevné schéma toho syntax highlighteru. Jak se jmenuje?
- id: 84430
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2012-08-01 08:33:31 +0200'
  date_gmt: '2012-08-01 07:33:31 +0200'
  content: "Můžeme si tykat :)\r\n\r\nJe to: http://code.google.com/p/syntaxhighlighter/
    \r\nTheme Midnight: http://alexgorbatchev.com/SyntaxHighlighter/manual/themes/midnight.html"
---
<p><img class="alignleft  wp-image-2157" title="Mockito" src="http://blog.novoj.net/binary/2012/07/logo-300x139.jpg" alt="" width="210" height="97" />Na tento poklad narazil kolega <a href="http://www.linkedin.com/in/jakubliska" target="_blank">Jakub Liška</a>, když si sám chtěl napsat něco podobného. Pokud používáte pro automatické testy podporu Springu a na vytváření mocků <a href="http://code.google.com/p/mockito/" target="_blank">Mockito</a>, máte řadu možností jak vytvářet mock objekty. Jednu z nich, která se mi zdála poměrně jednoduchá jsem popisoval v dřívějším článku <a href="http://blog.novoj.net/2011/10/18/jak-se-zbavit-neprijemnych-zavislosti-v-testech/" target="_blank">Jak se zbavit nepříjemných závislostí v testech</a>, nicméně tento přístup dotáhl <a href="http://kubek2k.w.ds14.agh.edu.pl/wiki/doku.php" target="_blank">Jakub Janczak</a> o kus dál (jo na světě jsou milóny lidí chytřejších jak já :) ).</p>
<p><a id="more"></a><a id="more-2152"></a></p>
<p>Problém mého přístupu spočívá v tom, že pro různé konstelace musíte vytvářet řadu doplňkových XML souborů s factory beanami. Navíc musíte dané beany vypárat z původních konfiguračních souborů, aby se daly jednoduše zaměňovat. Knihovna s názvem <a href="https://bitbucket.org/kubek2k/springockito/wiki/springockito-annotations" target="_blank">Springockito</a> vám pomocí jednoduchých anotací <strong>@ReplaceWithMock</strong> popř. <strong>@WrapWithSpy</strong> umožní beze změny odkazovaných XML Spring konfigurací nahradit konkrétní beanu mockem a danou instanci i Spring použije při wiringu ostatních bean.</p>
<p>Integrace do projektu je jednoduchá - stačí pro testy přilinkovat tyto dvě knihovny:</p>
<p>[source lang="xml"]<br />
&lt;dependencies&gt;<br />
     ...<br />
     &lt;dependency&gt;<br />
       &lt;groupId&gt;org.kubek2k&lt;/groupId&gt;<br />
       &lt;artifactId&gt;springockito&lt;/artifactId&gt;<br />
       &lt;version&gt;1.0.4&lt;/version&gt;<br />
       &lt;scope&gt;test&lt;/scope&gt;<br />
     &lt;/dependency&gt;<br />
     &lt;dependency&gt;<br />
       &lt;groupId&gt;org.kubek2k&lt;/groupId&gt;<br />
       &lt;artifactId&gt;springockito-annotations&lt;/artifactId&gt;<br />
       &lt;version&gt;1.0.2&lt;/version&gt;<br />
       &lt;scope&gt;test&lt;/scope&gt;<br />
     &lt;/dependency&gt;<br />
     ...<br />
&lt;/dependencies&gt;<br />
[/source]</p>
<p>A následně v konfiguraci testů vyměnit třídu pro nahrávání kontextu + použít anotaci <strong>@ReplaceWithMock</strong> u privátního pole testovací třídy. Springockito se postará o nalezení beany s názvem odpovídajícím názvu pole (a samozřejmě odpovídajícím typem) a nahradí jej vygenerovaným mockem:</p>
<p>[source lang="java"]<br />
@ContextConfiguration(<br />
   loader = SpringockitoContextLoader.class,<br />
   locations = &quot;classpath:/context.xml&quot;<br />
)<br />
@RunWith(SpringJUnit4ClassRunner.class)<br />
public class SpringockitoAnnotationsMocksIntegrationTest {</p>
<p>   @ReplaceWithMock<br />
   private InnerBean innerBean;</p>
<p>   ...<br />
}<br />
[/source]</p>
<p>Doposud nevyřešený problém je úklid mocku po proběhnutí testu (<a href="https://bitbucket.org/kubek2k/springockito/issue/6/ability-to-reinitialize-reset-all-mockito" target="_blank">issue 6</a>). Testovací podpora Springu totiž cachuje inicializované Spring kontexty mezi testy (pokud nepoužijete anotaci <strong><a href="http://static.springsource.org/spring/docs/3.0.x/javadoc-api/org/springframework/test/annotation/DirtiesContext.html" target="_blank">@DirtiesContext</a></strong>) a tudíž instruovaný mock včetně svého aktuální stavu se <strong>SDÍLÍ MEZI TESTY</strong>. Z toho důvodu vám mohou a budou dva testy pracující s mockem spuštěné za sebou failovat (ten druhý v pořadí). Naštěstí je možné v <a href="http://docs.mockito.googlecode.com/hg/org/mockito/Mockito.html#17" target="_blank">Mockitu </a>resetovat stav mocků, připravený právě pro tyto situace (v jiných je naopak doporučováno jej nepoužívat). O reinicializaci mocků se však musíte postarat sami následujícím způsobem:</p>
<p>[source lang="java"]<br />
@After<br />
public void clearMocks() {<br />
   Mockito.reset(innerBean)<br />
}<br />
[/source]</p>
<p>Z výpisu chyb a commit logu je patrné, že projekt má velmi nízkou úroveň aktivity a pouze jediného commitera. To ovšem nic nemění na tom, že nápad je to velmi zajímavý a implementace velmi jednoduchá. Pokud je Vám použití sympatické, myslím, že Jakub Janczak uvítá jakýkoliv pull request.</p>
