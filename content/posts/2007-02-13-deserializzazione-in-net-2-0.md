---
title: Deserializzazione in .NET 2.0
author: mtammacco
type: post
date: 2007-02-13T18:55:00+00:00
url: /archive/2007/02/13/deserializzazione-in-net-2-0.aspx
categories:
  - .NET Framework 1.0 / 1.1 / 2.0

---
<font face="Verdana" size="2" />

Il meccanismo di deserializzazione ha subito una modifica (a mio avviso migliorativa) in .NET 2.0 rispetto a quanto avveniva in .NET 1.1. La versione 2.0 ha la capacità di deserializzare un oggetto anche se questo presenta nella sua forma serializzata informazioni aggiuntive (es. membri pubblici) non presenti invece nella particolare versione dell&#8217;oggetto che  stiamo deserializzando. Mi spiego meglio. Supponiamo che abbiamo la nostra onnipresente classe Person con 3 campi pubblici, ovvero FirstName, LastName e Age, e che alcune istanze di questa classe siano serializzate in formato binario attraverso l&#8217;uso della classe BinaryFormatter utilizzando una applicazione scritta in .NET 2.0, e che il risultato della serializzazione sia memorizzato nel file BinaryPerson.dat. Un&#8217;altra applicazione, questa volta scritta in .NET 1.1, deserializza gli oggetti Person contenuti nel file binario, utilizzando però una vecchia versione dell&#8217;oggetto Person contenente solo 2 campi pubblici e non 3 (es. FirstName e LastName). In tale scenario il Framework 1.1 quando esegue il metodo Deserialize solleva una eccezione e precisamente:

_An unhandled exception of type &#8216;System.Runtime.Serialization.SerializationException&#8217; occurred in mscorlib.dll_

_Additional information: È possibile che la versione non corrisponda. Il tipo Person ha 2 membri, di cui 3 deserializzati._

<font face="Verdana" size="2"></p> 

<p>
  In pratica in .NET 1.1 non è possibile deserializzare un oggetto (Person, nell&#8217;esempio) se lo stesso è serializzato con un numero eccedente di membri. Questo comportamento è cambiato in .NET 2.0, in quanto tutti i membri eccedenti riscontrati sono ignorati e nessuna eccezione viene sollevata.
</p>

<p>
  Per completezza, nel caso di uno scenario esattamente opposto a quello descritto, cioè l&#8217;applicazione A serializza l&#8217;oggetto Person con 3 campi e l&#8217;applicazione B cerca di deserializzarlo mentre nel frattempo all&#8217;oggetto Person è stato aggiunto il quarto campo, si avrà sempre una eccezione a prescindere dalla versione del Framework utilizzata, tranne se il campo appena aggiunto viene decorato con l&#8217;attributo <em>OptionalField</em>. Il tal caso il nuovo campo è deserializzato con il valore <em>null</em> impostato.
</p>

<p>
  </font>
</p>