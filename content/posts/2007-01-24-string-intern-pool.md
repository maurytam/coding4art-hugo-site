---
title: String intern pool
author: mtammacco
type: post
date: 2007-01-24T19:01:00+00:00
url: /archive/2007/01/24/string-intern-pool.aspx
categories:
  - .NET Framework 1.0 / 1.1 / 2.0

---
L&#8217;Intern pool, di cui non è la <a title="" href="http://www.xplayn.org/articles/848.aspx" target="" name="" rel="noopener">prima volta</a> che ne parlo, è un hashtable mantenuto internamente dal CLR contenente stringhe generalmente usate per memorizzare valori costanti. In questo hashtable sono memorizzate le costanti stringa a livello di compilazione ed ogni stringa aggiunta esplicitamente attraverso l&#8217;utilizzo del metodo string.Intern, il quale aggiunge una stringa nell&#8217;intern pool (quindi nell&#8217;hashtable) e ne ritorna il riferimento se la stessa non è già presente, in caso contrario  ritorna sempicemente il riferimento ad essa. In questo modo è garantito che se due stringhe (o più) contengono gli stessi valori letterali sarà utilizzato (e quindi sarà presente in memoria) un unico riferimento, con evidente risparmio di risorse. Oltre a questo metodo, il metodo string.IsInterned ritorna il riferimento alla stringa nell&#8217;intern pool se presente, null in caso contrario.

L&#8217;intern pool è utile in opportuni scenari, ma ha un grosso svantaggio: poichè ogni stringa memorizzata nel pool è mantenuta all&#8217;interno di un hashtable interno del CLR, ne consegue che ogni stringa risulterà sempre raggiungibile dall&#8217;applicazione e quindi sopravviverà ad ogni garbage collector (poichè l&#8217;hashtable ne mantiene un riferimento). L&#8217;hashtable (e le stringhe in esso memorizzate) sarà distrutto e la memoria occupata reclamata solo quando il relativo appDomain (o processo) terminerà.

Come già detto, tutte le stringhe costanti sono inserite nell&#8217;intern pool automaticamente e quindi la memoria occupata non sarà reclamata fino a che il processo termina.  Questo comportamento è dimostrato dal seguente codice:

<pre class="brush: csharp; title: ; notranslate" title="">string a = “teststring”;
string b = “teststring”;
string x = string.IsInterned(a);
string y = string.IsInterned(b);
if (x != null)
    Console.WriteLine(“string a is interned”);
if (y != null)
    Console.WriteLine(“string b is interned”);
Console.WriteLine(object.ReferenceEquals(a,b));
</pre>

L&#8217;output prodotto è il seguente:

<pre class="brush: csharp; title: ; notranslate" title="">string a in interned
string b is interned
true
</pre>

Se questo comportamento non è quello desiderato è possibile utilizzare l&#8217;attributo a livello di assembly CompilationRelaxationsAttribute (namespace System.Runtime.CompilerServices), il quale permette disabilitare l&#8217;utilizzo dell&#8217;intern pool di stringhe da parte dell&#8217;assembly in cui l&#8217;attributo è definito, in questo modo:

<pre class="brush: csharp; title: ; notranslate" title="">[assembly: CompilationRelaxations(CompilationRelaxations.NoStringInterning)]
</pre>

Applicando questo attributo sarebbe lecito aspettarsi che l&#8217;intern pool di stringhe non sia più gestito. Invece non è così, nonostante la documentazione MSDN affermi il contrario. Sembra che questo attributo non abbia alcun effetto pratico se non negli assembly precompilati in codice nativo con l&#8217;utility NGEN. In altre parole, inserendo o non inserendo l&#8217;attributo, l&#8217;intern pool è comunque gestito dal CLR, a meno che non si precompili l&#8217;assembly con NGEN.

Come controprova di quanto affermato è possibile eseguire il codice sopraindicato con o senza l&#8217;attributo CompilationRelaxations. L&#8217;output sarà in ogni caso identico, e dimostrerà che le 2 stringhe sono inserite nell&#8217;intern pool.

Mi piacerebbe conoscere pareri di eventuali altri sviluppatori che hanno già riscontrato questo comportamento.