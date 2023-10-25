---
title: 'L&rsquo;evento page load &egrave; eseguito 2 volte'
author: mtammacco
type: post
date: 2009-11-15T05:17:00+00:00
url: /archive/2009/11/15/lrsquoevento-page-load-egrave-eseguito-2-volte.aspx
categories:
  - ASP .NET
  - Troubleshooting

---
Convertire un progetto ASP .NET dalla versione 1.1 ad una versione successiva del .NET Framework nasconde un inconveniente a cui occorre porre rimedio manualmente.

L&#8217;inconveniente è dovuto alla introduzione delle partial class a partire dalla versione 2.0 del .NET Framework, in contrapposizione al codice generato dal designer nella versione 1.1.

Questo fa si che importando il codice sorgente nella nuova versione utilizzata ci si ritrovi, ad esempio, con un event handler come questo nel metodo InitializeComponent

<pre class="brush: csharp; title: ; notranslate" title="">private void InitializeComponent() 
 { 
     this.Load += new System.EventHandler(this.Page_Load); 
 }
</pre>

Questo innocente codice derivante dalla conversione fa in modo che l&#8217;evento Page Load sia generato 2 volte, una volta dall&#8217;handler presente nella partial class ed una volta da quello presente nel metodo InitalizeComponent.

Per eliminare questo fastidioso inconveniente è sufficiente rimuovere l&#8217;handler presente nel metodo InitializeComponent