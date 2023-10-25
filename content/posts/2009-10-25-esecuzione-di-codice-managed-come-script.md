---
title: Esecuzione di codice managed come script
author: mtammacco
type: post
date: 2009-10-25T23:38:33+00:00
url: /archive/2009/10/25/esecuzione-di-codice-managed-come-script.aspx
categories:
  - Technical articles

---
La classe System.CodeDom.Compiler.CodeDomProvider è una classe astratta dalla quale derivano classi specifiche utilizzate dal .NET Framework per implementare i compilatori dei vari linguaggi da esso supportati. Il compilatore del linguaggio C#, ad esempio, è basato sulla classe Microsoft.CSharp.CSharpCodeProvider che eredita dalla classe astratta CodeDomProvider e permette di accedere ad una istanza del compilatore C# per la gestione del codice sorgente in detto linguaggio, così come il compilatore del linguaggio Visual Basic .NET è basato sulla classe Microsoft.VisualBasic.VBCodeProvider. Utilizzando tali classi è possibile compilare il codice sorgente, proveniente ad esempio da un file di script, per generare ed eseguire codice managed direttamente in memoria oppure creando un assembly. Ciò si rileva molto utile quando è necessario provare il funzionamento di porzioni di codice sorgente senza dover creare una soluzione da salvare su disco, come ad esempio accade se si utilizza l&#8217;ambiente Visual Studio .NET, oppure per fornire ad una applicazione la possibilità di integrazioni software da implementare a livello di scripting. Il primo passaggio consiste nel creare una istanza del compilatore C# oppure VB .NET rispettivamente attraverso la classe CSharpCodeProvider e VBCodeProvider, e di ottenere quindi un oggetto ICodeCompiler che rappresenta una interfaccia la cui implementazione da parte dello specifico compilatore permette di compilare dinamicamente il codice sorgente. E&#8217; opportuno inoltre creare una istanza della classe CompilerParameters per impostare le opzioni di compilazione appropriate.

**C#**



**VB .NET**



Alcune di queste opzioni permettono ad esempio di generare un eseguibile oppure una dll, di includere i simboli di debug, di creare un assembly in memoria o di produrre un file su disco (in questo caso è possibile assegnare un nome specifico al file attraverso la proprietà OutputAssembly). Una proprietà importante della classe CompilersParameters è ReferencedAssemblies, ovvero un oggetto di tipo collezione contenente la lista degli assemblies impostati come riferimento dell&#8217;assembly in compilazione. Occorre prevedere almeno gli assembly di uso più comune, altrimenti l&#8217;utilizzo di una classe senza il riferimento all&#8217;assembly che la contiene produce un errore. 

**C#**



**VB .NET**



A questo punto è possibile leggere il codice sorgente da compilare, tipicamente da un file di testo, e costruire l&#8217;entry point dell&#8217;assembly insieme al metodo Main che sarà invocato dinamicamente: 

**C#**



**VB .NET**



Per compilare il codice è necessario invocare il metodo CompileAssemblyFromSource esposto dall'interfaccia ICodeCompiler passandogli l'oggetto CompParameters creato in precedenza e la stringa contenente il codice. Questo metodo restituisce un oggetto CompilerResults che permette di verificare se la compilazione ha prodotto errori o avvertimenti mediante la collection Errors, la quale espone proprietà per individuare la riga e la colonna contenente l'istruzione che ha prodotto l'errore, il numero dell'errore stesso e la sua descrizione, oltre alla proprietà HasErrors che consente immediatamente di verificare se è presente almeno un errore: 

**C#**



**VB .NET**



Nel caso di compilazione terminata correttamente si effettua un ciclo sui tipi che appartengono all'assembly appena compilato e si ricava un riferimento al tipo "scripter" che costituisce l'entry point dell'assembly e, mediante l'uso di Reflection, si invoca dinamicamente il metodo Main: 

**C#**



**VB.NET**



Infine, è possibile registrare nel sistema l'applicazione impostando una particolare estensione di file, ad esempio "cssc" per indicare uno script in linguaggio C#, oppure "vbsc" per uno script in Visual Basic .NET. In tal modo attraverso un semplice doppio click sul file con tale estensione sarà eseguito il codice in esso contenuto, in modo simile ad un file di script Visual Basic.