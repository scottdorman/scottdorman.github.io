---
layout: post
title: Implementing IDisposable and the Dispose pattern, take 2
date: 2006-09-01 08:08:00 -05:00
---

My [article](http://www.codeproject.com/KB/dotnet/idisposable.aspx) on how to properly implement the IDisposable interface and the Dispose pattern has been very well received. There have been several comments that prompted me to review the article against the [Framework Design Guidelines](http://amzn.to/28JOJA1), and specifically against the [updates](http://www.bluebytesoftware.com/blog/CategoryView,category,DesignGuideline.aspx) made by Joe Duffy.

In doing this, not only have I learned a few new things about how the whole garbage collection process works, but I also discovered that some of the statements made in my article were incorrect.

This is discouraging for me in two ways. First, it means that everyone reading the article is getting false information. However, it also means that the original sources I used for the article were wrong as well. Some of those authors are very well respected in the .NET development community at Microsoft (in fact, at least one has helped design the Framework with [Anders](http://en.wikipedia.org/wiki/Anders_Hejlsberg)).

As soon as I discovered the discrepancies I went to work on updating the article, which turned in to an almost complete rewrite. (The article actually went from about 7 printed pages to 21!)

Despite the fact that the article expanded so much, I hope it is still serves as a good beginners guide to implementing the Dispose pattern properly.

*<small>[Update, 22-Jan-2008: Updated the article link for Code Project.]</small>*
