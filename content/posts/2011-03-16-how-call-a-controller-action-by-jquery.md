---
title: How to call a controller action by jQuery
author: mtammacco
type: post
date: 2011-03-16T16:16:03+00:00
url: /archive/2011/03/16/how-call-a-controller-action-by-jquery.aspx
categories:
  - ASP .NET MVC

---
With jQuery you are able to invoke an action of a Asp .Net MVC application&#8217;s controller.  
This is the code you need:



You can establish the request type (GET, SET and so), whether the request should be asynchronous or not (parameter async true or false), whether the request should be cached or not (parameter cache), a Javascript function to be called in case of success of the server request (parameter success) or in case of request fails (parameter error).  
The parameter &#8220;data&#8221; of the function called in case of success contains the return value by the server call.

However there are many others useful parameters you can use. For a complete list go <a target="_blank" href="http://api.jquery.com/jQuery.ajax#jQuery-ajax-settings" rel="noopener">here</a>. It&#8217;s also possible to make the same call but with a Json return value by the $.getJSON funtion.