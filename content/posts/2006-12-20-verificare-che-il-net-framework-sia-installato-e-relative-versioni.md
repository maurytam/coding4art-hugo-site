---
title: Verificare che il .NET Framework sia installato e relative versioni
author: mtammacco
type: post
date: 2006-12-20T12:40:00+00:00
url: /archive/2006/12/20/verificare-che-il-net-framework-sia-installato-e-relative-versioni.aspx
categories:
  - .NET Framework 1.0 / 1.1 / 2.0

---
Per verificare che il .NET Framework sia installato ed eventualmente in quali versioni è possibile procedere in questo modo:

  * La semplice presenza del file **MSCOREE.DLL** (Microsoft .NET Runtime Execution Engine) nella directory %**SYSTEMROOT\system32** è sintomo che almeno una versione del CLR è installata
  * La chiave del registry **HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\.NETFramework\policy** contiene delle sottochiavi, una per ogni versione installata, nella forma vX.X (es. v2.0)
  * La versione 2.0 del  .NET Framework contiene una nuova utility denominata **CLRVer.exe**, che, come il suo nome lascia intuire, elenca tutte le versioni del CLR installate sulla macchina su cui viene eseguita. Molto interessanti sono i parametri **-all**, che elenca tutte le applicazioni managed in esecuzione con la relativa versione del CLR con cui girano, e -PID, con cui è possibile ottenere lo stesso risultato ma relativamente ad un singolo processo identificato dal suo process ID