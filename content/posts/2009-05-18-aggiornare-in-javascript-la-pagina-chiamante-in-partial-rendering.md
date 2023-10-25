---
title: Aggiornare in JavaScript la pagina chiamante in partial-rendering
author: mtammacco
type: post
date: 2009-05-18T05:51:27+00:00
url: /archive/2009/05/18/aggiornare-in-javascript-la-pagina-chiamante-in-partial-rendering.aspx
categories:
  - Javascript

---
Mediante JavaScript è possibile eseguire programmaticamente un post della pagina mediante il richiamo della funzione

<pre class="brush: jscript; title: ; notranslate" title="">__doPostBack( 'EventName', 'EventArgs' );
</pre>

In questo caso il post generato è sincrono, ma, come ben spiegato in questo <a href="http://bloggingabout.net/blogs/mveken/archive/2008/01/02/performing-async-postback-from-javascript.aspx" target="_blank" rel="noopener">post</a>, è anche possibile effettuarlo asincrono mediante l&#8217;utilizzo di un array della classe PageRequestmanager, in questo modo:

<pre class="brush: jscript; title: ; notranslate" title="">function doPostBackAsync( eventTargetName, eventArgs )
{
     var prm = Sys.WebForms.PageRequestManager.getInstance();
     if( !Array.contains( prm._asyncPostBackControlIDs, eventTargetName) )
     {
         prm._asyncPostBackControlIDs.push(eventTargetName);
     }
     if( !Array.contains( prm._asyncPostBackControlClientIDs, eventTargetName) )   
     {
         prm._asyncPostBackControlClientIDs.push(eventTargetName);
     }

    __doPostBack( eventTargetName, eventArgs );    
}
</pre>

Mediante poi l&#8217;utilizzo dell&#8217;UpdatePanel otteniamo che a livello programmatico (quindi senza necessariamente l&#8217;interazione dell&#8217;utente mediante un controllo), possiamo generare un post asincrono con refresh parziale della pagina, mediante il richiamo esplicito della funzione di cui sopra.

Inoltre, poichè in Javascript è anche possibile, richiamare esplicitamente una funzione definita dall&#8217;utente in una pagina mentre ci si trova in un altra pagina (esempio popup), mediante il seguente costrutto:

<pre class="brush: jscript; title: ; notranslate" title="">window.opener.nomeFunzioneCustom(parametri); 
</pre>

otteniamo che, stando un una pagina secondaria come un popup, riusciamo ad aggiornare con il partial rendering la pagina chiamante.