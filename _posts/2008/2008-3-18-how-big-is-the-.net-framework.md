---
layout: post
title: How big is the .NET Framework?
date: 3/18/2008 11:44:17 PM
---

No, this question isn't asking how much disk space is required by the Framework. It's really asking "How complex is the .NET Framework for developers?" As you might guess, the answer is: It's pretty complex.

All joking aside, this is neither an uncommon nor unreasonable question and answer. The reality of it is that the .NET Framework is a very complicated application programming interface (API) but is designed in such a way to expose that complexity gradually (at least in most cases).

[Brad Abrams](http://blogs.msdn.com/brada/archive/2008/03/17/number-of-types-in-the-net-framework.aspx) has an excellent post that shows this complexity in a very easy to understand set of graphs. The side-benefit to these graphs is that they show the evolution of the Framework over time, not just the current release.

[![image_6](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/Howbigisthe.NETFramework_14B3C/image_6_thumb.png)](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/Howbigisthe.NETFramework_14B3C/image_6_2.png) [![image_8](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/Howbigisthe.NETFramework_14B3C/image_8_thumb.png)](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/Howbigisthe.NETFramework_14B3C/image_8_2.png) 

[![image_10](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/Howbigisthe.NETFramework_14B3C/image_10_thumb.png)](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/Howbigisthe.NETFramework_14B3C/image_10_2.png) [![image_12](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/Howbigisthe.NETFramework_14B3C/image_12_thumb.png)](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/Howbigisthe.NETFramework_14B3C/image_12_2.png) 

The interesting thing that these graphs show is that in every category the amount almost tripled between versions 1.0 and 3.5 of the Framework in almost 6 years. Given the complexity of a lot of the changes between versions that is an incredible amount of work.
