---
layout: post
title: Visual Studio 2008 Code Editor Improvements
date: 8/8/2007 9:16:55 PM
---

Scott Guthrie has a great blog [post](http://weblogs.asp.net/scottgu/archive/2007/07/28/nice-vs-2008-code-editing-improvements.aspx) about some really cool editor improvements in Visual Studio 2008. As Scott points out, one of the big annoyances with VS2005 as the fact that the intellisense window obscures any code behind it. In VS2008, if you hold down the "Ctrl" while the Intellisense window is visible it will switch to a semi-transparent mode that allows you to see the code beneath it. When you release the "Ctrl" key, it switches back to normal.

![](http://www.scottgu.com/blogposts/b2intellisense/step2.jpg)

There are a lot of improvements for VB developers, but one of the improvements for C# is the "Organize Usings" context menu.

![](http://www.scottgu.com/blogposts/b2intellisense/step13.jpg)

This allows you to better organizing your "using" statements, including the ability to sort them alphabetically (a pet peeve of both Scott and myself) and to remove any un-necessary declarations (another pet peeve of mine). It does this by analyzing the types used in the code file and automatically removes namespaces that are declared but not needed to support them.
