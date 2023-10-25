---
title: 'C# 7.0 – #2. Numbers code readability'
author: mtammacco
type: post
date: 2016-12-16T20:32:50+00:00
url: /archive/2016/12/16/c-7-0-2-numbers-code-readability.aspx
categories:
  - 'C# 7.0'
  - Visual Studio 2017
tags:
  - 'C# 7.0'
  - Visual Studio 2017

---
These are some minor but nice improvements regarding numbers code readability:

Now it is possible to write digit separator of number literals:  
The digit separator is the &#8220;_&#8221; character, like in Java language, isn&#8217;t it ?

<pre class="brush: csharp; title: ; notranslate" title="">int number = 1_345_782
Console.WriteLine(number); // prints 1345782
</pre>

This is mostly useful for large numbers.  
The separator is ignored by the compiler; it&#8217;s just used to improve the numbers readability, and it can be placed anywhere inside the number, but only inside, not at beginning or at the end for instance:

<pre class="brush: csharp; title: ; notranslate" title="">// this not compile
int number = _1_345_782
int number = 1_345_782_
</pre>

Strange but true, the separator can be multiple, i.e. you can place more than one separator one beside another:

<pre class="brush: csharp; title: ; notranslate" title="">// this is allowed
int strangeNumber = 1_____2______3______4______5;
</pre>

For decimal number, it cannot be placed right before the separator character:

<pre class="brush: csharp; title: ; notranslate" title="">// this not compile
double numberDouble = 12_.34;
</pre>

Same for type specifier:

<pre class="brush: csharp; title: ; notranslate" title="">// this not compile
float numbewFloat = 12_f;
</pre>

Finally it is available the literal for binary constant values (0b):

<pre class="brush: csharp; title: ; notranslate" title="">int binaryNumber = 0b0100_0010;
Console.WriteLine(binaryNumber); // prints 66
</pre>