---
layout: post
title: MSBuildContrib January Release
date: '2008-01-25 04:48:28 -05:00'
---

I have just uploaded a [new release](https://www.codeplex.com/Release/ProjectReleases.aspx?ProjectName=MSBuildContrib&ReleaseId=10182) of [MSBuildContrib](http://www.codeplex.com/MSBuildContrib) which brings the current list of tasks to:
 
|**NAnt/NAntContrib Task**|**MSBuildContrib Task**|**Status**|**Description**|
|----|----|----|----|
|attrib|Attrib|Complete|Changes the file attributes of a file or set of files and directories.|
|checksum|Checksum|Complete|Calculates checksums for a set of files.|
|codestats|CodeStats|Complete|Generates statistics from source code.|
|concat|Concat|Complete|A task that concatenates a set of files.|
|fxcop|FxCop|**Complete***|Analyzes managed code assemblies using the Microsoft FxCop.|
|gac-install|GacUtil|Complete|Installs assemblies into the Global Assembly Cache (GAC) by using the gacutil SDK tool.|
|gac-uninstall|GacUtil|Complete|Uninstalls assemblies into the Global Assembly Cache (GAC) by using the gacutil SDK tool.|
|grep|Grep|Complete|Searches files for a regular-expression and produces an XML report of the matches.|
|move|Move|Complete|Moves a file or set of files to a new file or directory.|
|regex|CreateItemRegex|**Complete***|Sets project properties based on the evaluation of a regular expression.|
|sysinfo|GetEnvironment|Complete|Sets properties with system information.|
||CheckDiskspace|**Complete***|Reports any local fixed disks that are less than the minimum available space.|
||UpdateItemMetadata|**Complete***|Adds or updates metadata to an item.|

\* Task was recently added.   

Thank you to everyone who downloaded the previous release. As always, there is still a long way to go, so if you are interested in helping out please let me know and I will add you to the project. Also, if you have implemented tasks and want to have them added to MSBuildContrib let me know.
