---
title: Implementazione esplicita di membri di interfaccia
author: mtammacco
type: post
date: 2007-10-25T10:13:00+00:00
url: /archive/2007/10/25/implementazione-esplicita-di-membri-di-interfaccia.aspx
categories:
  - .NET Framework 1.0 / 1.1 / 2.0

---
L&#8217;implementazione esplicita di una interfaccia presenta caratteristiche significative rispetto ad una implementazione per così dire non esplicita. Ad esempio, si consideri l&#8217;interfaccia:

<pre class="brush: csharp; title: ; notranslate" title="">public interface IExplicitImplementation 
{ 
   string Method1(string par); 
}
</pre>

e la seguente classe che la implementa in modo esplicito:

<pre class="brush: csharp; title: ; notranslate" title="">public class Class1 : IExplicitImplementation  
{
    string IExplicitImplementation.Method1(string par) 
    {
       return “Hello world “ + par;
    }
}
</pre>

Le caratteristiche salienti sono:

&#8211; Il client che consuma la classe Class1 utilizzando una istanza di quest&#8217;ultima è impossibilitato a richiamare il metodo Method1 in quanto quest&#8217;ultimo NON fa parte dell&#8217;interfaccia pubblica della classe (non è visibile con l&#8217;intellisense ed il tentativo di richiamare comunque il metodo genera un errore di compilazione).

Questo codice genera un errore di compilazione:

<pre class="brush: csharp; title: ; notranslate" title="">Class1  cl1 = new Class1();
cl1.Method1();
</pre>

&#8211; Il client che consuma la classe Class1 può invocare il metodo Method1 solo attraverso una istanza dell&#8217;interfaccia IExplicitImplementation che la classe stessa implementa esplicitamente. Vale a dire:

<pre class="brush: csharp; title: ; notranslate" title="">ExplicitImplementation i = new Class1();
Console.WriteLine( i.Method1(“Maurizio”));
</pre>

Quindi un metodo che implementa esplicitamente una interfaccia è, per così dire, privato e pubblico nello stesso tempo. E&#8217; privato perchè non compare nell&#8217;interfaccia pubblica della classe e non può essere richiamato attraverso una  istanza della classe stessa; è pubblico perchè può comunque essere richiamato utilizzando una istanza dell&#8217;interfaccia.

&#8211; Un metodo che implementa esplicitamente un membro di una interfaccia non può contenere alcun modificatore di accesso, nè i modificatori static, abstract, override e virtual. L&#8217;ultima caratteristica determina anche l&#8217;impossibilità di effettuare l&#8217;override di una implementazione esplicita di un membro di una interfaccia. Questo ostacolo è comunque raggirabile dichiarando un altro metodo virtuale (e quindi ridefinibile) e richiamando quest&#8217;ultimo metodo nel codice che implementa esplicitamente un membro di una interfaccia.