---
title: 'Visual Basic Tips & Tricks Community Day a Milano'
author: mtammacco
type: post
date: 2010-03-19T16:04:00+00:00
url: /archive/2010/03/19/visual-basic-tips-amp-tricks-community-day-a-milano.aspx
categories:
  - Entity Framework
  - Events and conferences
  - Thoughts

---
Ieri pomeriggio ho partecipato al <a href="http://www.visual-basic.it/" target="_blank" rel="noopener">Visual Basic Tips & Tricks Community Day</a> tenutosi a Milano.

Devo dire che è stato un pomeriggio decisamente interessante dal punto di vista tecnologico, permettendomi di focalizzare alcuni concetti su tecnologie che uso o che vorrei usare, e mi riferisco a TFS 2010 ed Entity Framework 4.0

L’evento si apre con una sessione di <a href="http://www.geniodelmale.info/" target="_blank" rel="noopener">Lorenzo Barbieri</a> che parla delle varie versioni di Visual Studio 2010 che saranno disponibili a breve e delle novità, veramente tante, della nuova versione dell’IDE.

In ordine sparso:

  1. <font face="Lucida Sans Unicode">Possibilità di effettuare ricerche parziali con l’Intellisense;</font> 
  2. Intellisense nei file Javascript migliorato, ora vengono risolti anche i simboli presenti nei files inclusi, e non solo quelli del file in debugging; 
  3. Funzionalità di “**search a you type**”, per intenderci tipo Google quando ci presenta i risultati della ricerca mano a mano che scriviamo il testo da ricercare; 
  4. Funzionalità di “**Call Hierarchy**”, per il momento presente solo con il linguaggio C#, ovvero la possibilità di navigare a partire da un metodo / proprietà / costruttore verso il codice chiamante / chiamato a partire dal punto di navigazione scelto; 
  5. Modalità “**Web only**” dell’IDE, ovvero la possibilità di utilizzare un IDE con il solo codice in primo piano e tutte le finestre di dialogo minimizzate; 
  6. Selezione del testo per colonne; 
  7. Gestione degli add-in con un apposito **Extention Manager** dedicato; 
  8. **Intellitrace** (feature molto molto utile ed interessante per troubleshooting), ovvero un componente capace di registrare tutto quello che avviene nel codice quando questo è in esecuzione, una specie di scatola nera dell’applicazione, utilizzabile su applicazioni scritte con la versione 2.0 del Framework in poi ; 
  9. Test di automazione della UI; 

<font face="Tahoma" /> 

<font face="Tahoma">Poi è stata la volta di <a href="http://community.visual-basic.it/Alessandro/" target="_blank" rel="noopener">Alessandro Del Sole</a>, che ha mostrato le novità di Team Foundation Server 2010 in ottica singolo sviluppatore o piccoli gruppi di lavoro.</font>

<font face="Tahoma">Successivamente <a href="http://community.visual-basic.it/tdj/" target="_blank" rel="noopener">Antonio Catucci</a> ha mostrato le novità di Entity Framework 4.0, ovvero:</font>

  * Possibilità di gestione della **Foreign Key** nel modello dati, senza che la stessa sia nascosta (come è noto nel mondo dei database relazionali una relazione tra 2 tabelle si traduce con la presenza di una colonna in comune tra le due tabelle, che costituisce appunto la relazione, nel mondo OOP una relazione di questo tipo si traduce con la presenza di una proprietà tipizzata nell’oggetto “padre”);
  * “**Lazy Loading**” attivo sempre di default;
  * “**Pluralization**” dell’Entity Set basato sulla grammatica inglese. Con Entity Framework 1.0 questa mancanza mi ha provocato qualche problema, in quanto va gestito a manina;
  * “**Model-First Design**”, feature decisamente interessante che consente di creare un domain model senza che sia necessariamente presente un database da cui partire. Con la versione 1.0 il domain model è forzatamente creato a partire da una base dati esistente;
  * “**T4 Code Generation**”. Con questa feature il codice generato da Entity Framework può essere basato su template, fornendo quindi la possibilità di generazione personalizzata dello stesso.
  * “**POCO Entity (Plain Old CLR Objects**)”, anche questa è una feature molto interessante, ovvero la possibilità di usare nel Domain Model della classi “pulite”, magari già esistenti senza che debbano per forza di cose ereditare da una classe specifica di Entity Framework;
  * Gestiona automatica delle relazioni molti a molti, senza la visualizzazione della terza tabella di legame tra le due relazionate;
  * Nuovo controllo **EntityDataSource** per il binding dei dati in ASP .NET.
  * Metodo “**ApplyCurrentValues**”. Permette di gestire le modifiche apportate su oggetti “detached”, ovvero al di fuori dell’ObjectContext attivo, e di propagare le stesse modifiche sull’oggetto avente la stessa chiave presente nell’ObjectContext (oggetto “attached”).

Come è evidente la versione 4.0 di Entity Framework contiene una pletora di novità, che sicuramente consentiranno a questo ORM made in Microsoft di superare alcuni limiti di “gioventù” della precedente versione.