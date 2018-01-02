---
status: publish
published: true
title: How to make Apache HttpClient trust Let's Encrypt Certificate Authority
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"wp-image-3139 alignleft\" src=\"http://blog.novoj.net/binary/2016/02/letsencrypt-logo-large-300x233.png\"
  alt=\"\" width=\"194\" height=\"151\" />Apache <a href=\"https://hc.apache.org/\"
  target=\"_blank\">HttpClient</a> is a popular library that many other frameworks
  build upon. Naming one for all - you can find it in Spring Framework RestTemplate.
  It's quite suprising that its not easy to find compherensible walkthroughs how to
  make it trust server certificates that are not validable by certificate chains baked
  in standard Java installation. Spending a few hours searching and tweaking the code
  I've decided to document easy - step by step solution how to do this for emerging
  Let's Encrypt certificate authority (but it's applicable to any other CA too).\r\n\r\nDo
  you want to save several hours of yours? Read on :)\r\n\r\n"
wordpress_id: 3128
wordpress_url: http://blog.novoj.net/?p=3128
date: '2016-02-29 23:43:48 +0100'
date_gmt: '2016-02-29 22:43:48 +0100'
categories:
- Programování
- Java
- English
tags:
- SpringFramework
- REST
- HttpClient
- LetsEncrypt
comments:
- id: 157901
  author: Michal Hlavac
  author_email: miso@hlavki.eu
  author_url: ''
  date: '2016-03-01 10:17:11 +0100'
  date_gmt: '2016-03-01 09:17:11 +0100'
  content: Preco nestaci vlozit certifikat do $JAVA_HOME/jre/lib/security/cacerts
    ?
- id: 157902
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2016-03-01 10:19:30 +0100'
  date_gmt: '2016-03-01 09:19:30 +0100'
  content: Přesně tohle píšu v třetím odstavci článku. Protože pokud máte cluster,
    dev, test a prod prostředí, tak to musíte obejít všechno. Tento způsob se dá jednoduše
    přibalit do aplikace, pokrýt testy a mít jistotu :)
- id: 157903
  author: Michal Nikodim
  author_email: michal.nikodim@topmonks.com
  author_url: https://plus.google.com/110388086139334922170
  date: '2016-03-01 21:38:05 +0100'
  date_gmt: '2016-03-01 20:38:05 +0100'
  content: "Vsechno jasny az na:\r\n\r\n   public X509Certificate[] getAcceptedIssuers()
    {\r\n      return this.fallbackTrustManager.getAcceptedIssuers();\r\n   }\r\n\r\ntady
    nepotrebujes slozeninu z mainTrustManageru a fallbackTrustManageru ?"
- id: 157904
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2016-03-01 21:42:47 +0100'
  date_gmt: '2016-03-01 20:42:47 +0100'
  content: Asi by bylo možná vhodné udělat join polí z obou TrustManagerů - nicméně
    nikde jsem nenašel, k čemu se tato metoda používá (v HttpClientu vůbec) a evidentně
    to nemá na funkci rostlináře žádný vliv. :)
- id: 157905
  author: Augi (@AugiCZ)
  author_email: AugiCZ@twitter.example.com
  author_url: http://twitter.com/AugiCZ
  date: '2016-03-01 22:06:56 +0100'
  date_gmt: '2016-03-01 21:06:56 +0100'
  content: A proč raději nevyužít -Djavax.net.ssl.trustStore= a -Djavax.net.ssl.trustStorePassword=
    ?
- id: 157906
  author: Augi (@AugiCZ)
  author_email: AugiCZ@twitter.example.com
  author_url: http://twitter.com/AugiCZ
  date: '2016-03-01 22:08:14 +0100'
  date_gmt: '2016-03-01 21:08:14 +0100'
  content: No ale kdo dnes obchází stroje a ručně na nich něco mění? :-) To stačí
    zadat jednou do Puppetu/Ansiblu/Chefu a hotovo, ne? :-)
- id: 157907
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2016-03-01 22:17:37 +0100'
  date_gmt: '2016-03-01 21:17:37 +0100'
  content: "No jestli správně chápu: http://stackoverflow.com/questions/5871279/java-ssl-and-cert-keystore\r\n\r\n\"javax.net.ssl.trustStore
    - Location of the Java keystore file containing the collection of CA certificates
    trusted by this application process (trust store). If a trust store location is
    not specified using this property, the SunJSSE implementation searches for and
    uses a keystore file in default Java locations.\"\r\n\r\nTak tím sice vyřešíš
    Let's Encrypt, ale odřízneš si cestu k těm zapečeným CA uvnitř Java trust storu
    ne?\r\n\r\nA druhý argument je opět to, že bys to musel nasetupovat na všech prostředích
    + tím ovlivníš celou JVM, což ne vždycky chceš.\r\n\r\nA navíc se to blbě testuje
    :)\r\n\r\nMá to ale tu výhodu, že to můžeš hodit na Operations :)"
- id: 157908
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2016-03-01 22:19:25 +0100'
  date_gmt: '2016-03-01 21:19:25 +0100'
  content: Dobrá připomínka - tady asi narážíme na to, že Chef si u nás spravují kluci
    z Operations a je to pro mě komplikovanější varianta, než výše popsaná věc.
- id: 157912
  author: Filip Jirsák
  author_email: filip@jirsak.org
  author_url: ''
  date: '2016-03-04 09:22:46 +0100'
  date_gmt: '2016-03-04 08:22:46 +0100'
  content: "V aktuálních verzích Apache HTTP Client není nutné vytvářet vlastní implementace
    TrustManageru apod., vše už je implementováno:\r\n\r\nFile certFile = …;\r\n\r\nSSLContext
    sslContext = SSLContexts\r\n\t\t.custom()\r\n\t\t.useProtocol(\"TLSv1\")\r\n\t\t.loadTrustMaterial(certFile)\r\n\t\t.build();\r\n\r\nthis.httpClient
    = HttpClients\r\n\t\t.custom()\r\n\t\t.setSSLContext(sslContext)\r\n\t\t.build();"
- id: 157913
  author: Filip Jirsák
  author_email: filip@jirsak.org
  author_url: ''
  date: '2016-03-04 09:23:43 +0100'
  date_gmt: '2016-03-04 08:23:43 +0100'
  content: "Pro jistotu ještě importy:\r\n\r\nimport org.apache.http.impl.client.HttpClients;\r\nimport
    org.apache.http.ssl.SSLContexts;"
- id: 157915
  author: Filip Jirsák
  author_email: filip.jirsak@gmail.com
  author_url: https://plus.google.com/+FilipJirsák-CZ
  date: '2016-03-05 08:11:12 +0100'
  date_gmt: '2016-03-05 07:11:12 +0100'
  content: "Novou certifikační autoritu lze přidat k těm systémovým (ať už úpravou
    toho systémového úložiště, nebo jeho kopií, přidáním nové CA a odkázáním přes
    tu systémovou proměnnou).\r\n\r\nJá v tom vidím jiný problém – touhle úpravou
    měním globálně certifikační autority pro celou Javu, a když používám systémové
    úložiště autorit, musí všechny části aplikace důvěřovat těm samým autoritám. To
    se mi z hlediska bezpečnosti nelíbí. Když má jedna služba komunikovat s nějakým
    HTTPS serverem, předám jí truststore s certifikátem jedné CA nebo přímo certifikátem
    serveru, a nechci tam mít povolené žádné jiné autority. Druhá služba pak bude
    komunikovat s jiným HTTPS serverem, a bude mít zase jiný truststore pouze s certifikáty,
    které potřebuje.\r\n\r\nMám třeba ne moc významnou službu, která komunikuje se
    serverem, který má certifikát vydaný privátní autoritou provozovatele té služby.
    OK, pro tu službu mi to nevadí, ta firma může vydáním špatného certifikátu hacknout
    maximálně sama sebe. Ale nemůžu jejich CA důvěřovat i pro ostatní služby, protože
    pak by mohla hacknout i ty."
- id: 157916
  author: Filip Jirsák
  author_email: filip.jirsak@gmail.com
  author_url: https://plus.google.com/+FilipJirsák-CZ
  date: '2016-03-05 08:17:24 +0100'
  date_gmt: '2016-03-05 07:17:24 +0100'
  content: "Tohle se používá na serveru při přihlášení klientským certifikátem. Když
    server vyžaduje přihlášení klientským certifikátem, může klientovi poslat seznam
    autorit, jejichž certifikáty akceptuje. Typicky webový prohlížeč dává uživateli
    na výběr, který certifikát se má pro přihlášení použít, a podle tohohle seznamu
    certifikáty vyfiltruje.\r\n\r\nV tomhle je to rozhraní hloupě navržené, protože
    míchá dohromady klientský a serverový kód. Ale bacha při implementaci, doporučuju
    implementovat všechny metody, i když implementujete jen klienta a nějaká metoda
    by měla být určená jen pro server. Měl jsem to implementované tak, že serverové
    metody vyhazovaly nějakou unsupported výjimku, a pak myslím s Javou 7 najednou
    aplikace začala padat, protože v rámci jakéhosi bezpečnostního vylepšení začali
    volat i na klientovi některé serverové metody."
- id: 157917
  author: Vít Šesták 'v6ak'
  author_email: 69@spam.v6ak.com
  author_url: https://v6ak.com
  date: '2016-03-05 12:48:10 +0100'
  date_gmt: '2016-03-05 11:48:10 +0100'
  content: "Few notes:\r\n\r\nFirst, the issue is missing DST certificate in trust
    store. Adding the DST certificate is more future-proof, because LE might switch
    from one intermediate CA to another one in case of some unfortunate event. Note
    that the issue is related to Java rather than to Apache HttpClient: https://community.letsencrypt.org/t/will-the-cross-root-cover-trust-by-the-default-list-in-the-jdk-jre/134/2\r\n\r\nSecond,
    there is an alternative (at least for Debian): You can install ca-certificates-java.
    Your Java CAs will be imported from OS then. (OK, these alternatives have their
    pros and cons. If adding a file to $JAVA_HOME/jre/lib/security/cacerts is too
    complicated, then ca-certificates-java will be probably also too complicated.)"
- id: 157918
  author: novoj
  author_email: novotnaci@gmail.com
  author_url: ''
  date: '2016-03-07 17:31:34 +0100'
  date_gmt: '2016-03-07 16:31:34 +0100'
  content: "Toto bohužel nefunguje - takto nahozený SSLContext správně zvaliduje pouze
    certifikáty uvnitř certFile v metodě .loadTrustMaterial, ale není tam už ten fallback
    na defaultní certifikáty v Java truststore.\r\n\r\nTotot jsem si teď prakticky
    znovu ověřil pomocí testů."
- id: 157919
  author: Filip Jirsák
  author_email: filip.jirsak@gmail.com
  author_url: https://plus.google.com/+FilipJirsák-CZ
  date: '2016-03-08 08:57:08 +0100'
  date_gmt: '2016-03-08 07:57:08 +0100'
  content: "Ano, ale to je záměr :-) Nechci důvěřovat certifikátům ze systémového
    úložiště, protože nevím, které certifikáty tam jsou, a které tam budou s jinou
    verzí JRE.\r\n\r\nChápu, že někomu to takhle může vyhovovat, ale osobně to nedoporučuju
    – jste pak závislí na tom, jaké certifikáty se dodavatel JRE zrovna rozhodne přibalit.
    Proto si raději udělám vlastní úložiště s certifikáty, které potřebuju – a u kterých
    mám jistotu, že je tam budu mít i za měsíc, až vyjde aktualizace JRE."
- id: 157920
  author: novoj
  author_email: novotnaci@gmail.com
  author_url: ''
  date: '2016-03-08 09:27:44 +0100'
  date_gmt: '2016-03-08 08:27:44 +0100'
  content: "Chápu - v mém případě byla geneze taková, že pro produkci jsem pro správnou
    funkcionalitu REST clienta nemusel dělat nic - produkční servery měly certifikát
    od \"standardních\" autorit.\r\n\r\nStejný kód na testu / preprodukci ovšem padal,
    protože tam byl certifikát od Let's Encrypt. Tj. chtěl jsem jen ošéfovat funkcionalitu
    pro test.\r\n\r\nAle dobrý argument a budu na něj myslet!"
- id: 157921
  author: novoj
  author_email: novotnaci@gmail.com
  author_url: ''
  date: '2016-03-08 09:29:01 +0100'
  date_gmt: '2016-03-08 08:29:01 +0100'
  content: Ok, I must study this a little bit deeper. I'm just scratching the surface
    here - but I've never needed to solve such issues so far. Thanks!
- id: 157967
  author: Vít Šesták 'v6ak'
  author_email: 69@spam.v6ak.com
  author_url: https://v6ak.com/
  date: '2016-03-28 15:40:12 +0200'
  date_gmt: '2016-03-28 14:40:12 +0200'
  content: "„Adding the DST certificate is more future-proof, because LE might switch
    from one intermediate CA to another one in case of some unfortunate event.“\r\n\r\nWell,
    even a fortunate event can cause change of the intermediate CA, which breaks the
    code that adds the single intermediate CA to the truststore. This is no longer
    a theoretical issue: The introduced WinXP support has caused this for new certs:
    https://community.letsencrypt.org/t/upcoming-intermediate-changes/13106 (via http://www.root.cz/clanky/let-s-encrypt-funguje-v-xp-veci-se-ale-mohou-rozbit/
    ).\r\n\r\nI can confirm having a new cert issued by Let's Encrypt Authority X3
    (not X1!). Any code relying on X1 will break after a certificate renewal. Because
    the renewal needs to be done at least every 90 days (but is usually done about
    every 60 days), thing will break soon.\r\n\r\nOne way to address this might be
    adding the X3 (and maybe also X4) to the truststore, but this might break in a
    similar way in the future. As I have written, a more future-proof way is adding
    the DST root: https://www.identrust.com/certificates/trustid/root-download-x3.html"
- id: 158033
  author: Otec Fura
  author_email: novotnaci@gmail.com
  author_url: http://blog.novoj.net
  date: '2016-04-18 16:12:23 +0200'
  date_gmt: '2016-04-18 15:12:23 +0200'
  content: You were right. I've corrected the article. Thanks for help.
---
<p><img class="wp-image-3139 alignleft" src="http://blog.novoj.net/binary/2016/02/letsencrypt-logo-large-300x233.png" alt="" width="194" height="151" />Apache <a href="https://hc.apache.org/" target="_blank">HttpClient</a> is a popular library that many other frameworks build upon. Naming one for all - you can find it in Spring Framework RestTemplate. It's quite suprising that its not easy to find compherensible walkthroughs how to make it trust server certificates that are not validable by certificate chains baked in standard Java installation. Spending a few hours searching and tweaking the code I've decided to document easy - step by step solution how to do this for emerging Let's Encrypt certificate authority (but it's applicable to any other CA too).</p>
<p>Do you want to save several hours of yours? Read on :)</p>
<p><a id="more"></a><a id="more-3128"></a></p>
<p>Let's make one thing clear in the beginning - this walkthrough guides you how to make certain CA trusted only by your application that you are developing. If you can and want to make CA trusted by entire Java installation (ie. all JVM instances running from it), you can add certificate to global Java truststore by <a href="http://javarevisited.blogspot.cz/2012/03/add-list-certficates-java-keystore.html" target="_blank">following walkthrough</a>. The reason I didn't want to go this way is that I didn't want to add certificate to truststore of all environments my application runs on (it's quite impractical).</p>
<h2>If you want to keep this internal to your project, you need to ...</h2>
<h3>1) Download certificate of CA</h3>
<p>In case of Let's Encrypt authority you'll find all certificates <a href="https://letsencrypt.org/certificates/" target="_blank">on this page</a>. Namely you need this one:</p>
<p><a href="https://letsencrypt.org/certs/isrgrootx1.pem" target="_blank">https://letsencrypt.org/certs/isrgrootx1.pem</a></p>
<p>Download it, place it in your <strong>src/main/resources/somedirectory</strong> path as <strong>letsencrypt.cer</strong> (naming is not important here).</p>
<h3>2) Download backup certificate of IdenTrust CA</h3>
<p>You may also want to include IdentTrust root chain in your trust store - in case something goes wrong with LetsEncrypt root certificate:</p>
<p><a href="https://www.identrust.com/certificates/trustid/root-download-x3.html" target="_blank">https://www.identrust.com/certificates/trustid/root-download-x3.html</a></p>
<p>Download it, place it in your <strong>src/main/resources/somedirectory</strong> path as <strong>identrust.cer</strong> (naming is not important here).</p>
<h3>3) Create truststore in a file on your classpath</h3>
<p>Now we need to create new truststore file where we'll import this CA certificate. You can do this by running <strong>keytool</strong> in the directory where you saved letsencrypt.cer in previous step:</p>
<p>[source]keytool -keystore letsencrypt-truststore -alias isrgrootx -importcert -file letsencrypt.cer<br />
keytool -keystore letsencrypt-truststore -alias identrust -importcert -file identrust.cer[/source]</p>
<p>File naming is again not important - but to successfully finish this walkthrough stick with these names. You can always rename files once your unit test is green. When executing this command you'll be asked for truststore passphrase. Enter passcode <strong>letsencrypt </strong>and hit enter. Next you'll be asked to confirm that you trust letsencrypt.cer file and you need to again confirm this.</p>
<p>If you want to verify that CA certificate is safely in your truststore run:</p>
<p>[source]keytool -list -v -keystore letsencrypt-truststore[/source]</p>
<p>If you want to play more with trustore read <a href="https://docs.oracle.com/cd/E19509-01/820-3503/6nf1il6er/index.html" target="_blank">official documentation here</a>.</p>
<p><strong>Note aside:</strong> Do you ever wonder how truststore differs from keystore when Java code always uses only KeyStore class? Read <a href="http://javarevisited.blogspot.cz/2012/09/difference-between-truststore-vs-keyStore-Java-SSL.html" target="_blank">more detailed description here</a> but in short - trust store is only name convention for file where you store external certificates you trust compared to keystore where you store digital keys you own.</p>
<h3>4) Exclude file from Maven filtering</h3>
<p>We've created nice binary file on classpath that will be probably immediatelly corrupted by wonderful Maven feature, that is called filtering. So let's tell Maven not to touch our files on classpath:</p>
<p>[source language="xml"]<br />
&lt;build&gt;<br />
   &lt;resources&gt;<br />
      &lt;resource&gt;<br />
         &lt;directory&gt;src/main/resources&lt;/directory&gt;<br />
         &lt;filtering&gt;false&lt;/filtering&gt;<br />
      &lt;/resource&gt;<br />
   &lt;/resources&gt;<br />
&lt;/build&gt;<br />
[/source]</p>
<p>We can be more specific and let Maven filter some files while others not - but that's a task you can solve on your own.</p>
<h3>5) Implement TrustManagerDelegate</h3>
<p>Now let's do some coding. We need to teach Java to use our own truststore on classpath but fallback to its default trustore preinstalled with Java (we want to trust to every CA Java does and add a new CA on top of it). So we create delegating TrustManager that will ask main TrustManager managing our classpath truststore if certificate chain can be trusted and if not it delegates decision to fallback TrustManager which is the main Java one:</p>
<p>[source language="java"]<br />
import javax.net.ssl.X509TrustManager;<br />
import java.security.cert.CertificateException;<br />
import java.security.cert.X509Certificate;</p>
<p>public class TrustManagerDelegate implements X509TrustManager {<br />
   private final X509TrustManager mainTrustManager;<br />
   private final X509TrustManager fallbackTrustManager;</p>
<p>   public TrustManagerDelegate(X509TrustManager mainTrustManager, X509TrustManager fallbackTrustManager) {<br />
      this.mainTrustManager = mainTrustManager;<br />
      this.fallbackTrustManager = fallbackTrustManager;<br />
   }</p>
<p>   @Override<br />
   public void checkClientTrusted(final X509Certificate[] x509Certificates, final String authType) throws CertificateException {<br />
      try {<br />
         mainTrustManager.checkClientTrusted(x509Certificates, authType);<br />
      } catch(CertificateException ignored) {<br />
         this.fallbackTrustManager.checkClientTrusted(x509Certificates, authType);<br />
      }<br />
   }</p>
<p>   @Override<br />
   public void checkServerTrusted(final X509Certificate[] x509Certificates, final String authType) throws CertificateException {<br />
      try {<br />
         mainTrustManager.checkServerTrusted(x509Certificates, authType);<br />
      } catch(CertificateException ignored) {<br />
         this.fallbackTrustManager.checkServerTrusted(x509Certificates, authType);<br />
      }<br />
   }</p>
<p>   @Override<br />
   public X509Certificate[] getAcceptedIssuers() {<br />
      return this.fallbackTrustManager.getAcceptedIssuers();<br />
   }</p>
<p>}[/source]</p>
<h3>6) Persuade HttpClient to use our truststore</h3>
<p>Now we have to wire it all together. Let's create Spring FactoryBean for constructing HttpClient instance that will be used in our RestTemplate. Note several important points in this class:</p>
<ul>
<li><strong>getKeyStore</strong> - this method loads contents of our truststore file from classpath and parses them into KeyStore memory object - it uses passphrase to open the file</li>
<li><strong>createSslContext</strong> - creates two TrustManagers - javaDefaultTrustManager that contains multiple CA certificates that Java trusts by default, customCaTrustManager that contains only single CA certificate that we imported to our file; these two managers are composed together by TrustManagerDelegate decribed above</li>
</ul>
<p>[source language="java"]<br />
import org.apache.commons.io.IOUtils;<br />
import org.apache.http.auth.AuthScope;<br />
import org.apache.http.auth.UsernamePasswordCredentials;<br />
import org.apache.http.client.CredentialsProvider;<br />
import org.apache.http.client.config.RequestConfig;<br />
import org.apache.http.config.RegistryBuilder;<br />
import org.apache.http.conn.socket.ConnectionSocketFactory;<br />
import org.apache.http.conn.socket.PlainConnectionSocketFactory;<br />
import org.apache.http.conn.ssl.SSLConnectionSocketFactory;<br />
import org.apache.http.conn.ssl.SSLInitializationException;<br />
import org.apache.http.conn.ssl.TrustSelfSignedStrategy;<br />
import org.apache.http.impl.client.BasicCredentialsProvider;<br />
import org.apache.http.impl.client.CloseableHttpClient;<br />
import org.apache.http.impl.client.HttpClients;<br />
import org.apache.http.impl.conn.PoolingHttpClientConnectionManager;<br />
import org.springframework.beans.factory.FactoryBean;<br />
import org.springframework.beans.factory.annotation.Autowired;<br />
import org.springframework.core.io.ClassPathResource;<br />
import org.springframework.stereotype.Service;</p>
<p>import javax.annotation.PostConstruct;<br />
import javax.annotation.PreDestroy;<br />
import javax.net.ssl.SSLContext;<br />
import javax.net.ssl.TrustManager;<br />
import javax.net.ssl.TrustManagerFactory;<br />
import javax.net.ssl.X509TrustManager;<br />
import java.io.IOException;<br />
import java.io.InputStream;<br />
import java.net.URI;<br />
import java.security.KeyManagementException;<br />
import java.security.KeyStore;<br />
import java.security.KeyStoreException;<br />
import java.security.NoSuchAlgorithmException;<br />
import java.security.SecureRandom;<br />
import java.security.cert.CertificateException;</p>
<p>@Service<br />
public class RestTemplateFactory implements FactoryBean&amp;lt;CloseableHttpClient&amp;gt; {<br />
   private CloseableHttpClient client;<br />
   private final SecureRandom secureRandom = new SecureRandom();</p>
<p>   @PostConstruct<br />
   public void init() throws Exception {<br />
      final SSLContext sslContext = createSslContext();</p>
<p>      SSLConnectionSocketFactory sslSocketFactory = new SSLConnectionSocketFactory(sslContext);</p>
<p>      PoolingHttpClientConnectionManager cm = new PoolingHttpClientConnectionManager(<br />
            RegistryBuilder.&amp;lt;ConnectionSocketFactory&amp;gt;create()<br />
                  .register(&quot;http&quot;, PlainConnectionSocketFactory.getSocketFactory())<br />
                  .register(&quot;https&quot;, sslSocketFactory)<br />
                  .build()<br />
      );</p>
<p>      client = HttpClients.custom()<br />
                     .setConnectionManager(cm)<br />
                     .build();<br />
   }</p>
<p>   @Override<br />
   public CloseableHttpClient getObject() throws Exception {<br />
      return client;<br />
   }</p>
<p>   @Override<br />
   public Class&amp;lt;?&amp;gt; getObjectType() {<br />
      return CloseableHttpClient.class;<br />
   }</p>
<p>   @Override<br />
   public boolean isSingleton() {<br />
      return true;<br />
   }</p>
<p>   @PreDestroy<br />
   public void close() throws Exception {<br />
      client.close();<br />
   }</p>
<p>   private SSLContext createSslContext() throws KeyStoreException, IOException, CertificateException {<br />
      final SSLContext sslContext;<br />
      try {<br />
         sslContext = SSLContext.getInstance(&quot;TLS&quot;);<br />
         final TrustManagerFactory javaDefaultTrustManager = TrustManagerFactory.getInstance(TrustManagerFactory.getDefaultAlgorithm());<br />
         javaDefaultTrustManager.init((KeyStore)null);<br />
         final TrustManagerFactory customCaTrustManager = TrustManagerFactory.getInstance(TrustManagerFactory.getDefaultAlgorithm());<br />
         customCaTrustManager.init(getKeyStore());</p>
<p>         sslContext.init(<br />
               null,<br />
               new TrustManager[]{<br />
                     new TrustManagerDelegate(<br />
                           (X509TrustManager)customCaTrustManager.getTrustManagers()[0],<br />
                           (X509TrustManager)javaDefaultTrustManager.getTrustManagers()[0]<br />
                     )<br />
               },<br />
               secureRandom<br />
         );</p>
<p>      } catch (final NoSuchAlgorithmException ex) {<br />
         throw new SSLInitializationException(ex.getMessage(), ex);<br />
      } catch (final KeyManagementException ex) {<br />
         throw new SSLInitializationException(ex.getMessage(), ex);<br />
      }<br />
      return sslContext;<br />
   }</p>
<p>   private KeyStore getKeyStore() throws KeyStoreException, IOException, NoSuchAlgorithmException, CertificateException {<br />
      KeyStore ks = KeyStore.getInstance(&quot;JKS&quot;);<br />
      InputStream is = new ClassPathResource(&quot;META-INF/lib_rest_api/certificate/letsencrypt-truststore&quot;).getInputStream();<br />
      try {<br />
         ks.load(is, &quot;letsencrypt&quot;.toCharArray());<br />
      } finally {<br />
         IOUtils.closeQuietly(is);<br />
      }<br />
      return ks;<br />
   }</p>
<p>}[/source]</p>
<h3>7) Write the test</h3>
<p>Now we have to write test to prove that we are able to communicate with TEST server using Let's Encrypt SSL certificate as well as PRODUCTION server using SSL certificate of some other trusted certificate authority:</p>
<p>[source language="java"]import org.apache.http.HttpHost;<br />
import org.apache.http.client.methods.CloseableHttpResponse;<br />
import org.apache.http.client.methods.HttpGet;<br />
import org.apache.http.impl.client.CloseableHttpClient;<br />
import org.junit.Assert;<br />
import org.junit.Test;</p>
<p>public class RestTemplateFactoryTest {<br />
   private RestTemplateFactory tested;</p>
<p>   @Test<br />
   public void shouldContactTestApi() throws Exception {<br />
      tested = new RestTemplateFactory();</p>
<p>      tested.init();<br />
      final CloseableHttpClient client = tested.getObject();</p>
<p>      final CloseableHttpResponse response = client.execute(new HttpHost(&quot;test.mysecureddomain.com&quot;, 443, &quot;https&quot;), new HttpGet(&quot;/api/test&quot;));<br />
      Assert.assertNotNull(response);<br />
   }</p>
<p>   @Test<br />
   public void shouldContactProductionApi() throws Exception {<br />
      tested = new RestTemplateFactory();</p>
<p>      tested.init();<br />
      final CloseableHttpClient client = tested.getObject();</p>
<p>      final CloseableHttpResponse response = client.execute(new HttpHost(&quot;www.mysecureddomain.com&quot;, 443, &quot;https&quot;), new HttpGet(&quot;/api/test&quot;));<br />
      Assert.assertNotNull(response);<br />
 }</p>
<p>}[/source]</p>
<p>Oh wait! Shouldn't we started with the test in the first place? :D</p>
<p>Happy coding ...</p>
<p><strong>Credits:</strong> thanks for corrections from v6ak</p>
