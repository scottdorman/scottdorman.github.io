---
layout: post
title: MSBuildContrib Updates
date: '2007-12-24 10:42:58 -05:00'
---

I know I just [mentioned]({% post_url 2007-12-23-msbuildcontrib-project-on-codeplex %}) this project yesterday, but I wanted to thank those of you who have already downloaded it. Hopefully you have found it useful so far. I have already updated the project for the 1.0.2913.51352 release, which adds a few new tasks and cleans up some of the existing ones.

Here is the current list of tasks:

|**NAnt/NAntContrib Task**|**MSBuildContrib Task**|**Status**|**Description**|
|-------------------------|-----------------------|----------|---------------|
|attrib                   |Attrib                 |Complete\*|Changes the file attributes of a file or set of files and directories.|
|checksum                 |Checksum|Complete\*|Calculates checksums for a set of files.|
|codestats                |CodeStats|Complete|Generates statistics from source code.|
|concat|Concat|Complete\*|A task that concatenates a set of files.|
|gac-install|GacUtil|Complete|Installs assemblies into the Global Assembly Cache (GAC) by using the gacutil SDK tool.|
|gac-uninstall|GacUtil|Complete|Uninstalls assemblies into the Global Assembly Cache (GAC) by using the gacutil SDK tool.|
|grep|Grep|Complete|Searches files for a regular-expression and produces an XML report of the matches.|
|move|Move|Complete\*|Moves a file or set of files to a new file or directory.|
|sysinfo|GetEnvironment|Complete\**|Sets properties with system information.|

\* Task was recently added.      
\** This task was actually in the first release, I forgot to mention it.

The following tasks are currently planned for a later release.

|**NAnt/NAntContrib Task**|**MSBuildContrib Task**|**Description**|
|---|---|---|
|asminfo|AssemblyInfo|Generates an AssemblyInfo file using the attributes given.|
|fxcop|FxCop|Analyzes managed code assemblies using the Microsoft FxCop.|
|get|RequestUrl|Gets a particular file from a URL source.|
|iniread|IniFileRead|Reads String values in INI files.|
|iniwrite|IniFileUpdate|Sets String values in INI files.|
|mail|SendMailMessage|Sends an SMTP message.|
|nantschema|MSBuildContribSchema|Creates an XSD file for all available tasks.|
|nunit2|NUnit|Runs tests using the NUnit V2.2 framework.|
|regex|CreatePropertyRegex|Sets project properties based on the evaluation of a regular expression.|
|servicecontroller|ServiceController|Allows a Windows service to be controlled.|
|sleep|Sleep|Sleeps a specified period of time.|
|style|Style|Processes a document via XSLT.|
|tstamp|Timestamp|Sets properties with the current date and time.|
|unzip|Unzip|Extracts files from a zip file.|
|uptodate|UpToDate|Check modification dates on groups of files.|
|version|VersionNumber|Increments a four-part version number stored in a text file.|
|xmlpeek|XmlRead|Extracts text from an XML file at the location specified by an XPath expression.|
|xmlpoke|XmlUpdate|Replaces text in an XML file at the location specified by an XPath expression.|
|zip|Zip|Creates a zip file from the specified filesets.|
