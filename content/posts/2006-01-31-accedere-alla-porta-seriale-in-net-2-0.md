---
title: Accedere alla porta seriale in .NET 2.0
author: mtammacco
type: post
date: 2006-01-31T18:29:00+00:00
url: /archive/2006/01/31/accedere-alla-porta-seriale-in-net-2-0.aspx
categories:
  - .NET Framework 1.0 / 1.1 / 2.0

---
Nella versione 1.1 del .NET Framework accedere alla porta seriale per poter leggere/scrivere dei dati richiede l&#8217;uso delle API di Windows preposte allo scopo. Pertanto è necessario creare una classe wrapper che incapsula l&#8217;accesso alle API e fornisce i metodi pubblici necessari alla gestione della porta ed all&#8217;invio/ricezione delle informazioni. Nel .NET Framework 2.0 questa classe wrapper è già presente e ne viene fornito un esempio di utilizzo attraverso uno snippet code presente nell&#8217;elenco degli snippet code di Visual Studio 2005. 

Pertanto, questa operazione, prima non certamente banale, è diventata di una semplicità disarmante nel Framework .NET 2.