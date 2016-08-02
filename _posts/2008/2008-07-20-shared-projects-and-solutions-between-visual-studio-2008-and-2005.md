---
layout: post
title: Shared Projects and Solutions between Visual Studio 2008 and 2005
date: 2008-07-20 12:17:44 -05:00
---

There are still a large number of developers that have both Visual Studio 2005 and 2008 installed on the same machine and probably an even larger number of development teams that use a mixture of VS 2008 and 2005. 

[DJ Park](http://blogs.msdn.com/djpark/archive/2007/11/07/how-to-use-solutions-and-projects-between-visual-studio-2005-and-2008.aspx), one of the PM's on the Visual Studio team has a great blog post that explains the possibilities and limitations of using solutions and projects between both versions of Visual Studio.

To quickly summarize:

*   Solutions created in Visual Studio 2008 **<u>cannot</u>** be opened in Visual Studio 2005.
*   Projects created in Visual Studio 2008 **<u>can</u>** be opened in Visual Studio 2005.
*   Solutions and projects created in Visual Studio 2005 **<u>can</u>** be opened in Visual Studio 2008.  

Be sure to take a look at DJ's post as well if you want to know the specific differences in the solution and project files between the versions. He does an excellent job explaining the differences and shows some ways to work around some of the restrictions.
