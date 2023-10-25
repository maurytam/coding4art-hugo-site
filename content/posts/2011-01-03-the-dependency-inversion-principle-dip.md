---
title: The Dependency Inversion Principle (DIP)
author: mtammacco
type: post
date: 2011-01-03T16:47:01+00:00
url: /archive/2011/01/03/the-dependency-inversion-principle-dip.aspx
categories:
  - SOLID Principles

---
The last of SOLID principles about OOD is known as Dependency Inversion Principle (DIP).

This principle says that:

> &nbsp;
> 
> _**High-level modules should not depend on low-level modules. Both should depend on abstractions.**_ _**Abstractions should not depend upon details. Details should depend upon abstractions.**_
> 
> &nbsp;

This principle, with the <a href="http://www.coding4art.com/archive/2010/11/26/the-second-solid-principle-ocp.aspx" target="_blank" rel="noopener"><span style="color: #0066cc;">OCP principle</span></a> already discussed, are intended to make software application loosely coupled. This feature is achieved by removing as much as possible dependencies between higher level modules (those usually more general) and the low-level modules (those usually more specific). In fact, usually in conventional application architecture, the high level modules use the functionality exposed by low-level modules using direct references to the latter, thus creating a strong coupling between them.

This coupling results in any change of low-level modules, also lead inevitably change of high-level, and this situation is certainly not desirable.

So instead of depending directly on low-level modules, the high-level modules should depend on abstractions, such as interfaces or abstract classes. In this way if you change some details behind those abstractions the high level modules remain unchanged as they depend on abstractions (interfaces).

The term &#8220;inversion&#8221;means that by applying this principle the direction of the dependency is reversed because the high-level modules do not depend on low-level modules buy they depend on abstractions, as well as the implementation details.

Moreover, as the abstractions raise a &#8220;wall&#8221; between the different levels, any changes can not propagate everywhere, but there are only confined within the module to which these changes belong logically.

The latter is a fundamental prerequisite so that software applications are easily maintainable.

You can find an implementation of DIP in **Dependency** **Injection** **Pattern** or in the **Inversion of Control.**

In fact there is some confusion around these terms and many people use them interchangeably, both refer to the principle or  refer to patterns, but the fact remains that the inversion of control or dependency injection is an implementation of DIP.

Just to add to the confusion  the Hollywood Principle is just another way of calling the Inversion Of Control.

<div>
</div>