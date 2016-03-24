---
layout: post
title: Visual Studio 2008 Multi-targeting
date: 2007-09-30 11:24:53 -05:00
---

One of the new features in Visual Studio 2008 is the ability to target a project to any version of the .NET Framework from 2.0 and up. This is an excellent feature as it allows the entire development team to work with the same version of the IDE. Since it's a project based setting, it also allows you to mix projects in the same solution.

The interesting thing about multi-targeting is that it potentially allows developers to share projects across different versions of the IDE as well. Starting with Visual Studio 2005, the project files are simply MSBuild files and are actually compatible between versions. The problem is that the solution files are not compatible.

Rick Strahl has a great [post](http://www.west-wind.com/weblog/posts/122975.aspx "Solutions between Orcas and VS 2005") that explains how to make Visual Studio 2005 and Visual Studio 2008 work together. The issue, as [Steve Harman](http://stevenharman.net/blog/Default.aspx "Multi-Targeting VS2005 and VS2008 Web Application Projects, a Gotcha!") discovered, is with Web Application projects. This was discovered while Steve was upgrading the [Subtext Project](http://subtextproject.com/ "Subtext Project") to work with Visual Studio 2008 and he describes the problem and solution in detail by using the Condition attribute in MSBuild.
