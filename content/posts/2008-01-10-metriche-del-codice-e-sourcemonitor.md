---
title: Metriche del codice e SourceMonitor
author: mtammacco
type: post
date: 2008-01-10T14:21:00+00:00
url: /archive/2008/01/10/metriche-del-codice-e-sourcemonitor.aspx
categories:
  - .NET Framework 1.0 / 1.1 / 2.0
  - .NET Framework 3.0
  - Visual Studio 2005

---
Ho provato [SourceMonitor][1], un interessante tool freeware per effettuare metriche sul codice sorgente scritto in vari linguaggi di programmazione, tra cui C#, C, C++, VB .NET, Delphi.

Attraverso una interfaccia di gestione molto semplice acquisisce una serie di informazioni, le metriche appunto, analizzando il codice sorgente di un progetto. Queste informazioni possono essere salvate in diversi momenti e nominate (checkpoints), onde poter mettere a confronto metriche di uno stesso progetto create in momenti diversi.

Analizzare le metriche del proprio codice aiuta ad evidenziare eventuali colli di bottiglia, ovvero parti dello stesso da sottoporre a code review, e a migliorare quindi la qualità del codice scritto.

Ecco un elenco delle metriche a mio avviso più importanti:

-% delle linee di codice commentate rispetto al totale delle linee di codice presenti in un file;  
-Numero delle classi, interfacce o strutture definite in un file;  
-Numero medio di metodi per classe, interfaccia o struttura;  
-Valore di complessità per tutti i metodi, ovvero numero totale dei diversi percorsi di esecuzione che ogni metodo  possiede (maggiore è questo valore, più &#8220;complesso&#8221; è il metodo). Questo valore si puo&#8217; ottenere sia per singolo  metodo, sia come media della complessità di tutti i metodi presenti.

Come detto, analizzare le metriche del codice può aiutare a scrivere codice di qualità, e quindi ad essere uno sviluppatore migliore.

 [1]: http://www.campwoodsw.com/sourcemonitor.html