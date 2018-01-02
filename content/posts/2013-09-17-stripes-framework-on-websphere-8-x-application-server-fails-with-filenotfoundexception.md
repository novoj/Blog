---
status: publish
published: true
title: Stripes Framework on WebSphere 8.x application server fails with FileNotFoundException
author:
  display_name: Otec Fura
  login: admin
  email: novotnaci@gmail.com
  url: http://blog.novoj.net
author_login: admin
author_email: novotnaci@gmail.com
author_url: http://blog.novoj.net
excerpt: "<img class=\"alignleft  wp-image-2766\" alt=\"stripes_framework\" src=\"http://blog.novoj.net/binary/2013/09/stripes_framework.png\"
  width=\"121\" height=\"121\" />\r\n\r\nIf you are struggling with running <a href=\"stripesframework.org\"
  target=\"_blank\">Stripes framework</a> based application on IBM WebSphere application
  server 8.x I may help you. You probably end up with getting HTTP 403 error pages
  on every request. If you persuade your app server to give you some reasonable logging
  data (which is not easy in the world of Java application servers :/ ) you probably
  see FileNotFoundException logged during the request.\r\n\r\nHere comes the explanation
  and a solution for you ...\r\n\r\n<em> (bug is also documented in issue <a href=\"http://www.stripesframework.org/jira/browse/STS-905\"
  target=\"_blank\">STS-905</a> and will be hopefully merged into the next version
  of Stripes framework)</em>\r\n\r\n"
wordpress_id: 2765
wordpress_url: http://blog.novoj.net/?p=2765
date: '2013-09-17 11:52:02 +0200'
date_gmt: '2013-09-17 10:52:02 +0200'
categories:
- Programování
- Stripes
tags: []
comments: []
---
<p><img class="alignleft  wp-image-2766" alt="stripes_framework" src="http://blog.novoj.net/binary/2013/09/stripes_framework.png" width="121" height="121" /></p>
<p>If you are struggling with running <a href="stripesframework.org" target="_blank">Stripes framework</a> based application on IBM WebSphere application server 8.x I may help you. You probably end up with getting HTTP 403 error pages on every request. If you persuade your app server to give you some reasonable logging data (which is not easy in the world of Java application servers :/ ) you probably see FileNotFoundException logged during the request.</p>
<p>Here comes the explanation and a solution for you ...</p>
<p><em> (bug is also documented in issue <a href="http://www.stripesframework.org/jira/browse/STS-905" target="_blank">STS-905</a> and will be hopefully merged into the next version of Stripes framework)</em></p>
<p><a id="more"></a><a id="more-2765"></a>Stripes use 2 servlet filters to handle all requests - StripesFilter and DynamicMappingFilter. First one prepares request for later processing and cleans up afterwards and is not important for us in this case. The problem lies in DynamicMappingFilter in following statement:</p>
<p>[source lang="java"]<br />
// Catch FileNotFoundException, which some containers (e.g. GlassFish) throw instead of setting SC_NOT_FOUND<br />
boolean fileNotFoundExceptionThrown = false;</p>
<p>try {<br />
   chain.doFilter(request, wrapper);<br />
} catch (FileNotFoundException exc) {<br />
   fileNotFoundExceptionThrown = true;<br />
}[/source]</p>
<p>DynamicMappingFilter delegates request processing through filter chain and when application server says that there is no resource there it gets into the way and tries to find appropriate ActionBean for it to handle request. In version 1.5.1 of the Stripes framework it only wrapped HTTP response object to intercept setting status code SC_NOT_FOUND for detecting such situation but in version 1.5.7 there is also try ... catch clausule for FileNotFoundException that is thrown instead on some application servers.</p>
<p>And there is the catch - WebSphere 8.x wraps FileNotFoundException into the ServletException and thus it is not caught by this code. Until patch is included in the Stripes framework core you have to duplicate the filter class with application of this patch:</p>
<p>[source lang="java"]<br />
try {<br />
    chain.doFilter(request, wrapper);<br />
} catch (FileNotFoundException exc) {<br />
    fileNotFoundExceptionThrown = true;<br />
} catch (ServletException ex) {<br />
    if (ex.getCause() instanceof FileNotFoundException) {<br />
        fileNotFoundExceptionThrown = true;<br />
    } else {<br />
        throw ex;<br />
    }<br />
}[/source]</p>
<p>And there is another tweak you have to make - in the very same class you have to modify inner class <em>ErrorTrappingResponseWrapper</em> by overriding two more methods:</p>
<p>[source lang="java"]<br />
@Override<br />
public void setStatus(int sc) {<br />
   this.errorCode = sc;<br />
}</p>
<p>@Override<br />
public void setStatus(int sc, String sm) {<br />
   this.errorCode = sc;<br />
   this.errorMessage = sm;<br />
}[/source]</p>
<p><a href="https://gist.github.com/novoj/6593787" target="_blank">Click here</a> to download full class.</p>
<p>Also you have to alter your web.xml configuration to map patched filter:</p>
<p>[source lang="xml"]<br />
&lt;filter&gt;<br />
   &lt;filter-name&gt;DynamicMappingFilter&lt;/filter-name&gt;<br />
   &lt;filter-class&gt;net.sourceforge.stripes.controller.HackedDynamicMappingFilter&lt;/filter-class&gt;<br />
&lt;/filter&gt;</p>
<p>....</p>
<p>&lt;filter-mapping&gt;<br />
   &lt;filter-name&gt;DynamicMappingFilter&lt;/filter-name&gt;<br />
   &lt;url-pattern&gt;/*&lt;/url-pattern&gt;<br />
   &lt;dispatcher&gt;REQUEST&lt;/dispatcher&gt;<br />
   &lt;dispatcher&gt;FORWARD&lt;/dispatcher&gt;<br />
   &lt;dispatcher&gt;INCLUDE&lt;/dispatcher&gt;<br />
&lt;/filter-mapping&gt;<br />
[/source]</p>
<p>Happy coding!</p>
