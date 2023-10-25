---
title: Impossibile aggiungere una service reference in visual studio 2008
author: mtammacco
type: post
date: 2008-07-28T10:03:31+00:00
url: /archive/2008/07/28/impossibile-aggiungere-una-service-reference-in-visual-studio-2008.aspx
categories:
  - Troubleshooting
  - Visual Studio 2008
  - WCF
  - Web services
  - Workaround

---
Questo workaround spero sia utile a chi si è trovato nella stessa mia situazione, e cioè che improvvisamente Visual Studio 2008 si rifiuta di aggiungere una Service Reference ad un servizio WCF, dando questo errore:

> ### The components required to enumerate web references are not installed on this computer. Please re-install Visual studio.

Ho poi scoperto che il problema si presentava anche aggiungendo semplici web reference (ASP .NET web services) a progetti creati con Visual Studio 2005.

Per risolvere il problema non è mica necessario reinstallare Visual Studio 🙂

Basta lanciare l&#8217;ambiente di sviluppo da prompt dei comandi (quello di Visual Studio) con il parametro /resetskippkgs, quindi in questo modo:

> devenv /resetskippkgs

Il parametro /resetskippkgs impedisce che siano caricati eventuali VSPackages aggiuntivi, che potrebbero creare problemi con lo startup dei componenti di Visual Studio. Era proprio quello che accadeva a me. Chiaramente basta lanciare solo una volta Visual Studio in quel modo, giusto per disabilitare il caricamento dei VSPackages.