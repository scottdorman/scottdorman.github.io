---
layout: post
title: Multi-component Installers
date: 2007-11-22 00:18:49 -05:00
---

With the deluge of blog posts talking about the recently releases of Visual Studio 2008 and the .NET Framework 3.5, Scott Guthrie [talks](http://weblogs.asp.net/scottgu/archive/2007/11/20/steps-to-uninstall-vs-2008-beta2-before-installing-the-vs-2008-final-release.aspx) about the steps to uninstall the Visual Studio 2008 Beta 2 release you should follow before installing the final release.

It's great that Scott has put together this list since it not only tells you all of the components that are installed when you install Visual Studio 2008 Beta 2 but also tells you the order to uninstall them. This post also indirectly brings to light a different problem as well.

This problem is what I call "multi-part installers". If you've installed any of the recent Microsoft developer products like Visual Studio or Microsoft SQL Server or even the new Windows Live applications, you have seen and used a multi-part installer. These are single installer applications that allow you to choose multiple (and sometimes technically unrelated) applications that install as a "bundle". Looking at Scott's post, here are all of the potential components that could have been installed when you installed Visual Studio 2008 Beta 2:

*   MSDN Library for Visual Studio 2008 Beta
*   Microsoft SQL Server Compact Edition 3.5 
*   Microsoft SQL Server Compact Edition 3.5 Design Tools 
*   Microsoft SQL Server Compact Edition 3.5 for Devices 
*   Microsoft Visual Studio Performance Collection Tools 
*   Windows Mobile 5.0 SDK R2 for Pocket PC 
*   Windows Mobile 5.0 SDK R2 for Smartphone 
*   Crystal Reports 2007 
*   Visual Studio Asset System 
*   Microsoft Visual Studio Web Authoring Component / Microsoft Web Designer Tools 
*   Microsoft Visual Studio 2005 Tools for the 2007 Microsoft Office System Runtime 
*   Microsoft Visual Studio 2005 Tools for the 2007 Microsoft Office System Runtime Language Pack (non-English editions only) 
*   Microsoft Visual Studio Tools for Office Runtime 3.0 
*   Microsoft Document Explorer 
*   Microsoft Document Explorer 2005 Language Pack (non-English editions only) 
*   Microsoft Device Emulator 3.0 
*   Microsoft .NET Compact Framework 3.5 
*   Microsoft .NET Compact Framework 2.0 SP1 
*   .NET Framework 2.0 SDK 
*   Microsoft Visual Studio Codename Orcas Remote Debugger 
*   Microsoft Visual Studio 64bit Prerequisites Beta (64-bit platforms only) 
*   Microsoft .NET Framework 3.5 

That's a lot of components and it's great that I can install all of this through a single installer. In this case, I would have installed all of these components as part of the overall Visual Studio 2008 Beta 2 installation experience. The problem comes about when I need to uninstall Visual Studio 2008 Beta 2.

Since I installed all of these components under the auspices of a single installer, why do I then need to uninstall each individual component separately? This is loaded with potential pitfalls since I might not know what components were actually installed as part of the main install and in what order those components should be uninstalled.

It seems that the trend is for the install portion to become smarter while the uninstall portion has become dumber. I realize that the vast majority of time you won't be uninstalling applications (or maybe you will...it all depends on how you use the computer), but I shouldn't be required to know the correct order to uninstall over a dozen different applications when I installed them as part of a single product. I just want to be able to select Visual Studio 2008 Beta 2 from the list of installed applications and uninstall it, knowing that all of the component applications that were installed with it will also be uninstalled correctly.

I will actually be spending the weekend doing this on two different computers and it's not something I'm particularly looking forward to.
