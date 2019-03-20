---
layout: post
title: Debugging in Visual Studio 2005 with a Symbol Server
date: '2007-05-23 16:21:20 -05:00'
---

We have all had the experience of debugging an application in Visual Studio and run into the problem of not having the debugging symbols or having incorrect symbols. This is particularly true when you need to step into .NET CLR code to track down a problem. 

Microsoft maintains a public symbol server that provides symbols for the different Windows operating system versions, MDAC, IIS, ISA, and the .NET Framework. This server is for symbol downloads only and is not browseable. In addition to the Microsoft symbol server, you can create your own local symbol server for your own application on either a network share or your own local machine.

In order to setup a symbol server, open the **Options** dialog, then open the **Debugging** node and click **Symbols**. To use the Microsoft symbol server, enter 

> [http://msdl.microsoft.com/download/symbols](http://msdl.microsoft.com/download/symbols)

as a new symbol file (.pdb) location by clicking the ![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image-0-10.png) button and editing the text. You will need to enter a path for the cache directory, which can be either a network share or a local directory.

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image-0-5.png) 

Once you click the **OK** button, an End User License Agreement dialog will appear (only if you use the Microsoft public symbol store). Once you click **Yes** to accept the agreement, the symbols will be automatically downloaded to your local cache.
