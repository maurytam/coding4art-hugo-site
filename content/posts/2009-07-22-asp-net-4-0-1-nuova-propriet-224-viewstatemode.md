---
title: 'ASP .NET 4.0 #1 Nuova proprietà ViewStateMode'
author: mtammacco
type: post
date: 2009-07-22T05:10:20+00:00
url: /archive/2009/07/22/asp-net-4-0-1-nuova-propriet-224-viewstatemode.aspx
categories:
  - ASP .NET 4.0

---
Per una applicazione ASP .NET soprattutto di livello enterprise la gestione del viewstate è sempre stato uno degli aspetti più delicati e, aggiungo io, più bistrattati in assoluto. Spesso e volentieri ho visto applicazioni di una certa complessità che ignorano completamente questo aspetto, che si traduce in pratica nell&#8217;utilizzo del valore di default della proprietà EnableViewState dei controlli di pagina (ovvero True), con conseguente saltataggio dei valori dello stato per tutti i controlli, a prescindere se questo salvataggio ha senso oppure no.

Anzi, spesso ho addirittura visto un utilizzo del ViewState a mò di Session, ovvero ho visto salvare informazioni aggiuntive rispetto allo stato dei controlli, e non parlo di tipi primitivi ma di veri e propri oggetti complessi, la cui serializzazione nel markup html provoca inevitabilmente un incremento notevole del peso della pagina web, con conseguenze facilmente immaginabili.

Con la prossima uscita della versione 4.0 di ASP .NET, lo sviluppatore avrà un controllo più fine sull&#8217;utilizzo del ViewState, soprattutto potrà impostare il valore di default desiderato in funzione della pagina che lo utilizza. Infatti, ogni server control (e quindi anche la classe Page) avrà a disposizione la proprietà ViewStateMode che potrà permettere ai controlli child situati all&#8217;interno di un contenitore (e quindi a tutti i controlli della pagina se guardiamo il livello più alto della gerarchia dei controlli), di ereditare la modalità di utilizzo dal rispettivo controllo container (valore _**Inherit**_), oppure di abilitare (**_Enabled_**) o disabilitare (valore **_Disabled_**) esplicitamente il Viewstate per un singolo controllo a prescindere dal valore impostato nel container.

Poichè il valore di default di questa nuova proprietà è **_Inherit_**, significa che a livello di pagina nessun controllo avrà il ViewState abilitato se non esplicitamente impostato dal programmatore.

Secondo me è un buon passo avanti verso la scrittura di applicazioni più efficienti.