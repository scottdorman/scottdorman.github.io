---
layout: post
title: Performance in .NET managed applications
date: '2006-06-18 17:00:00 -05:00'
---

Building managed applications is generally a lot different than building non-managed applications. The problems faced by .NET developers are different than those faced by C++ (or even VB) developers. Since .NET is a garbage-collected language and the development process seems to be generally more intuitive (at least in C#) than many other programming languages and environments it is very easy to build applications rapidly.

Visual Stduio 2005 definately takes the concept of rapid application development to the next level and allows developers to raapidly create applications in a much shorter time frame. However, this ease of use does come with a cost. Visual Studio 2005 allows developers to write code fast, but it doesn't help us write fast code. There is an important distinction between the two.

In order to write fast code, you need to have an understanding of two things:

1. Know the performance cost of the features you use
2. Choose appropriate algorithms and data structures

At this point, many of you may be screaming the words “Premature optimization is the root of all evil!”. (This is also known as "Hoare's Dictum".) To those of you who fall whole-heartedly in to this camp, I need to point out a couple of things. This quote most likely originated from [Tony Hoare](http://en.wikiquote.org/wiki/C._A._R._Hoare) and was restated by [Donald Knuth](http://en.wikipedia.org/wiki/Donald_Knuth). I first heard this quote about two years ago and something about it always bothered me. Too many times I have seen this concept applied to the wrong areas of software design and at the wrong times. I've worked on projects that followed "Hoare's Dictum" and everything goes well until a realistic large-scale test is performed and it very quickly becomes obvious that the application is never going to upwardly scale. The problem is that by the time this is discovered it is usually very difficult to fix the problems without a lot of rework.

The full version of the quote is:

```We should forget about small efficiencies, say about 97% of the time: premature optimization is the root of all evil.```

What this is really telling us is that we shouldn't worry about viewing the code through a microscope trying to determine where the performance bottlenecks can be found; we should consider performance issues at the design level by keeping the two points I mentioned above in mind. A good developer will almost always do this automatically, having developed a "sixth-sense" for where performance issues are most likely to occur. Everyone knows the pitfalls of performing a large number of string concatenations inside a tight loop and can immediately see the performance improvement when those string concatenations are changed to use a StringBuilder instead.

That being said, there will always be performance issues that need to be resolved in applications. The larger the application, the more chance there is for performance problems. There is a simple 3-step process for investigating performance problems:

1. Identify Critical Resources
2. Collect Data
3. Identify the cause and fix the problem

This process repeats until you have acchieved the desired performance.

Identifying the critical resouces can be broken down to the following cases:

* Intra-Process - performance is determined by how the process uses resources
* Inter-Process - performance is determined by how long the process waits for another process

Collecting the data is usually done by using a variety of tools and methods. High CPU utilization is most easily seen in Task Manager or [Process Explorer](http://www.sysinternals.com/Utilities/ProcessExplorer.html). The best tools for collecting data for these types of problems are the Visual Studio Performance Profiler or the [CLRProfiler](http://msdn.microsoft.com/netframework/downloads/tools/default.aspx) for user mode applications and the [Kernrate viewer](http://www.microsoft.com/whdc/system/sysperf/krview.mspx).

There are two ways to profile an application: Sampling and Instrumentation.

Sampling is non-intrusive and many problems can be diagnosed with a sampling profiler. Instrumentation is very intrusive and can cause between a 10-100 time slowdown.

Memory issues manifest themselves thorugh paging and are a system-wide phenomenon.