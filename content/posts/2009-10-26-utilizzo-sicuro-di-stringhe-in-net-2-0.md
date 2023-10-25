---
title: Utilizzo “sicuro” di stringhe in .NET 2.0
author: mtammacco
type: post
date: 2009-10-26T00:45:50+00:00
url: /archive/2009/10/26/utilizzo-sicuro-di-stringhe-in-net-2-0.aspx
categories:
  - Technical articles

---
La classe System.String non rappresenta la soluzione più sicura quando è necessario memorizzare sotto forma di stringa contenuti confidenziali, ad esempio stringhe di connessione a database, password varie, numeri di carta di credito, ecc.. Informazioni di questo genere andrebbero mantenute in memoria solo il tempo strettamente necessario alla loro elaborazione, e la memoria occupata andrebbe rilasciata il più presto possibile. Questo accorgimento è necessario poichè il contenuto della memoria utilizzata da un processo in esecuzione potrebbe essere letta attraverso varie tecniche di hacking, e quindi il suo eventuale contenuto confidenziale correrebbe seri pericoli di manomissione. Inoltre, un processo in esecuzione potrebbe utilizzare un file di swap su disco che provocherebbe la scrittura anche di questo genere di informazioni.

<u>[Perchè una stringa è insicura]<br /> </u>La classe System.String non si adatta affatto a queste caratteristiche. Infatti, una stringa è un oggetto immutabile, per cui ogni modifica ad essa comporta la creazione di una nuova stringa memorizzata in un&#8217;area di memoria differente, mentre la vecchia stringa continuerà  ad esistere fino alla successiva operazione di garbage collection, che, a causa della sua natura non deterministica, potrebbe avvenire ben più tardi rispetto al momento in cui tutti i riferimenti ad essa sono rilasciati.  
L&#8217;immutabilità  delle stringhe costituisce un serio problema se una stringa contiene informazioni confidenziali per almeno 3 motivi:  
&#8211; Ogni manipolazione effettuata su di essa lascia in memoria una copia della stessa, in attesa del garbage collector;  
&#8211; Non esiste alcun modo per resettare il contenuto della stringa una volta utilizzato; il tentativo di assegnare un valore nullo provocherà  la creazione di un nuovo oggetto stringa con il nuovo contenuto lasciando invariato il vecchio;  
&#8211; L&#8217;indirizzo di memoria in cui è memorizzata una stringa non è costante una volta creata;  
&#8211; Non è possibile criptare il contenuto di una stringa senza provocare la creazione di un nuovo oggetto con il contenuto criptato;  
<u>[La soluzione in .NET 1.0/1.1]</u>  
Nella versione 1.0/1.1 del Microsoft .NET Framework non esiste una soluzione semplice a questo problema. Infatti l&#8217;unica strada percorribile è quella di criptare/decriptare manualmente il contenuto di una stringa confidenziale utilizzando un array di caratteri come area di lavoro. Non è invece possibile resettare una stringa senza attendere che il garbage collector agisca.

<u>[La soluzione in .NET 2.0]<br /> </u>La versione 2.0 del .NET Framework pone rimedio a tutti i problemi di sicurezza precedentemente elencati attraverso la nuova classe SecureString presente nel namespace System.Security. Questa nuova classe permette di memorizzare in modo sicuro e criptato una stringa contenente contenuto confidenziale, utilizzando DPAPI (Data Protection API), ovvero una serie di API per il criptaggio ed il decriptaggio di informazioni mediante l&#8217;algoritmo Triple-DES.

Ecco un esempio di utilizzo:

<pre class="brush: csharp; title: ; notranslate" title="">public SecureString SetSecurePassword(string password)
{
   SecureString ss = new SecureString();
   foreach (char c in password.ToCharArray())
   {
         ss.AppendChar(c);
   }
        
   return ss;
}
</pre>

Come si può; notare, l&#8217;utilizzo di SecureString è un pò più macchinoso rispetto alla creazione di un semplice oggetto stringa; infatti esso richiede che la stringa sicura sia costruita aggiungendo un carattere alla volta attraverso il metodo AppendChar(). Il motivo di questo utilizzo dovrebbe essere ovvio: non è possibile costruire una stringa sicura a partire da una stringa già in memoria in testo in chiaro, poichè quest&#8217;ultima sarebbe immutabile con gli identici problemi di sicurezza visti precedentemente. Inoltre, una istanza di SecureString è mutabile, il suo indirizzo di memoria non cambia una volta creata e può quindi facilmente essere azzerata attraverso il metodo Clear() senza attendere il garbage collector. Oltre al metodo AppendChar() esistono altri metodi per modificare il contenuto, ad es. InsertAt(), RemoveAt(), SetAt(), il cui nome è abbastanza intuitivo per comprendere il loro utilizzo. La proprietà MakeReadOnly blocca il contenuto dell&#8217;oggetto SecureString non permettendo più alcuna modifica. Questa caratteristica può essere letta attraverso la proprietà  IsReadOnly. Inoltre, la classe SecureString implementa l&#8217;interfaccia IDisposable, ovvero permette al suo utilizzatore di distruggere l&#8217;istanza in memoria senza attendere il garbage collector.

Dopo aver creato e popolato una istanza della classe SecureString occorre leggere il valore in essa contenuto. Questa operazione non può essere fatta richiamando semplicemente il metodo ToString() della classe, in quanto quest&#8217;ultimo non è stato ridefinito e ritorna semplicemente l&#8217;oggetto sotto forma di stringa così come ereditato da System.Object, vale a dire System.Security.SecureString, non di grande utilità , e non è semplicissima in quanto comporta una operazione di marshalling (attraverso l&#8217;utilizzo della classe Marshal presente nel namespace System.Runtime.InteropServices) che coinvolge l&#8217;utilizzo di un puntatore alla stringa, anche se il tutto si risolve con poche righe di codice, come in questo esempio:

<pre class="brush: csharp; title: ; notranslate" title="">public string GetPassword(SecureString ss)
 {
     IntPtr bstr = Marshal.SecureStringToBSTR(ss);
   
     try
     {
        password = Marshal.PtrToStringUni(bstr);
     }
     finally
     {
         Marshal.ZeroFreeBSTR(bstr);
     }
   
     return password;
}
</pre>

Una volta ottenuta la controparte immutabile della stringa, è necessario assicurarsi che l&#8217;area di memoria puntata dal puntatore sia azzerata attraverso l&#8217;utilizzo del metodo ZeroFreeBSTR della classe Marshal.  
<u>[Riferimenti]<br /> </u>**[1]** Maurizio Tammacco &#8211; [Pinned object in .NET][1]  
**[1]** Maurizio Tammacco &#8211; [Uso efficiente delle stringhe in .NET][2]

 [1]: http://www.coding4art.com/articles/pinned-object-in-.net.aspx
 [2]: http://www.coding4art.com/articles/uso-efficiente-delle-stringhe-in-.net.aspx