---
title: 'Inconsistenza operatori di confronto dei Nullable Types in C#'
author: mtammacco
type: post
date: 2007-10-14T14:23:00+00:00
url: /archive/2007/10/14/inconsistenza-operatori-di-confronto-dei-nullable-types-in-c.aspx
categories:
  - 'C# e VB .NET in comparison'

---
Il linguaggio C# offre un supporto decisamente migliore dei Nullable Types rispetto a VB .NET. Nonostante ciò, utilizzando gli operatori di confronto su un tipo Nullable, es. un intero, il risultato è a dir poco strano e può dar luogo a bug piuttosto subdoli.  
Infatti, eseguendo il seguente codice:

<pre class="brush: csharp; title: ; notranslate" title="">int? a;
int? b;
a=null;
b=null;
Debug.WriteLine(a == b);
Debug.WriteLine(a != b);
</pre>

l&#8217;uguaglianza dei due tipi nullable con entrambe le variabili impostate a null dà come risultato &#8220;true&#8221;, mentre  l&#8217;operatore  di disuguaglianza  sulle stesse variabili produce come risultato &#8220;false&#8221;. Sin qui il comportamento è coerente.

Questo codice invece:



produce in entrambi i casi un risultato pari a "false", risultato a prima vista strano, oserei quasi dire illogico.

In sostanza:

  * "a" è uguale a "b", ma "a" non è maggiore "**oppure**" uguale a "b".
  * "a" è uguale a "b", ma "a" non è minore "**oppure**" uguale a "b"

I commenti sono aperti.