---
title: Da VB6 a VB.NET ….
author: mtammacco
type: post
date: 2006-03-10T07:10:00+00:00
url: /archive/2006/03/10/da-vb6-a-vb-net.aspx
categories:
  - Thoughts

---
**<u>Premessa</u>**:  
ho iniziato a programmare seriamente (per lavoro) utilizzando il linguaggio Visual Basic; ho utilizzato questo linguaggio per parecchi anni nelle varie versioni che via via si sono succedute (3.0, 4.0, 5.0, 6.0). Su questo linguaggio ho investito parecchio tempo sia per apprenderlo che per approfondirlo, ricevendo un enorme aiuto dalle community quali [Visual Basic Tips & Tricks][1], solo per citarne una. Ho anche investito del denaro, in quanto i primi esami di certificazione Microsoft che ho passato riguardavano VB6 Desktop & Enterprise, comprandomi libri sull&#8217;argomento e pagandomi i test di tasca mia.  
Ho scritto parecchie linee di codice in VB6, e le soddisfazioni professionali non sono mancate; ho considerato questo linguaggio altamente produttivo e facile da imparare, ma, confesso, alcune volte mi sono scontrato con problemi non facili da superare dovuti essenzialmente alla intrinseca facilità del linguaggio che tende a mascherare dettagli importanti della programmazione a beneficio della velocità di scrittura del codice.

Con l&#8217;avvento di .NET  ho utilizzato da subito il linguaggio Visual Basic .NET, soprattutto perchè provenivo dal VB6 e mi è sembrato naturale continuare ad utilizzare la stessa sintassi, conscio però del fatto che la semantica era completamente diversa. Ho approfondito parecchio la conoscenza del .NET Framework, e questa conoscenza mi ha agevolato tantissimo quando ho dovuto per forza di cose programmare in C#; infatti questo linguaggio l&#8217;ho appreso nel giro di pochi giorni poichè il tutto si limita all&#8217;apprendimento della sintassi tipica dello stesso, e questo grazie all&#8217;indipendenza del Framework .NET dal linguaggio utilizzato.

Adesso uso i due linguaggi in modo intercambiabile, ma la mia preferenza è senza ombra di dubbio per il C#, poichè, a mio avviso, nonostante il VB .NET sia completamente diverso dal suo predecessore, sia finalmente un vero linguaggio ad oggetti e fornisca la stessa potenza del C#, soffre ancora di qualche retaggio del suo passato di linguaggio &#8220;facile&#8221; ed alla portata di tutti.  
   
Sono sicuro che se dovessi aver bisogno di programmare in un altro linguaggio .NET compliant, l&#8217;apprendimento dello stesso non durerebbe più di qualche giorno,e questo non per merito mio ma del framework .NET.

Questa lunga premessa mi è saltata in mente leggendo queto interessantissimo [post][2] di [Diego Cattaruzza][3] in risposta a questo [articolo][4] dove si pone in risalto il fatto che Microsoft &#8220;costringerebbe&#8221; i programmatori VB6 a passare forzatamente a Visual Basic .NET poichè il supporto per VB6 terminerà a Marzo del 2008.

La mia opinione è che Microsoft abbia fatto tantissimo per agevolare questo passaggio, in ordine sparso:

  * Eventi gratuiti dove si cerca di fornire una risposta agli interrogativi di chi ha codice VB6 da migrare; 
  * Rilascio di Visual Basic .NET 2005 Express, versione gratuita dell&#8217;ambiente di sviluppo che, seppure con qualche limitazione, permette quantomeno di provare in prima persona la nuova tecnologia; 
  * Disponibilità gratuita di blocchi di codice (Application blocks) già pronti all&#8217;uso per fornire immediatamente le funzionalità comuni di ogni applicazione (log, configurazione, accesso ai dati,ecc) 
  * il termine della fine del supporto per VB6, inizialmente fissato a Marzo 2005, è stato spostato a Marzo 2008, anche grazie alla famosa [petizione][5] internazionale sottoscritta da oltre 10000 programmatori;

Inoltre, come sottolinea chiaramente e giustamente lo stesso Cattaruzza, la vecchia infrastruttura basata sull&#8217;accoppiata Win32/COM+ è assolutamente inadeguata a sostenere l&#8217;evolversi dei sistemi di comunicazione attuali; la nuova infrastruttura è basata sul .NET Framework e quindi non ha assolutamente senso continuare a supportare un linguaggio basato su una piattaforma ormai superata.

Questo discorso resta valido anche per il cosiddetto &#8220;programmatore hobbysta&#8221;, perchè se cambia l&#8217;infrastruttura sottostante lo sviluppo di software basato su Win32 e COM+ perde di significato.

Infine, un parere personale che ritengo di fondamentale importanza: l&#8217;evoluzione tecnologica per un informatico deve essere un aspetto da non mettere mai in discussione; è errato pensare che solo perchè si è speso tempo e denaro per essere padroni di una tecnologia non ci si possa rimettere in discussione spendendo altro tempo per impararne un&#8217;altra, più evoluta della precedente che permette di essere più produttivi e di scrivere software più efficiente. Questo lo afferma una persona che ha speso tantissimo tempo e denaro su VB6, ma cha ha fatto altrettanto quando l&#8217;evolversi della tecnologia lo ha messo di fronte a strumenti più evoluti.  
Se si pensa che aver fatto sacrifici per impadronirsi di una tecnologia basta per mantenersi a galla nel mondo informatico sempre in continua evoluzione si commette un grave errore che può riflettersi negativamente sul proprio futuro professionale.

 

 [1]: http://www.visual-basic.it/
 [2]: http://community.visual-basic.it/Diego/archive/2006/03/07/16928.aspx
 [3]: http://community.visual-basic.it/Diego/
 [4]: http://www.maurorossi.net/pagine/vbornetvb.htm
 [5]: http://www.classicvb.org/petition/?lang=it