---
title: Come terminare un processo corrotto in .NET
author: mtammacco
type: post
date: 2007-10-25T04:54:00+00:00
url: /archive/2007/10/25/come-terminare-un-processo-corrotto-in-net.aspx
categories:
  - .NET Framework 1.0 / 1.1 / 2.0
  - .NET Framework 3.0

---
Da .NET 2.0 in poi è possibile terminare un processo corrotto irreparabilmente attraverso il medodo Environment.Failfast(string message), il quale provvede a:

  1. Scrivere una entry nell&#8217;Application Event Log con il messaggio specificato
  2. NON eseguire alcun blocco try-finally ancora in sospeso
  3. NON esegue alcun finalizer sugli oggetti ancora in memoria
  4. Esegue un dump dell&#8217;applicazione
  5. Termina il processo

I punti 2-3 sono necessari in un contesto simile in quanto la loro esecuzione potrebbe danneggiare risorse usate dall&#8217;applicazione stessa. Tuttavia gli oggetti CriticalFinalizerObject (di cui magari parlerò in un post a parte) sono comunque eseguiti prima di terminare il processo.