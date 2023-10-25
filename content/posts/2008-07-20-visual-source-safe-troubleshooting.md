---
title: Visual source safe – troubleshooting
author: mtammacco
type: post
date: 2008-07-20T16:20:43+00:00
url: /archive/2008/07/20/visual-source-safe-troubleshooting.aspx
categories:
  - Troubleshooting
  - Visual Source Safe
  - Workaround

---
Nel mio lavoro quotidiano come consulente uso spesso e volentieri Visual Source Safe (sigh!)  come repository del codice sorgente. Come chi già lo usa sicuramente ben sa, Source Safe è un prodotto ormai datato che si porta dietro un pò di problemi di varia natura. Quindi, non è sempre facile &#8220;addomesticarlo&#8221; per ottenere quello che si vuole. Appunto un paio di workaround su come evitare certe situazioni che possono portare a problemi:

  1. Se si usa una cartella diversa da c:\inetpub\wwwroot per salvare i propri progetti web, non usare mai il comando File|Open fron Source Control. Questo comando, a dispetto della working folder impostata, salverà sempre il progetto web in una sottodirectory della directory c:\inetpub\wwwroot, con il risultato di avere una doppia copia del progetto web sulla propria macchina se si è scelto di utilizzare una directory differente per il proprio progetto. Questo comportamento si può evitare impostando la virtual directory della propria applicazione (che dovrà puntare alla directory fisica prescelta) PRIMA di eseguire il comando &#8220;Open from Source Control&#8221;.
  2. Source Safe NON è transazionale, quindi un crash del sistema nel bel mezzo di una operaizione di scrittura porta quasi sempre a corruzione del database, non sempre risolvibili attraverso l&#8217;utility &#8220;**Analyze**&#8220;
  3. L&#8217;esecuzione del comando &#8220;**Analyze**&#8221; come pure di altri comandi di diagnostica non và a buon fine se risultano utenti ancora connessi al database; questo è anche logico, se non fosse per il fatto che non esiste un metodo &#8220;pulito&#8221; per disconnettere utenti che risultano ancora connessi. Per far questo occorre utilizzare alcuni strumenti del sistema operativo per disconnettere forzatamente un utente dalla rete.
  4. Effettuare un backup dell&#8217;intero database quanto più frequentemente possibile