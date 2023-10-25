---
title: Visualizers in Visual Studio 2005
author: mtammacco
type: post
date: 2006-03-14T11:32:00+00:00
url: /archive/2006/03/14/visualizers-in-visual-studio-2005.aspx
categories:
  - Visual Studio 2005

---
I visualizers sono una utilissima feature del debugger Visual Studio .NET 2005. Questi componenti agiscono in fase di debug di una applicazione per visualizzare una interfaccia utente creata ad hoc contenente i valori di variabili o di interi oggetti. Un visualizer riflette il particolare tipo di oggetto in fase di debug e visualizza le sue informazioni con l&#8217;interfaccia utente appropriata rispetto all&#8217;oggetto.

Ad es., il visualizer per il Dataset, già previsto in Visual Studio insieme a quelli per testo, xml e html, visualizza le informazioni di ogni singola tabella in esso contenuta attraverso una visione tabellare delle informazioni.

Un visualizer può funzionare in entrambe le direzioni, vale a dire che l&#8217;interfaccia grafica può sia visualizzare le informazioni che modificarle, reinviandole al debugger

Si possono creare custom visualizer ed utilizzarli in fase di debugging. [Questo][1] utilissimo visualizer, segnalato anche da MSDN Magazine come uno dei [10 tools][2] che ogni sviluppatore dovrebbe avere installato, permette di visualizzare le informazioni sugli oggetti inseriti nella cache di ASP .NET, comprendenti scadenza, dipendenze da file, da chiave o da tabella.

 [1]: http://blog.bretts.net/ct.ashx?id=07cd8437-862e-45c6-b24e-3a286fce1b66&url=http%3a%2f%2fblog.bretts.net%2fcontent%2fbinary%2fJohnson.Visualizers.zip
 [2]: http://msdn.microsoft.com/msdnmag/issues/05/12/VisualStudioAddins/default.aspx