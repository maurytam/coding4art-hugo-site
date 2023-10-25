---
title: 'C# 7.0 – #7. An improved expression body feature'
author: mtammacco
type: post
date: 2017-01-19T21:57:43+00:00
url: /archive/2017/01/19/c-7-0-7-an-improved-expression-body-feature.aspx
categories:
  - 'C# 7.0'
  - Visual Studio 2017
tags:
  - 'C# 7.0'
  - Visual Studio 2017

---
In C# 6.0 a read-only property like this:

<pre class="brush: csharp; title: ; notranslate" title="">public string SomeProperty
{
    get { return "sometext"; }
}

</pre>

can be rewritten in a more compact way:

<pre class="brush: csharp; title: ; notranslate" title="">public string SomeProperty =&gt; "sometext";
</pre>

This feature is called &#8220;expression body&#8221;, but it has some limitations, e.g. the property is turned into field, it only works with read-only properties and not with constructors, deconstructor, getter, setter and so on.

C# 7.0 add all these constructs and then expands the usage of this feature.

Here&#8217;s an example, which was taken &#8220;as is&#8221; from the <a href="https://blogs.msdn.microsoft.com/dotnet/2016/08/24/whats-new-in-csharp-7-0/" target="_blank" rel="noopener">.Net blog</a> without any test in development environment because by the time of the last released build of <a href="https://w ww.visualstudio.com/vs/visual-studio-2017-rc/" target="_blank" rel="noopener">Visual Studio 2017 (15.0.26020.0)</a> this new feature doesn&#8217;t work yet:

<pre class="brush: csharp; title: ; notranslate" title="">class Person
{
    private static ConcurrentDictionary&lt;int, string&gt; names = new ConcurrentDictionary&lt;int, string&gt;();
    private int id = GetId();

    public Person(string name) =&gt; names.TryAdd(id, name); // constructors

    ~Person() =&gt; names.TryRemove(id, out *);              // destructors
    
    public string Name
    {
        get =&gt; names[id];                                 // getters
        set =&gt; names[id] = value;                         // setters
    }
}
</pre>