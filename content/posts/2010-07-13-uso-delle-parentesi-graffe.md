---
title: Uso delle parentesi graffe
author: mtammacco
type: post
date: 2010-07-13T15:15:00+00:00
url: /archive/2010/07/13/uso-delle-parentesi-graffe.aspx
categories:
  - Design Guidelines
  - Design patterns

---
Sono sempre stato piuttosto &#8220;maniacale&#8221; nella scrittura di codice, circa il rispetto delle guidelines e circa uno stile di codifica che aiuti a migliorare la leggibilità dello stesso, e la sua manutenibilità.

Ho sempre sostenuto che il pezzo di codice scritto stilisticamente bene è quello che si &#8220;autodocumenta&#8221; semplicemente solo leggendolo.

La leggibilità aumenta, a mio parere, anche con opportuni accorgimenti o tecniche, non sempre utilizzati da tutti, anzi spesso ci sono pareri discordanti sull&#8217;effettiva utilità di alcune modalità di scrittura.

Mi riferisco, ad esempio, all&#8217;utilizzo delle parentesi graffe in alcuni casi particolari dove possono essere evitate (ovviamente il contesto è quello di applicazione scritta in C#, linguaggio principe nel mondo .Net).

A mio avviso, la leggibilità beneficia del fatto di scrivere qualcosa del genere:

<pre class="brush: csharp; title: ; notranslate" title="">if (condizione)
    a = 1;
</pre>

rispetto a questo codice:

<pre class="brush: csharp; title: ; notranslate" title="">if (condizione)
   {
     a = 1;
   }
</pre>

Quando mi ritrovo a svolgere code review oppure solo a guardare codice scritto da altri, la tentazione di eliminare le graffe è troppo forte, e, quando posso, finisco per toglierle.

La stessa tecnica la applico al _ciclo for_, ovviamente anche in questo caso l’istruzione da eseguire deve essere una sola.

Circa le if, sarebbe addirittura più valida l&#8217;idea di toglierle proprio, in perfetta aderenza ai principi della campagna [anti-if][1], a cui ho aderito con entusiasmo, anche se qui il contesto è differente poichè le &#8220;if&#8221; andrebbero usate con parsimonia o evitate del tutto quando particolarmente annidate e ripeture (così come l&#8217;istruzione &#8220;switch&#8221;),  sostituendole con una applicazione più rigorosa dei principi della programmazione ad oggetti, polimorfismo ed ereditarietà in primis.

 [1]: http://www.antiifcampaign.com/