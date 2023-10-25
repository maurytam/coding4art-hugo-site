---
title: Web services Contract First development
author: mtammacco
type: post
date: 2012-05-30T09:37:58+00:00
url: /archive/2012/05/30/web-services-contract-first-development.aspx
categories:
  - Open source
  - Tools
  - Web services

---
<a href="http://wscfblue.codeplex.com/" target="_blank" rel="noopener">WSCF.blue</a> is a great tool for developing web services in a Contract First mode.

Develop in such a way means that you start from a WSDL contract that describes everything is concerned with a web service, and only after that you can write code which  that contract is based on.

Working with a WSDL can be a very error-prone task because a WSDL is a XML file. The <a href="http://wscfblue.codeplex.com/" target="_blank" rel="noopener">WSCF.blue tool</a> is able (among other things) building the server code you need from that file.

But this tool is also useful in some particular scenario where you have to change the web service code that “answers” to a particular call. I will explain it better.

Imagine you have a old application using a old web service developed by a third part, and you don’t have the source code of that service. What if you have to rewrite the web service for changed requirements without affecting the application which use it by simply changing the service’s url in configuration files ?. in other words, it needs to create another web service’s implementation without changing the WSDL in any way. In this case <a href="http://wscfblue.codeplex.com/" target="_blank" rel="noopener">WSCF.blue</a> can greatly save your time recreating the server code starting from the WSDL input, and with this server code you can write the new implementation. At this point you can just change the url of the service in application which was using the old implementation.

As unit test, it is possible to add a proxy reference to the old implementation of the service. After that you can create a new instance of the service by the proxy, change the url property and invoke methods and obviously the new service’s implementation at the new url will respond.

<div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:a334e716-8650-481d-be76-aebc6593ca58" class="wlWriterEditableSmartContent">
  Technorati Tags: <a href="http://technorati.com/tags/Web+services" rel="tag">Web services</a>,<a href="http://technorati.com/tags/Contract+First" rel="tag">Contract First</a>,<a href="http://technorati.com/tags/Tools" rel="tag">Tools</a>,<a href="http://technorati.com/tags/Open+Source" rel="tag">Open Source</a>,<a href="http://technorati.com/tags/Wsdl" rel="tag">Wsdl</a>
</div>