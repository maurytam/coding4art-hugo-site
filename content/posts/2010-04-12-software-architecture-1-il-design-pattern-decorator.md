---
title: 'Software Architecture #1 Il design pattern Decorator'
author: mtammacco
type: post
date: 2010-04-12T04:40:00+00:00
url: /archive/2010/04/12/software-architecture-1-il-design-pattern-decorator.aspx
categories:
  - Architecture
  - Design patterns

---
Il pattern “Decorator” appartiene alla famiglia dei design pattern della GoF (Gang of Four), ed è classificato come pattern strutturale. E’ un pattern molto semplice da usare, che permette di aggiungere dei comportamenti personalizzati, e quindi delle responsabilità, ad una certa classe senza per questo utilizzare tecniche di subclassing.

Immaginiamo di avere un componente per il log delle informazioni. Esso invoca un servizio di logging e rispetta questo contratto definito mediante una semplice interfaccia:

<pre class="brush: csharp; title: ; notranslate" title="">public interface ILogger
{
    void Write(Exception ex);

}  
public class Logger : ILogger
{
   public void Write(Exception ex)
   {
      Console.WriteLine(ex.Message);
   }
}
</pre>

Abbiamo la necessità di aggiungere una informazione aggiuntiva al messaggio di log, ovvero la data odierna. Questo significa aggiungere responsabilità alla classe, ma per ottenere questo non intendiamo nè modificare la classe originaria, nè usare il subclassing. Il design pattern “decorator” permette di ottenere questo risultato in un modo molto semplice:

<pre class="brush: csharp; title: ; notranslate" title="">public class LoggerDecorator : ILogger
{
   private ILogger loggerObj;
  
   public LoggerDecorator(ILogger logger)
   {
        loggerObj = logger;
   }

public void Write(Exception ex)
{
       Console.WriteLine(DateTime.Now.Date.ToShortDateString());
       loggerObj.Write(ex);
}
</pre>

Il “decorator” consiste in una classe che implementa la stessa interfaccia della classe originaria, e con un costruttore che accetta come parametro una istanza di quest’ultima. L’implementazione dell’interfaccia permette al “decorator” di iniettare codice aggiuntivo prima ed anche dopo l’invocazione del corrispondente metodo della classe estesa.

Esempio di utilizzo:



E’ importante notare che la classe estesa (Logger in questo caso) non sa assolutamente nulla che un’altra classe è usata come “decorator”.

Nonostante la semplicità e l’utilità di questo pattern è opportuno ricordare che con l’introduzione degli “extention methods” a partire dalla versione 3.5 del .Net Framework è possibile estendere una qualsiasi classe senza usare l’ereditarietà e con l’indubbio vantaggio di ritrovarsi gli extention methods di un tipo visibili nell’Intellisense di Visual Studio.

Esempio con l’extention method:

<pre class="brush: csharp; title: ; notranslate" title="">public static class LoggerExtention
 {
     public static void WriteData(this Logger logger)
     {
         Console.WriteLine(DateTime.Now.Date.ToShortDateString());
     }
 }
   
// Utilizzo:
Logger loggerEx = new Logger();
loggerEx.WriteData();
</pre>