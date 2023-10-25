---
title: 'Visual studio ide crash #2'
author: mtammacco
type: post
date: 2008-12-09T06:44:28+00:00
url: /archive/2008/12/09/visual-studio-ide-crash-2.aspx
categories:
  - Tips and tricks
  - Troubleshooting
  - Visual Studio 2008

---
Avevo già parlato <a href="http://xplayn.org/cs/blogs/maurizio/archive/2008/09/04/visual-studio-2008-ide-crash-dopo-quot-choose-items-quot-dalla-toolbox.aspx" target="_blank" rel="noopener">qui</a> (post immediatamente sotto :-)) di uno strano crash di Visual Studio 2008 SP1, a seguito dell&#8217;esecuzione comando &#8220;Choose items&#8221; della toolbox.

Il problema sembrava essere dovuto alla presenza dei PowerCommands e di una loro presunta incompatibilità con il Service Pack 1. Infatti per poter tornare alla &#8220;normalità&#8221; era necessario un&#8217;azione estrema, ovvero rimuovere i PowerCommands, ed a quel punto il problema spariva.

Oggi scopro che attraverso un assemply redirection nel file di configurazione di Visual Studio (devenv.exe.config) il problema si risolve definitivamente, e che il crash si verificava anche nell&#8217;editor XAML. Maggiori info <a href="http://social.msdn.microsoft.com/Forums/en-US/vssetup/thread/e2434065-9921-4861-b914-9cc9d6c55553/" target="_blank" rel="noopener">qui</a>.

Quindi la soluzione è inserire questo frammento XML nel file di configurazione di Visual Studio: