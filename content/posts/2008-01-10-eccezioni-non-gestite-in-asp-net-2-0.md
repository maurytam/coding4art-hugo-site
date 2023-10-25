---
title: Eccezioni non gestite in ASP .NET 2.0
author: mtammacco
type: post
date: 2008-01-10T18:43:00+00:00
url: /archive/2008/01/10/eccezioni-non-gestite-in-asp-net-2-0.aspx
categories:
  - .NET Framework 1.0 / 1.1 / 2.0
  - ASP .NET

---
Le eccezioni non gestite generate da una applicazione ASP .NET compilata con la versione 2.0 del .NET Framework sono trattate diversamente da quanto avveniva con le applicazioni ASP .NET compilate con la versione 1.0/1.1. Queste ultime semplicemente ignoravano le eccezioni non gestite sollevate all&#8217;esterno del contesto corrente, es. un thread diverso da quello principale, mentre le eccezioni sollevate all&#8217;interno del contesto erano trattate normalmente come qualsiasi eccezione non gestita. Con il .NET Framework 2.0 questo comportamento è cambiato: le eccezioni non gestite sollevate fuori dal contesto provocano l&#8217;immediata interruzione del worker process e conseguentemente dell&#8217;applicazione. L&#8217;unica traccia è un laconico messaggio nell&#8217;event viewer  (System Log) del tipo &#8220;DefaultAppPool terminated unexpected&#8221;, seguito da un ancor più generico messaggio nell&#8217;Application Log (Event Source: .NET Runtine 2.0 Error Reporting).

Ma questo comportamento (il default) è legato ad una precisa policy di gestione delle eccezioni non gestite e può essere modificato in 2 modi:

-Aggiungendo le seguenti righe nel file Aspnet.config:



per fare in modo che le eccezioni non gestite siano trattate come nel .NET Framework 1.0/1.1, ovvero ignorate (scelta non  
raccomandata da Microsoft)

-Creando un opportuno httpModule che si registra per l&#8217;evento AppDomain.CurrentDomain.Unhandledexception, attraverso il quale loggare i dettagli dell&#8217;eccezione  non gestita verificatasi.

Il tutto è documentato in questo [articolo][1], con un esempio di httpModule.

 [1]: http://support.microsoft.com/default.aspx?scid=kb%3bEN-US%3b911816