---
layout: post
title: Performance in managed applications
date: '2019-02-27 16:58:00 -05:00'
tags: .net
---

In 2006 I wrote, but apparently never published a blog post (it's now [published]({% post_url /2006/2006-06-18-performance-in-net-managed-applications %})) talking about performance in .NET managed applications. 

In some ways, not much has changed in the last 13 years about writing efficient code. You still need to have an understanding of the performance cost of the features you use and to choose the appropriate algorithms and data structures.

There are a lot of people who live by the words "Premature optimization is the root of all evil!". (This is also known as "Hoare's Dictum".)

To those of you who fall whole-heartedly in to this camp, I need to point out a couple of things. This quote most likely originated from [Tony Hoare](http://en.wikiquote.org/wiki/C._A._R._Hoare) and was restated by [Donald Knuth](http://en.wikipedia.org/wiki/Donald_Knuth). I first heard this quote sometime in 2004 and something about it always bothered me. Too many times I have seen this concept applied to the wrong areas of software design and at the wrong times. I've worked on projects that followed "Hoare's Dictum" and everything goes well until a realistic large-scale test is performed and it very quickly becomes obvious that the application is never going to upwardly scale. The problem is that by the time this is discovered it is usually very difficult to fix the problems without a lot of rework.

The full version of the quote is:

> We should forget about small efficiencies, say about 97% of the time: premature optimization is the root of all evil.

What this is really telling us is that we shouldn't worry about viewing the code through a microscope, trying to determine where the performance bottlenecks can be found; we should consider performance issues at the design level by keeping the two points I mentioned above in mind. 

Some developers will almost always do this automatically, having developed a "sixth-sense" for where performance issues are most likely to occur. Everyone knows the pitfalls of performing a large number of string concatenations inside a tight loop and can immediately see the performance improvement when those string concatenations are changed to use a `StringBuilder` instead.

That being said, there will always be performance issues that need to be resolved in applications. The larger the application, the more chance there is for performance problems. 

Collecting the data is usually done by using a variety of tools and methods. Sampling is non-intrusive and many problems can be diagnosed with a sampling profiler. Instrumentation is usually very intrusive and can sometimes cause a noticeable slowdown in your application.


While high CPU utilization is most easily seen in Task Manager or [Process Explorer](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer), the best tools for collecting data for these types of problems are the Visual Studio Performance Profiler or a commercial tool. Stackify has a great [article](https://stackify.com/three-types-of-net-profilers/) on the different types of profiling tools available, which also lists some of the more common ones.