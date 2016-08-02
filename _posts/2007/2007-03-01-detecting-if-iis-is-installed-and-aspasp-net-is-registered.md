---
layout: post
title: Detecting if IIS is installed and ASP/ASP.NET is registered
date: 2007-03-01 23:06:00 -05:00
---

Recently, someone sent me an email about my [post]({% post_url 2007-02-04-detecting-installed-net-framework-versions-and-service-packs-update %}) on using managed code to detect the installed Framework versions and services packs. The posts were really just pointers to my [article](http://www.codeproject.com/useritems/frameworkversiondetection.asp?msg=1903766) on The Code Project, but it did bring up an interesting topic.

The question at hand really boils down into two separate issues:

1.  How to detect if Internet Information Services (IIS) is installed.
2.  How to detect if ASP and/or ASP.NET is *registered* with IIS. 

The best way to detect if IIS is installed is to look for the presence of the following registry key:

> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\InetStp

If this key exists, then IIS is installed. If it doesn't exist, IIS isn't installed. It really doesn't get any simpler than that. This key also provides some additional interesting information, such as the IIS version number. The version information is kept in the following registry values, both DWORDs:

MajorVersion

*   4: Shipped in NT Option Pack for Windows NT 4
*   5: Shipped in Windows 2000 Server and Windows XP Professional
*   6: Shipped in Windows Server 2003 

MinorVersion

*   1: Indicates that IIS is installed on Windows XP Professional 

Ok, now that we know IIS is installed, what about detecting if the *web service* components of IIS are installed? There are two ways to do this. One is to look for the following key:

> HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W3SVC

Again, if you don't have the web service components of IIS installed, this key shouldn't exist. 

The other way is to look at the IIS subcompoments registry key:

> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Setup\Oc Manager\Subcomponents

All of the values under this key are DWORDs, so if the value is 1 then it is installed. There are a lot of values listed here, but the interesting ones (at least for this discussion) are:

*   iis_common - IIS Common Files
*   iis_asp - Active Server pages (ASP) for IIS
*   iis_www - World Wide Web (WWW) service 

As you can see, this key can tell you if ASP is registered with IIS and if the web service components are installed.

Now that we know if ASP is registered, what about ASP.NET? Once again, we turn to the registry and look for the presence of the following keys:

*   .NET 1.1 - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\1.1.4322.0
*   .NET 2.0 - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\2.0.50727.0 

I don't actually have access to a .NET 1.0 system anymore, so I don't know what the correct registry keys would be for that release. (If someone knows what they are, please let me know by a comment on this post.)

I will be updating my Code Project article (and the associate component) to also report this information sometime later this month when I get some free time.
