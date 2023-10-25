---
title: AddessAccessDeniedException in WCF 4.0
author: mtammacco
type: post
date: 2011-06-28T15:38:55+00:00
url: /archive/2011/06/28/addessaccessdeniedexception-in-wcf-4-0.aspx
categories:
  - .NET Framework 4.0
  - WCF

---
If you host a WCF service on a machine with UAC enabled, Vista or Win7 for example, you might run into a seemingly strange exception:

The reason is due to the fact that to host a WCF service you need to register its url, and this task requires administrator privileges, and this means as well that if you run Visual Studio as Administrator everything works fine, but what if you don’t have this possibility ? Or how to register an URL for it to work ?

If you follow the link mentioned in the error message you waste your time because the resulting link is too general for this specific error. I used this approach: I downloaded <a href="http://blogs.msdn.com/cfs-file.ashx/__key/communityserver-components-postattachments/00-02-41-62-36/HttpNamespaceManager.zip" target="_blank" rel="noopener">HttpNamespaceManager</a>, a little and nice open source utility (not an official Microsoft tool), also provided with source code, that just does this, register an URL even assigning permissions to users.

After the URL registration your service will work fine.