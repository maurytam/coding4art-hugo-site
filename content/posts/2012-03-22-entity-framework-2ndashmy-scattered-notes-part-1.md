---
title: 'Entity Framework #2&ndash;my scattered notes Part 1'
author: mtammacco
type: post
date: 2012-03-22T16:05:38+00:00
url: /archive/2012/03/22/entity-framework-2ndashmy-scattered-notes-part-1.aspx
categories:
  - Entity Framework

---
Here are a few scattered notes on the use of Entity Framework 4.2 Code First:

  * The core EF Api is contained in the System.Data.Entity.dll assembly
  * The DbContext Object is a lightweight version of the ObjectContext object, the former provides more functionality than the first. If you need to get an ObjectContext instance starting from a DbContext instance you can use the IObjectContextAdapter interface for casting, as shown in the following example:

<pre class="brush: csharp; title: ; notranslate" title="">(myDbContext as IObjectContextAdapter).ObjectContext;
</pre>

  * The DbSet class is just a wrapper around the ObjectSet class
  * A Complex Type has some limitations, the main are: a) it can expose only properties with primitive types b) it cannot be exposed as a multi-instance (collection)
  * The EntityTypeConfiguration<T> class has an interesting method called WillCascadeOnDelete(bool), whose name makes the idea of the action it takes. Invoking this method with true parameter allows dependent data to be automatically deleted when main data is deleted, but you must pay attention to some aspects: a) it doesn’t work with optional relations but only with required relations b) The dependent data must be explicitly loaded into the context by invoking the “Include” extension method. If you don’t, there are no dependent data in memory and therefore no data will be deleted on database
  * Table splitting requirements: a) entities must have a 1 to 1 relation b) entities must share a common key
  * How a particular class is part of the EF context ? a) Because the context as a property DbSet<T> which reference that class b) Because the class is referenced by another class already tracked by the context c) Because you just inserted a configuration for that class and added to the model builder
  * EF supports three mapping inheritance typologies a) TPH (table per hierarchy) => a base type and all its inherited types are mapped to a single database table with a discriminator column b) TPT (table per type) => There are distinct tables for base type and all its derived types. The tables for derived types contain only the additional fields exposed, while the common fields are mapped to the base type’s table c) TPC (table per concrete type), very similar to TPT. The only difference is that all derived type’s fields are stored in separate tables and not only the common ones. For guidance on which typology to choose depending on various scenarios, you can see this <a href="http://blogs.msdn.com/b/alexj/archive/2009/04/15/tip-12-choosing-an-inheritance-strategy.aspx" target="_blank" rel="noopener">link</a>
  * EF Code First is based on conventions. Conventions are assumptions that can save developers from a lot of work when you define the mapping between domain classes and tables. For example, a convention states that the Id property of a class is also the primary key for that class. Conventions can be singly removed by code, as shown here: