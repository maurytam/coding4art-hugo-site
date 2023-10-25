---
title: Impostare il calendarextender ad una cultura specifica
author: mtammacco
type: post
date: 2009-03-06T06:11:34+00:00
url: /archive/2009/03/06/impostare-il-calendarextender-ad-una-cultura-specifica.aspx
categories:
  - ASP .NET Ajax
  - Tips and tricks

---
L&#8217;extender CalendarExtender presente nell&#8217;Ajax Toolkit presenta un bug se si cerca di globalizzarlo, ovvero adattarlo ad una specifica cultura. Infatti, la label presente in basso con l&#8217;indicazione della data odierna non viene globalizzata ma rimane impostata fissa alla cultura inglese, per cui apparirà sempre la scritta &#8220;Today&#8221;. Affinchè i controlli dell&#8217;Ajax Toolkit possano essere personalizzati sulla base delle varie culture non basta impostare la specifica cultura nel file di configurazione dell&#8217;applicazione web (tag globalization), oppure impostarla tramite browser, ma occorre anche abilitare il rendering dello script al supporto di culture specifiche, tramite la proprietà <a href="http://www.asp.net/Ajax/documentation/live/mref/P_System_Web_UI_ScriptManager_EnableScriptGlobalization.aspx" target="_blank" rel="noopener">EnableScriptGlobalization</a> dello ScriptManager, che deve essere ovviamente impostata a True (il valore di default è False).