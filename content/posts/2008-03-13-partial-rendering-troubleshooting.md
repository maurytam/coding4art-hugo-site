---
title: Partial rendering troubleshooting
author: mtammacco
type: post
date: 2008-03-13T10:24:00+00:00
url: /archive/2008/03/13/partial-rendering-troubleshooting.aspx
categories:
  - ASP .NET
  - ASP .NET Ajax
  - Troubleshooting

---
Regola importante: l&#8217;update parziale di una pagina ASP .NET 2.0 (o successivi) attraverso l&#8217;UpdatePanel di Ajax non funziona in presenza di questo tag nel file di configurazione dell&#8217;applicazione (o nel machine.config):



Infatti, con questa impostazione la proprietà &#8220;SupportPartialRendering&#8221; dell&#8217;oggetto ScriptManager ritorna il valore false.

Il tag in questione imposta la modalità di rendering dei controlli, es.:  in modalità compatibile XHTML (mode=&#8221;Transitional&#8221; o &#8220;Strict&#8221;) oppure no (mode=&#8221;Legacy&#8221;).

In ASP .NET 1.1 i controlli subivano un rendering non XHTML compatibile, e questo comportamento è stato modificato in ASP .NET 2.0, che invece effettua il rendering XHTML compliant. Questo significa che se si migra una applicazione scritta con la versione 1.1 del .NET Framework ad una versione più recente, il wizard di migrazione imposta l&#8217;xhtml conformance mode in modalità Legacy, provocando di fatto il mancato funzionamento del partial rendering. Per risolvere il problema è sufficiente impostare il tag mode a &#8220;Transitional&#8221; (valore di default) oppure &#8220;Strict&#8221;, oppure rimuovere il nodo in modo tale da assegnargli il valore  di default, es.: