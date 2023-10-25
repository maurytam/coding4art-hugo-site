---
title: Esecuzione side by side di applicazioni ASP .NET
author: mtammacco
type: post
date: 2006-01-29T18:49:00+00:00
url: /archive/2006/01/29/esecuzione-side-by-side-di-applicazioni-asp-net.aspx
categories:
  - Workaround

---
Con l&#8217;uscita della versione 2.0 del Framework .NET molte applicazioni ASP .NET migreranno alla nuova versione, che assicura una compatibilità al 100% all&#8217;indietro e una migliore compatibilità verso gli standard Web (vedi XHTML). Questa migrazione avverrà certamente per gradi, e ci troveremo sicuramente in situazioni in cui sullo stesso server saranno installate applicazioni ASP .NET compilate con differenti versioni del Framework. Questo non è affatto un problema grazie alla cosiddetta esecuzione side by side del codice gestito, mediante la quale differenti versioni del Framework .NET possono essere installate sullo stesse ambiente di esecuzione; quindi saranno comuni i casi in cui sulla stessa macchina gireranno applicazioni ASP .NET compilate con differenti versioni del Framework, le quali conviveranno in modo pacifico.

Ma c&#8217;è una eccezione a questa regola e riguarda le applicazioni ASP .NET che, come sappiamo, possono essere eseguite all&#8217;interno di processi distinti attraverso la creazione di uno o più application pool, configurabili attraverso il pannello di controllo di IIS.

La regola è questa: non è possibile far girare applicazioni ASP .NET compilate con differenti versioni del .NET Framework all&#8217;interno di uno stesso processo (worker process), pena un errore a run-time documentato chiaramente nell&#8217;application log. In casi del genere occorre creare differenti application pool (almeno 2, uno per il framework 2.0 e l&#8217;altro per la versione 1.1) ed associare ad ognuno le applicazioni compilate con la stessa versione.

Un&#8217;altra soluzione può essere quella di creare application pool distinti per ogni applicazione ASP .NET funzionante 