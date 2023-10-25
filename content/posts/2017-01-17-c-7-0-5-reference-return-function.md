---
title: 'C# 7.0 – #5. reference return function'
author: mtammacco
type: post
date: 2017-01-17T21:35:31+00:00
url: /archive/2017/01/17/c-7-0-5-reference-return-function.aspx
categories:
  - 'C# 7.0'
  - Visual Studio 2017
tags:
  - 'C# 7.0'
  - Visual Studio 2017

---
In addition to function input parameters, which can be passed by value (default) or by reference (with the keyword ref), in C# 7.0 the value return function can also be returned by reference with the same keyword; furthermore it can be stored in a local variable by reference; this local variable stores the memory address of the data and not the value, and then modifiyng this variable means that every variable that points at the same address would be modified too.

Example:

<pre class="brush: csharp; title: ; notranslate" title="">public struct Point
{
   public int X { get; set; }
   public int Y { get; set; }
}

Point[] arr = new[]
{
   new Point {X=12, Y=15 }, new Point {X=56, Y = 754}, 
   new Point {X=65, Y= 39}, new Point {X=21, Y=63}
};

var p = new Point { X = 65, Y = 39 };
ref Point place = ref Find(p, arr);
place.X = 99;
place.Y = 99;    // replaces 3rd Point element in the array
Console.WriteLine("X=" + arr[2].X + " " + "Y=" + arr[2].Y); // prints X=99 Y=99

public ref Point Find(Point p, Point[] points)
{
   for (int i = 0; i &lt; points.Length; i++)
   {
      if (points[i].X == p.X && points[i].Y == p.Y)
      {
         return ref points[i]; // return the storage location, not the value
      }
   }
   throw new IndexOutOfRangeException($"{nameof(p)} not found");
}
</pre>

In this example Point is a structure, and then it is a value type.  
The variable called &#8220;arr&#8221; contains an array (a reference type) of this structure.  
The Find method simply searches a value in that array, but it returns the reference of the Point structure founded, and not its value. You can notice the &#8220;ref&#8221; keyword before the return type and the &#8220;ref&#8221; keyword after the return statement. Then the code stores this reference in a local &#8220;ref&#8221; variable (called &#8220;place&#8221;) containing the reference to the Point structure searched (the third element of the array).  
After that the values are modified (X=99; Y=99), and the array element is modified too, which proves that the memory address has been used instead of the value.