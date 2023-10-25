---
title: Object Identity / Equality
author: mtammacco
type: post
date: 2010-05-04T03:03:00+00:00
url: /archive/2010/05/04/object-identity-equality.aspx
categories:
  - .NET Framework 3.5

---
E’ noto che il metodo virtuale **Equals** ereditato da ogni oggetto dalla classe **System.Object** permette di definire un criterio di uguaglianza tra due oggetti non basato esclusivamente sulla reference (ovvero 2 oggetti sono uguali se puntano alla stessa istanza di un determinato oggetto).

E’ altresì noto che ridefinendo il metodo **Equals** siamo costretti a ridefinire il metodo **GetHashCode** per far si che in presenza di 2 oggetti uguali (**Equals** che ritorna true), il metodo **GetHashCode** ritorni lo stesso valore di hash per i 2 oggetti, questo perchè l’oggetto in questione potrebbe essere usato come chiave in una collezione di tipo **HashTable** o **Dictionary<T,V>.**

L’implementazione di **GetHashCode** fornita dalla classe **System.Object** fornisce un valore di hash distinto per ogni istanza di una data classe presente in un dato **AppDomain**, e tutto ciò è in linea con l’implementazione di **Equals** fornita da **System.Object**.

Ma se per un dato oggetto volessimo forzare l’uguaglianza per riferimento ?

Non basta usare **ReferenceEquals(x, y)** perchè, come detto, alcune classi come i dizionari utilizzano il metodo **Equals** per definire l’uguaglianza tra due oggetti (che di default si traduce in “identità” di un oggetto e non in “uguaglianza”).

Dovremmo ridefinire il medoto Equals in questo modo:

<pre class="brush: csharp; title: ; notranslate" title="">public override bool Equals(object obj) 
{ 
   return System.Object.ReferenceEquals(this, obj); 
}
</pre>

ma in questo modo saremmo costratti ancha a ridefinire **GetHashCode** senza poter fornire l’implementazione standard di **System.Object**.

Questo problema si risolve utilizzando il medoto **GetHashCode**, ma quello fornito dalla classe **System.Runtime.CompilersServices.RuntimeHelpers**.

Questo metodo infatti, a dispetto del nome identito al metodo della classe **System.Object**, ritorna sempre un valore hash univoco per ogni istanza distinta di ogni oggetto in memoria, ovvero esattamente l’implementazione standard fornita da **System.Object** a prescindere se il metodo virtuale **Object.GetHashCode** sia o non sia ridefinito, ed adatta alla sola uguaglianza per riferimento.

Il tutto può essere inglobato in una classe **Comparer** apposita, in questo modo: