---
title: 'Sottili differenze tra C# e VB .NET #Part 2#'
author: mtammacco
type: post
date: 2008-02-26T07:24:58+00:00
url: /archive/2008/02/26/sottili-differenze-tra-c-e-vb-net-part-2.aspx
categories:
  - 'C# e VB .NET in comparison'
  - Visual Studio 2005
  - Visual Studio 2008

---
Questa informazione me la annoto perchè sicuramente utile. Avevo già parlato [precedentemente][1] delle sottili e a volte subdole differenze esistenti tra il linguaggio VB .NET  e C#, differenze che possono anche riguardare il comportamento di Visual Studio, quindi non strettamente legate a costrutti di programmazione o alla semplice sintassi.

Questa differenza però mi sorprende parecchio e non riesco a comprenderne a fondo il motivo. Presto detto: se si utilizza l&#8217;incremento automatico nel numero di versione in un assembly (per intenderci quando impostiamo questa riga

<pre class="brush: csharp; title: ; notranslate" title="">[assembly: AssemblyVersion("1.0.*")]
</pre>

nel file AssemblyInfo, otteniamo un risultato differente a seconda se l&#8217;assembly è scritto in VB .NET o in C#. Se è scritto in VB .NET l&#8217;incremento automatico è operato solo alla prima build, mentre alle successive build sulla stessa istanza di Visual Studio il numero di versione resta invariato (se l&#8217;assembly viene ricompilato in una differente istanza di Visual Studio il numero di versione è incrementato).

Se, viceversa, l&#8217;assembly è scritto in C#, ogni build produce un incremento automatico del numero di versione. Appena mi è possibile proverò questa funzionalità, anche se la [documentazione][2] MSDN è abbastanza chiara.

Questo comportamento differente in funzione del linguaggio avrà anche una sua logica, ma non è sicuramente immediatamente chiara.

Inoltre, non condivido la motivazione che la documentazione MSDN produce per spiegare il tutto: poichè il numero di versione è inserito solo a titolo informativo in un assembly non firmato con uno strong name, il problema non si pone. Viceversa, se l&#8217;assembly deve essere dotato di strong name, viene sconsigliato l&#8217;uso dell&#8217;incremento automatico, in VB .NET chiaramente, perchè in C# non c&#8217;è alcuna controindicazione.

 [1]: http://xplayn.org/cs/blogs/maurizio/archive/2007/06/02/181.aspx
 [2]: http://msdn2.microsoft.com/en-us/library/ms998223.aspx