---
title: Oracle Data Provider for .NET
author: mtammacco
type: post
date: 2008-04-17T10:00:37+00:00
url: /archive/2008/04/17/oracle-data-provider-for-net.aspx
categories:
  - .NET Framework 3.0
  - ADO .NET
  - Sql Server 2005
  - Visual Studio 2005
  - Visual Studio 2008

---
Negli ultimi tempi mi è capitato spesso di lavorare su applicazioni che utilizzano Oracle come database piuttosto che Sql Server e, naturalmente, ho dovuto utilizzare nello strato di accesso ai dati le classi specifiche di Oracle, meglio note come Oracle Data Provider for .NET. Utilizzare queste classi significa avere a che fare con oggetti tipici di Oracle, es. gli Oracle data type, o i cursori utilizzati per contenere i resultset derivanti da una chiamata ad una store procedure, ecc.

Non avendo una esperienza significativa in Oracle ho sempre pensato che il supporto per .NET fosse alquanto limitato e ridotto all&#8217;essenziale,  es.  aprire una connessione ed eseguire un comando SQL che ritorna un resultset.  Ma noto con piacere che mi sbagliavo. La versione 11.1.0.6.20 dell&#8217;ODP for .NET fornisce sia una [integrazione][1] con l&#8217;ambiente Visual Studio  in versione 2005/2008, es. Server Explorer, wizards e designer, sia una integrazione con la piattaforma ASP .NET. Quest&#8217;ultima per me è la più interessante in quanto è possibile utilizzare alcuni providers  (argomento di cui ho già parlato in un mio [articolo][2] apparso sul sito dello user group [DotNetSide][3]) ed utilizzare come repository un database Oracle. Nello specifico i providers sono i seguenti:

  * Memberhip (gestione degli utenti e validazione)
  * Role (ruoli)
  * SiteMap (mappa del sito)
  * SessionState (  la Sessione di una applicazione ASP .NET )
  * Profile (profili degli utenti)
  * Web Event (informazioni circa lo &#8220;stato di salute&#8221; delle applicazione ASP .NET)
  * Web Part personalization (chi lavora con le WebParts può ora memorizzare le informazioni di personalizzazione in un db Oracle)
  * Cache Dependency

Il supporto per il Cache Dependency Provider a mio avviso è il più interessante di tutti. Ho già avuto modo di utilizzare ed apprezzare questo meccanismo (invalidazione automatica di un oggetto in cache a fronte di modifiche apportate a resultset memorizzati in un database mediante il meccanismo di notifica) su applicazioni basate su database SqlServer. Sarà sicuramente interessante e produttivo poterlo utilizzare anche in quei contesti dove il database è Oracle.

 [1]: http://www.oracle.com/technology/tech/windows/odpnet/newfeatures.html#ODT
 [2]: http://www.dotnetside.org/blogs/articoli/pages/Servizi-basati-su-Provider-Model-in-ASP.NET-2.0.aspx
 [3]: http://www.dotnetside.org/