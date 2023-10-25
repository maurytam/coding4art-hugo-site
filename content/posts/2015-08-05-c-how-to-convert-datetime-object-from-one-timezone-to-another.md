---
title: 'c#–how to convert datetime object from one timezone to another'
author: mtammacco
type: post
date: 2015-08-05T13:31:39+00:00
draft: true
private: true
url: /archive/2015/08/05/c-how-to-convert-datetime-object-from-one-timezone-to-another.aspx
categories:
  - Uncategorized

---
What you need to convert time in Microsoft .net from one timezone to another are essentially the source timezone id and the destination timezone id, or just the destination if you are going to use the system timezone as source (e.g. the time zone based on operative system installation).

But, what exactly timezone ids really are ? 

It&#8217;s a simple standard description of each timezone across the globe.  
For example, the time zone id for Rome is “W. Europe Standard Time”, while the New York’s one is “Eastern Standard Time”.

At this <a href="http://www.iana.org/time-zones" target="_blank" rel="noopener">link</a> (IANA web site) you can download a list of all these ids.

In .net the TimeZoneInfo object has a static method called “GetSystemTimeZones” which returns a list of all time zones registered into the system where the code is being executed. Each object contains a bunch of information about a specific timezone, such the id, the display name, the base utc offset, and so on.

<pre class="brush: csharp; title: ; notranslate" title="">var list = TimeZoneInfo.GetSystemTimeZones();
</pre>

For time conversion just needs the id.

Then you can convert time assuming that the source timezone will be the system timezone or whatever timezone you want.

This code converts time from my system time zone (Italy) to New York City time.