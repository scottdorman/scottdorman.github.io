---
layout: post
title: .NET Memory Management &ndash; Resources
redirect_from: /2008/09/14/.net-memory-management-ndash-resources/
date: '2008-09-14 16:16:11 -05:00'
tags: .net garbage-collection
---

I present at a lot of the local Florida code camps (and some out of state ones as well) and have a set of presentations that I do which focus on .NET memory management, specifically a "deep dive" on how the GC works and another presentation which talks about how to implement the Dispose pattern properly.

I was doing some additional research today to update my list of resources in the presentations and decided to publish that list here as well. This is not an exhaustive list, but it is a subset of the books, articles, blogs and presentations that I used to form the content for my presentations.

**Books**

* [CLR via C#](http://amzn.to/28JSmWn)
* [C# Essentials](http://amzn.to/28M3fX6) 
* [.NET Framework Essentials](http://amzn.to/28IJrmC)
* [.NET Gotchas](http://amzn.to/28JRVvj)
* [Programming .NET Components](http://amzn.to/28JudAR)
* [Framework Design Guidelines](http://amzn.to/28JOJA1)

**Articles**

*   [Garbage Collection: Automatic Memory Management in the Microsoft .NET Framework](http://msdn.microsoft.com/magazine/bb985010.aspx) (Jeffrey Richter) 
*   [Garbage Collection - Part 2: Automatic Memory Management in the Microsoft .NET Framework](http://msdn.microsoft.com/magazine/bb985011.aspx) (Jeffrey Richter) 
*   [CLR Inside Out: Investigating Memory Issues](http://msdn.microsoft.com/en-us/magazine/cc163528.aspx) (Claudio Caldato and Maoni Stephens) 
*   [Implementing IDisposable and the Dispose Pattern Properly](http://www.codeproject.com/KB/cs/idisposable.aspx) (Scott Dorman) 
*   [SafeHandle and Constrained Execution Regions](http://www.codeproject.com/KB/dotnet/safehandle.aspx) (Scott Dorman) 
*   [Production Debugging for .NET Framework Applications](http://msdn.microsoft.com/library/ms954591.aspx)  (MSDN Library, patterns & practices) 
*   [Automatic Memory Management](http://msdn.microsoft.com/library/f144e03t.aspx) (MSDN Library, Visual Studio 2008 Developer Center) 
*   [Garbage Collection](http://msdn.microsoft.com/library/0xy59wtx.aspx) (MSDN Library, Visual Studio 2008 Developer Center)   

**Presentations, Webcasts, Podcasts**

*   [.NET Framework: CLR Internals](http://www.microsoft.com/seminar/en/DEV424_files/default.htm) (Jeffrey Richter, TechEd 2005 presentation) 
*   [CLR Garbage Collector](http://www.infoq.com/presentations/justin-smith-clr-gc;jsessionid=C807360EAE7829AAD96A98841AFF6205) (Justin Smith)   

**Blogs**

*   Paul Wilson      
    *   [.NET Memory Management and Garbage Collection](http://weblogs.asp.net/pwilson/archive/2004/02/14/73033.aspx) 
    *   [.NET GC Myth #1 -- Set Object to Null](http://weblogs.asp.net/pwilson/archive/2004/02/20/77422.aspx)    
*   Maoni Stephens      
    *   [Using GC Efficiently – Part 1](http://blogs.msdn.com/maoni/archive/2004/06/15/156626.aspx) 
    *   [Using GC Efficiently – Part 2](http://blogs.msdn.com/maoni/archive/2004/09/25/234273.aspx) 
    *   [Using GC Efficiently – Part 3](http://blogs.msdn.com/maoni/archive/2004/12/19/327149.aspx) 
    *   [Using GC Efficiently – Part 4](http://blogs.msdn.com/maoni/archive/2005/05/06/415296.aspx) 
    *   [So, what's new in the CLR 2.0 GC?](http://blogs.msdn.com/maoni/archive/2005/10/03/so-what-s-new-in-the-clr-2-0-gc.aspx) 
    *   [Clearing up some confusion over finalization and other areas in GC](http://blogs.msdn.com/maoni/archive/2004/11/04/252697.aspx) 
    *   [Large Object Heap](http://blogs.msdn.com/maoni/archive/2006/04/18/large-object-heap.aspx) 
    *   [GC Performance Counters](http://blogs.msdn.com/maoni/archive/2004/06/03/148029.aspx) 
    *   [I Am a Happy Janitor – Part 1: Finding garbage](http://blogs.msdn.com/maoni/archive/2006/08/18/i-am-a-happy-janitor-part-1-finding-garbage.aspx)    
*   [DG Update: Dispose, Finalization, and Resource Management](http://www.bluebytesoftware.com/blog/PermaLink,guid,88e62cdf-5919-4ac7-bc33-20c06ae539ae.aspx)  (Joe Duffy) 
*   [When GC.KeepAlive Doesn't](http://blogs.msdn.com/clyon/archive/2006/08/28/728688.aspx) (Chris Lyon) 
*   [How To: Tune the .NET Framework](http://channel9.msdn.com/wiki/performancewiki/howtotunenetframework/) (Channel 9) 
*   [Notes on the CLR Garbage Collector](http://vineetgupta.spaces.live.com/blog/cns!8DE4BDC896BEE1AD!1104.entry) (Vineet Gupta) 
*   [Mid-life crisis](http://blogs.msdn.com/ricom/archive/2003/12/04/41281.aspx) (Rico Mariani) 
*   [Memory management in the .NET Framework](http://blogs.msdn.com/johan/archive/2007/04/20/memory-management-in-the-net-framework.aspx) (Johan Straarup)   

**Tools**

*   [CLR Profiler](http://blogs.msdn.com/jmstall/archive/2005/12/17/CLR-profiler-2-0-available.aspx)
*   [FxCop](http://blogs.msdn.com/fxcop) 
*   Performance Monitor
*   [WinDbg](http://microsoft.com/whdc/devtools/debugging)
*   [SOS Debugging Extensions](http://msdn2.microsoft.com/ms404370.aspx)
