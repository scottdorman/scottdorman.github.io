---
layout: post
title: .NET Framework Library Source Code
date: '2007-10-05 00:00:35 -05:00'
---

I'm sure most of you are familiar with [Reflector](http://www.aisto.com/roeder/dotnet/). If you're not you should download it immediately and become familiar with it. It is an invaluable tool for looking at .NET assemblies and decompiling them to C#, Visual Basic or even IL. I have used both Reflector and [Rotor](http://www.microsoft.com/downloads/details.aspx?FamilyId=8C09FD61-3F26-4555-AE17-3121B4F51D4D&displaylang=en) extensively to investigate how the .NET runtime is actually doing things.

I have done this for various reasons, including trying to track down bugs in my code. Why would I need to look at what the runtime is doing to find a bug in my code? Most of the time it's to try and find out why one of my event handler is running when I'm not expecting it to or why it isn't running when I thought it should. No matter what the reason, it always involved looking at the .NET runtime source code in some external tool rather than in a debugger.

Yesterday, Scott Guthrie [announced](http://weblogs.asp.net/scottgu/archive/2007/10/03/releasing-the-source-code-for-the-net-framework-libraries.aspx) that the source code for the .NET Framework libraries is being made available for .NET 3.5 and Visual Studio 2008 later this year. That, in and of itself, isn't the big news in this announcement since we've already had access to this through Reflector or Rotor. The big news is that you will actually be able to enable debug support for the libraries.

The first libraries to be released will the the source code (complete with comments) for:

*   .NET Base Class Libraries (System, System, System.IO, System.Collections, System.Configuration, System.Threading, System.Net, System.Security, System.Runtime, System.Text)
*   ASP.NET (System.Web)
*   Windows Forms (System.Windows.Forms)
*   ADO.NET (System.Data)
*   XML (System.Xml)
*   WPF (System.Windows) 

Libraries for WCF, Workflow and LINQ will be added shortly after that.

The source code will be released under the [Microsoft Reference License](http://www.microsoft.com/resources/sharedsource/licensingbasics/referencelicense.mspx) (MS-RL) and you will also be able to download it as a standalone install which you could browse using any text editor or through integrated debugging support in Visual Studio 2008. You can check out [Podcast](http://www.hanselminutes.com/default.aspx?showid=101) that [Scott Hanselman](http://www.hanselman.com/blog/) and [Shawn Burke](http://blogs.msdn.com/sburke/) recently recorded.  Shawn is also going to be publishing a cool [Channel9 video](http://channel9.msdn.com/) later this week that shows using the VS 2008 integrated debugging support with it.

While I agree with Scott that having source code access and debugger integration of the .NET Framework libraries will provide better insight into how the .NET Framework libraries are implemented and enable developers to build better applications, it is this same insight that can potentially cause problems. By providing such easy access, the chance becomes higher that developers will start making decisions based on specific implementation details rather than the documented public API. Hopefully, I'm just being pessimistic and seeing a possible outcome that won't actually happen.
