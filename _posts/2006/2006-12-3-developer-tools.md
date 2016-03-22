---
layout: post
title: Developer Tools
date: 12/3/2006 9:48:00 AM
---

As a developer I use a lot of additional tools to get my work done in the most efficient and accurate way possible. That involves a lot of things, such as unit testing, code analysis and additional productivity inside the Visual Studio 2005 IDE. I have seen a lot of blog posts extolling the virtues of one tool or another, but there were not many (at least that I could find) that provided a semi-comprehensive list. (I say "semi-comprehensive" because there is always going to be a new tool available that the list maker doesn't know about or hasn't updated the list.) I am going to try to fill that void by providing such a list.

Some of these tools I personally use and some I do not. The purpose of this list is to provide a list of available tools, not just document the ones that I use. I will note which ones I have not used. Most of the descriptions have been taken from the respective sites.

* * *

**Code Coverage**
 <div style="margin-left: 16px"> 

**NCover and NCoverExplorer**

NCover provides statistics about your code, telling you how many times each line of code was executed during a particular run of the application.  The most common use of code coverage analysis is to provide a measurement of how thoroughly your unit tests exercise your code.  After running your unit tests under NCover, you can easily pinpoint sections of code that are poorly covered and write unit tests for those portions.  Code coverage measurement is a vital part of a healthy build environment. 

NCoverExplorer allows you to open a coverage.xml file produced by NCover and navigate the source code. The source code is highlighted to clearly show which statements were visited and not visited. You can filter, sort and report on the coverage results.

[http://ncover.org/site/](http://ncover.org/site/ "http://ncover.org/site/")

[http://www.kiwidude.com/blog/](http://www.kiwidude.com/blog/ "http://www.kiwidude.com/blog/")
</div> 

* * *

**Unit Testing**
 <div style="margin-left: 16px"> 

**NUnit**

NUnit is a unit-testing framework for all .Net languages. Initially ported from [JUnit](http://www.junit.org), the current production release, version 2.2, is the fourth major release of this xUnit based unit testing tool for Microsoft .NET. It is written entirely in C# and has been completely redesigned to take advantage of many .NET language features, for example custom attributes and other reflection related capabilities. NUnit brings xUnit to all .NET languages.

[http://www.nunit.org](http://www.nunit.org)

**MbUnit**

MbUnit is an advanced, extensible unit testing framework. As in NUnit, tests are created at runtime using Reflection and custom attributes. MbUnit differentiates itself from NUnit in it's extensibility model. It contains a number of tests that go beyond the simple unit testing, such as combinatorial testing, data oriented testing, etc... 

[http://www.mertner.com/confluence/display/MbUnit/Home](http://www.mertner.com/confluence/display/MbUnit/Home)

*I have not personally used MbUnit.*
</div> 

* * *

**Code Analysis**
 <div style="margin-left: 16px"> 

**FxCop**
 <div style="margin-left: 12px"> 

FxCop is a code analysis tool that checks .NET managed code assemblies for conformance to the Microsoft .NET Framework Design Guidelines. It uses reflection, MSIL parsing, and callgraph analysis to inspect assemblies for more than 200 defects in the following areas: 

*   Library design  Localization  Naming conventions  Performance  Security </div> 

[http://www.gotdotnet.com/team/fxcop/](http://www.gotdotnet.com/team/fxcop/ "http://www.gotdotnet.com/team/fxcop/")
</div> 

* * *

**Visual Studio 2005 IDE Add-Ons**
 <div style="margin-left: 16px"> 

**MzTools** (not free)

MZ-Tools allows you to write code, find code, design your forms, document your applications, and review their quality **much faster** than you do it today. **It saves you valuable time each and every time you use it**. Tens of thousands of satisfied developers worldwide have found MZ-Tools to be invaluable.

[http://www.mztools.com/index.htm](http://www.mztools.com/index.htm "http://www.mztools.com/index.htm")

**PowerToys for Visual Studio**

Power Toys Pack Installer - [http://www.codeplex.com/PackInstaller](http://www.codeplex.com/PackInstaller "http://www.codeplex.com/PackInstaller")

Resource Refactoring Tool - [http://www.codeplex.com/ResourceRefactoring](http://www.codeplex.com/ResourceRefactoring "http://www.codeplex.com/ResourceRefactoring")

VS Command Shell - [http://www.codeplex.com/VSCmdShell](http://www.codeplex.com/VSCmdShell "http://www.codeplex.com/VSCmdShell")

VS Window Manager - [http://www.codeplex.com/VSWindowManager](http://www.codeplex.com/VSWindowManager "http://www.codeplex.com/VSWindowManager")

Source Code Outliner - [http://www.codeplex.com/SourceCodeOutliner](http://www.codeplex.com/SourceCodeOutliner "http://www.codeplex.com/SourceCodeOutliner")
</div> 

* * *

**Documentation Generators**
 <div style="margin-left: 16px"> 

**NDoc**

NDoc generates class library documentation from .NET assemblies and the XML documentation files generated by the C# compiler (or with an [add-on tool for VB.NET](http://www.gotdotnet.com/workspaces/workspace.aspx?id=112b5449-f702-46e2-87fa-86bdf39a17dd)).

[http://ndoc.sourceforge.net/](http://ndoc.sourceforge.net/ "http://ndoc.sourceforge.net/")
</div> 

* * *

**Miscellaneous Tools**  

 <div style="margin-left: 16px"> 

**Reflector for .NET**

Reflector is the class browser, explorer, analyzer and documentation viewer for .NET. Reflector allows to easily view, navigate, search, decompile and analyze .NET assemblies in C#, Visual Basic and IL.  

[http://www.aisto.com/roeder/dotnet/](http://www.aisto.com/roeder/dotnet/ "http://www.aisto.com/roeder/dotnet/")

**[http://www.aisto.com/Incoming/Reflector/AddIns/](http://www.aisto.com/Incoming/Reflector/AddIns/ "http://www.aisto.com/Incoming/Reflector/AddIns/")**  

**Resourcer for .NET**  

Resourcer is an editor for .resources binaries and .resX XML file formats used with the .NET platform. The program allows the integration of bitmaps, icons and text strings into resource packages. Resourcer allows editing of name/string pairs, import of various kinds of data formats (bitmaps, icons, etc) and merging of resources from different sources.  

[http://www.aisto.com/roeder/dotnet/](http://www.aisto.com/roeder/dotnet/ "http://www.aisto.com/roeder/dotnet/")

**Snippet Compiler**  

This is a great tool that allows you to edit and run snippets of code. It has absolutely nothing to do with the Visual Studio 2005 snippets.

[http://www.sliver.com/dotnet/SnippetCompiler/](http://www.sliver.com/dotnet/SnippetCompiler/ "http://www.sliver.com/dotnet/SnippetCompiler/")

**Compare It!** (not free)

Compare It! is a full featured visual files compare and merge tool. It helps you to compare and work with different versions of the same text file. A color-coded side-by-side comparison makes it easy to understand differences between two files at a glance, powerful editing engine helps you to merge found changes.

[http://www.grigsoft.com/wincmp.htm](http://www.grigsoft.com/wincmp.htm "http://www.grigsoft.com/wincmp.htm")
</div>
