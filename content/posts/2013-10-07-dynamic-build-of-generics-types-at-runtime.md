---
title: Dynamic build of generics types at runtime
author: mtammacco
type: post
date: 2013-10-07T09:38:37+00:00
url: /archive/2013/10/07/dynamic-build-of-generics-types-at-runtime.aspx
categories:
  - .NET Framework 4.0
  - 'C# 4.0'

---
How to create dynamically a type in .Net when it’s only known a string representation of that type, I think it’s an operation known to almost all .Net programmers, but what happened with types with type parameters (or generics) ?

In .Net is possible to create dynamically both generics with a known type, i.e. List<>, and generics with type in turn dynamically built.

Here’s an example:

a) Dynamic generated both type parameter and type

<pre class="brush: csharp; title: ; notranslate" title="">Type collectionType = Type.GetType("System.Collections.Generic.List`1, mscorlib");
if (collectionType == "null")
    throw new InvalidOperationException("Invalid type");
Type genericType = Type.GetType("MyNamespace.MyType, MyAssembly");
Type listWithGeneric = collectionType.MakeGenericType(genericType);
var myList = Activator.CreateInstance(listWithGeneric) as IList;
</pre>

b) Dynamic generated type parameter with a known type (System.Collection.Generic.List in this case):

<pre class="brush: csharp; title: ; notranslate" title="">Type genericType = Type.GetType("MyNamespace.MyType, MyAssembly");
Type listWithGeneric = typeof(List&lt;&gt;).MakeGenericType(genericType);
var myList = Activator.CreateInstance(listWithGeneric) as IList;
</pre>

<div id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:1a59f2b2-098b-40f7-9cf4-acde5f4aface" class="wlWriterEditableSmartContent" style="float: none; margin: 0px; display: inline; padding: 0px;">
  Technorati Tags: <a href="http://technorati.com/tags/C%23" rel="tag">C#</a>,<a href="http://technorati.com/tags/Generics" rel="tag">Generics</a>,<a href="http://technorati.com/tags/Type+generation" rel="tag">Type generation</a>
</div>