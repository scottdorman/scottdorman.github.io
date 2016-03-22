---
layout: post
title: Visual J# Retiring
date: 3/4/2007 12:24:00 PM
---

I'm sure there's a clearer explanation somewhere, but reading the [announcement](http://msdn2.microsoft.com/en-us/vjsharp/default.aspx) on the J# home page is just a bit confusing. So far, what I've been able to piece together is that Visual J# 2.0 Redistributable will still be released sometime in Q2 of 2007 and support for English locales will continue through 20017. Along with this, the Visual J# 2.0 Redistributable Second Edition will also be released that will enable Visual J# code to run natively on 64-bit versions of Windows and the .NET Framework, with support for .NET 2.0 and higher.

This all sounds great if you're a Java/J# developer. Now comes the confusing part.

The J# product and the Java Language Conversion Assistant (JLCA) tool are being retired. According to the announcement, 

> ...customers have told us [Microsoft] that the existing J# feature set largely meets their needs and usage of J# is declining, Microsoft is retiring the Visual J# product...the J# language and JLCA tool will not be available in future versions of Visual Studio. To preserver existing customer investments...continue to support the J# and JLCA technology that shipped with Visual Studio 2005 through 2015.

Why is adding 64-bit support important? This seems like a waste of resources given the following statements from the announcement:

1.  The feature set largely meets client needs
2.  Usage of J# is declining
3.  The product is being retired 

When does support actually end? There are two different dates listed in the announcement: 2015 and 2017. it isn't entirely clear what ends when. As best as I can tell, the dates play out like this:

1.  2015 - End of support for the version of J# and the JLCA tool that shipped with Visual Studio 2005
2.  2017 - End of support for the Visual J# 2.0 Redistributable Second Edition 

This product retirement doesn't affect me in the least as I'm not a J# developer. I liked the Java language since it had a lot of promise, but it wasn't great on the follow through. Anyway, the thing that will be interesting to watch is if Microsoft makes counterparts in C# and VB for some of the more common J# libraries that people import, mostly the Zip and Unzip capabilities.
