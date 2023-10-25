---
title: 'The second Solid principle: OCP'
author: mtammacco
type: post
date: 2010-11-26T10:14:52+00:00
url: /archive/2010/11/26/the-second-solid-principle-ocp.aspx
categories:
  - SOLID Principles

---
In this post I will speak about the second principle of Object Oriented Design (OOD), i.e. the Open-Closed Principle (OCP). in addition to the first one (SRP)  which I have already spoken in my previous <a href="http://www.coding4art.com/archive/2010/11/22/the-first-solid-principle-srp.aspx" target="_blank" rel="noopener">post</a>.

This principle was coined by Bertrand Meyer, the same person who coined the term &#8220;design by contract&#8221;, to which I devoted an <a href="http://www.ugidotnet.org/Article/Detail/1321" target="_blank" rel="noopener">article</a> that you can view on the  <a href="http://www.ugidotnet.org/" target="_blank" rel="noopener">UgiDotNet</a> site.

This principle simply states that software entities, i.e. class, &#8220;**should be opened for extensions but closed for modifications**&#8220;.

Now, what does it really means ?

We all know that code changes according to changing requirements. When we design a module software, we design it according to certain requirements valid at the time. When requirements change we should be able to extend that software module, i.e. add new features in addition to existing ones, and the latter should not be changed for any reason.

In other words, when we create a module with certain features, that module must be immutable, and immutable means stable.

This principle apparently shows a contradiction: how can something that is immutable be subject to extensions, and then ultimately to change?

The answer lies in the use of abstract classes or interfaces. In fact, you can see it from this point of view: an interface or an abstract class, once created and established the methods and properties with their signatures, must be unalterable, but you can create different concrete classes which implement that interfaces and abstract classes, and then different implementations, and then modify or extend their behavior leaving the contract intact.

In this way, the software module is closed for modifications (the interface doesn&#8217;t never change), but is also open for extensions as you can create different implementations.

This principle would imply another principle: it&#8217;s necessary to design on interface and not on concrete implementations, otherwise the OCP would inexorably violated.