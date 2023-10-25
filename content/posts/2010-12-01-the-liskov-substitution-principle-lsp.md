---
title: The Liskov Substitution Principle (LSP)
author: mtammacco
type: post
date: 2010-12-01T10:59:07+00:00
url: /archive/2010/12/01/the-liskov-substitution-principle-lsp.aspx
categories:
  - SOLID Principles

---
The Liskov Substitution Principle (LSP) is another principle  that has to do with software design and namely with inheritance.

This principle takes its name from <a href="http://en.wikipedia.org/wiki/Barbara_Liskov" target="_blank" rel="noopener">Barbara Liskov</a>, U.S. scientist in computer science.

This principle simply states that

> **_“CLASSES THAT USE REFERENCES TO_** **_BASE_** **_CLASSES MUST BE  ABLE TO USE OBJECTS OF DERIVED CLASSES_** **_WITHOUT KNOWING IT&#8221;_**

In other words, if we have a class (say Class C)  that use a reference to a base class inside (Class B), then Class C MUST be able to use a reference with ANY derivate class of Class B (present and future), without knowing it and especially without changing the logical behaviour.

It &#8216;s very easy to violate this principle when overriding virtual methods defined in a base class.

Let&#8217;s consider an example like this:

<pre class="brush: csharp; title: ; notranslate" title="">public class BaseClass
{
   protected double n1;
   protected double n2;
  
   public BaseClass(double a, double b)
   {
      this.n1 = a;
      this.n2 = b;
   }
  
   public virtual double Multiply()
   {
      return this.n1 * this.n2;
   }
}
 
</pre>

This class simply accepts 2 double numbers by it’s constructor, and by a virtual method returns the two numbers multiplied together.

Now, let’s create a derived class like this:

<pre class="brush: csharp; title: ; notranslate" title="">public class DerivedClass : BaseClass
{
   const double COEFFICIENT = 1.1;

   public DerivedClass(double a, double b)
       : base(a, b) { }

   public override double Multiply()
   {
      return base.Multiply() * COEFFICIENT;
   }
}
 
</pre>

This class is derived by the first one and simply overrides the virtual method “Multiply” defining another implementation of it where the result of the multiplication is further multiplied by a fixed coefficient.

Therefore, having a method that takes a reference to BaseClass, like this:

<pre class="brush: csharp; title: ; notranslate" title="">public double DoSomeWork(BaseClass b)
{
   return b.Multiply();
}

</pre>

we can pass as a parameter any derived class, as in the example below:

<pre class="brush: csharp; title: ; notranslate" title="">BaseClass b = new BaseClass(-5, 20);
double result = DoSomeWork(b);
Console.WriteLine(result);

DerivedClass d= new DerivedClass(-5, 20);
double result2 = DoSomeWork(d);
Console.WriteLine(result2);
 
</pre>

Very trivial, right ? And everything works fine.

But when you develop your derived class and specifically when the virtual method is redefined, you must pay attention to some situations that, if they occur, involving the violation of the Liskov substitution principle. Specifically, a general rule to keep in mind is that a derived class should ***not*** require additional conditions or either provide fewer conditions than those required by the base class.

For example, what would happen if you change the redefinition of the method Multiply in this way  ?

<pre class="brush: csharp; title: ; notranslate" title="">public override double Multiply()
 {
   if (this.n1 &lt; 0)
        throw new InvalidOperationException(
             "Number n1 cannot be negative");
 
    return base.Multiply() * COEFFICIENT;
 }
  
</pre>

The overridden method adds an additional condition, namely that the parameter n1 cannot be negative by raising an exception, and then is demanding something more than its base class that takes two double numbers instead through its constructor, also providing negative numbers. This additional condition required makes the base class and derived class not interchangeable anymore and therefore the Liskov Substitution Principle is violated.

The LSP can be violated in different ways, but everyone has to do with inheritance. Therefore you must take extreme care when you redefine virtual methods.