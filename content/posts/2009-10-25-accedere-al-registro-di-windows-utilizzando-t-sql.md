---
title: Accedere al registro di Windows utilizzando T-SQL
author: mtammacco
type: post
date: 2009-10-25T23:46:55+00:00
url: /archive/2009/10/25/accedere-al-registro-di-windows-utilizzando-t-sql.aspx
categories:
  - T-SQL

---
Sql Server prevede una serie di stored procedure di sistema per svolgere funzioni di amministrazione del server, gestione della posta elettronica, esecuzione di comandi di sistema, etc., alcune delle quali anche non documentate, e che possono tornare utili in diverse occasioni. Poichè si tratta di una applicazione basata su COM utilizza il registro di sistema per memorizzare informazioni vitali per il suo funzionamento. Attraverso una store procedure non documentata chiamata xp_regread è possibile leggere il valore di una qualsiasi chiave di registro, utilizzando il tal modo solo codice T-SQL. Lo script seguente legge il contenuto della chiave utilizzata da Sql Server per memorizzare il percorso fisico di installazione. 

**T-SQL**

<pre class="brush: csharp; title: ; notranslate" title="">declare @sqlpath varchar(200)
exec master..xp_regread @root='HKEY_LOCAL_MACHINE', 
     @key='SOFTWARE\MICROSOFT\MICROSOFT SQL SERVER\80\TOOLS\CLIENTSETUP', 
     @value_name='SqlPath', @value=@sqlpath OUT 
</pre>

Il parametro di output @value conterrà il contenuto della chiave chiamata SqlPath situata nel percorso &#8216;SOFTWARE\MICROSOFT\MICROSOFT SQL SERVER\80\TOOLS\CLIENTSETUP&#8217; 

**T-SQL** 

<pre class="brush: csharp; title: ; notranslate" title="">print @sqlpath 
</pre>