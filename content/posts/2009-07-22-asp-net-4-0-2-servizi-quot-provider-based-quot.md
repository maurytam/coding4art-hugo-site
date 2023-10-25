---
title: 'ASP .NET 4.0 #2 Servizi "provider based"'
author: mtammacco
type: post
date: 2009-07-22T09:15:34+00:00
url: /archive/2009/07/22/asp-net-4-0-2-servizi-quot-provider-based-quot.aspx
categories:
  - ASP .NET 4.0

---
Proseguendo nell&#8217;analisi delle nuove feature di ASP .NET 4.0 è evidente che l&#8217;architettura a providers, di cui tempo fa ho parlato in un <a href="http://www.dotnetside.org/blogs/articoli/pages/Servizi-basati-su-Provider-Model-in-ASP.NET-2.0.aspx" target="_blank" rel="noopener">articolo</a> apparso su <a href="http://www.dotnetside.org" target="_blank" rel="noopener">DotNetSide</a>, è sempre più usata in modo intensivo per rendere quanto più modulare e personalizzabile l&#8217;application framework a disposizione.

Con la nuova versione di ASP .NET infatti questa architettura noto che sarà introdotta nei servizi di Output Caching, Browser Capabilities e Auto Start Application, almeno dalla documentazione in mio possesso.

**Output Caching**

Uno dei grossi limiti dell&#8217; output caching delle precedenti versioni di ASP .NET è la limitatà flessibilità sul repository di memorizzazione dei dati in cache (output). Questi infatti potevano essere memorizzati solo nella memoria del server e da nessun altra parte. Come è facile intuire con la nuova versione è possibile scriversi un provider personalizzato per la memorizzazione dei dati e quindi utilizzare qualsivoglia repository a disposizione (es. disco locale, disco di rete, database, ecc)

**Auto Start Application**

Se si utilizza IIS 7.5 e Windows Server 2008 R2 insieme ad ASP .NET 4.0, è possibile far in modo che una applicazione si avvii in automatico ed esegua del codice di inizializzazione. Questo scenario si applica soprattutto a quelle applicazioni che necessitano di tempi lunghi per inizializzarsi, e quindi per evitare che questo overhead ricada totalmente sulla prima richiesta è possibile eseguire questo codice allo start-up automatico, ovvero senza che ci sia una richiesta di pagina esplicita. Questo codice può essere incapsulato in una classe provider, e quindi si possono avere n provider da utilizzare all&#8217;occorrenza in base alle specifiche esigenze.

**Browser Capabilities**

Questa funzionalità nelle precedenti versioni era fruibile solo mediante la modifica di files xml (.browser), a livello di macchina o di singola applicazione. Questi files xml non sono proprio il massimo per descrivere funzionalità come quelle del browser. Ora è possibile definire proprie funzionalità a livello di browser mediante l&#8217;uso di classi &#8220;provider based&#8221;