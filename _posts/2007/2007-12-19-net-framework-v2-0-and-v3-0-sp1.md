---
layout: post
title: .NET Framework v2.0 and v3.0 SP1
date: '2007-12-19 20:38:10 -05:00'
---

Now that Visual Studio 2008 and the .NET Framework v3.5 have shipped, you may have noticed that Service Pack 1 for .NET Framework 2.0 and Service Pack 1 for .NET Framework 3.0 also shipped at the same time. 

Both are automatically installed with .NET Framework v3.5, Windows Server 2008 and Windows Vista Service Pack 1. For Windows XP and Windows Server 2003 they are available as a standalone update. 

[Daniel Moth](http://www.danielmoth.com/Blog/index.htm) has an excellent [post](http://feeds.feedburner.com/~r/DanielMoth/~3/202141242/net-framework-v20-sp1.html) that describes what is actually in the service packs. Here is the list for Fx v2.0 SP1:

* [Bug fixes](http://support.microsoft.com/?id=945757)
* Performance improvements.
* Some new public APIs:
    *   [New members on the GC class](http://www.danielmoth.com/Blog/2007/03/gccollectionmode-and.html).
    *   [DateTimeOffset class](http://www.danielmoth.com/Blog/2007/06/datetimeoffset.html) (used by DateTime and many other APIs, e.g. XmlConvert.ToDateTimeOffset()).
    *   [Addition of the ShieldIcon for drawing](http://www.danielmoth.com/Blog/2007/12/systemiconsshield.html)
    *   [IME additions](http://www.danielmoth.com/Blog/2007/12/canenableime.html)
    *   [File Dialog Enhancements](http://www.danielmoth.com/Blog/2007/12/filedialog-additions-in-sp1.html)    Internal changes:
*   [Increase of ThreadPool limit](http://www.danielmoth.com/Blog/2007/11/threadpool-in-net-framework-v20-service.html)   

The list of fixes for Fx v3.0 SP1 is also available in this [KB article](http://support.microsoft.com/default.aspx?id=945826).

Daniel has points out an important caution that I felt was important enough to repeat:

> If you use VS2008 to target Fx v2.0, you are really targeting Fx v2.0 SP1.
