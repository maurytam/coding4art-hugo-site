---
title: Righe casuali in SQL Server 2000
author: mtammacco
type: post
date: 2009-10-26T00:10:33+00:00
url: /archive/2009/10/26/righe-casuali-in-sql-server-2000.aspx
categories:
  - T-SQL

---
Ordinare le righe di una tabella di Sql Server in modo casuale, cioè con ordinamento variabile di volta in volta, non è certamente una operazione di ogni giorno e, a prima vista, può anche sembrare una operazione complessa. In realtà è abbastanza semplice se ci si affida alla funzione NEWID() che ritorna un GUID univoco in assoluto; pertanto la seguente query:

**T-SQL**

<pre class="brush: csharp; title: ; notranslate" title="">select * from orders order by newid()
</pre>

restituirà un resultset ordinato ogni volta in modo differente.

Basandoci su questo esempio è anche possibile estrarre una riga diversa ogni volta che si esegue lo statement:

**T-SQL**

<pre class="brush: csharp; title: ; notranslate" title="">select top 1 * from orders order by newid()
</pre>

Quest&#8217;ultima istruzione andrebbe usata però con cautela su tabelle di grandi dimensioni, in quanto prima di restituire  la riga casuale l&#8217;engine SQL legge tutte le righe della tabella, per ognuna di esse calcola il GUID, ed infine ordina le stesse, come si evince dando uno sguardo al piano di esecuzione.