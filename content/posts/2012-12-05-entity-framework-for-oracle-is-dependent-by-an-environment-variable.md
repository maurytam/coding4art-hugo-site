---
title: Entity Framework for Oracle is dependent by an environment variable
author: mtammacco
type: post
date: 2012-12-05T15:13:53+00:00
url: /archive/2012/12/05/entity-framework-for-oracle-is-dependent-by-an-environment-variable.aspx
categories:
  - CodeProject

---
Those who using Entity Framework Provider for Oracle have certainly already run into this issue, i.e., the proper functioning of this provider depends on an environment variable! It’s a bit strange, but it’s the truth.

If you forget (or if you simply don’t know) to setup an environment variable named “TNS_ADMIN” which contains the full path used by Oracle software to search for the “tnsnames” file, which in turn is used for reading the necessary parameters to establish a connection to the database server, attempting to open a connection will fail.

After setup the environment variable you have to reboot Visual Studio, if already opened, in order to apply the change.

After applying the environment variable if you try to create a new Oracle connection using the Visual Studio wizard, if all is working fine you will see the list of the tnsnames file entries in the data source dropdown list instead of a blank list.

Also, this environment variable needs only to Entity Framework for Oracle, as other software, like Toad for example, doesn’t need it to search for tnsnames files.

You can obtain the same result by adding a registry key, but it’s certainly easier to create an environment variable than modifying the registry.

Hope this helps.

<a style="display: none" href="http://www.codeproject.com" rel="tag">CodeProject</a>