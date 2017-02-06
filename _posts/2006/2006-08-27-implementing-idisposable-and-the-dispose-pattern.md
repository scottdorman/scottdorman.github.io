---
layout: post
title: Implementing IDisposable and the Dispose pattern
date: '2006-08-27 20:34:00 -05:00'
---

I just posted a new [article](http://www.codeproject.com/KB/dotnet/idisposable.aspx) on Code Project that explains the proper way to implement the IDisposable interface and the Dispose pattern.

Implementing `IDisposable` is something that often times gets skipped over and when it does get implemented, it is usually implemented simply by following the interface template.

Unfortunately, this doesn't cover all of the situations where the class's resources should be released. This article hopes to dispel some of the myths around implementing the Dispose pattern and provides the rules to implement it properly.

*<small>[Update, 22-Jan-2008: Updated the article link for Code Project.]</small>*
