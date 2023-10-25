---
title: Messaggio di errore Ambiguous match found e httpParseException
author: mtammacco
type: post
date: 2008-03-17T08:58:15+00:00
url: /archive/2008/03/17/messaggio-di-errore-ambiguous-match-found-e-httpparseexception.aspx
categories:
  - ASP .NET
  - Troubleshooting
  - Visual Studio 2008

---
Scenario: web application che utilizza la versione 1.1 di ASP .NET migrata direttamente alla versione 3.5. Dopo la migrazione su una delle pagine ASPX viene sollevato una HttpParseException durante il caricamento della stessa. L&#8217;eccezione in questione, come si evince dal nome, viene generata dal runtime di ASP .NET quando il parsing di una pagina ASPX fallisce a runtime. Il messaggio di errore recita &#8220;Ambiguous match found&#8221;, e quindi non aiuta granchè. La cosa curiosa è che l&#8217;eccezione non si verifica in ambiente di sviluppo ma solo sulla versione di deploying dell&#8217;applicazione, quindi non è &#8220;debuggabile&#8221; in Visual Studio 2008 ( a meno di non effettuare un debug in remoto, cosa quasi mai possibile in ambiente di produzione) , e quindi non è di facile risoluzione.

In questi casi la prima cosa che penso è: sicuramente altri developers sparsi per il mondo hanno già sperimentato lo stesso problema, quindi  mi metto a perlustrare blogs e forum e normalmente alla fine il problema si risolve !

E così è stato anche stavolta, anche se le cause di questa eccezione possono essere diverse e quindi non esiste una soluzione universalmente applicabile.

Alcune delle cause che possono produrre una httpParseException sono, in ordine sparso:

  1. la pagina contiene un campo hidden che ha un ID con lo stesso nome di una variabile querystring usata dalla stessa pagina;
  2. la pagina ha un controllo (non ascx) inserito nel file ASPX (e quindi inserito nella partial class non visibile), e nel code-behind della stessa è dichiarato un altro controllo protected con lo stesso nome;
  3. la pagina contiene un controllo ASCX con lo stesso nome di un controllo nativo ASP .NET;

Tutte queste situazioni generano evidentemente una ambiguità dei tipi, che porta all&#8217;eccezione.

Inoltre,  effettuando un deploy del sito con l&#8217;opzione &#8220;non aggiornabile&#8221;, ovvero deselezionando l&#8217;opzione &#8220;Allow this precompiled site to be updateable&#8221;, l&#8217;eccezione dovrebbe scomparire, salvo poi approfondire le sue cause e riabilitare nel caso l&#8217;opzione.