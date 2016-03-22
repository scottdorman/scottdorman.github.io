---
layout: post
title: Stop Visual Studio From Automatically Connecting to TFS
date: 2/24/2008 7:53:09 PM
---

A while ago I came across this excellent tip from [Colin Beales](http://blogs.msdn.com/colinbeales/archive/2007/11/02/stop-connecting-to-tfs-on-visual-studio-2005.aspx) that explains how to stop Visual Studio from automatically connecting to a TFS server when it starts up. I didn't need it until this weekend, but it works great and shortens the startup time as well. The tip couldn't be simpler and works for both Visual Studio 2005 and Visual Studio 2008.

In order to make this change, you will need to modify the registry so be sure to back it up first. After that, add a DWORD value named AutoLoadServer to the HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\9.0\TeamFoundation key and set the value to 0. Setting it to 1 (or deleting the key) will cause the "normal" behavior. (For Visual Studio 2005, change the 9.0 in the registry key above to read 8.0.)
