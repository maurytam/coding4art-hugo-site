---
title: Pluralisation services in .Net Framework
author: mtammacco
type: post
date: 2013-10-07T14:12:04+00:00
url: /archive/2013/10/07/pluralisation-services-in-net-framework.aspx
categories:
  - .NET Framework 4.0

---
Starting from .Net Framework version 4.0 developers have available a new service for converting a single word from singular to plural form, or from plural to singular form.

I’m talking about the class **PluralizationService** contained in namespace **System.Data.Entity.Design.PluralizationServices** in assembly **System.Data.Entity.Design**.

it’s very simple to use it:

<pre class="brush: csharp; title: ; notranslate" title="">string plural = System.Data.Entity.Design.PluralizationServices
        .PluralizationService.CreateService(new System.Globalization.CultureInfo("en-US"))
        .Pluralize(singular);
// returns "dresses";
</pre>

or

<pre class="brush: csharp; title: ; notranslate" title="">string singular = "woman";
string plural = System.Data.Entity.Design.PluralizationServices
         .PluralizationService.CreateService(new System.Globalization.CultureInfo("en-US"))
         .Pluralize(singular);
// returns "women";
</pre>

I don’t know how reliable a translation service inside a framework can be, but it’s use can be very useful.

Be careful because the only supported culture is “**English**” (so far). Then if you call the service with another culture, i.e. Italian (it-IT), you end up with a **NotImplementedException**, as shown here:

Technorati Tags: <a href="http://technorati.com/tags/Pluralization+services" rel="tag">Pluralization services</a>,<a href="http://technorati.com/tags/.Net+Framework+4.5" rel="tag">.Net Framework 4.5</a>