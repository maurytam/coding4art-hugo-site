---
title: xp_cmdshell, appunti di utilizzo
author: mtammacco
type: post
date: 2006-10-20T10:33:00+00:00
url: /archive/2006/10/20/xp_cmdshell-appunti-di-utilizzo.aspx
categories:
  - Sql Server 2005

---
Non è un semplice tip, infatti sottintende parecchio di più. Sto parlando di come impedire ad una istanza di Sql Server di avviarsi utilizzando&#8230;..sql stesso, reperibile sul sito della community <a title="" href="http://www.dotnetside.org/" target="" name="" rel="noopener">.netSide</a>, e scritto da <a title="" href="http://www.xplayn.org/cs/blogs/francesco" target="" name="" rel="noopener">Francesco Quaratino</a>, disponibile [qui][1] Per quanto possa sembrare a prima vista strano voler impedire ad una istanza di Sql di avviarsi, ritengo tuttavia plausibile uno scenario reale in cui questa situazione possa verificarsi. Ad esempio, potremmo utilizzare una istanza di Sql solo per motivi amministrativi, e quindi solo un DBA può usufruire del servizio, ma è comunque necessario garantire agli utenti un accesso amministrativo al PC per altri motivi; infatti, in questo scenario è necessario assicurarsi che l&#8217;utente amministratore, ma non DBA, non possa avviare l&#8217;istanza. 

L&#8217;utilizzo della store xp_cmdshell, tuttavia, è disabilitato di default in Sql Server 2005 per motivi di sicurezza, come spiegato esaurientemente in questo <a title="" href="http://weblogs.sqlteam.com/tarad/archive/2006/09/14/12103.aspx" target="" name="" rel="noopener">post</a> di <a title="" href="http://weblogs.sqlteam.com/tarad/Default.aspx" target="" name="" rel="noopener">Tara Kizer</a> (un blog assolutamente da leggere per tutti gli aficionados di Sql); occorre quindi abilitarne prima l&#8217;uso attraverso &#8220;sp_configure&#8221; oppure utilizzando il tool Surface Area Configuration.

Ottimo tip e ottimo blog.

 [1]: http://www.dotnetside.org/blogs/tips/archive/2006/10/12/Impedire-avvio-istanza-SQL-Server.aspx