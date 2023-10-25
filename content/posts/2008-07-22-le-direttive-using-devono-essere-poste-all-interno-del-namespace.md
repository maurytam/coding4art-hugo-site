---
title: Le direttive using devono essere poste all’interno del namespace
author: mtammacco
type: post
date: 2008-07-22T08:59:42+00:00
url: /archive/2008/07/22/le-direttive-using-devono-essere-poste-all-interno-del-namespace.aspx
categories:
  - .NET Framework 3.5
  - Thoughts
  - Tools
  - Visual Studio 2008

---
Questo post inizia con una frase tratta da un <a href="http://www.hanselman.com/blog/BackToBasicsDoNamespaceUsingDirectivesAffectAssemblyLoading.aspx" target="_blank" rel="noopener">post</a> di <a href="http://www.hanselman.com/blog/" target="_blank" rel="noopener">Scott Hanselmann</a> con cui mi trovo completamente d&#8217;accordo:

> <p style="text-align: center;">
>   <em>Don&#8217;t believe everything you read, even on a Microsoft Blog.              </em>
> </p>
> 
> <p style="text-align: center;">
>   <em>Don&#8217;t believe this blog, either!</em>
> </p>
> 
> <p style="text-align: center;">
>   <em>Decide  for yourself with experiments if you need a tiebreaker!</em>
> </p>

Credo sia proprio vero, mai fidarsi ciecamente di quello che si legge in giro, soprattutto quando seri dubbi farebbero pensare il contrario.

Il motivo è presto detto: utilizzo normalmente **FxCop** come strumento di analisi del codice sorgente, lo trovo molto completo e ben fatto. Spinto dalla curiosità ho voluto utilizzare **Source Analysis**, un tool gratuito fornito da Microsoft ed integrato nell&#8217;IDE di Visual Studio. Dopo la primissima prova fatta mi ha incuriosito una sua segnalazione:

**<span style="font-size: medium;">SA1200 &#8211; All using directives must be placed inside of the namaspace.</span>**

Per farla breve, tutti i files sorgenti del mio progetto provocavano una segnalazione di questo tipo poichè le direttive using erano poste esternamente alla definizione del namespace, così come automaticamente viene creato uno scheletro di una classe all&#8217;interno dell&#8217;IDE. La segnalazione in questione invita invece ad includere le direttive using all&#8217;interno della definizione del namespace, semprecchè sia presente. Facendo qualche ricerca in giro ho scoperto che in questo modo il compilatore segnala immediatamente una eventuale ambiguità tra i nomi dei tipi creati all&#8217;interno del proprio namespace e i tipi presenti nei vari namespace del .NET Framework. E fin qui nulla di strano.

Ho scoperto inoltre che questa guideline servirebbe anche ad aumentare le prestazioni, almeno nei casi specifici, in quanto forzarebbe il &#8220;lazy loading&#8221; degli assembly e non il caricamento immediato. In altre parole, quando il viene invocato un metodo di una classe e viene compilato il codice &#8220;just in time&#8221; (JITTED) il lazy loading permette di caricare in memoria solo gli assembly referenziati che servono all&#8217;invocazione del metodo stesso, e non tutti gli assembly referenziati da una classe, a prescindere se utilizzati o no da una specifica invocazione di un metodo. Questo permette di caricare solo lo stretto necessario anche se una classe referenzia un assemby non utilizzato da un metodo.

Sinceramente non mi è venuto in mente un solo valido motivo per cui una direttiva using posta in un certo modo potesse influenzare l&#8217;attività del CRL a runtime, e sono rimasto alquanto dubbioso sulla effettiva validità. Prima che potessi avere il tempo di fare una prova specifica mi son trovato questo <a href="http://www.hanselman.com/blog/BackToBasicsDoNamespaceUsingDirectivesAffectAssemblyLoading.aspx" target="_blank" rel="noopener">post</a> di <a href="http://www.hanselman.com/blog/" target="_blank" rel="noopener">Scott Hanselmann</a>, al quale rimando per una esauriente spiegazione, che dimostra come purtroppo ciò non sia affatto vero, cioè gli assembly referenziati vengono caricati tutti i memoria immediatamente, a prescindere se il metodo in questione li usa oppure no, ed a prescindere se le direttive using vengono poste all&#8217;interno o all&#8217;esterno della definizione di namespace.

Quindi la morale è: non credere mai a quello che leggi, neanche se lo leggi da questo blog :), ma sperimenta sempre.