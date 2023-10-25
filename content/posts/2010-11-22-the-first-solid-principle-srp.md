---
title: 'The first Solid principle: SRP'
author: mtammacco
type: post
date: 2010-11-22T13:15:00+00:00
url: /archive/2010/11/22/the-first-solid-principle-srp.aspx
categories:
  - SOLID Principles

---
Some of the principles about the object oriented programming (**OOD**) deal with design.

This design principles are known with the acronym of **SOLID**.

**SOLID** stands for:

(**S**)ingle Responsibility principle;  
(**O**)pen closed principle;  
(**L**)iskov substitution principle;  
(**I**)nterface segregation principle;  
(**D**)ipendency inversion principle

In my opinion, these principles are very important to understand if we are to achieve the greatest benefits of OOP.

In this post, I&#8217;ll speak about the first of these principles, i.e. the **Single Responsibility Principle (SRP).  
** In future posts, I hope, I&#8217;ll speak about the others.

The **SRP** is perhaps the easiest to understand and the easier to violate.  
This principle states that a class should have one and only one reason to change (responsibility).  
One responsibility is associated with a potential reason for change the code of a class. So, if a class has more than 1 responsibility, also has more than 1 reason for change, and then the class violates the SRP.

For example, consider a interface like this, which is implemented by a hypothetical class that manages documents:

<pre class="brush: csharp; title: ; notranslate" title="">public interface IDocument
 {
    Document LoadDocument(int id)
    void SaveDocument(Document document)
    decimal GetTotalDocument(int id);
}
</pre>

What&#8217;s wrong with this simple code ?

Apparently nothing, but in terms of design this class violates the **SRP**, because the first two methods having to do with the persistence, while the third returns the result of a state variable according to a specific business rule, and then has to do with business rules. Thus, this hypothetical class may change if we change repository of persistence and /or if we change the business rules, and thus violates the SRP.

A better approach is to split this class into 2 separate classes, one for each responsibility, i.e.:

<pre class="brush: csharp; title: ; notranslate" title="">public interface IDocumentPersistence
 {
     Document LoadDocument(int id)
     void SaveDocument(Document document)
 }
 
 public interface IDocumentRules
 {
     decimal GetTotalDocument(int id);
 }
 
</pre>

The application of this principle maximizes the cohesion between the various parts of an application and minimizes the coupling between the same parts.

In the previous example the two interfaces are likely to be called from different parts of an application and are also subject to change for different reasons, so it is proper to keep them separate.