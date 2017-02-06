---
layout: post
title: CI Factory
date: '2007-03-17 09:36:00 -05:00'
---

As you know, I'm working with the [Subtext](http://www.subtextproject.com/) project. Subtext uses [CruiseControl.NET](http://confluence.public.thoughtworks.org/display/CCNET/Welcome+to+CruiseControl.NET) (CC.NET) as it's [continuous integration](http://confluence.public.thoughtworks.org/display/CCNET/What+is+Continuous+Integration) (CI) build system. One of the nice features of CC.NET is the web dashboard that provides the visibility in to the builds. Over the last month, I have been upgrading the Subtext [dashboard](http://build.subtextproject.com/ccnet/) with a new look and feel as well as some additional features. As a result, the dashboard caught the attention of [Jay Flowers](http://jayflowers.com/), who owns the [CI Factory](http://jay.flowers.googlepages.com/cifactory) project.

For those of you who don't know about CI Factory, it is a turnkey solution to provide a working CI server in just a few minutes. It's a great concept that removes a lot of the complex work of setting up CC.NET and creating custom [NAnt](http://nant.sourceforge.net/) build scripts. The other nice thing about CI Factory is that it can be pretty easily extended by adding new Packages. A package is essentially a self-contained CI Factory extension that adds functionality for one specific technology. Right now, CI Factory comes with the following packages as part of the install:

*   Visual Source Safe
*   Subversion
*   PVCS Tracker
*   .NET Visual Studio 2003/2005 solution compilation
*   Unit Test execution with MbUnit
*   Code Coverage with CoverageEye
*   nDepend
*   Deployment artifact publication
*   InstallShield or VS Deployment packages
*   Assembly and product version 

There are also third-party packages available for:

*   Ant
*   VB6 Compile
*   Lines of Code
*   MSTest
*   NCover
*   Backup
*   Simian
*   Analytics 

Since CI Factory is built on top of CC.NET, it also offers a web dashboard. Jay and I have started discussions regarding enhancing the CI Factory dashboard to give it a custom look and feel that matches the CI Factory website look and possibly extending the customizations to a few pre-defined looks to choose from. It's all in the very early stages of discussion, but it should help make an already good product even more appealing.
