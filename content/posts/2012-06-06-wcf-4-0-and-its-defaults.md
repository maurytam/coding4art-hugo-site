---
title: WCF 4.0 and its defaults
author: mtammacco
type: post
date: 2012-06-06T13:41:35+00:00
url: /archive/2012/06/06/wcf-4-0-and-its-defaults.aspx
categories:
  - .NET Framework 4.0
  - WCF

---
The default endpoint and default binding provided by WCF 4.0 are obviously great features that can save developing and testing time, but sometimes this conventional configuration don’t help in case you have some trouble with certain setting that doesn’t work.

The setting I mean in this case concern the Windows Authentication over HTTP.

To enable this setting you have only to configure the basic http bindings with a specified security mode, and then, obviously, configure the IIS authentication for the site/virtual directory that host your service to enable Windows Authentication and disable Anonymous access.

If you make this two simple change, you end up with an ASP .Net error page which says this:

**“Security settings for this service require Anonymous Authentication, but it is not enabled for the IIS application that hosts this service”**,

that is to say that the Windows Authentication isn’t working and the service requires Anonymous Authentication that is not enabled and then here’s the error.

Why although the configuration is it not working? Because you have not specified a binding for your service, and then the default binding comes into play, and the default binding requires Anonymous Authentication, which is not enabled.

The next logical step is to provide a specific binding configuration,  which maps the binding named “BasicHttpEndpointBinding” defined early with your service.

But when you run the service the error is always the same. What’s wrong with this configuration ?

The problem here is the service name you provided. This name must match with the service name written inside the .svc file of your service. If this name doesn’t match, the explicit binding configuration doesn’t match with those provides by your service as well, and then you fall into the default binding behavior again.

Otherwise, if the service name matches everything works fine.

Moral of the story: “Pay always attention to the default values of any configuration”!

<div id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:aaf88423-1419-4446-ae10-8c68d101af21" class="wlWriterEditableSmartContent" style="margin: 0px; display: inline; float: none; padding: 0px;">
  Technorati Tags: <a href="http://technorati.com/tags/WCF" rel="tag">WCF</a>,<a href="http://technorati.com/tags/Web+Services" rel="tag">Web Services</a>,<a href="http://technorati.com/tags/Configuration" rel="tag">Configuration</a>,<a href="http://technorati.com/tags/Binding" rel="tag">Binding</a>
</div>