---
title: DotNet Core “Unable to load DLL ‘System.Security.Cryptography.Native” error
author: mtammacco
type: post
date: 2016-11-25T17:52:12+00:00
url: /archive/2016/11/25/dotnet-core-unable-to-load-dll-system-security-cryptography-native-error.aspx
categories:
  - DotNet Core
  - Troubleshooting
  - Visual Studio Code
tags:
  - DotNetCore
  - Troubleshooting
  - VisualStudioCode

---
I was trying to play with [DotNet Core][1] in [Visual Studio Code][2], and I was following the instructions as stated [here][1].

After installed [Brew][3] I installed the latest version of OpenSSL as required by DotNet Core and then I tried to run the classic &#8220;Hello World&#8221; program, but the command

**dotnet restore** 

failed with this error:

<p class="gh-header-title">
  <em><strong><span class="js-issue-title">&#8220;Unable to load DLL &#8216;System.Security.Cryptography.Native&#8221;</span></strong></em>
</p>

This error has to do with OpenSSL, or even better with Brew that refuseed to correctly link OpenSSL.

Here is the correct command sequence that needs to correctly setting up OpenSSL for DotNet Core.

<pre><strong><code>brew update
brew install openssl
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/Cellar/openssl/1.0.2j/bin/openssl openssl</code></strong></pre>

Hope this helps

 [1]: https://www.microsoft.com/net/core#macos
 [2]: https://code.visualstudio.com/c?utm_expid=101350005-35.Eg8306GUR6SersZwpBjURQ.2&utm_referrer=https%3A%2F%2Fwww.google.it%2F
 [3]: http://brew.sh/