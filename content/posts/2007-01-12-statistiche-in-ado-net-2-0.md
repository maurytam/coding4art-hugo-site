---
title: Statistiche in ADO .NET 2.0
author: mtammacco
type: post
date: 2007-01-12T11:57:00+00:00
url: /archive/2007/01/12/statistiche-in-ado-net-2-0.aspx
categories:
  - ADO .NET

---
In ADO .NET 2.0 è possibile programmaticamente ottenere delle informazioni statistiche circa l&#8217;uso di una connessione ad un database. Bastano infatti solo 2 righe di codice:

<pre class="brush: csharp; title: ; notranslate" title="">connSQL.StatisticsEnabled = true;
System.Collections.IDictionary statsDict = connSQL.RetrieveStatistics();
</pre>

per ottenere un dictionary di valori statistici validi nel momento in cui il metodo RetrieveStatistics() è invocato.  
Tratto dalla documentazione MSDN, ecco un elenco (parziale) dei valori statistici più interessanti:

**NetworkServerTime**

Restituisce il tempo cumulativo atteso dal provider prima di ricevere una risposta dal database server, a partire dal momento in cui le statistiche sono abilitate.

**PreparedExecs**

Restituisce il numero dei comandi precompilati eseguiti, a partire dal momento in cui le statistiche sono abilitate.

**Prepares**

Restituisce il numero delle istruzioni precompilate eseguite, a partire dal momento in cui le statistiche sono abilitate.

**SelectCount**

Restituisce il numero delle istruzioni SELECT eseguite, a partire dal momento in cui le statistiche sono abilitate, incluse le istruzioni FETCH usate per leggere le righe da un cursore; il conteggio delle SELECT è aggiornato quando viene raggiunta la fine di un SqlDataReader

**SelectRows**

Ritorna il numero delle righe interessate, a partire dal momento in cui le statistiche sono abilitate. Il conteggio comprende tutte le righe generate da istruzioni SQL, anche se non utilizzate dal chiamante, ad esempio eventuali righe derivanti da un data reader chiuso prima di leggere l&#8217;intero resultset oppure le righe di un cursore. ****

**ServerRoundtrips**

Ritorna il numero di volte in cui viene inviato un comando al server ed attesa la conseguente risposta, a partire dal momento in cui le statistiche sono abilitate.

**Transactions**

Restituisce il numero delle transazioni utente iniziate, a partire dal momento in cui le statistiche sono abilitatea prescindere se andate a buon fine o no. In caso di auto commit impostato su on ogni comando è considerato una transazione.

**UnpreparedExecs**

Ritorna il numero delle istruzioni non compilate eseguite, a partire dal momento in cui le statistiche sono abilitate.

Curiosando il metodo RetrieveStatistics() con il tool Reflector si nota che esso utilizza una classe interna dell&#8217;assembly System.Data, precisamente SqlStatistics, marcata appunto come &#8220;internal sealed&#8221; (C#), oppure &#8220;Friend NotInheritable&#8221; (Visual Basic .NET). Quindi la suddetta classe non è nè visibile dall&#8217;esterno dell&#8217;assembly System.Data nè tantomeno ereditabile.