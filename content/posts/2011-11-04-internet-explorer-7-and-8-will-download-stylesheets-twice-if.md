---
title: Internet Explorer 7 and 8 will download stylesheets twice if the http(s) protocol is missing
author: mtammacco
type: post
date: 2011-11-04T15:03:20+00:00
url: /archive/2011/11/04/internet-explorer-7-and-8-will-download-stylesheets-twice-if.aspx
categories:
  - Web standards

---
This is hard to believe, but is true:

_Internet Explorer 7 & 8 will download stylesheets twice if the http(s) protocol is missing._

If you have a page with mixed protocol url request (i.e. a https page with tags “link” or “script” with http links), Internet Explorer displays a security warning.

This is a security warning which alerts the user that a web page requested by a security connection (https) contains web request using a non secure connection (http) as well. It’s not clear what is the answer that user must supply to this message to download both the secure and unsecure content. To make things more complicated, this answer is different between Internet Explorer version 7 and 8 (strange but true, too). In fact, in version 7 user had to click the “Yes” button (the default one), but in version 8 user would have to click “No” (it’s incredible, I know it, but it is so).

So, to avoid this confusion, it’s necessary avoiding mixed content on https requests, and this can be obtained using the short sintax for urls, that is a special sintax in which the protocol part of the url is missing.

Doing this browsers automatically use the same protocol as web page, and the problem seems solved, but Internet Explorer version 7 and 8, in this particular condition (missed protocol), download stylesheets twice, as you may easily notice using any software for capturing the http traffic, like <a href="http://www.httpwatch.com/" target="_blank" rel="noopener">HttpWatch</a>

Hard to imagine, right ?

<div id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:6cb5413b-19c8-4cfc-a818-3c5fe3a963b7" class="wlWriterEditableSmartContent" style="margin: 0px; display: inline; float: none; padding: 0px;">
  Technorati&#8217;s Tag: <a href="http://technorati.com/tags/Web+standards" rel="tag">Web standards</a>,<a href="http://technorati.com/tags/browsers" rel="tag">browsers</a>,<a href="http://technorati.com/tags/Internet+Explorer" rel="tag">Internet Explorer</a>
</div>