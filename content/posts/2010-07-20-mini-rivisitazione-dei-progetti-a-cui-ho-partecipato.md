---
title: Mini rivisitazione dei progetti a cui ho partecipato
author: mtammacco
type: post
date: 2010-07-20T16:16:00+00:00
url: /archive/2010/07/20/mini-rivisitazione-dei-progetti-a-cui-ho-partecipato.aspx
categories:
  - Thoughts

---
Avendo visto negli ultimi anni un bel pò di applicazioni .Net di ogni tipo, avendo partecipato ad un bel pò di progetti e conseguentemente visto una quantità considerevole di righe di codice, di seguito elenco (in ordine sparso) le mie considerazioni sulla qualità media del codice sorgente da me visionato e su cui spesso e volentieri sono intervenuto in prima persona per correzioni e/o nuove funzionalità (leggasi elenco di brutture e/o coding horror):

&#8211; La visibilità delle classi è una questione non tenuta nella giusta considerazione. Quando si crea una classe la si marca come &#8220;public&#8221;, e tale resta per sempre, anche se la classe potrebbe essere &#8220;internal&#8221;;

&#8211; il paradigma &#8220;[Object Oriented Programming][1]&#8221; è scarsamente applicato, ed anche scarsamente conosciuto, e cosi si finisce spesso per avere, solo a titolò di esempio, codice duplicato, scarsamente coeso e altamente accoppiato;

&#8211; [Boxing e unboxing][2]: concetto non conosciuto dai più, e cosi accade che il tipo &#8220;object&#8221; è usato a sproposito, e la tipizzazione dei dati diventa una rarità;

&#8211; Concatenazioni di stringhe a go-gò, anche se è arcinoto che questa operazione non è performante a causa dell&#8217;immutabilità dell&#8217;oggetto stringa che &#8220;stressa&#8221; parecchio il garbage collector;

&#8211; Utilizzo delle eccezioni nella logica di business dell&#8217;applicazione per notificare situazioni particolari;

&#8211; Utilizzo indiscriminato di Dataset/Datatable in ogni layer applicativo (front-end compreso), al posto di oggetti di dominio non anemici, cioè dotati di attributi e di comportamento (sì lo so, chiedo forse troppo, questo è [Domain Driven Design][3]&#8230;), con conseguente profilerazione di classi per la gestione delle entità trattate dalla applicazione, es. CustomerManager, OrderManager, ecc.  
Su questo argomento potrei aprire una lunga discussione, circa colui che io definisco &#8220;il programmatore del dataset&#8221;;

&#8211; La modularità di una applicazione e il concetto di [&#8220;Separation of Concern&#8221; (Soc)][4]  non attira l&#8217;interesse della maggior parte degli addetti ai lavori. Come già discusso [qui][5], è più importante rispettare i termini di consegna puttosto che creare software di qualità, ed ecco che si finiisce per scrivere software quasi monolitici, dove le responsabilità si &#8220;accavallano&#8221; in modo netto ed evidente tra i vari moduli. In applicazioni ASP .Net il code-behind si è spesso rivelato una trappola, nel senso che la classe &#8220;pagina&#8221; contiene una quantità spropositata di codice, ad esempio negli event handlers, alla faccia del concetto di basso accoppiamento;

&#8211; Assenza di Unit Test, non nel senso che nessuno li scrive ma nel senso che il [Test Driven Development][6] per molti è una sigla non pienamente compresa; in quei pochi scenari in cui ho visto scrivere Unit Tests questi non erano mai strutturati nel modo corretto secondo lo schema **_arrange-act-assert_** ma erano per lo più invocazioni di metodi a scopo di debugging. In pratica, più che &#8220;Sviluppo guidato dal test&#8221; ho visto l&#8217;esatto opposto.

Fortunatamente ho anche visto codice scritto benissimo, bene, o almeno in modo decente

 [1]: http://it.wikipedia.org/wiki/Programmazione_orientata_agli_oggetti
 [2]: http://msdn.microsoft.com/it-it/library/yz2be5wk(VS.80).aspx
 [3]: http://domaindrivendesign.org/resources/what_is_ddd
 [4]: http://en.wikipedia.org/wiki/Separation_of_concerns
 [5]: http://www.coding4art.com/archive/2010/07/09/settore-ingegneristico-o-artigianale.aspx
 [6]: http://www.agiledata.org/essays/tdd.html