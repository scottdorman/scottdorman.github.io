---
layout: post
title: MSBuildContrib project on CodePlex
date: '2007-12-23 12:14:11 -05:00'
tags: msbuild
---

[MSBuildContrib](http://www.codeplex.com/MSBuildContrib) is the project for tasks and tools that aren't in MSBuild. This is similar to the [NAntContrib](http://nantcontrib.sourceforge.net/) project and will be incorporating as many of the [NAnt](http://nant.sourceforge.net/) and NAntContrib tasks as possible. There is still a long way to go, so if you are interested in helping out please let me know and I will add you to the project.

Here is the list of NAnt or NAntContrib tasks that are planned and the current status:

|**NAnt/NAntContrib Task**|**MSBuildContrib Task**|**Status**|**Description**|
|---|----|---|---|
|codestats|CodeStats|Complete|Generates statistics from source code.|
|gac-install|GacUtil|Complete|Installs assemblies into the Global Assembly Cache (GAC) by using the gacutil SDK tool.|
|gac-uninstall|GacUtil|Complete|Uninstalls assemblies into the Global Assembly Cache (GAC) by using the gacutil SDK tool.|
|grep|Grep|Complete|Searches files for a regular-expression and produces an XML report of the matches.|
|attrib|Attrib|In Progress|Changes the file attributes of a file or set of files and directories.|
|checksum|Checksum|In Progress|Calculates checksums for a set of files. Loosely based on Ant's Checksum task.|
|concat|Concat|In Progress|A task that concatenates a set of files. Loosely based on Ant's Concat task.|
|mail|Mail|Planned|Sends an SMTP message.|
|move|Move|In Progress|Moves a file or set of files to a new file or directory.|
|servicecontroller|ServiceController|Planned|Allows a Windows service to be controlled.|
|sleep|Sleep|Planned|A task for sleeping a specified period of time, useful when a build or deployment process requires an interval between tasks.|
