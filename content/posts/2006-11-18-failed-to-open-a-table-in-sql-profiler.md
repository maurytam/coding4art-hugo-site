---
title: Failed to open a table in Sql Profiler
author: mtammacco
type: post
date: 2006-11-18T08:13:00+00:00
url: /archive/2006/11/18/failed-to-open-a-table-in-sql-profiler.aspx
categories:
  - Sql Server 2005

---
Applicare un service pack è una operazione che andrebbe meditata un pò, almeno andrebbe fatta dopo aver letto quali sono le fix apportate e quali sono gli eventuali impatti. A volte un però l&#8217;applicazione di un service pack provoca che una qualche funzionalità smette di &#8230;.funzionare. A parte gli scherzi, applicando il service pack 4 a Sql Server 2000 diventa impossibile aprire un trace table con Sql Profiler a causa del seguente errore bloccante:

&#8220;Failed to open a table&#8221;.

Soluzione immediata ? Aprirlo con il profiler di Sql Server 2005.

Il tutto è ampiamente documentato in [questo][1] articolo della KB Microsoft 

 [1]: http://support.microsoft.com/kb/900629/en-us