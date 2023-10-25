---
title: Messaggio di errore e/o eccezione in applicatione ASP .NET in configurazione application pool multiplo
author: mtammacco
type: post
date: 2006-01-29T16:40:00+00:00
url: /archive/2006/01/29/messaggio-di-errore-eo-eccezione-in-applicatione-asp-net-in.aspx
categories:
  - Workaround

---
Se si ospitano più applicazioni web ASP .NET in application pool distinti su macchine multiprocessore dotati di SO Windows 2003 si potrebbe andare incontro ad un lento degrado delle prestazioni fino ad ottenere: 

a) OutOfMemoryException 

b) Classico messaggio d&#8217;errore &#8220;Server Application Unavailable&#8221;

Questo comportamento è causato dal funzionamento del meccanismo del garbage collector su sistemi multiprocessore. Su tali sistemi il GC è attivo in modalità Server; questa modalità permette di aumentare le sue prestazioni attraverso la creazione di un heap distinto per ogni processore presente, caratteristica che in presenza di vari worker process porta ad un consumo eccessivo di memoria e da qui ai messaggi di errore menzionati. Questo indesiderato comportamento delle applicazioni ASP .NET è indipendente dalla versione del .NET Framework utilizzata, e si verifica su tutte le versioni di Windows 2003 con IIS 6.0 in modalità nativa con multiple appication pool configurate.

Per ovviare a tale inconveniente occorre forzare l&#8217;utilizzo della modalità di funzionamernto &#8220;Workstation&#8221; del GC, modalità che crea sempre un solo heap e quindi non causa un eccessivo consumo di memoria anche in presenza di application pool distinti.

Per abilitare questa modalità occorre modificare il file aspnet.config, raggiungibile nella directory della specifica versione del Framework che si sta utilizzando nel percorso WIndows\Microsoft.NET\Framework, aggiungendo la seguente riga:

**<gcServer enabled=&#8221;false&#8221;/>**

al nodo configuration\runtime.

Questa anomalia è documentata [qui][1]

 [1]: http://support.microsoft.com/kb/911716/en-us