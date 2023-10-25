---
title: 'Delete Subdirectory & AppDomain recycle'
author: mtammacco
type: post
date: 2006-10-09T10:59:00+00:00
url: /archive/2006/10/09/delete-subdirectory-amp-appdomain-recycle.aspx
categories:
  - ASP .NET

---
Tra le cause che provocano lo scaricamento immediato dell&#8217;AppDomain di una applicazione ASP .NET 2.0 è presente anche la cancellazione di una sub-directory della applicaizione principale, operata attraverso Windows Explorer. Infatti, dopo tale operazione nell&#8217;Event Viewer del server appare un messaggio di tipo informativo.

Questo comportamento è differente rispetto a ad ASP.NET 1.0/1.1, dove la stessa operazione non produceva assolutamente nulla nè l&#8217;engine veniva notificato dell&#8217;evento; quindi il contenuto della directory cancellata continuava ad essere considerato valido con il potenziale rischio di errore a run-time.

Il team di sviluppo di ASP .NET 2.0 ha considerato un bug il comportamento delle versioni precedenti (a mio avviso giustamente) ed ha modificato il comportamento come fosse un bug-fixing, cioè piuttosto di rischiare di servire una pagina non più esistente viene ora scaricato l&#8217;intero AppDomain. L&#8217;unica nota stonata è che nel messaggio scritto nell&#8217; Event Viewer l&#8217;applicazione risulta scaricata a causa di &#8220;reason unknown&#8221; che non permette di capire immediatamente la causa, invece di un bel &#8220;reason:directory xyz deleted&#8221;