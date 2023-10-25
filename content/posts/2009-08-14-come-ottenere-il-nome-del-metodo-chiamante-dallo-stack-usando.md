---
title: Come ottenere il nome del metodo chiamante dallo stack usando reflection
author: mtammacco
type: post
date: 2009-08-14T05:41:14+00:00
url: /archive/2009/08/14/come-ottenere-il-nome-del-metodo-chiamante-dallo-stack-usando.aspx
categories:
  - .NET Framework 3.5
  - Tips and tricks

---
Cosi:

<pre class="brush: csharp; title: ; notranslate" title="">using System.Diagnostics;
void Log(string eventMessage)
{ 
   Console.WriteLine("Event logged by " + (new StackTrace()).GetFrame(1).GetMethod().Name); 
   Console.WriteLine("Event: " + eventMessage);
}
</pre>

Fonte: <a href="http://blogs.msdn.com/webdevelopertips/archive/2009/06/23/tip-83-did-you-know-you-can-get-the-name-of-the-calling-method-from-the-stack-using-reflection.aspx" target="_blank" rel="noopener">Tips & Tricks for ASP.NET, IIS, and Visual Web Developer</a>