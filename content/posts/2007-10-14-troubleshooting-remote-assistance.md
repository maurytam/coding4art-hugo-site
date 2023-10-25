---
title: Troubleshooting remote assistance
author: mtammacco
type: post
date: 2007-10-14T13:08:00+00:00
url: /archive/2007/10/14/troubleshooting-remote-assistance.aspx
categories:
  - Workaround

---
Per una volta parlo di come risolvere un piccolo ma noioso problema sistemistico: provando ad utilizzare l&#8217;assistenza remota di MSN mi appariva questo strano errore:

**&#8220;Impossibile aprire la Guida in linea e supporto tecnico perchè un servizio di sistema non è in esecuzione. Per risolvere il problema, avviare il servizio denominato &#8216;Help Service&#8221;**

Il servizio in questione, chiamato &#8220;Guida in linea e supporto tecnico&#8221; nella versione italiana, è chiaramente la Guida in linea di Windows XP, che evidentemente non era presente sulla macchina. Ma l&#8217;aspetto più imbarazzante era che non  vi era nessun  servizio chiamato in quel modo tra l&#8217;elenco dei servizi di Windows.  Quindi, come  (re)installare la Guida  in linea ?  In questi casi, come al solito, non esiste aiuto migliore dei gruppi di discussione sull&#8217;argomento specifico.

Ecco come procedere:

  * Browse della directory c:\windows\inf e cercare il file pchealth.inf. Click destro e scegliere installa.
  * Al temine, installare il servizio attraverso questo comando: Start /w helpsvc /svchost netsvcs /regserver /install 
  * Al termine dell&#8217;installazione riavviare Windows XP,  ed ecco che magicamente comparirà il servizio in questione tra i servizi di Windows

Con il servizio avviato, l&#8217;assistenza remota di Windows non dà più problemi.

Ora mi chiedo: cosa c&#8217;entra la guida in linea di Windows con l&#8217;assistenza remota. ?

P.S: Un grazie a Rossano Orlandini, MVP Windows Server, per la soluzione al problema.