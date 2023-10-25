---
title: How to debug Log4Net
author: mtammacco
type: post
date: 2012-05-18T09:51:23+00:00
url: /archive/2012/05/18/how-to-debug-log4net.aspx
categories:
  - Tips and tricks

---
If you use Log4Net as log engine for your applications (in my opinion is the best choice), this simple row in application configuration file can save you by a waste of time and probably by a headache too.



When Log4Net doesn’t log anything due to a configuration error it never throw an exception, and this is the expected (and correct) behavior of a log system which should never block an application due to its internal error. Unfortunately when something went wrong it is quite difficult discover the reason if you don’t have a break in your code.

With that configuration instruction Log4Net “logs” its initialization process in output windows and in Trace system.

If you add a trace listener you can also save this output in a file.

Here’s an example:



This is very useful in production environment where Visual Studio is not installed and then an output window is not available.

<div id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:4044083e-bb76-4115-bee6-7b6b77c5ca1b" class="wlWriterEditableSmartContent" style="margin: 0px; display: inline; float: none; padding: 0px;">
  Technorati Tags: <a href="http://technorati.com/tags/Log4Net" rel="tag">Log4Net</a>,<a href="http://technorati.com/tags/configuration" rel="tag">configuration</a>
</div>