---
title: 'C# 7.0 – #3. New Tuple value type'
author: mtammacco
type: post
date: 2016-12-19T20:16:21+00:00
url: /archive/2016/12/19/c-7-0-3-new-tuple-value-type.aspx
categories:
  - 'C# 7.0'
  - Visual Studio 2017
tags:
  - 'C# 7.0'
  - Visual Studio 2017

---
First of all, at least for C# 7.0 included in [Visual Studio 2017 RC][1], it needs to download the [System.ValueTuple Nuget Package][2], providing the System.ValueTuple structs, which implement the underlying types for C# 7 tuples.

In C# 6.0 after invoking an appropriate Tuple object constructor, the object magically contains a series of properties named Item1, Item2 and so on, one for each type parameter.  
There wasn&#8217;t an easy way to rename the property names with most significant one.  
The best way to accomplish this is to create a custom class that inherits from System.Tuple and then expose the Items properties with significant names.

C# 7.0 comes with a much better Tuple object. First of all it is a value type, then it performs faster (reference type can still be used).

A Tuple variable, known as Tuple literal, containing multiple values each of which may have its own data type:

<pre class="brush: csharp; title: ; notranslate" title="">var axes = ("Axis X", "Axis Y", "Axis Z");
Console.WriteLine("Axes are: {0}, {1} and {2} ", axes.Item1, axes.Item2, axes.Item3);
Console.WriteLine($"Axes are: {axes.Item1}, {axes.Item2}, {axes.Item3}");
</pre>

Members type are automatically inferred by the compiler, in the above example are string, string, string. Furthermore, it&#8217;s possible to override the default named Tuple public properties ItemX

<pre class="brush: csharp; title: ; notranslate" title="">var points = (x: 100, y: 20, z: 50);
Console.WriteLine("Points are : {0} , {1}, {2} ", points.x, points.y, points.z);
</pre>

And different data types are also possible:

<pre class="brush: csharp; title: ; notranslate" title="">var customerInfo = ("Joe Doe", 10, false); //(string,int,bool)
Console.WriteLine("Customer information: Name: {0}, Discount: {1}, IsProspect: {2} ", customerInfo.Item1, customerInfo.Item2, customerInfo.Item3);
</pre>

A Tuple member may be a reference type:

<pre class="brush: csharp; title: ; notranslate" title="">var customerInformation = (customer: new Customer { FirstName = "Foo", LastName = "Bar" }, Id: 1 );
Console.WriteLine("Customer details are - Id: {0}, First Name: {1}, Last Name: {2}", customerInformation.Id, customerInformation.customer.FirstName, customerInformation.customer.LastName);

public class Customer
{
   public string FirstName { get; set; }
   public string LastName { get; set; }
}
</pre>

A function may return a Tuple literal:

<pre class="brush: csharp; title: ; notranslate" title="">(string description, double x, double y, double z) GetMultipleValues()
{
   return ("Short description", 100D, 120D, 140D);
}
</pre>

In this case the funcion gets called in this way:

<pre class="brush: csharp; title: ; notranslate" title="">var values = GetMultipleValues();
Console.WriteLine("Values are: string value={0}, first double value={1}, second double value={2}, third double value={3}", values.Item1, values.Item2, values.Item3, values.Item4);
</pre>

The return statement in the above function may contain the explicit name of each field:

<pre class="brush: csharp; title: ; notranslate" title="">return (description: "Short description", x: 100D, y: 120D, z: 140D);
</pre>

So in this way the function would get called:

<pre class="brush: csharp; title: ; notranslate" title="">var values = GetMultipleValues();
Console.WriteLine("Values are: string value={0}, first double value={1}, second double value={2}, "third double value={3}", values.description, values.x, values.y, values.z);
</pre>

 [1]: https://www.visualstudio.com/vs/visual-studio-2017-rc/
 [2]: https://www.nuget.org/packages/System.ValueTuple