---
title: Invocazione di metodo remoto da Javascript
author: mtammacco
type: post
date: 2009-08-21T10:38:40+00:00
url: /archive/2009/08/21/invocazione-di-metodo-remoto-da-javascript.aspx
categories:
  - ASP .NET 4.0
  - Javascript

---
A partire da ASP .NET 3.5 è possibile da JavaScript richiamare un metodo esterno, implementato nella stessa pagina aspx che invoca il codice Javascript, oppure in un ASP .NET XML Web Services (per intenderci, quello in formato .asmx), oppure in un WCF Services (in formato .svc), tutto questo senza passare attraverso il normale ciclo di vita della pagina, ma invocando semplicemente un metodo pubblico di una classe, visto che la pagina aspx è una classe a tutti gli effetti.

Al metodo è possibile passare dei parametri e ricevere indietro un valore di ritorno, che sarà serializzato / deserializzato in modalità JSON.

Se si ha la necessità di eseguire codice lato server senza passare dall&#8217;intero ciclo di vita della pagine, invocare un metodo pubblico della pagina è sicuramente la soluzione più veloce da implementare, poichè non necessita di creare una applicazione a sè stante (il web service o il WCF Service), e quindi è anche più facile da installare e da manutenere, ma non è esente da limitazioni, la maggiore delle quali è l&#8217;impossibilità di richiamare il metodo pubblico da parte di pagine diverse rispetto a quella in cui lo stesso è dichiarato (in tal caso è necessario creare un servizio web, ASP .NET XML Web Service oppure WCF Service).

Di seguito i passi necessari per richiamare un metodo pubblico esposto dalla classe che genera la pagina aspx, da codice Javascript:

  * E&#8217; necessario creare un metodo pubblico e statico all&#8217;interno della classe che identifica la pagina aspx e decorarlo con l&#8217;attributo System.Web.Services.WebMethodAttribute;

<pre class="brush: csharp; title: ; notranslate" title="">[WebMethod]
public static string GetValueFromServer(string param1, string param2)
{
    return "TEST_RETURN_VALUE";
}
</pre>

  * E&#8217; necessario assegnare True alla proprietà  EnablePageMethods dell&#8217;oggetto ScriptManager ospitato dalla pagina in questione (il valore di default è False), per abilitare l&#8217;invocazione di metodi di pagina;

<pre class="brush: csharp; title: ; notranslate" title="">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" EnablePageMethods="true" /&gt;
</pre>

  * I due passaggi precedenti fanno in modo che nella pagina aspx sia iniettato del codice di script (inline) che permette di richiamare il &#8220;Web Method&#8221;. Questo codice di script comprende essenzialmente un oggetto chiamato &#8220;**PageMethods**&#8220;, il cui nome è hardcoded e quindi non modificabile, avente metodi statici con lo stesso nome dei metodi statici di pagina, mediante cui è possibile richiamare questi ultimi passando gli opportuni parametri, e indicando una funzione di callback che sarà automaticamente richiamata al termine dell&#8217;invocazione del metodo remoto e che conterrà il valore di ritorno di quest&#8217;ultimo, piu un metodo di callback opzionale che sarà automaticamente richiamato in caso di errore del metodo remoto.

<pre class="brush: csharp; title: ; notranslate" title="">function Function1 {
    PageMethods.GetValueFromServer( param1, param2, onSuccessfullCall, onErrorCall);
}
</pre>

  * La funzione di callback richiamata in caso di errore è opzionale. Occorre tener presente che l&#8217;invocazione del metodo remoto è asincrona, quindi il controllo tornerà immediatamente al codice Javascript chiamante. Al termine della invocazione del metodo sarà invocata automaticamente la funzione di callback opportuna (chiamata conlusa con successo o con errore). Nel caso di chiamata conclusa con esito positivo, la funzione di callback conterrà anche il valore di ritorno del metodo remoto invocato.

<pre class="brush: csharp; title: ; notranslate" title="">function onSuccessfullCall(results, userContext, methodName) {
    alert(results);
}
 
function onErrorCall(error, userContext, methodName) {
    if (error !== null)
        alert(error.get_message());
}
</pre>

  * Il parametro results della funzione di callback richiamata in caso di invocazione riuscita conterrà il valore di ritorno del metodo remoto