---
layout: post
title: Visual Studio 2013 RC
date: '2013-09-09 14:34:58 -05:00'
tags: visual-studio
---

If you want to build Windows 8.1 apps or just want to see what's new with Visual Studio and the .NET Framework, you can now [download](http://go.microsoft.com/fwlink/p/?LinkId=306566) the Visual Studio 2013 RC.

There are a lot of new features and improvements, but almost all of them are aimed at making our life as a developer easier.

If you do any XAML development (and if you're building on the Microsoft stack today you almost certainly do), there are several improvements, including:

*   IntelliSense for Data Binding to the XAML editor.  This works with a DataContext defined in the markup, or with a design-time DataContext for cases where the context is provided in code-behind.
*   Support for Go To Definition for Resources, Bindings, Properties and XAML Elements.support for Go To Definition for Resources, Bindings, Properties and XAML Elements.

For much more detail on these improvements, see Harikrishna Menon's [post](http://blogs.msdn.com/b/visualstudio/archive/2013/08/09/xaml-editor-improvements-in-visual-studio-2013.aspx) on the Visual Studio blog.

If you want to build modern business applications that can use the power of Office 365 as part of your application, you can use the Office 365 Cloud Business App template. See Soma's [post](http://blogs.msdn.com/b/somasegar/archive/2013/06/27/build-2013-day-2.aspx) from Build 2013 for more details about this template.

For C++ developers, Microsoft has made more steps along the roadmap laid out at Build, adding C++ 11 features like *using* aliases, *= default* and non-static data member initializers. For more details, check out Herb Sutter's ["The Future of C++"](http://channel9.msdn.com/Events/Build/2013/2-306) talk from Build.

To me, however, one of the most exciting new features (available in Visual Studio Ultimate) is CodeLens, available for C# and Visual Basic.

{% include post/image.html image-file="ic677894-1916188352.png" alt="" %}

Think of CodeLens as a heads-up display for your code. You can use it to get faster answers about the code:

*   Find changes to your code and who made those changes
*   References
*   Bugs, work items, and code review requests.
*   Find and run unit tests for methods and properties.

All of this allows you to stay in the editor longer and stay focused on your work. More details about the CodeLens feature are [available on MSDN](http://msdn.microsoft.com/en-us/library/vstudio/dn269218(v=vs.120).aspx).
