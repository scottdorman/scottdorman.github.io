---
layout: post
title: Release builds are not Debug builds
date: '2007-10-25 19:22:46 -05:00'
---

Scott Hanselman has an excellent [post](http://www.hanselman.com/blog/ReleaseISNOTDebug64bitOptimizationsAndCMethodInliningInReleaseBuildCallStacks.aspx) on his blog where he talks about the differences between release builds and debug builds. Just to reiterate what should be obvious, as Scott points out:

> Release builds are optimized for speed and debug builds are optimized for, well, debug-ability. However, most of the optimizations in managed code are done by the JIT compiler rather than the language compiler.

If you want to know about some of the real difference between release and debug builds, including C# method inlining and runtime optimizations, you should definitely take a look at his post.
