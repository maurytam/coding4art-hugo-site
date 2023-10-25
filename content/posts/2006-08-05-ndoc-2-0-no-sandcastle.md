---
title: NDOC 2.0 ? No, Sandcastle
author: mtammacco
type: post
date: 2006-08-05T14:00:00+00:00
url: /archive/2006/08/05/ndoc-2-0-no-sandcastle.aspx
categories:
  - .NET Framework 1.0 / 1.1 / 2.0

---
La versione di NDOC per il Framework 2.0 sembra che non vedrà mai la luce, almeno leggendo le ultimissime <a title="" href="http://www.charliedigital.com/PermaLink,guid,95b2ab68-ba92-413a-b758-2783cde5df9c.aspx" target="" name="" rel="noopener">notizie</a>. Peccato, ho usato NDOC su parecchi progetti e devo dire che sono sempre stato soddisfatto dei risultati raggiunti con l&#8217;utilizzo di questo tool, soprattutto quando manca il tempo per documentare un progetto usando classiche soluzioni alternative. Però potremo produrre docuntazione &#8220;MSDN like&#8221; usando Sandcastle, il tool usato internamente da Microsoft per la documentazione tecnica dei progetti che la stessa ha deciso di rendere disponibile al <a title="" href="http://www.microsoft.com/downloads/details.aspx?familyid=E82EA71D-DA89-42EE-A715-696E3A4873B2&displaylang=en" target="" name="" rel="noopener">download</a>. Si tratta di un tool che via reflection ottiene le informazioni sui vari assembly integrandole con la eventuale documentazione inserita direttamente nel codice sorgente, producendo un contenuto che, manipolato via XSL, permette di ottenere la classica documentazione style MSDN che siamo abituati a vedere ogni giorno.