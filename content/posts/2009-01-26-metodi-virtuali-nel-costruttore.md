---
title: Metodi virtuali nel costruttore
author: mtammacco
type: post
date: 2009-01-26T14:33:24+00:00
url: /archive/2009/01/26/metodi-virtuali-nel-costruttore.aspx
categories:
  - Design Guidelines

---
Tra le guidelines da seguire circa la scrittura del costruttore di una classe questa assume una certa importanza:

**Evitare di richiamare all&#8217;interno di un costruttore un metodo virtuale.**

Questa guidelines è dovuta al fatto che in presenza di un metodo che ridefinisce un metodo virtuale (ne fa l&#8217;override insomma), viene richiamato sempre il metodo esposto dalla classe derivata, ovvero il metodo più specifico della implementazione, a prescindere se il costruttore della classe che espone il metodo derivato sia stato richiamato.  L&#8217;esempio sotto, tratto dalla documentazione MSDN, chiarisce bene questo concetto.

La creazione della classe **DerivedFromBad**, cioè il richiamo del suo costruttore, provoca la chiamata immediata  al costruttore della sua classe di base, ovvero **BadBaseClass**, il quale prima inizializza una variabile (state) e poi richiama il metodo virtuale **SetState**. Peccato che poiche l&#8217;oggetto che si sta cercando di costruire (**DerivedFromBad**) ridefinisce il metodo **SetState**, all&#8217;interno del costruttore della classe **BaseClass** il metodo effettivamente chiamato è l&#8217;implementazione fornita dalla classe **DerivedFromBad**, e non quella della classe base **BadBaseClass**. L&#8217;esecuzione  del metodo ridefinito **SetState** avviene a prescindere se il costruttore della classe derivata sia o no stato richiamato. In questo caso, poiche non  viene richiamato, l&#8217;inizializzazione della variabile state non  avviene ed il suo contenuto resta fermo a quello impostato dalla classe base, ovvero &#8220;**BadBaseClass**&#8220;.

<pre class="brush: csharp; title: ; notranslate" title="">public class tester
 {
     public static void Main()
     {
         DerivedFromBad b = new DerivedFromBad();
     }
 }
      
 public class BadBaseClass
 {
      protected string state;
      public BadBaseClass()
      {
          state = "BadBaseClass";
          SetState();
      }
      public virtual void SetState()
      {
 
      }
 }
   
 public class DerivedFromBad : BadBaseClass
 {
      public DerivedFromBad()
      {
        state = "DerivedFromBad ";
      }
      public override void SetState()
      {
        Console.WriteLine(state);
      }
 }  
</pre>