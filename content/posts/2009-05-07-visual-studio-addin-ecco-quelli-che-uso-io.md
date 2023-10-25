---
title: Visual Studio Addin – ecco quelli che uso io
author: mtammacco
type: post
date: 2009-05-07T10:56:22+00:00
url: /archive/2009/05/07/visual-studio-addin-ecco-quelli-che-uso-io.aspx
categories:
  - Tools

---
L&#8217;utilizzo degli add-in di Visual Studio 2008 consente di incrementare a volte notevolmente la produttività di chi sviluppa, ad esempio rendendo possibile effettuare con pochi click operazioni ripetitive e lunghe. Tratto da <a href="http://www.visualstudiogallery.com/Default.aspx" target="_blank" rel="noopener">Visual Studio Gallery</a>, ecco la serie di add-in, rigorosamente free, che utilizzo giornalmente durante l&#8217;attività di sviluppo del software: 

**<a href="http://www.visualstudiogallery.com/ExtensionDetails.aspx?ExtensionID=800978aa-2aac-4440-8bdf-6d1a76a5c23c" target="_blank" rel="noopener">Regionerate</a>**, permette di creare in automatico le regioni di codice su un intero file, applicando un layout predefinito o scelto tra i layout forniti. Uno dei layout a corredo addirittura effettua il conteggio automatico degli items presenti in ogni regione e lo inserisce nel nome della stessa. E&#8217; anche possibile crearsi propri layout o scaricarli. Davvero utile. 

<a href="http://www.visualstudiogallery.com/ExtensionDetails.aspx?ExtensionID=df3f0c30-3d37-4e06-9ef8-3bff3508be31" target="_blank" rel="noopener">PowerCommands</a>, add-in abbastanza conosciuto e molto utile, anche se responsabile di un crash documentato di Visual Studio, di cui ho già parlato <a href="http://xplayn.org/cs/blogs/maurizio/archive/2008/09/04/visual-studio-2008-ide-crash-dopo-quot-choose-items-quot-dalla-toolbox.aspx" target="_blank" rel="noopener">qui</a> e <a href="http://xplayn.org/cs/blogs/maurizio/archive/2008/12/09/visual-studio-ide-crash-2.aspx" target="_blank" rel="noopener">qui</a>. Trattasi di una serie di comandi aggiuntivi sistemati in diversi punti dell&#8217;IDE. I principali comandi che uso sono:  
&#8211;**Show All Files** (Solution Explorer, a livello di nodo solution)  
Questo comando mostra tutti i file per tutti i progetti caricati nella soluzione attiva, e non solo invece per il progetto attivo, come opera invece il comando omonimo a livello di progetto;  
&#8211;**Collapse Projects**. Questo comando collassa il nodo selezionato e contemporaneamente tutti i suoi sottonodi. La funzionalità fornita dalla Treeview del Solution Explorer invece collassa solo il nodo selezionato, lasciando invariato lo stato dei suoi sottonodi;  
&#8211;**Copy Class**. Come si può intuire, questo comando copia una intera classe o nodo nella Clipboard, permettendo di incollarla altrove (comando **Paste Class**) dopo averla opportunamente rinominata per evitare errori di compilazione;  
&#8211;**Copy References** (e **Paste References**). Copia una reference o un set di reference nella Clipboard, per poi incollarla altrove;  
&#8211;**Open Containing Folder** (davvero utile). Dal nodo di un progetto o item, apre una finestra di Windows Explorer che punta al path fisico del progetto (o dell&#8217;item) puntato;  
&#8211;**Open Command Prompt,** simile a **Open Containing Folder**, ma apre un prompt dei comandi invece che una finestra di windows explorer;  
&#8211;**Remove and Sort Usings**, altro comando utilissimo, elimina tutti gli using inutili e ordina quelli indispensabili, in un colpo solo, per singola classe o per tutte le classi di un progetto;  
&#8211;**Extract Constant**, dall&#8217;editor di codice, crea la definizione di costante per la stringa selezionata;  
&#8211;**Clear Recent Project List**, elimina la lista degli ultimi progetti aperti, permettendo di selezionarli. 

<a href="http://www.visualstudiogallery.com/ExtensionDetails.aspx?ExtensionID=d467cd03-8393-4172-a25a-7a586577f4fb" target="_blank" rel="noopener">Sticky Notes</a>, fornisce una windows dockable nella quale scrivere appunti, una per ogni file. Funzionalità sinceramente non utilissima perchè è comunque possibile inserire i propri appunti in un file sorgente a mo&#8217; di commento oppure utilizzare la window Task List. L&#8217;unico vantaggio è la possibilità di eliminare i propri appunti in un colpo solo o di inviarli per posta elettronica; 

<a href="http://www.visualstudiogallery.com/ExtensionDetails.aspx?ExtensionID=75453691-dce3-4b02-adf9-de3449ca1a23" target="_blank" rel="noopener">Clone Detective</a>, ho già parlato <a href="http://xplayn.org/cs/blogs/maurizio/archive/2009/03/06/rilevare-codice-duplicato.aspx" target="_blank" rel="noopener">qui</a> di questo tool. Consente di cercare facilmente codice duplicato all&#8217;interno della propria solution. 

<a href="http://www.codeplex.com/ExportAsCodeSnippet" target="_blank" rel="noopener">Export code as Code Snippet</a>, add-in scritto dall&#8217;MVP <a href="http://community.visual-basic.it/Alessandro" target="_blank" rel="noopener">Alessandro Del Sole</a>, consente di esportare facilmente blocchi di codice nel formato .snippet, e quindi riutilizzarli come Snippet Code direttamente attraverso la funzionalità presente nell&#8217;IDE 

<a href="http://www.visualstudiogallery.com/ExtensionDetails.aspx?ExtensionID=0099ed9b-8a69-4cb2-85f8-d996a228c158" target="_blank" rel="noopener">Code Style Enforcer</a>. Questo add-in permette di ottenere segnalazioni evidenti nel proprio codice nel caso in cui siano violate regole di naming e di best practices (visibilità membri e interfacce esplicite o no), configurabili mediante file XML; 

<a href="http://www.techinceptions.com/CodeMetrics.html" target="_blank" rel="noopener">OxyProjectMetrics</a>, estrae informazioni inerenti la metrica del codice e le mostra in un formato tabellare; 

<a href="http://www.codeplex.com/ResourceRefactoring" target="_blank" rel="noopener">ResourceRefactor</a>, estrae la stringa selezionata e cablata nel codice sorgente e la invia ad un apposito file di risorse; 

<a href="http://www.visualstudiogallery.com/ExtensionDetails.aspx?ExtensionID=0aeaaeee-3ef0-48ea-a6a9-af94c8e7c77a" target="_blank" rel="noopener">AutoCode</a>, add-in per automatizzare attività ripetitive di scrittura di codice mediante la creazione di comandi parametrici, come da esempio sotto.   

<a href="http://tytannet.codeplex.com/" target="_blank" rel="noopener">TytanNET</a>, insieme di utili tool windows che incrementano le possibilità di refactoring del codice, e forniscono ulteriori visualizers per il debugging. Decisamente molto utile.

Su Visual Studio Gallery sono presenti decine e decine di altr utili add-in, sia gratuiti che non, per tutte le esigenze.