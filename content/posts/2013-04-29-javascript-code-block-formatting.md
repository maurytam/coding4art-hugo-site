---
title: Javascript code block formatting
author: mtammacco
type: post
date: 2013-04-29T10:24:20+00:00
url: /archive/2013/04/29/javascript-code-block-formatting.aspx
categories:
  - Javascript
  - Tips and tricks

---
For those who develop applications using C# or Javascript, but I think Java too, (I’m not a Java developer and then I don’t know if what I’m going to say is true for them as well) ,  there are two kind of writing styles for indentation and code’s blocks formatting .

These styles, known as <a href="http://en.wikipedia.org/wiki/Indent_style#K.26R_style" target="_blank" rel="noopener">K&R (Kernighan & Ritchie) style</a> and <a href="http://en.wikipedia.org/wiki/Indent_style#Allman_style" target="_blank" rel="noopener">Allman style</a>, concern the way the opening curly brace is opened, when defining a block of code.

The former places the brace in the same line as the preceding line of code, as you can see in this example:

<pre class="brush: jscript; title: ; notranslate" title="">return {
   name: "Joe"
};
</pre>

the latter places the curly brace in its own line, as shown here:

<pre class="brush: jscript; title: ; notranslate" title="">return
      {
        name: "Joe"
      };
</pre>

So, the question is:

_**Can I use both of these styles or not when writing code ?**_

The answer is: yes, except for Javascript code.

In Javascript you must always use the K&R style if you want to avoid some subtle bugs that may be very difficult to identify.

For example, if you used the code in Allman style showed below

the return value would be &#8220;**undefined**&#8221; and not an object as expected, because the browser insert a semicolon after the word &#8220;return&#8221;.

If the code below had written in K&R (Kernighan & Ritchie) style:

as shown in first example, the return value would have been an object as expected.

<div id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:12e565c0-3037-4ca7-9311-e80f46a98696" class="wlWriterEditableSmartContent" style="float: none; margin: 0px; display: inline; padding: 0px;">
  Tag di Technorati: <a href="http://technorati.com/tags/Javascript" rel="tag">Javascript</a>,<a href="http://technorati.com/tags/programming" rel="tag">programming</a>
</div>