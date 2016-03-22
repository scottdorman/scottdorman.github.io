---
layout: post
title: Understanding the .NET Framework 3.5
date: 6/12/2007 9:59:48 PM
---

Daniel Moth has an excellent [post](http://www.danielmoth.com/Blog/2007/06/net-framework-35.html) that explains what makes up the .NET Framework 3.5. This post also sparked a very good [discussion](http://www.codeproject.com/lounge.asp?select=2074979&df=100&forumid=1159&fr=766.5#xx2074979xx) on [The Code Project](http://www.codeproject.com).

There are two elements that make up version 3.5 of the Framework: the "green bits" and the "red bits". This model is aimed at minimizing the impact of delivering new features and functionality. The red bits are those parts of the Framework that exist in release today, which include the .NET Framework 2.0 and 3.0 releases. The green bits are brand new assemblies with brand new types in them.

![](http://www.danielmoth.com/Blog/fx35.png)

Looking at the diagram above, you might notice that the full version number for the .NET Framework v2.0 bits is different across the different versions. The important thing to understand here is how Microsoft views version numbers. In the Microsoft world, the version number is the first three parts - the Major.Minor.Build parts. The fourth part is the Revision, which corresponds to the service pack level.

The end result of this is that the .NET Framework v3.0 is at a different service pack on Vista then it is on other versions of Windows. The .NET Framework v3.5 includes updates to both the v2.0 and v3.0 frameworks. These updates are not new changes or features, but are really a service pack with bug fixes and performance improvements.

As was mentioned, the green bits add new assemblies with new types. These simply add to the .NET Framework without changing the CLR engine. In [Beta 1](http://www.microsoft.com/downloads/details.aspx?familyid=36b6609e-6f3d-40f4-8c7d-ad111679d8dc&displaylang=en&tm "here") of Orcas, the new assembles are:

1.  System.Data.Linq.dll - Implementation for LINQ to SQL.
2.  System.Xml.Linq.dll - Implementation for LINQ to XML.
3.  System.Addin.dll, System.Addin.Contract.dll - Implementation for the AddIn model.
4.  System.Net.dll - Peer to Peer APIs.
5.  System.DirectoryServices.AccountManagement.dll - Wrapper for Active Directory APIs.
6.  System.Management.Instrumentation.dll - WMI 2.0 managed provider (combined with the System.Management namespace in System.Core.dll).
7.  System.WorkflowServices.dll, System.ServiceModel.Web.dll - WF and WCF enhancements.
8.  System.Web.Extensions.dll - Implementation for ASP.NET AJAX, plus the implementation of [Client Application Services](http://www.danielmoth.com/Blog/2007/05/client-application-services-in-orcas.html).
9.  System.Core.dll - Implementation for LINQ to Objects, plus a lot of new namespaces and types.
