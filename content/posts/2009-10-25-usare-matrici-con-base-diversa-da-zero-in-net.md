---
title: Usare matrici con base diversa da zero in .NET
author: mtammacco
type: post
date: 2009-10-25T23:16:17+00:00
url: /archive/2009/10/25/usare-matrici-con-base-diversa-da-zero-in-net.aspx
categories:
  - Technical articles

---
I linguaggi .NET permettono di definire matrici con un limite inferiore, ovvero l&#8217;indice dell&#8217;elemento iniziale della matrice stessa, che è sempre uguale a zero. Infatti essi non permettono di gestire array con base personalizzata, ovvero diversa da zero. La seguente istruzione VB .NET dichiara una variabile matrice contenente 11 elementi di tipo stringa, il cui limite inferiore è sempre e solo zero ed il cui limite superiore è 10:

<pre class="brush: csharp; title: ; notranslate" title="">Dim s(10) As String 
</pre>

Questa caratteristica è ben nota a chi sviluppa in C++/C#, poichè in questi linguaggi un array ha sempre base zero e non è permesso definire basi definite dal programmatore. Al contrario, coloro che hanno scritto programmi utilizzando precedenti versioni del linguaggio Visual Basic, ad esempio Visual Basic 6.0, hanno invece avuto la possibilità di utilizzare matrici con limite inferiore diverso da zero, impostando questo valore nella dichiarazione dell&#8217;array. Questa non è affatto una caratteristica del VB6 a cui non si può assolutamente rinunciare, ma è semplicemente una facilitazione per chi sviluppa. Come riportato nel seguente esempio di codice VB6, indicando una matrice di 10 elementi con limite inferiore uguale a 1 e limite superiore uguale a 10, il numero degli elementi della stessa è uguale al suo limite superiore presente nella dichiarazione. Viceversa, nei linguaggi .NET una matrice con limite superiore uguale a 10 contiene in realtà 11 elementi, poichè il limite inferiore parte da zero.

<pre class="brush: csharp; title: ; notranslate" title="">Dim s(1 To 10) As String 
</pre>

Tuttavia, utilizzare matrici con base personalizzata è una tecnica che potrebbe compromettere l&#8217;affidabilità di un&#8217;applicazione generando errori anche piuttosto difficili da individuare, soprattutto quando alla stessa ci lavora un team di sviluppo composto da più programmatori. Il CLS (Common Language Specification), ovvero le specifiche tecniche a cui devono obbligatoriamente conformarsi tutti i linguaggi .NET, stabiliscono che una matrice può avere solo un limite inferiore pari a zero, e questo chiaramente per non compromettere l&#8217;interoperabilità tra i vari linguaggi. Nonostante le specifiche del CLS, la classe System.Array propria del .NET Framework permette al programmatore di definire un limite inferiore personalizzato per le matrici, e quindi di creare codice non compatibile con il CLS stesso. System.Array costituisce la classe di base utilizzata dai vari linguaggi del .NET Framework per fornire l&#8217;implementazione delle matrici utilizzando i costrutti che il linguaggio specifico mette a disposizione. Essa espone metodi shared che consentono di creare un array di elementi e di gestire l&#8217;assegnazione dei valori e la lettura degli stessi. Questo approccio richiede la scrittura di codice leggermente più prolisso, ma consente una maggiore flessibilità nell&#8217;uso degli array, come appunto creare una matrice con una base diversa da zero. Occorre sempre ricordare però che quest&#8217;approccio genera codice non compatibile con le specifiche CLS, e quindi un componente contenente codice di questo tipo potrebbe non essere utilizzato da codice che invece utilizza la sintassi dei linguaggi .NET per creare e gestire gli array. Per ottenere questo risultato è necessario innanzitutto dichiarare una variabile di tipo System.Array, come nel seguente esempio:

<pre class="brush: csharp; title: ; notranslate" title="">Dim Arr As System.Array 
</pre>

A questo punto è possibile creare una istanza della classe System.Array utilizzando il metodo shared Createnstance. Questo metodo ha una versione di overloading che permette di creare array anche multidimensionali passando 3 parametri, e precisamente un riferimento al tipo di oggetto che dovrà essere contenuto in ogni elemento dell&#8217;array, un intero che specifica le dimensioni dell&#8217;array da creare, ed ancora un intero che indica il limite inferiore dell&#8217;array stesso. Gli ultimi 2 parametri sono array monodimensionali, e ciò significa in pratica che è possibile creare una istanza di un array multidimensionale, ed indicare per ognuna delle sue dimensioni sia la lunghezza che il limite inferiore. Il seguente esempio crea un array di stringhe monodimensionale la cui lunghezza è uguale a 10 ed il cui limite inferiore è uguale a 2:

<pre class="brush: csharp; title: ; notranslate" title="">Dim Lengths as Integer() = {10} 
Dim LowerBounds as Integer() = {2} 
Arr=Array.CreateInstance(GetType(String),Lengths,LowerBounds) 
</pre>

Dopo aver creato una istanza di un array è possibile popolarlo con dati e in seguito leggerli. Per far questo occorre utilizzare rispettivamente i metodi di istanza SetValue e GetValue della classe System.Array. Il seguente esempio mostra come utilizzarli effettuando un ciclo sull&#8217;array appena creato dall&#8217;indice zero fino al suo limite superiore. Poichè l&#8217;array è stato creato con indice inferiore uguale a 2 e non zero, i primi due cicli generano una eccezione di tipo IndexOutOfRangeException, dimostrando di fatto che il .NET Framework supporta array con base personalizzata, al contrario dei suoi linguaggi di programmazione.

<pre class="brush: csharp; title: ; notranslate" title="">Dim I as Integer 
 For I = 0 To Arr.GetUpperBound(0) 
 Try 
     Arr.SetValue("Stringa alla posizione " & CStr(I), I) 
     System.Console.WriteLine(Arr.GetValue(I)) 
     Catch ex As IndexOutOfRangeException 
         System.Console.WriteLine(ex.Message) 
End Try 
Next 
</pre>

Inoltre, se si invoca il metodo System.Array.GetLowerBound(0), il quale ritorna il limite inferiore della dimensione dell&#8217;array specificata come parametro, si otterrà il valore 2, che corrisponde al limite inferiore personalizzato impostato come parametro del metodo CreateInstance, come nel seguente frammento di codice:

<pre class="brush: csharp; title: ; notranslate" title="">System.Console.Writeline(Arr.GetLowerBound(0)) 
</pre>

La classe System.Array è dichiarata utilizzando la parola chiave MustInherit. Questo potrebbe far pensare che è possibile creare una propria classe che eredita da System.Array, e che gestisce funzionalità aggiuntive o ridefinisce i membri della classe base. Sfortunatamente se si tenta di ereditare una propria classe da System.Array si ottiene un errore di compilazione il cui messaggio è &#8220;Non è consentito ereditare da System.Array&#8221;, poiché solo i linguaggi di programmazione, e quindi i compilatori, possono ereditare da questa classe per fornire i vari costrutti di gestione.