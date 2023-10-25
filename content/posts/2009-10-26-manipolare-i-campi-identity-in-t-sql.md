---
title: Manipolare i campi identity in T-SQL
author: mtammacco
type: post
date: 2009-10-26T00:07:08+00:00
url: /archive/2009/10/26/manipolare-i-campi-identity-in-t-sql.aspx
categories:
  - T-SQL

---
Spesso può essere utile verificare il valore identity associato ad una colonna di una tabella di database ed eventualmente modificarlo, impostandolo chiaramente ad un valore almeno uguale al valore più alto del campo. Questa operazione è  utile soprattutto quando si popola una tabella con un campo di questo tipo con informazioni di test, che successivamente sono eliminate, ed è quindi utile azzerare il valore identity per farlo ripartire da 1. 

Il comando T-SQL per manipolare il campo identity è **DBCC CHECKIDENT**.

Alcuni esempi:

**T-SQL**

<pre class="brush: csharp; title: ; notranslate" title="">-- visualizza il valore corrente del campo identity di &lt;nome tabella
DBCC CHECKIDENT (&lt;nome tabella&gt;, NORESEED)  
  
-- verifica il valore corrente del campo identity di &lt;nome tabella&gt; e, 
-- se errato, lo corregge
DBCC CHECKIDENT (&lt;nome tabella&gt;) 
  
-- imposta a 50 il valore corrente del campo identity di &lt;nome tabella&gt;
DBCC CHECKIDENT (&lt;nome tabella&gt;, RESEED, 50) 
</pre>