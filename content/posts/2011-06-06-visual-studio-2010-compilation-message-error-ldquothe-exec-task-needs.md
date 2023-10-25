---
title: 'Visual Studio 2010 compilation message error &ldquo;The exec task needs a command to execute&rdquo;'
author: mtammacco
type: post
date: 2011-06-06T13:20:14+00:00
url: /archive/2011/06/06/visual-studio-2010-compilation-message-error-ldquothe-exec-task-needs.aspx
categories:
  - Troubleshooting

---
If it happens this strange and cryptic error in Visual Studio 2010 while compiling any project:

_**“The exec task needs a command to execute”**_

the reason is this: in any pre or post build event, there is a carriage return character to remove, because Visual Studio 2010 poorly digested the carriage return characters in &#8216;text editor pre-post build events.