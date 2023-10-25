---
title: 'C# 7.0 – #6. Usage expanded for statement  “throw”'
author: mtammacco
type: post
date: 2017-01-18T22:16:49+00:00
url: /archive/2017/01/18/c-7-0-6-usage-expanded-for-statement-throw.aspx
categories:
  - 'C# 7.0'
  - Visual Studio 2017
tags:
  - 'C# 7.0'
  - Visual Studio 2017

---
Until C# 6.0 the &#8220;throw&#8221; keyword must be used only as a standalone statement, that is it cannot be part of an expression. C# 7.0 overcomes this limitation, and then allows this keyword to be placed everywhere, e.g. in the middle of a ternary operator:

<pre class="brush: csharp; title: ; notranslate" title="">string  a = null;
try
{
    // this row doesn't compile in C# 6.0 because of throw statement
    a = a !=  null ? a = " some value" : throw new NullReferenceException("a");
}
catch (Exception ex)
{
    a = "some other value";
    Console.WriteLine("New throw feature: " + a);  // prints "some other value"
}
</pre>