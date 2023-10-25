---
title: Rilevare codice duplicato
author: mtammacco
type: post
date: 2009-03-06T05:56:52+00:00
url: /archive/2009/03/06/rilevare-codice-duplicato.aspx
categories:
  - Design Guidelines
  - Tools
  - Visual Studio 2008

---
<a href="http://clonedetectivevs.codeplex.com/" target="_blank" rel="noopener">Clone Detective for Visual Studio</a> è una integrazione dell&#8217;ambiente Visual Studio (completamente free) in gradi di rilevare porzioni di codice duplicato tra i vari progetti che compongono una solution. Il fine è ambizioso, poichè come dice la stessa presentazione del prodotto presente su <a href="http://www.codeplex.com/" target="_blank" rel="noopener">CodePlex</a>

> _&#8220;Having duplicates can easily lead to inconsistencies and often is an indicator for poorly factored code&#8221;_

Un componente del genere può davvero essere utilissimo, anche oltre lo scopo che si prefigge. Ad esempio, conoscendo accuratamente il numero di cloni presenti all&#8217;interno di un software con parecchie linee di codice, è possibile valutarne il costo di manutenzione, ovvero il costo a cui si va incontro se si decidesse di apportarvi delle modifiche. 

Il componente si basa su <a href="http://conqat.cs.tum.edu/index.php/What_is_ConQAT%3F" target="_blank" rel="noopener">ConQAT</a> (Continuous Quality Assessment Toolkit) per rilevare le parti di codice duplicato. Questo toolkit fornisce una serie di tools e linee guida per il controllo della qualità del software