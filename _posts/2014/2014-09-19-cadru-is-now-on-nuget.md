---
layout: post
title: Cadru is now on NuGet
date: 2014-09-19 00:31:42 -04:00
---

A little over a year ago I [announced](http://geekswithblogs.net/sdorman/archive/2013/08/05/introducing-cadru.aspx) the availability of [Cadru](https://github.com/scottdorman/cadru), an open source utility framework containing new APIs and extensions to the core .NET Framework to help complete your developer toolbox. 

> I am very pleased to announce that the Cadru assemblies are now available on [NuGet](https://www.nuget.org/packages?q=Tags%3A%22cadru%22).

To install one of the assemblies, run the corresponding command in the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console):

*   **[Cadru.Core](https://www.nuget.org/packages/Cadru.Core/)** - A portable class library which provides the majority of the framework.       <div class="nuget-badge">       

`PM> Install-Package Cadru.Core `
     </div>   
*   **[Cadru.Core.Windows](https://www.nuget.org/packages/Cadru.Core.Windows/)** - A non-portable class library (targeting .NET Framework 4) meant for Windows desktop applications.       <div class="nuget-badge">       

`PM> Install-Package Cadru.Core.Windows `
     </div>   
*   **[Cadru.UnitTest.Framework](https://www.nuget.org/packages/Cadru.UnitTest.Framework/)** - A non-portable class library (targeting .NET Framework 4) which adds additional assert capabilities for MSTest.       <div class="nuget-badge">       

`PM> Install-Package Cadru.UnitTest.Framework`
     </div>     

#### [](https://github.com/scottdorman/cadru/blob/master/README.md#bugs-and-feature-requests)Bugs and feature requests

Do you have a bug or a feature request? Please use the [issue tracker](https://github.com/scottdorman/cadru/issues) and search for existing and closed issues. If your problem or request isn't addressed yet, go ahead and [open a new issue](https://github.com/scottdorman/cadru/issues/new). 

#### [](https://github.com/scottdorman/cadru/blob/master/README.md#contributing)Contributing

You can also get involved and [fork the repository](https://github.com/scottdorman/cadru/fork) to submit your own pull requests. (More detailed contributor guidelines will be available soon.)
