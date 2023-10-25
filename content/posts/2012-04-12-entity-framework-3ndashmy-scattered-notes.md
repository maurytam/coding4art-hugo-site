---
title: 'Entity Framework #3&ndash;my scattered notes'
author: mtammacco
type: post
date: 2012-04-12T07:56:39+00:00
url: /archive/2012/04/12/entity-framework-3ndashmy-scattered-notes.aspx
categories:
  - Entity Framework

---
When using Entity Framework 4.x Code First you can put your validation code in Data Annotations or inside the DbContext class (this is my preferred mode).

It’s possible to override the virtual method ValidateEntity exposed by the DbContext class and then define your own validation logic in one place.

This method is called once for each distinct entity being modified in your context, and it provides an opportunity for developers to stop the entity update process when some properties are in invalid state.

Here’s an example:



This code will be invoked only if the “ValidateOnSaveEnabled” property of the class DbContextConfiguration is set to true.

<div id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:882b78d6-6e7f-4798-8830-b7586616d557" class="wlWriterEditableSmartContent" style="margin: 0px; display: inline; float: none; padding: 0px;">
  Technorati Tags: <a href="http://technorati.com/tags/ORM" rel="tag">ORM</a>,<a href="http://technorati.com/tags/Entity+Framework" rel="tag">Entity Framework</a>,<a href="http://technorati.com/tags/Code+First" rel="tag">Code First</a>,<a href="http://technorati.com/tags/Validation+entity" rel="tag">Validation entity</a>
</div>