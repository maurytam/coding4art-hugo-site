---
title: 'Snippets code #1 – Extension method to raise an event via reflection'
author: mtammacco
type: post
date: 2011-09-25T20:14:56+00:00
url: /archive/2011/09/25/snippets-code-1-extension-method-to-raise-an-event-via-again.aspx
categories:
  - CodeProject

---
This extension method, applied to the **object** class and then available for all classes, allows to raise any events via reflection, providing as parameters the event name (as a string) and the TEvenArgs generic parameter.



Example of use:

<pre class="brush: csharp; title: ; notranslate" title="">CustomerViewModel vm = new CustomerViewModel();
vm.Raise("PropertyChanged", new PropertyChangedEventArgs("Name"));
</pre>

<a href="http://stackoverflow.com/questions/198543/how-do-i-raise-an-event-via-reflection-in-net-c" target="_blank" rel="noopener">Source for code in this example</a>

<div id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:1c3aed61-de32-4d39-884b-a4be3e1d4956" class="wlWriterEditableSmartContent" style="margin: 0px; display: inline; float: none; padding: 0px;">
  Technorati&#8217;s Tag: <a href="http://technorati.com/tags/Snippet+code" rel="tag">Snippet code</a>,<a href="http://technorati.com/tags/C%23" rel="tag">C#</a>,<a href="http://technorati.com/tags/Generic" rel="tag">Generic</a>,<a href="http://technorati.com/tags/Extension+methods" rel="tag">Extension methods</a>,<a href="http://technorati.com/tags/event" rel="tag">event</a>
</div>