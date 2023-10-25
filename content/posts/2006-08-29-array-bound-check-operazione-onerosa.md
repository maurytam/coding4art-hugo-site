---
title: 'Array bound check: operazione onerosa ?'
author: mtammacco
type: post
date: 2006-08-29T13:00:00+00:00
url: /archive/2006/08/29/array-bound-check-operazione-onerosa.aspx
categories:
  - .NET Framework 1.0 / 1.1 / 2.0

---
Questa è una domanda che mi sono posto anch&#8217;io parecchie volte: il controllo dei limiti inferiore e superiore di un array che il compilatore JIT opera durante l&#8217;esecuzione di una tipica applicazione .NET è una operazione onerosa o no, e se si di quanto ? Ci si può fare una idea abbastanza significativa leggendo questo [post][1] di [Rico Mariani][2], il quale ha effettuato dei test comparati su una applicazione .NET che utilizza il compilatore JIT tradizionale e la stessa applicazione che invece utilizza un compilatore JIT da lui stesso modificato, e precisamente senza il controllo dei limiti degli array (mscorjit.dll). Dal post si evince che il controllo sui limiti di un array non introduce un overhead significativo, anche se ritengo che la valutazione dipende dal tipo di applicazione. Comunque, aggiungo, se si programma in C# è possibile costruirsi routine di codice unsafe che permettono, tra le altre cose, di gestire array ad alte prestazioni memorizzate sullo stack e non sull&#8217;heap gestito, i cui membri sono acceduti sfruttando la semplice aritmetica dei puntatori,  senza alcun controllo di nessun tipo. Questo argomento è stato da me già trattato (spero esaurientemente :)) in un articolo pubblicato sul sito [xplayn.org][3].

 [1]: http://blogs.msdn.com/ricom/archive/2006/07/12/663642.aspx
 [2]: http://blogs.msdn.com/ricom/
 [3]: http://www.xplayn.org/cs/blogs/maurizio/