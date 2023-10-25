---
title: Pinned object in .NET
author: mtammacco
type: post
date: 2009-10-25T23:54:15+00:00
url: /archive/2009/10/25/pinned-object-in-net.aspx
categories:
  - Technical articles

---
E&#8217; noto che il meccanismo del Garbage Collector del .NET Framework, a cui ho dedicato un articolo apparso sulla rivista [<u>Visual Basic Journal</u>][1], compatta l&#8217; heap dopo aver effettuato la pulizia ed il rilascio della memoria occupata dagli oggetti non più referenziati dall&#8217;applicazione. Questa compattazione dispone in modo contiguo gli oggetti ancora in vita per un più efficiente utilizzo della memoria, e chiaramente per tutti gli oggetti spostati vengono aggiornati i rispettivi puntatori a causa del nuovo indirizzo di memoria a cui punta l&#8217;oggetto; inoltre, per evitare lunghe operazioni di spostamento, gli oggetti troppo grandi (oltre 85K) non sono spostati. Quindi, a seguito di un GC, un oggetto ancora valido può puntare ad una locazione di memoria diversa rispetto alla locazione che lo stesso oggetto possedeva prima della operazione di GC. Questa situazione comporta problemi se l&#8217;oggetto in questione viene passato attraverso il suo indirizzo ad una DLL unmanaged attraverso P/Invoke. Infatti, se il GC cambiasse la locazione di memoria dell&#8217;oggetto a seguito di una compattazione dopo la chiamata alla DLL, l&#8217;indirizzo passato alla DLL non sarebbe più valido e la DLL non avrebbe alcun modo per accorgersene, con conseguenze facilmente immaginabili. Per ovviare a questo problema è possibile ricorrere alla struttura GCHandle, attraverso cui è possibile creare i cosiddetti oggetti &#8220;pinned&#8221;, ovvero oggetti non rilocabili in memoria e quindi passabili come parametro a DLL unmanaged. Tuttavia, sono gli oggetti &#8220;blittable&#8221; possono essere gestiti come pinned (un oggetto blittable è tale se la sua rappresentazione in memoria è la stessa nel codice gestito e nel codice non gestito, es. valori integer, double, ecc; non lo è in caso contrario). Questa struttura permette inoltre di conoscere l&#8217;indirizzo in cui un oggetto &#8220;pinned&#8221; è memorizzato. Se questo valore venisse passato ad un componente unmanaged, si andrebbe incontro al rischio di corruzione della memoria in quanto il componente non gestito avrebbe (teoricamente) la possibilità di scrivere nella memoria puntata dall&#8217;indirizzo passato. In questo esempio viene creato un array di interi, reso &#8220;pinned&#8221; l&#8217;oggetto corrispondente e letto il suo indirizzo di memoria. 

**C#**

<pre class="brush: csharp; title: ; notranslate" title="">int[] arrInt = new int[10]; 
arrInt[0]=1; 
arrInt[1]=2; 
arrInt[2]=3; 
System.Runtime.InteropServices.GCHandle GCH = 
System.Runtime.InteropServices.GCHandle.Alloc(
        arrInt, System.Runtime.InteropServices.GCHandleType.Pinned); 
IntPtr a = GCH.AddrOfPinnedObject();
</pre>

 [1]: http://www.infomedia.it/