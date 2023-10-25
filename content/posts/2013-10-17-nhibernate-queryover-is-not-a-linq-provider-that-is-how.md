---
title: NHibernate QueryOver is not a Linq provider (that is how to do join with QueryOver API)
author: mtammacco
type: post
date: 2013-10-17T13:38:44+00:00
url: /archive/2013/10/17/nhibernate-queryover-is-not-a-linq-provider-that-is-how.aspx
categories:
  - .NET Framework 4.0

---
Starting from [NHibernate][1] 3.0 a new API was build as a wrapper around the ICriteria object.

Obviously I’m talking about the powerful API called [QueryOver][2]. With this API you can build a wide range of query object, from the simplest to the more complicated one. But you need to remember that this API is not a Linq provider, and then you cannot apply those constructs typically applied in a Linq query. I explain with an example what I really mean.

Introduction: you have a data model with 2 table, Category and Customer, with a one-to-many relationship between them.

With Entity Framework and Linq To Entities it’s pretty simple to query data that belong to both entities, thanks to navigation properties and Linq provider, i.e. all customers that belong to a category with a specified Id, as shown in this example:

<pre class="brush: csharp; title: ; notranslate" title="">var customerList = customers.Where(c =&gt; c.CategoryId == 1);

</pre>

If you try to execute the same query with the same where conditions applied to a QueryOverObject, like this example:

<pre class="brush: csharp; title: ; notranslate" title="">QueryOver&lt;Customer&gt;; qu = QueryOver.Of&lt;Customer&gt;()
      .Where(c =&gt; c.CategoryId == 1);

</pre>

This code throws a NHibernateException saying that “**could not resolve property: Category.Id of : MyNamespace.Customer**”, suggesting to verify the mapping as property “Category.Id” could not be found”.

Obviously such a property doesn’t exist at all, it’s only the QueryOver API that concatenates the Navigation property and and its field named Id (in this example).

This means that: you cannot make a query with QueryOver API that refers to fields belonging to a navigation property in where clause….without explicitly defying a join between the object itself and its navigation property. An example will help to understand better.

<pre class="brush: csharp; title: ; notranslate" title="">Category cat = null;
QueryOver&lt;Customer&gt; query = QueryOver.Of&lt;Customer&gt;()
 .JoinAlias(x =&gt; x.Category, () =&gt;; cat)
 .Where(x =&gt; cat.Id == 1);
</pre>

I have defined a join with the JoinAlias method, which uses an alias (the Category object declared two rows before) to project the object under the navigation property. After that you can use this alias inside the others method (such as “Where” in this example) to refer to the navigation property field (cat.Id).

As you can see, the way you write the lambda expression inside a Linq provider’s where clause is quite different than the &#8220;”Where” condition of a QueryObject object.

Not even the logical operator “And” can be used in the same way. To apply this logical operator to the “where” filter you have to use the “And” method, as shown here:

<pre class="brush: csharp; title: ; notranslate" title="">Category cat = null;
QueryOver&lt;Customer&gt; query = QueryOver.Of&lt;Customer&gt;()
   .JoinAlias(x =&gt; x.Category, () =&gt; cat)
   .Where(x =&gt; cat.Id == 1)
   .And(x =&gt; cat.IsEnabled);
</pre>

<div id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:eec4448a-c3b5-42c8-bfff-11cf74c71be4" class="wlWriterEditableSmartContent" style="float: none; margin: 0px; display: inline; padding: 0px;">
  Technorati Tags: <a href="http://technorati.com/tags/NHibernate" rel="tag">NHibernate</a>,<a href="http://technorati.com/tags/QueryOver" rel="tag">QueryOver</a>,<a href="http://technorati.com/tags/EntityFramework" rel="tag">EntityFramework</a>,<a href="http://technorati.com/tags/LinqToEntities" rel="tag">LinqToEntities</a>
</div>

 [1]: http://nhforge.org/
 [2]: http://nhforge.org/blogs/nhibernate/archive/2009/12/17/queryover-in-nh-3-0.aspx