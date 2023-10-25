---
title: 'Entity Framework #1 &ndash;How to get the original type of an entity when dynamic proxy is enabled'
author: mtammacco
type: post
date: 2012-03-13T16:09:51+00:00
url: /archive/2012/03/13/entity-framework-1-ndashhow-to-get-the-original-type-of.aspx
categories:
  - Entity Framework

---
If your Entity Framework context is proxy-enabled, the runtime will create a proxy instance of your entities, i.e. a dynamically generated class which inherits from your entity class and overrides its virtual properties by inserting specific code useful for example for tracking changes and lazy loading.

The proxy instance has a dynamically generated name by the runtime that looks like this:

<pre class="brush: csharp; title: ; notranslate" title="">{System.Data.Entity.DynamicProxies User_00394CF1F92740F13E3EDBE858B6D599DFAF87AA5A089245977F61A32C75AA22}
</pre>

(User is the original entity class name which the proxy class inherited from).

Starting from the proxy type, if you need to know the original type you have to use the static method GetObjectType of ObjectContext type, as shown in this example:

<pre class="brush: csharp; title: ; notranslate" title="">var userType = ObjectContext.GetObjectType(user.GetType());
</pre>

Through the FullName property of the type returned by this method you can get the full name of the original type (User in this example)

<div id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:09543f39-eb24-44be-89e6-09469b02c0b2" class="wlWriterEditableSmartContent" style="margin: 0px; display: inline; float: none; padding: 0px;">
  Technorati Tags: <a href="http://technorati.com/tags/Entity+Framework" rel="tag">Entity Framework</a>,<a href="http://technorati.com/tags/dynamic+proxy" rel="tag">dynamic proxy</a>
</div>