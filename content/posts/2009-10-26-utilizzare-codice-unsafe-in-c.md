---
title: 'Utilizzare codice unsafe in C#'
author: mtammacco
type: post
date: 2009-10-26T00:32:30+00:00
url: /archive/2009/10/26/utilizzare-codice-unsafe-in-c.aspx
categories:
  - Technical articles

---
Il linguaggio C# permette di scrivere codice cosiddetto **unsafe**, cioè eseguito al di fuori del controllo del CLR (Common Language Runtime).In questo ambito il programmatore può accedere, seppure con le dovute limitazioni rispetto a linguaggi più specifici quali C/C++, direttamente alla memoria attraverso l&#8217;uso dei puntatori. Un puntatore è una particolare variabile il cui contenuto è un indirizzo di memoria. In un sistema a 32 bit quindi un puntatore occupa 4 byte.

L&#8217;utilizzo diretto della memoria offre vantaggi e svantaggi. Da un lato è possibile superare i controlli imposti dal CLR e dal compilatore C#, e questo permette di scrivere routine altamente ottimizzate e generalmente più efficienti; dall&#8217;altro canto però la programmazione **unsafe** è senz&#8217;altro più ostica e complessa della stesura di normale codice gestito, sia per la particolare sintassi a cui bisogna attenersi, sia perchè è facilissimo commettere errori che a questo livello risultano fatali per l&#8217;applicazione e per l&#8217;intero sistema.

<u>Come utilizzare il codice unsafe</u>

Prima di eseguire codice unsafe è necessario utilizzare l&#8217;omonimo modificatore, il quale può essere associato ad una intera classe, ad uno o più metodi, ad una o più variabili membro, oppure ad un singolo blocco di codice all&#8217;interno di un metodo.

Nel seguente esempio vengono mostrati tutti i possibili usi:

<pre class="brush: csharp; title: ; notranslate" title="">// Qualsiasi metodo della classe può usare i puntatori
public unsafe class MyClass {}
// I membri (tipi valore) della classe possono essere puntatori, anche con
// diversi livelli di visibilità (private, public, protected)
public class MyClass2 
{
   private unsafe float* pFloat;
   public unsafe int* px2;
   protected unsafe int* px3;

  
// Il metodo può usare i puntatori in qualsiasi punto al suo interno
public unsafe void Method1() {}
 
public void Method2() 
{
   int a=0;
   unsafe
   {
      // E' possibile usare i puntatori all'interno di questo blocco
   }
}
</pre>

Non è invece possible applicare la parola chiave **unsafe** ad una variabile privata a livello di metodo. Il seguente codice, infatti, non compilerà :

<pre class="brush: csharp; title: ; notranslate" title="">public void Method3() 
 {
   // errore di compilazione
   unsafe int* a=0;
}
</pre>

Tuttavia, pur definendo correttamente un contesto **unsafe** contenente l&#8217;opportuno modificatore, il compilatore C# genererà  comunque un errore di compilazione. Come passo ulteriore, è richiesto il parametro /unsafe da associare alla esecuzione della compilazione (comando csc.exe), oppure, se si utilizza l&#8217;ambiente Visual Studio 2003/2005, basta attivare l&#8217;opportuno check nella finestra delle proprietà  del progetto.

Un aspetto importantissimo da considerare è che in un contesto **unsafe**  è possibile utilizzare puntatori solo a tipi valore (tutti i tipi numerici primitivi, datetime e strutture), i quali sono memorizzati all&#8217;interno dello stack; non è ammesso quindi l&#8217;utilizzo di un puntatore ad un tipo riferimento (tutte le classi del .NET Framework più quelle definite dall&#8217;utente che derivano direttamente o indirettamente da System.Object, memorizzate invece nell&#8217;heap gestito). Questa limitazione è dovuta al fatto che i tipi riferimento sono appunto memorizzati in una area di memoria chiamata heap costantemente monitorata dal meccanismo del garbage collector e su cui esso agisce per liberare la memoria occupata da oggetti non più referenziati. Risulta evidente che se il programmatore avesse la possibilità  di manipolare l&#8217;indirizzo di memoria di un tipo riferimento, il garbage collector non avrebbe più la possibilità di tenerne traccia per poter rilasciare la memoria utilizzata quando il riferimento non è più puntato da nessuna variabile.

<u>Utilizzo dei puntatori in pratica.</u>

Le seguenti righe di codice dichiarano due puntatori rispettivamente ad un intero 32 bit ed ad un float:

<pre class="brush: csharp; title: ; notranslate" title="">int* pintValue;.
float* pfloatValue;
</pre>

Il seguente snippet code evidenzia invece alcune delle operazioni possibili con i puntatori:



Si dichiarano 2 puntatori ad interi (righe 1 e 2).

Si dichiara una variabile intera assegnandole il valore 20 (riga 3).

Successivamente si assegna l&#8217;indirizzo di memoria di **intValue** al puntatore **pintValue** attraverso operatore &#8220;&&#8221; (riga 4). Questo operatore permette appunto di ricavare l&#8217;indirizzo di memoria di una variabile e di convertirlo in un puntatore.

Nella riga 5 al puntatore **pintValue2** viene assegnato il contenuto del puntatore **pintValue**.

Successivamente si modifica il valore puntato dal puntatore **pintValue2** assegnandogli il valore 50 (riga 6) mediante l&#8217;operatore &#8220;*&#8221;, il quale ha l&#8217;effetto opposto rispetto all&#8217;operatore &#8220;&&#8221;, ovvero converte un puntatore verso un tipo di dato a valore.

La riga 7 stampa su console lo spazio di memoria occupato da un intero a 32 bit. Questo valore si ottiene attraverso l&#8217;operatore **sizeof** che accetta un tipo valore come parametro e restituisce la sua occupazione in memoria. Le righe 8 e 10 stampano l&#8217;indirizzo ed il valore dei 2 puntatori utilizzati in questo esempio. Per poter stampare l&#8217;indirizzo di memoria memorizzato in un puntatore è necessario prima convertire quest&#8217;ultimo in un tipo di dato numerico abbastanza ampio da poterlo rappresentare (in questo caso un intero senza segno) attraverso una operazione di cast esplicito.

L&#8217;output mostrato a video evidenzia come il primo puntatore (int\* pintValue) contenga il valore 50 (il valore assegnato al secondo puntatore int\* pintValue2). Questo risultato dimostra l&#8217;utilizzo dei puntatori come semplici indirizzi di memoria; infatti, nella riga 6 è stato effettuato un assegnamento dell&#8217;indirizzo puntato da pintValue alla variabile pintValue2, e, poichè trattasi di puntatori, ciò che è stato effettivamente assegnato non è il valore di pintValue ma l&#8217;indirizzo di memoria. Ne consegue che dopo l&#8217;istruzione visualizzata alla riga 6 entrambi i puntatori puntano alla stessa area di memoria per cui qualsiasi modifica al contenuto puntato da uno dei due si riflette anche sull&#8217;altro.

<u>Aritmetica dei puntatori</u>

Ad un puntatore è possibile sommare o sottrarre un valore intero. Tuttavia il risultato di questa operazione non è immediatamente intuitivo. Il compilatore, infatti, applica sempre la seguente formula quando esegue una operazione di somma (o sottrazione) su un puntatore:



dove **X** rappresenta un indirizzo di memoria, ovvero un puntatore, **n** un valore intero da sommare, **T** il tipo valore a cui il puntatore si riferisce.

Esempio:

dato un puntatore ad un valore double:



che punta al seguente indirizzo di memoria (valore decimale): 1201550

se sommiamo 1 a tale puntatore attraverso questa istruzione:



il risultato sarà  che il puntatore **pDouble** conterrà  l&#8217;indirizzo di memoria 1201558, ovvero all&#8217;indirizzo iniziale sono stati aggiunti 8 byte, vale a dire l&#8217;ampiezza in memoria di una variabile di tipo double.

Se avessimo aggiunto il valore intero 3, in questo modo:



l&#8217;indirizzo di memoria sarebbe cambiato in 1201574, cioè sarebbero stati aggiunti 24 byte (l&#8217;equivalente di 3 valori double) al valore iniziale.

Analogamente, in una operazione di sottrazione i bytes sarebbero sottratti dal valore iniziale.

Da ciò si evince una regola importantissima: se si effettua una operazione di somma o sottrazione su un puntatore di un certo tipo valore, il puntatore risultante punterà  ad una area di memoria contigua in funzione del numero di byte che servono a rappresentare il suddetto tipo. Questa operazione andrebbe effettuata con molta cautela, in quanto non si ha nessuna informazione circa il contenuto dell&#8217;area di memoria puntata in seguito alla operazione matematica. Non è affatto garantito, infatti, che essa non contenga alcun dato; al contrario, potrebbe contenere informazioni fondamentali per il corretto funzionamento del processo in esecuzione, ad esempio l&#8217;indirizzo di ritorno del metodo corrente. Se queste informazioni venissero sovrascritte da un puntatore sicuramente si otterrebbe un crash del sistema.

<u>Puntatori a strutture</u>

Una struttura è un tipo valore in quanto è memorizzata nello stack esattamente come i tipi numerici primitivi. Quindi è possibile definire un puntatore ad una struttura, ma essa non potrà contenere alcun tipo riferimento, esempio una stringa, in quanto ciò provocherebbe, come già menzionato, un errato funzionamento del garbage collector.

Quindi, disponendo di una struttura come da esempio:

<pre class="brush: csharp; title: ; notranslate" title="">public struct Article
{
   public int code;
   public float price;
   public short foo;
}
</pre>

è possibile utilizzare i puntatori in questo modo:



(Riga 1) E&#8217; dichiarato un puntatore ad una struttura contenente un valore intero a 32 bit, un float ed un intero a 16 bit (short).

(Riga 2) E&#8217; stampato l&#8217;indirizzo a cui punta il puntatore alla struttura e l&#8217;ampiezza in memoria della stessa. Quest&#8217;ultimo valore è pari a 12 byte, e non coincide con la somma delle ampiezze dei singoli campi della struttura. Infatti il tipo Int32 occupa 4 byte, il tipo float occupa 4 byte ed il tipo short 2, per un totale di 10 byte, e tuttavia lo spazio allocato per la struttura è pari a 12 byte. Questo comportamento è normale su un processore a 32 bit dove la memoria è suddivisa in blocchi da 4 byte poichè tale processore lavora in modo più efficiente quando opera su blocchi di memoria di 4 byte, meglio conosciuto nel sistema Windows come DWORD. Il .NET Framework, quindi, alloca memoria in blocchi di 4 byte anche se la memoria indispensabile per ogni tipo a valore è inferiore.

(Righe 3, 4 5) E&#8217; creata una istanza della struttura Article con l&#8217;inizializzazione dei suoi campi

(Riga 6) Il puntatore **pArticleStruct** punta all&#8217; istanza della struttura Article appena creata

(Righe 7, 8) Attraverso il puntatore **pArticleStruct** sono letti i valori dei singoli campi della struttura e memorizzati in variabili

(Righe 9, 10) Attraverso il puntatore **pArticleStruct** sono scritti nuovi valori dei singoli campi della scrittura

(Righe 11, 12) Sono creati puntatori ai singoli campi della struttura Article

(Righe 13, 14) Queste righe sono equivalenti alle righe 12, 13; mostrano quindi una sintassi alternativa per creare dei puntatori ai campi interni di una struttura

(Riga 15) E&#8217; stampato il contenuto dei campi della struttura letti attraverso variabili di appoggio

(Riga 16) E&#8217; stampato il contenuto dei campi della struttura letti attraverso i rispettivi puntatori

(Righe 17, 18, 19, 20) Sono stampati gli indirizzi memorizzati nelle variabili di tipo puntatore

<u>Puntatori a campi di una classe</u>

E&#8217; stato detto che non è possibile creare un puntatore ad un tipo riferimento, almeno utilizzando il linguaggio C#, ma solo ad un tipo valore, in quanto si comprometterebbe il corretto funzionamento del garbage collector. Ad esempio, la compattazione della memoria effettuata dopo una operazione di pulizia non potrebbe più aver luogo se il codice avesse la capacità  di manipolare gli indirizzi di memoria. Tuttavia, una classe può contenere membri di tipo valore, ad esempio un campo pubblico di tipo double. Il compilatore C# permette di definire un puntatore ad un campo di una classe, ma, se si applicasse la stessa logica vista per le strutture, non si avrebbe il risultato desiderato.

Ad esempio, considerando l&#8217;esempio **Article** come una classe:

<pre class="brush: csharp; title: ; notranslate" title="">public class ArticleClass
{
   public int code;
   public float price;
}
</pre>

compilando il seguente codice:

<pre class="brush: csharp; title: ; notranslate" title="">ArticleClass ArticleObj=new ArticleClass();
ArticleObj.code=5;
ArticleObj.price=50.78f;
int* pIntOfClass=&(ArticleObj.code);
float* pFloatOfClass=&(ArticleObj.price);
</pre>

si otterrebbe il seguente errore di compilazione:

_**You can only take the address of an unfixed expression inside of a fixed statement initializer**_

Questo comportamento è dovuto al meccanismo del garbage collector che potrebbe spostare spostare il riferimento **ArticleObj** in una zona di memoria diversa da quella in cui è stato creato. Per evitare quindi che a seguito di ciò il riferimento non sia più valido il compilatore C# impedisce di utilizzare puntatori a tipi valore membri di una classe, a meno di non utilizzare la parola chiave **fixed** che, come facilmente intuibile, obbliga il garbage collector a non spostare il riferimento ad **ArticleObj** in un&#8217;altra zona di memoria perchè è molto probabile che ci siano puntatori ai suoi campi.

Il seguente esempio mostra il suo utilizzo:

<pre class="brush: csharp; title: ; notranslate" title="">fixed (int* pIntOfClass=&(ArticleObj.code))
 {
   Console.WriteLine("Code: {0}", *pIntOfClass);
 }
   
 fixed (float* pFloatOfClass=&(ArticleObj.price))
 {
   Console.WriteLine("Price: {0}", *pFloatOfClass);
 }
</pre>

<u>Uso di un array basato sui puntatori</u>

Attraverso l&#8217;utilizzo dei puntatori è possibile gestire array ad alte prestazioni basati sullo stack. Un array è rappresentato da una istanza della classe **System.Array**, e, per tale motivo, è memorizzato nell&#8217;heap gestito.

Quindi, se si prova a creare un array di tipi double (cioè un tipo valore) in un metodo, ciò che sarà  memorizzato nello stack è semplicemente il riferimento all&#8217;heap gestito che conterrà  i dati veri e propri. Se si ha la necessità  di manipolare un array nello stack in modo da guadagnare in termini di performance è necessario ricorrere ad un puntatore.

Nell&#8217;esempio che segue:

<pre class="brush: csharp; title: ; notranslate" title="">double[] doubleArray=new double[20];
</pre>

E&#8217; dichiarato un array di double di 20 elementi memorizzati nell&#8217;heap gestito.

In questo esempio, al contrario, è dichiarato un array di 20 elementi di tipo double memorizzati nello stack:

<pre class="brush: csharp; title: ; notranslate" title="">double* pDoubleArray=stackalloc double[20];
</pre>

Come si può notare occorre utilizzare la parola chiave **stackalloc** per la dichiarazione dell&#8217;array, seguita dal tipo di dato e dall&#8217;ampiezza dell&#8217;area di memoria da allocare. Dopo tale dichiarazione la variabile **pDoubleArray** punterà  al primo elemento dello stesso, quindi la seguente istruzione assegna il valore **10.37** al primo elemento dell&#8217;array:

<pre class="brush: csharp; title: ; notranslate" title="">*pDoubleArray=10.37;
</pre>

Sfruttando l&#8217;aritmetica dei puntatori è possibile accedere ad uno qualsiasi degli elementi di un array in questo modo:

<pre class="brush: csharp; title: ; notranslate" title="">*(pDoubleArray+10)=20.45;
</pre>

Tuttavia, è possibile utilizzare una sintassi più semplice:

<pre class="brush: csharp; title: ; notranslate" title="">pDoubleArray[10]=20.45;
</pre>

Il compilatore C# riconosce che la variabile **pDoubleArray** è un puntatore ad un array di double e permette di accedere all&#8217;elemento con l&#8217;indice indicato tra parentesi quadre. Quindi le 2 righe di codice viste in precedenza sono equivalenti.

Sfruttando questo meccanismo il seguente blocco di codice crea un array di 20 elementi di tipo intero basato sullo stack, ed assegna ad ogni elemento un numero casuale compreso tra 1 e 100. Successivamente il contenuto dell&#8217;array è stampato a video:



Occorre però tenere in considerazione un aspetto importantissimo quando si utilizzano i puntatori per accedere agli elementi di un array. Nell'esempio precedente è stata allocata sufficiente memoria per memorizzare un array di venti interi a 32 bit utilizzando la keyword **stackalloc**. Se si tentasse di accedere ad un elemento fuori dal range ammesso utilizzando l'array creato in questo modo, ad esempio:

<pre class="brush: csharp; title: ; notranslate" title="">pintArray[50]=10;
</pre>

non si otterrebbe alcun errore di run-time ma molto probabilmente si comprometterebbe la stabilità  del sistema in quanto l'applicazione avrebbe accesso ad una area di memoria esterna rispetto a quella occupata dall'array di 20 elementi. Se si facesse la stessa operazione su un normale array creato a partire da una istanza di System.Array, il CLR solleverebbe l'eccezione **System.IndexOutOfRangeException**, preservando in tal modo l'integrità del sistema.

<u><strong>Conclusioni</strong></u>

In questo articolo abbiamo visto come poter accedere direttamente alle memoria utilizzando il linguaggio C#, e come questa operazione possa incrementare le performance di routine in cui la velocitÃ  rappresenta un aspetto critico. Analogamente si è visto che questa possibilità  andrebbe usata con molta cautela e solo quando realmente necessario poichè il codice **unsafe** non è eseguito nel contesto di sicurezza imposto dal CLR, risultando potenzialmente pericoloso per l'integrità  dell'applicazione e dell'intero sistema.