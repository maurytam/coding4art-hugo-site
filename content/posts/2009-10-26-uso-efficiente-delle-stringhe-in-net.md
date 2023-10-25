---
title: Uso efficiente delle stringhe in .NET
author: mtammacco
type: post
date: 2009-10-26T00:00:01+00:00
url: /archive/2009/10/26/uso-efficiente-delle-stringhe-in-net.aspx
categories:
  - Technical articles

---
L&#8217;architettura Microsoft .NET Framework considera una stringa come un &#8220;oggetto immutabile&#8221;. Ciò significa che una volta assegnato un valore la stessa non potrà mai più mutare il suo contenuto. Questo comporta che qualsiasi manipolazione effettuata sul contenuto di una stringa una volta che è stata creata produrrà sempre una nuova stringa, ovvero la stringa originaria risulterà raggiungibile dal successivo garbage collector, e una nuova stringa sarà creata e conterrà il risultato della manipolazione. Il seguente pezzo di codice:

**C#**

<pre class="brush: csharp; title: ; notranslate" title="">string s="SONO UNA STRINGA"; s=s.ToLower(); 
</pre>

a) crea una stringa; b) la manipola trasformando tutti i caratteri in essa contenuti in minuscolo; c) assegna il risultato alla medesima variabile. La variabile &#8220;s&#8221; dopo la manipolazione punterà ad un indirizzo diverso rispetto a quello puntato al momento della creazione e dell&#8217;inizializzazione del valore. In pratica conterrà un&#8217;altro oggetto rispetto a quello originario, appunto perchè l&#8217;immutabilità delle stringhe comporta che una volta creato ed inizializzato un oggetto, lo stesso non potrà più mutare per il restante tempo in cui rimarrà in vita. Questa caratteristica presenta vantaggi e svantaggi, ma nel complesso offre un accettabile compromesso per quanto concerne l&#8217;efficienza dell&#8217;utilizzo della memoria e le prestazioni che ne derivano. Il vantaggio principale dell&#8217;immutabilità di una stringa consiste nell&#8217;ottimizzazione di operazioni &#8220;time-consuming&#8221; come la copia, soprattutto nel caso di stringhe grandi. Infatti, poichè è certo che il contenuto di una stringa non muterà mai, una copia del suo contenuto si traduce in una semplice copia dell&#8217;indirizzo di memoria a cui essa punta, operazione molto più veloce ed efficiente della copia dell&#8217;intero contenuto. Tuttavia, un uso intenso di operazioni di manipolazione di stringhe comporta a lungo andare un degrado delle prestazioni, a causa delle continue operazioni di allocazione e deallocazione di aree di memoria dovuto appunto alla immutabilità della stringhe. Per attenuare questo possibile degrado di prestazioni il .NET Framework mette a disposizione il cosiddetto &#8220;intern pool&#8221;, ovvero un buffer di memoria in cui è possibile memorizzare stringhe di uso frequente, il cui ciclo di vita coincide con quello dell&#8217;intera applicazione. In questo modo le stringhe memorizzate, sono sempre disponibili e non sono mai raggiunte dal garbage collector. Il metodo statico Intern della classe System.String ricerca e memorizza una stringa nel pool in un&#8217; unica operazione. Infatti esso accetta un parametro di tipo stringa che rappresenta la stringa da ricercare; se è presente nel pool il metodo restituisce un riferimento ad essa; se non presente viene aggiunta una nuova stringa e restituito il riferimento, come da esempio:

**C#**

<pre class="brush: csharp; title: ; notranslate" title="">string s=System.String.Intern("una stringa"); 
</pre>

Inoltre, operazioni comunissime come la concatenazione producono sempre una stringa temporanea che contiene il risultato della elaborazione che sarà successivamente assegnato alla stringa di risultato. Il seguente semplicissimo codice:

**C#**

<pre class="brush: csharp; title: ; notranslate" title="">string str="sono una"; string str2=" stringa"; str=str+str2;
</pre>

Genera una stringa temporanea che conterrà il risultato della concatenazione che sarà assegnato ad un oggetto diverso da quello puntato dalla variabile &#8220;str&#8221;. Questa operazione di concatenazione, che coinvolge valori non letterali è eseguita a run-time, a differenza della concatenazione di valori letterali eseguita invece durante la compilazione. Per ridurre l&#8217;impatto della immutabilità delle stringhe su applicazioni che effettuano parecchie concatenazioni, soprattutto con stringhe abbastanza grandi, è possibile utilizzare l&#8217;oggetto StringBuilder, una sorta di buffer preallocato che può essere usato per contenere stringhe concatenate senza la necessità di ulteriori allocazioni di memoria. Una versione di overload del costruttore dell&#8217;oggetto StringBuilder accetta un valore intero indicante l&#8217;ampiezza della memoria preallocata, il cui valore di default è pari a 16. Fino all&#8217;ampiezza massima del buffer preallocato è possibile concatenare stringhe senza ulteriori allocazioni. Oltre questo valore viene allocata nuova memoria, la cui capacità è il doppio dell&#8217;ampiezza del vecchio buffer; quest&#8217;ultimo è copiato nel nuovo buffer e risulta raggiungibile da una operazione di garbage collection. Infine, le seguenti tecniche possono ridurre la possibilità di scrivere codice inefficiente durante la concetenazione di stringhe: -usare il metodo String.Concat per concatenare una espressione stringa. L&#8217;utilizzo di questo metodo non genera una o più stringhe temporanee come invece accade se si usa l&#8217;operatore &#8220;+&#8221;; -usare l&#8217;operatore &#8220;+&#8221; per concatenare stringhe che contengono valori letterali; -usare l&#8217;oggetto StringBuilder per concatenare stringhe durante operazioni in cui il numero di concatenazioni non è noto a priori, esempio durante un loop.