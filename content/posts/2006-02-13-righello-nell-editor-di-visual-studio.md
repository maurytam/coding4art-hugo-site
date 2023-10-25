---
title: Righello nell’ editor di Visual Studio
author: mtammacco
type: post
date: 2006-02-13T18:51:00+00:00
url: /archive/2006/02/13/righello-nell-editor-di-visual-studio.aspx
categories:
  - Tips and tricks

---
<font face="Tahoma" size="2">Una caratteristica che ogni buon software dovrebbe, a mio avviso, avere riguarda la leggibilità del codice sorgente, intesa nel senso letterale del termine. Leggibilità significa che, quando si legge codice scritto da altri, non si dovrebbe faticare più di tanto a leggerlo &#8220;a colpo d&#8217;occhio&#8221;.<br />Molto spesso però si finisce per fare una gran fatica per comprendere codice magari anche non troppo complesso dal punto di vista della tecnica di programmazione, ma scritto decisamente senza alcuna linea guida.<br />Tra le linee guida minori che, secondo il mio parere, riveste comunque una certa importanza, è da menzionare la lunghezza delle varie linee di codice. Mi riferisco a quelle linee, es dichiarazioni di metodi, di interfacce, ecc., che superano di gran lunga la larghezza di uno schermo a media risoluzione (es. 1024&#215;768) e che costringono ad un lunghissimo scrolling in orizzontale per leggere tutto il contenuto. L&#8217;abitudine a scrivere su una sola riga fisica una istruzione peggiora a mio parere la leggibilità del codice, al pari di scrivere senza conformarsi ad alcuna linea guida.<br />L&#8217;ambiente VS non aiuta certamente, in quanto l&#8217;editor di codice sorgente non fornisce una guida, una specie di righello alla Word per intenderci, in modo da rendere immediatamente percebibile al programmatore che la scrittura sta per superare il margine destro della finestra.<br />Però, attraverso un trick non documentato che comporta una semplice modifica al registro di Windows, è possibile ottenere una linea guida verticale del colore desiderato e posizionata alla colonna desiderata, rendendo la soluzione flessibile alle varie risoluzioni dello schermo.<br />Basta infatti aprire l&#8217;editor del registro ed inserire la chiave &#8220;Guides&#8221; di tipo stringa<br />nella posizione:</font>

<font face="Tahoma" size="2">[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\7.1\Text Editor] </font>

<font face="Tahoma" size="2">attribuendogli ad es. il valore</font>

<font face="Tahoma" size="2">&#8220;RGB(255,0,0) 120&#8221;</font>

<font face="Tahoma" size="2">Come è facile intuire questa chiave crea un righello del colore specificato (in questo caso rosso)<br />alla colonna specificata (120),  all&#8217;interno dell&#8217;editor del codice di Visual Studio.<br />E&#8217; possibile anche creare più di un righello indicando più posizioni di colonna separate da virgola.<br />Questa soluzione funziona con VS 2003. Per VS 2005 occorre creare la chiave alla posizione<br />&#8220;&#8230;\8.0\Text Editor&#8221; invece che 7.1.</font>

<font face="Tahoma" size="2">Se si modifica il Registry mentre VS è in esecuzione occorre riavviarlo affinchè la modifica abbia effetto.</font>