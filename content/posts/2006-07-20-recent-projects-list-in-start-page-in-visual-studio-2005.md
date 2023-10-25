---
title: Recent projects list in start page in Visual Studio 2005
author: mtammacco
type: post
date: 2006-07-20T11:12:00+00:00
url: /archive/2006/07/20/recent-projects-list-in-start-page-in-visual-studio-2005.aspx
categories:
  - Visual Studio 2005

---
La start page di Visual Studio 2005 presenta la lista dei recents projects, contenente progetti e soluzioni aperti di recente. Questa lista può diventare presto inutile per coloro che aprono/creano un progetto/soluzione &#8220;una tantum&#8221; solo per motivi di test, e magari dopo aver verificato il funzionamento il progetto viene addirittura cancellato dal disco.  Infatti la lista non è modificabile in alcun modo tramite GUI, ma da registry sì.

Posizionandosi su questa chiave 

**HKEY\_CURRENT\_USER\Software\Microsoft\VisualStudio\8.0\ProjectMRUList** è possibile cancellare le voci non più valide e &#8220;ripulire&#8221; quindi la lista dei recents projects.