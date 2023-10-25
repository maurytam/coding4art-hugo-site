---
title: Extentions Methods, come crearli
author: mtammacco
type: post
date: 2008-05-13T11:32:22+00:00
url: /archive/2008/05/13/extentions-methods-come-crearli.aspx
categories:
  - .NET Framework 3.5

---
Una delle più interessanti feature disponibili con la versione 3.5 del .NET Framework sono, a mio avviso, gli Extention Methods, caratteristica legata al linguaggio di programmazione che permette di aggiungere metodi personalizzati a qualsiasi classe/interfaccia del .NET Framework, incluse le classi usate come classi di base (un esempio per tutte: la classe object),  &#8220;estendendo&#8221; appunto il tipo originale. 

In tal modo è possibile estendere il contratto pubblico  esposto dalla classe /interfaccia senza per questo ricorrere all&#8217;ereditarietà. Utilizzando invece quest&#8217;ultima tecnica si era limitati alle solo classi ereditabili (non dichiarate &#8220;sealed&#8221;, come ad esempio la classe System.String), e soprattutto si correva il rischio di compromettere la consistenza dell&#8217;oggetto nel caso in cui facendo l&#8217;override di un metodo ci si dimenticava di richiamare il corrispondente metodo della classe di base.

A volte molti programmatori ricorrono all&#8217;ereditarietà per la semplice esigenza di aggiungere propri metodi ad una classe, non certo per ridefinire il comportamento della classe di base.

Inoltre, l&#8217;Intellisense di Visual Studio fornisce pieno supporto per gli Extention Methods, visualizzandoli correttamente all&#8217;interno del tipo che estendono, con una icona personalizzata.

Guardando i numerosi esempi di &#8220;Extention methods&#8221; disponibili sulla rete ho notato però che questi metodi sono inclusi in una classe avente un namespace custom, esempio Mycomponent.Extentions.StringExtentions per gli extention methods della classe String. Questo è a mio avviso un errore, in quanto così facendo l&#8217;Intellisense di Visual Studio non mostra gli Extention Methods di una certa classe se il relativo namespace non viene importato (cosa ovvia). Questo comportamento sicuramente disorienta, in quanto dato un certo tipo la lista dei suoi metodi visualizzata è parziale.

Quindi, gli Extention Methods di un tipo dovrebbero essere raggruppati un una classe inserita nello stesso namespace del tipo che estendono. Nell&#8217;esempio precedente per estendere la classe System.String la relativa classe statica dovrebbe essere inclusa nel namespace System.

In questo modo, importando un solo namespace sono visibili sia i metodi pubblici che i metodi estesi.

D&#8217;altronde, questo è il comportamento dello stesso Framework. Ad esempio tutti gli Extentions Methods della classe System.Data.DataTable sono racchiusi nella classe DataTableExtentions inserita nel namespace System.Data.