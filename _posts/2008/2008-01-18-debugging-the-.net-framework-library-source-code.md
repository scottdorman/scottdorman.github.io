---
layout: post
title: Debugging the .NET Framework Library Source Code
date: 2008-01-18 00:06:22 -05:00
---

A while ago, I [talked](http://geekswithblogs.net/sdorman/archive/2007/10/05/.NET-Framework-Library-Source-Code.aspx) about Microsoft releasing the source code for the .NET Framework in order for you to debug it through Visual Studio 2008. Just a few days ago, it was finally released. [Shawn Burke](http://blogs.msdn.com/sburke/archive/2008/01/16/configuring-visual-studio-to-debug-net-framework-source-code.aspx) has an excellent and detailed post explaining how to set this up and also has a trouble shooting section.

Currently, the following libraries have been released:

*   NET Base Class Libraries (including System, System.CodeDom, System.Collections, System.ComponentModel, System.Diagnostics, System.Drawing, System.Globalization, System.IO, System.Net, System.Reflection, System.Runtime, System.Security, System.Text, System.Threading, etc). 
*   ASP.NET (System.Web, System.Web.Extensions) 
*   Windows Forms (System.Windows.Forms) 
*   Windows Presentation Foundation (System.Windows) 
*   ADO.NET and XML (System.Data and System.Xml) 

I have set this up on one of my development systems and it works well. I'll like it better when I can download all of the symbols in one shot, but this works for now.
