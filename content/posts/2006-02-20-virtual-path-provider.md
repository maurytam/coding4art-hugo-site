---
title: Virtual Path Provider
author: mtammacco
type: post
date: 2006-02-20T18:02:00+00:00
url: /archive/2006/02/20/virtual-path-provider.aspx
categories:
  - ASP .NET

---
Una tra le feature più innovative di ASP .NET 2.0 è il cosiddetto Virtual Path Provider. Devo dire però che, dopo aver approfondito l&#8217;argomento grazie a questo [post][1] di [Dino Esposito][2] e da lì al link relativo all&#8217;[articolo][3] su MSDN, non riesco ancora a trovare un campo di applicazione &#8220;logico&#8221; per questa nuova funzionalità, almeno in ambienti di produzione ad alta disponibilità. Attraverso questa feature si avrà la possibilità di astrarre la risorsa fisica (file, directory) che viene inglobata nella richiesta di una pagina ASP. NET. Questa risorsa fisica in ASP .NET 1.1 deve obbligatoriamente trovarsi sul file system e da nessun&#8217;altra parte. In ASP .NET 2.0 questo non è più vero, nel senso che ogni risorsa fisica si troverà di default sul file system, a meno che non venga implementato un Virtual Path Provider personalizzato che a fronte di una richiesta di risorsa effettui un mapping della stessa su un diverso repository, es. database, file ZIP. ecc. 

Insomma, potremo creare un intero sito web senza alcun file aspx presente su disco (a parte il global.asax). Sono curioso di capire quanto questa innovazione potrà davvero essere utile in scenari già di per sè complessi, quanto potrà incidere sulle prestazioni in generale e che impatto avrà su attività comuni quali il deployment e l&#8217;aggiornamento di un sito web.

Sono graditi eventuali feedback di coloro che avessero già avuto modo di implementare questa funzionalità in ambiente di produzione.

 [1]: http://weblogs.asp.net/despos/archive/2006/02/09/437821.aspx
 [2]: http://weblogs.asp.net/despos
 [3]: http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnaspp/html/vpp_vga.asp