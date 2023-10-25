---
title: Visual studio 2008 ide crash dopo "Choose items" dalla toolbox
author: mtammacco
type: post
date: 2008-09-04T15:54:08+00:00
url: /archive/2008/09/04/visual-studio-2008-ide-crash-dopo-quot-choose-items-quot.aspx
categories:
  - Troubleshooting
  - Visual Studio 2008
  - Workaround

---
Qualche giorno fa mi sono imbattuto in uno strano crash di Visual Studio 2008, dopo aver installato il Service Pack 1, vale a dire che il comando &#8220;Choose items&#8221; della toolbox era capace di mandare in crash l&#8217;intero IDE, scrivendo un laconico messaggio nell&#8217;Event viewer, del tipo

> **NET Runtime version 2.0.50727.3053 &#8211; Fatal Execution Engine Error (7A035E00) (80131506)**

di nessuna utilità per la risoluzione del problema,  senza possibilità di scampo quindi. Dopo aver cercato invano per la rete per evitare di perdere ulteriore tempo ho evitato di disporre del controllo che mi interessava nella toolbox (precisamente una PropertyGrid) e l&#8217;ho inserito direttamente nel markup XAML della mia applicazione (una XBAP application).

Oggi ho letto questo <a href="http://blogs.ugidotnet.org/ddl/archive/2008/09/04/vs2008-sp1---problema-con-quotadd-item.quot-toolbox.aspx" target="_blank" rel="noopener">post</a> di <a href="http://blogs.ugidotnet.org/ddl/Default.aspx" target="_blank" rel="noopener">Nazareno</a> e speravo veramente di risolvere il problema, anche perchè questa volta la toolbox era indispensabile poichè dovevo inserire una intera suite di controlli.

Purtroppo non c&#8217;è stato niente da fare. Il problema sparisce solo dopo aver disinstallato i <a href="http://code.msdn.microsoft.com/PowerCommands/" target="_blank" rel="noopener">Power Commands</a>, senza più reinstallarli.  Ma sono abituato ai Power Commands  e li trovo veramente utili. 

Vale a dire che li disintallerò solo per utilizzare la toolbox, e poi li reinstallerò di nuovo&#8230;:-)