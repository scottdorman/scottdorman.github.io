---
layout: post
title: Are you running Debug or Release mode bits?
date: 9/2/2006 12:02:00 PM
---

Have you ever wanted to know if a compiled assembly was compiled in Debug or Release mode? I know I have.

I came across a post on [Computer Zen](http://www.hanselman.com/blog/HowToProgrammaticallyDetectIfAnAssemblyIsCompiledInDebugOrReleaseMode.aspx) today that shows exactly how to do this. There is also a similar tool written by Jeff Key, called [IsDebug](http://www.sliver.com/dotnet/IsDebug/).

For my part, I always make sure that the following snippet of code is in my AssemblyInfo.cs

#<span style="COLOR: #0000ff">if</span> (Debug || DEBUG)
[assembly: AssemblyConfiguration("<span style="COLOR: #8b0000">Debug</span>")]
#<span style="COLOR: #0000ff">else</span>
[assembly: AssemblyConfiguration("<span style="COLOR: #8b0000">Release</span>")]
#<span style="COLOR: #0000ff">endif</span>

<span style="COLOR: #0000ff"></span>

This attribute doesn't show up in the file properties (when viewed from Explorer) but it can be queried programmatically.
