---
title: 'CLR &ndash; Forwarding type'
author: mtammacco
type: post
date: 2010-05-03T00:36:09+00:00
url: /archive/2010/05/03/clr-ndash-forwarding-type.aspx
categories:
  - .NET Framework 4.0

---
Il CLR consente di spostare il codice di una classe da un assembly ad un altro senza  dover ricompilare il codice client che usa la classe in questione.

Questa caratteristica è nota come **Type Forwarding**.

Supponendo di avere la classe **Class1** nell’assembly **Ass1**, se per questioni di refactory del codice sorgente la classe viene spostata nell’assembly **Ass2**, sembrerebbe a prima vista necessario ricompilare anche il codice che referenzia l’assembly **Ass1** per aggiungere una reference all’assembly **Ass2** e modificare la dichiarazione della classe **Class1**.

Tutto ciò non è necessario. Basta decorare l’assembly **Ass1** (la nuova versione, quella priva della classe **Class1**) con l’attributo **TypeForwardedToAttribute**, in questo modo:

<pre class="brush: csharp; title: ; notranslate" title="">[assembly:TypeForwardedToAttribute(typeof(Class1))]
</pre>

Così facendo, il codice client può continuare a referenziare l’assembly **Ass1**, e quindi non è necessaria una sua ricompilazione. Ogni richiesta che l’assembly riceverà per quella classe verrà reindirizzata al nuovo assembly che conterrà la classe stessa.

Ma tutto ciò ha una controindicazione a mio avviso non indifferente: l’assembly **Ass1** che conteneva la classe che ora non contiene più dovrà per forza di cose referenziare l’assembly **Ass2** che ora contiene il tipo.

Inoltre, e qui sarei curiosissimo di conoscere la motivazione, questo attributo non è utilizzabile in **Visual Basic 2005** (e quindi con il **.Net Framework 2.0**). Infatti **Visual Basic 2005** può solo “consumare un forwarded type” scritto in un altro linguaggio.