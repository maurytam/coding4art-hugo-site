---
title: Default endpoints in WCF 4.0
author: mtammacco
type: post
date: 2011-06-28T14:55:52+00:00
url: /archive/2011/06/28/default-endpoints-in-wcf-4-0.aspx
categories:
  - .NET Framework 4.0
  - WCF

---
Starting from WCF 4.0 it’s possible to use a default endpoint in absence of explicit configuration. This means that you can avoid to configure an explicit endpont because of a default mapping between protocol schema and bindings described in the configuration file machine.config.

Here is the default content of that mapping:



For example, in the case of presence of “http” in the protocol, it will be used the default binding “basicHttpBinding” without the need to configure an endpoint explicitly.

Now, to test this new feature all you need is to create a simple service without an explicit endpoints configuration and then read hits configuration such as the following example:



This code in .Net Framework 4.0 will work fine, while .Net 3.5 would have required the endpoint configuration