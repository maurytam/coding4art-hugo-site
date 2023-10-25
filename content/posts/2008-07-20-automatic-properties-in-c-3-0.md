---
title: 'Automatic properties in c# 3.0'
author: mtammacco
type: post
date: 2008-07-20T15:27:31+00:00
url: /archive/2008/07/20/automatic-properties-in-c-3-0.aspx
categories:
  - .NET Framework 3.5
  - Visual Studio 2008

---
Utilizzando C# 3.0 è possibile scrivere le proprietà di una classe in modo estremamente compatto, in questo modo:

<pre class="brush: csharp; title: ; notranslate" title="">Public string Nome {get; set;}
</pre>

Questa modalità, chiamata &#8220;Automatic properties&#8221; permette quindi di omettere il riferimento al membro privato che normalmente viene &#8220;wrappato&#8221; dalla proprietà stessa.

Sarà compito del compilatore autogenerare al volo il membro privato al momento della compilazione. Questa caratteristica impone che il codice della classe non può in nessun modo accedere alla variabile privata, appunto perchè al momento della stesura del codice essa non esiste ancora in quanto sarà autogenerata in fase di compilazione. E&#8217; quindi necessario utilizzare direttamente il nome della proprietà nel codice della classe per accedere al suo contenuto e/o modificarlo.

L&#8217;impossibilità del codice ad accedere alla variabile privata è dovuta al fatto che, poichè è possibile in qualsiasi momento tornare alla dichiarazione classica della proprietà indicando esplicitamente una variabile privata, è necessario assicurare al codice la piena compatibilità tra le due modalità. In altre parole, se si trasforma una &#8220;Automatic property&#8221; in una proprietà diciamo così &#8220;classica&#8221;, il codice che la utilizza continuerà a funzionare senza problemi perchè è certo che non avrà in nessun modo potuto utilizzare la variabile privata autogenerata. Per lo stesso motivo, non è possibile indicare un solo &#8220;accessor&#8221; per la proprietà ma dovranno essere indicati obbligatoriamente entrambi (get; set;), fermo restando che è sempre possibile indicare un ambito di visibilità diverso tra i due &#8220;accessor&#8221; (es. **get;** con visibilità public e **set;** con visibilità private)