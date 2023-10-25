---
title: 'L&rsquo;evento Application_Start ed il suo corretto utilizzo'
author: mtammacco
type: post
date: 2010-02-24T04:29:00+00:00
url: /archive/2010/02/24/lrsquoevento-application_start-ed-il-suo-corretto-utilizzo.aspx
categories:
  - ASP .NET

---
**Regola importante in una applicazione ASP .NET:** 

durante l&#8217;evento Application\_Start dovrebbero essere assegnate solo variabili statiche e mai variabili d&#8217;istanza; ciò è dovuto al fatto che questo evento viene sollevato solo 1 volta durante il ciclo di vita dell&#8217;applicazione e, insieme all&#8217;evento Application\_End, non è legato alla istanza in esecuzione della classe HttpApplication ma, al contrario, entrambi sono considerati eventi speciali.

Infatti, ogni applicazione ASP .NET in esecuzione è associata ad un oggetto HttpApplication, capace di gestire una richiesta alla volta. Durante il suo ciclo di vita possono essere create più istanze della classe HttpApplication, ognuna delle quali in ottica di ottimizzazione delle performance può essere riciclata. Tuttavia, i due eventi sopra citati non vengono sollevati per ogni istanza creata di HttpApplication ma, come detto, solo 1 volta durante la vita di una applicazione.

Un membro d&#8217;istanza creato in Application_Start quindi sarebbe visibile solo per la prima istanza creata di HttpApplication e non anche per le successive.

Viceversa, l&#8217;evento sollevato per ogni istanza creata di HttpApplication è invece Application_Init.