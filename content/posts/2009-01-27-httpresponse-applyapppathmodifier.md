---
title: HttpResponse.ApplyAppPathModifier
author: mtammacco
type: post
date: 2009-01-27T14:00:20+00:00
url: /archive/2009/01/27/httpresponse-applyapppathmodifier.aspx
categories:
  - ASP .NET

---
Se si usano le sessioni ASP .NET coockieless, ovvero sessioni in cui il SessionID viene inserito nell&#8217;url nella seguente forma:

> **/App/(S(avsbnbml2n1n5mi5rmfqnu65))/default.aspx**

il metodo **ApplyAppPathModifier** della classe **HttpResponse** risulta estremamente utile, poichè, passandogli come parametro stringa un path virtuale, restituisce lo stesso path con il SessiondID inserito correttamente nell&#8217;url, sollevando lo sviluppatore dalla costruzione manuale dello stesso. Ciò risulta evidente ogni qual volta è necessario utilizzare url caricati dinamicamente.