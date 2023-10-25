---
title: Check-list per applicazioni ASP .NET in produzione
author: mtammacco
type: post
date: 2006-09-15T10:22:00+00:00
url: /archive/2006/09/15/check-list-per-applicazioni-asp-net-in-produzione.aspx
categories:
  - ASP .NET

---
Riporto di seguito una lista, in ordine sparso, tratta dalla mia esperienza sul campo dei possibili accorgimenti e/o errori che influiscono sulla scalabilità o sulle performance e che tornano quindi utili quando si trasferisce su di un server di produzione una applicazione ASP .NET complessa con elevato numero di accessi concorrenti:

  * <div>
      Di default il numero di connessioni HTTP concorrenti su uno specifico indirizzo IP e per uno specifico AppDomain è pari a 2. Questo valore è sufficiente ad esempio nel caso di web services che vengono acceduti da un unica applicazione ASP .NET e le cui pagine non effettuano chiamate multiple allo stesso web service. Nell&#8217;ipotesi in cui il servizio web riceve richieste da più applicazioni o dalla stessa applicazione ma con chiamate multiple dalla stessa pagina, questo valore potrebbe causare che il worker thread che esegue la richiesta resti in attesa che si liberi una connessione, causando chiaramente una situazione di contesa delle risorse che porta a problemi di scalabilità e, nel peggiore dei casi. al riciclo dell&#8217;applicazione con esplicito messaggio di errore nel log degli eventi. Il numero delle connessioni può essere applicato per ogni singolo IP richiesto; il valore consigliato da Microsoft nel caso sopra esposto è di 12 * N ( dove N è il numero di CPU disponibili sul server)
    </div>



  * <div>
      Gli assembly usati da più di una applicazione devono essere firmati con strong name e installati in GAC. In questo modo 1 sola copia dell&#8217;assembly è presente in memoria a prescindere dal numero di applicazioni che lo usano; se, al contrario, lo stesso assembly viene installato nella directory bin di ogni applicazione che lo utilizza, esso sarà presente in memoria N volte, una per applicazione, con conseguente spreco di risorse.
    </div>

  * <div>
      Evitare situazioni che possono causare memory-leak. Ciò si verifica quando l&#8217;occupazione di memoria cresce in modo incontrollabile, ad es. perchè esistono oggetti i cui puntatori non possono essere gestiti nel modo corretto, tipico caso applicabile all&#8217;utilizzo di risorse unmanaged, e pertanto la memoria occupata da essi non può essere liberata dal GC ma solo da un riciclo dell&#8217;applicazione o peggio ancora da un riavvio di IIS. Le risorse unmanaged devono essere liberate implementando un distruttore per l&#8217;oggetto che ne fa uso oppure esplicitamente da codice attraverso l&#8217;interfaccia IDisposable. Tra le condizioni che possono provocare un alto utilizzo della memoria e quindi il rischio di memory leak meritano una menzione particolare l&#8217;utilizzo di oggetti del Framework che creano dinamicamente assembly. Ad esempio, se ogni volta che si intende serializzare un oggetto in XML si crea una istanza della classe xmlSerializer utilizzando una particolare versione di overload del suo costruttore, e cioè quella che prevede il passaggio degli extraTypes, per ogni istanza sarà creato un assembly dinamico dietro le quinte. L&#8217;assembly dinamico non potrà essere scaricato dalla memoria se non quando viene scaricato l&#8217;Application Domain che lo contiene. Altre situazioni analoghe a quest&#8217;ultima riguardano l&#8217;uso di RegEx o di xmlTransform. In quest&#8217;ultimo caso il problema è identico in quanto durante una trasformazione XSLT se si utilizzano blocchi di script inline il .NET Framework genera un assembly dinamico che resta in memoria fino al riciclo del processo host.  Maggiori informazioni <a title="" href="http://support.microsoft.com/kb/886385/en-us" target="" name="" rel="noopener">qui</a> e <a title="" href="http://support.microsoft.com/kb/313997/en-us" target="" name="" rel="noopener">qui</a>.
    </div>

  * <div>
      Il riciclo di un application pool avviene di default ogni 1740 minuti, pari a 29 ore. Questo valore non è chiaramente appropriato per tutti gli scenari. Sarebbe a mio avviso preferibile impostare il riciclo ad un&#8217;ora prefissata, magari notturna.
    </div>

  * <div>
      Quando un application pool viene riciclato per un qualsiasi motivo non sempre viene tracciato nel log degli eventi. Per permettere il log degli eventi al verificarsi di determinati eventi occorre modificare il metabase di IIS, impostando la proprietà <strong>LogEventOnRecycle </strong>con il parametro desiderato. A seconda della politica di riciclo impostata sul server di produzione è preferibile settare questo parametro al valore più opportuno per un troubleshooting più efficiente. Maggiori informazioni in questo <a title="" href="http://support.microsoft.com/default.aspx?scid=kb;EN-US;332088" target="" name="" rel="noopener">articolo</a>.
    </div>

  * <div>
      Il riciclo di un processo ASP .NET può avvenire anche al raggiungimento di una certa soglia di memoria occupata dallo stesso (parametro memoryLimit in machine.config o nelle proprietà dell&#8217;applicazione web in IIS6). Questa soglia è impostata di default al 70% di memoria fisica disponibile nel sistema, e andrebbe tarata su misura in base alle proprie esigenze. Da notare che il calcolo percentuale della memoria a disposizione viene influenzato dal parametro webGarden e cpuMask. Quindi, se si imposta il parametro webGarden a true e cpuMask a 4 CPU, la soglia di memoria RAM oltre la quale si scatena il riciclo del processo è 1/4 della percentuale impostata nel parametro memoryLimit, quindi una soglia decisamente bassa che potrebbe far aumentare il numero di ricicli che si verificano.
    </div>

  * <div>
      Il valore dell&#8217;attributo &#8220;debug&#8221; dell&#8217;elemento &#8220;compilation&#8221; nel file di configurazione &#8220;web.config&#8221; deve essere impostato a &#8220;false&#8221; in ambiente di produzione. Per una trattazione dei problemi a cui si può andare incontro lasciando il valore predefinito &#8220;true&#8221; è possibile far riferimento ad un mio precedente <a title="" href="http://www.xplayn.org/cs/blogs/maurizio/archive/2006/04/18/64.aspx" target="" name="" rel="noopener">post</a> sull&#8217;argomento.
    </div>

Chiaramente questa non vuole essere una lista esaustiva circa tutti i possibili scenari a cui si può andare incontro quando si effettua il deployment in produzione di una applicazione web, ma solo una semplice check-list pronta all&#8217;uso che provvederò magari ad aggiornare man mano che entrano in gioco altri fattori.