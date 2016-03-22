---
layout: post
title: Volatile Registry Keys
date: 12/24/2007 5:47:09 PM
---

Up until recently, I had never heard of a [volatile registry key](http://msdn2.microsoft.com/en-gb/library/ms891450.aspx). I cam across a post by [Daniel Moth](http://www.danielmoth.com/Blog/2007/12/volatile-registrykey.html) that presents an extension method that adds support for both .NET and NETCF. While I haven't looked at the [projects](http://www.danielmoth.com/Blog/VolatileRegSolution.zip) he provides, it did get me thinking about what this support would actually mean.

A volatile registry key is one whose information is stored only in memory and is not preserved when the corresponding registry hive is unloaded. For keys created under the HKEY_LOCAL_MACHINE hive, this occurs when the system is shutdown. For keys loaded by the [RegLoadKey](http://msdn2.microsoft.com/en-gb/library/ms724889(VS.85).aspx) function, this occurs when the corresponding [RegUnLoadKey](http://msdn2.microsoft.com/en-gb/library/ms724924(VS.85).aspx) is performed. To put it simply, this means that volatile registry keys do not survive a reboot.

At this point, you may be wondering why a volatile registry key would be useful. Normally, when you create a registry key for an application you want it persisted. However, there are times when you may want to store transient information in the registry. A volatile key would be perfect for this scenario since you don't have to worry about explicitly cleaning it up afterwards. Another scenario would be for use in build scripts, particularly scripts that build InstallShield projects. One feature of InstallShield is that you can create path variables that reference registry keys. This is useful in creating installer projects that are build server independent. If you create the required registry keys through the build script, you will probably be creating them each time the build script runs to ensure that they are always present and have the correct values. These registry keys are only important during the actual build process and, since they are recreated each time, don't really need to be persisted.
