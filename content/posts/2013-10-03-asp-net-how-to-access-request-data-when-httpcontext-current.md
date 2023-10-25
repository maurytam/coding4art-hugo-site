---
title: '[ASP .NET] How to access Request data when HttpContext.Current.Request is unavailable'
author: mtammacco
type: post
date: 2013-10-03T13:13:07+00:00
url: /archive/2013/10/03/asp-net-how-to-access-request-data-when-httpcontext-current.aspx
categories:
  - ASP .NET

---
What happened if you need to access the HttpRequest object whitin the event Application_Start of an ASP .NET Web Application ?

Response: you end up with an exception.

Someone might observe that such event is not a valid place for a task like that, but sometimes things are simply different from those that appear at first sight.

So, if you want to get for example the virtual path or the physical path of a web application before the HttpRequest object is constructed  this is a valid solution:

<pre class="brush: csharp; title: ; notranslate" title="">HttpRuntime.AppDomainAppVirtualPath;
HttpRuntime.AppDomainAppPath;
</pre>

Simply use HttpRuntime instead of HttpContext.Current.Request!

<div id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:7f7c6815-5efd-4cdd-9f9e-02aaac75b619" class="wlWriterEditableSmartContent" style="float: none; margin: 0px; display: inline; padding: 0px;">
  Technorati Tags: <a href="http://technorati.com/tags/Web+development" rel="tag">Web development</a>,<a href="http://technorati.com/tags/ASP+.NET" rel="tag">ASP .NET</a>
</div>