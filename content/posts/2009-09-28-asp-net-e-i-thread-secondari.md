---
title: ASP .Net e i thread secondari
author: mtammacco
type: post
date: 2009-09-28T06:24:09+00:00
url: /archive/2009/09/28/asp-net-e-i-thread-secondari.aspx
categories:
  - ASP .NET
  - Tips and tricks

---
Interessantissimo <a href="http://blogs.msdn.com/itasupport/archive/2009/09/27/sempre-chiamare-il-metodo-dispose.aspx" target="_blank" rel="noopener">post</a> di <a href="http://blogs.msdn.com/itasupport/archive/tags/Stefano+Pronti/default.aspx" target="_blank" rel="noopener">Stefano Pronti</a> del nuovo <a href="http://blogs.msdn.com/itasupport/" target="_blank" rel="noopener">blog MSDN di Supporto Tecnico agli Sviluppatori</a>, che spiega le disastrose conseguenze di non richiamare il metodo Dispose su risorse unmanaged, utilizzate all&#8217;interno di una web application.

Per farla breve, le risorse unmanaged utilizzavano un thread secondario rispetto a quello che prende in carico la web request, ed in questo thread secondario veniva sollevata una eccezione non gestita durante la fase di finalizzazione del garbage collector, che, come è noto, viene eseguito in un thread diverso.

In questo caso il comportamento di ASP .NET a partire dalla versione 2.0 è quello di interrompere immediatamente il processo in esecuzione, con conseguenze facilmente immaginabili.

Ho già parlato <a href="http://xplayn.org/cs/blogs/maurizio/archive/2008/01/10/311.aspx" target="_blank" rel="noopener">qui</a> di questo comportamento di ASP .NET e di come sia possibile utilizzare la modalità pre-versione 2.0 di gestione delle eccezioni non gestite sollevate all&#8217;interno di thread diversi.

Anche a me è capitato di dover &#8220;impazzire&#8221; con una applicazione in produzione, abbastanza vasta, che soffriva di frequenti ed improvvise cadute della sessione corrente, con enorme disagio degli utenti.

Nel caso specifico non è stato indispensabile attaccare un debugger per ottenere il dump della memoria al momento dell&#8217;eccezione, è bastato debuggare il codice, che non conoscevo neanche bene, e scoprire che venivano creati thread aggiuntivi (!?) il cui codice, in particolari circostanze, sollevava l&#8217;eccezione fatale che provocava il riavvio del worker process.