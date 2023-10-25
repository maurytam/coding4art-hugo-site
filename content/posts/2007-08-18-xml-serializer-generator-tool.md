---
title: XML Serializer Generator Tool
author: mtammacco
type: post
date: 2007-08-18T13:24:00+00:00
url: /archive/2007/08/18/xml-serializer-generator-tool.aspx
categories:
  - .NET Framework 1.0 / 1.1 / 2.0

---
La serializzazione XML in .NET è una operazione onerosa in termini di risorse di sistema a causa della creazione a runtime di un assembly temporaneo contenente funzionalità fortemente tipizzate di &#8220;reader&#8221; e &#8220;writer&#8221; del tipo da serializzare, le quali comportano un utilizzo intensivo di **CodeDom** e **Reflection**. Osservando con il tool Reflector il codice del costruttore della classe **XmlSerializer** (comprendente vari overloads) è possibile notare tutto ciò unito all&#8217;utilizzo del meccanismo di caching dell&#8217;assembly temporaneo creato (sembra però che non tutti gli overloads del costruttore facciano uso della cache con conseguente creazione dell&#8217;assembly ad ogni utilizzo). Questo meccanismo è poco performante sia a causa dell&#8217;utilizzo delle classi di **CodeDom** e **Reflection**, sia per il rischio di creare più assembly temporanei in funzione del numero di classi da serializzare, che resterebbero in memoria fino allo scaricamento del relativo **AppDomain** o fino a che non termina il processo. Tutto ciò si riflette negativamente soprattutto sulle applicazioni lato server, ed a lungo andare potrebbe provocare eccezioni fatali, es. una **OutOfMemoryException**. Per ovviare a questo inconveniente il .NET Framework mette a disposizione il tool a riga di comando **SGEN** (XML Serializer Generator Tool), il quale, lanciato sull&#8217;assembly che contiene i tipi da serializzare, genera un nuovo assembly contenente lo stesso codice che verrebbe generato a runtime con la creazione dell&#8217;assembly temporaneo. In definitiva è anticipata la creazione dell&#8217;assembly, in questo caso non più temporaneo ma definitivo, poichè basta aggiungere un riferimento ad esso, evitando quindi l&#8217;overhead della sua creazione a runtime ed eliminando il rischio di crescita incontrollata delle dimensioni dell&#8217;**AppDomain.**

Tra le opzioni del comando **SGEN:**

**-/compiler** permette di aggiungere qualsiasi opzione da passare al compilatore **C#.** Utile per firmare con strong name l&#8217;assembly da generare. 

**-/keep** permette di eliminare la cancellazione dei files sorgenti dell&#8217;assembly generato. In altre parole lascia i files sorgenti a disposizione dello sviluppatore

-/**proxytypes** genera il codice di serializzazione solo per i tipi proxy di un XML Web Service

-/**reference** permette di specificare eventuali assembly referenziati dalle classi oggetto di serializzazione

-/**type** permette di filtrare i tipi da serializzare che si vogliono includere nell&#8217;assembly da generare

Il comando crea un assembly dal nome <proprio assembly>.XlmSerializers.dll che è possibile aggiungere come riferimento alla propria applicazione.

Naturalmente qualsiasi aggiunta/cancellazione/modifica ai membri pubblici della classe da serializzare necessiterà della ricreazione dell&#8217;assembly attraverso il comando SGEN (la serializzazione XML serializza solo i campi pubblici di una classe, a differenza della serializzazione standard, binaria o SOAP,  che invece serializza anche i campi privati).