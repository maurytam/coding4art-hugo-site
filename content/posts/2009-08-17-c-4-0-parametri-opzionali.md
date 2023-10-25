---
title: 'C# 4.0 – Parametri opzionali'
author: mtammacco
type: post
date: 2009-08-17T08:27:25+00:00
url: /archive/2009/08/17/c-4-0-parametri-opzionali.aspx
categories:
  - 'C# 4.0'

---
Leggo che tra le nuove feature di C# 4.0 c&#8217;è la possibilità di indicare come opzionali i parametri di un metodo o di un costruttore, in tal caso il parametro viene inizializzato con un valore di default fornito dal programmatore.

Una cosa di questo tipo:

<pre class="brush: csharp; title: ; notranslate" title="">public Person(string firstName, string lastName, string city = "")
{    
        //
}
</pre>

che può essere istanziata in entrambi le modalità:

<pre class="brush: csharp; title: ; notranslate" title="">Person p = new Person("Maurizio", "Tammacco");
Person p1 = new Person("Maurizio", "Tammacco", "Bari");
</pre>

Nel primo esempio, poichè il parametro &#8220;City&#8221; è opzionale, viene automaticamente assegnato il valore di default, ovvero stringa vuota in questo caso.

Sinceramente questa nuova funzionalità non mi entusiasma per niente, anzi la ritengo quasi inutile visto che comunque una funzionalità analoga è possibile ottenerla con le &#8220;Automatic properties&#8221;, ovvero proprietà pubbliche inizializzabili nella stessa istruzione che crea l&#8217;istanza di un oggetto, anche se questa funzionalità riguarda comunque un membro definito come proprietà.

I parametri opzionali sono da sempre presenti in Visual Basic, sin dalla versione 6 e poi anche nelle varie versioni .NET. Questo comportava che, in caso di interoperabilità tra i due linguaggi, il codice C# che richiamava un metodo scritto in VB .NET con parametri opzionali era costretto a passargli comunque tutti i parametri, opzionali e non;  la stessa cosa accadeva nell&#8217;utilizzo della COM Interop da C#. Adesso non sarà più necessario passare i parametri opzionali, ma, ripeto, a mio avviso l&#8217;utilità di questa funzionalità è discutibile, e riguarda unicamente una più stretta compatibilità tra i due linguaggi più usati nel mondo .NET.