---
title: Data Scripter per Sql Server 2005
author: mtammacco
type: post
date: 2006-07-28T09:40:00+00:00
url: /archive/2006/07/28/data-scripter-per-sql-server-2005.aspx
categories:
  - Sql Server 2005

---
Scripting dei dati di una tabella di Sql Server 2005 mediante generazione automatica di istruzioni di insert. Questa funzionalità avrebbero a mio avviso dovuto includerla almeno già da un paio di versioni poichè in alcuni casi risulta davvero utile. Anzi, ricordo che durante consulenze passate qualche collega particolarmente devoto a Oracle trovava motivo di denigrare il dbengine di Microsoft a favore di Oracle solo perchè questa funzionalità era assente. Da quell&#8217;immenso repository di codice e documentazione che va sotto il nome di <a title="" href="http://www.codeproject.com/" target="" name="" rel="noopener">Code Project</a> è possibile scaricare questo <a title="" href="http://www.codeproject.com/useritems/enisey.asp" target="" name="" rel="noopener">add-in</a> per Sql Server 2005 Management Studio, che mette a disposizione una nuova voce di menù contestuale sull&#8217;item di una qualsiasi tabella permettendo di generare automaticamente le istruzioni di insert per tutte le righe o per un sottoinsieme di esse. L&#8217;add-in è  un assembly .NET 2.0 che si registra come componente COM e come add-in per SSMS. E&#8217; disponibile al download sia la versione <a title="" href="http://www.codeproject.com/useritems/enisey/EniseySetup.zip" target="" name="" rel="noopener">binaria</a> che quella con i <a title="" href="http://www.codeproject.com/useritems/enisey/EniseySource.zip" target="" name="" rel="noopener">sorgenti</a> (C#). Quest&#8217;ultima torna utile soprattutto come modello per creare altri add-in per SSMS.