---
layout: post
title: Debugging Finalizers
date: '2007-10-25 22:24:24 -05:00'
---

For the last few years, I've tried to make more .NET developers aware of the [IDisposable](http://msdn2.microsoft.com/aax125c9.aspx) interface, the Dispose pattern, and the importance of having at least a basic understanding of how the Garbage Collector works. I have one [article](http://www.codeproject.com/KB/dotnet/idisposable.aspx) on [The Code Project](http://www.codeproject.com/) and various blog posts (see [Catching (Handling) Exceptions in .NET]({% post_url 2007-09-26-Catching-Handling-Exceptions-in-.NET %}), [Using vs. Using]({% post_url 2007-08-28-Using-vs.-Using %}), [.NET 3.5 changes to GC.Collect]({% post_url 2007-08-26-.NET-3.5-changes-to-GC.Collect %}), or [Using Garbage Collection in .NET]({% post_url 2007-07-21-using-garbage-collection-in-.net %})) that talk about these topics. I have also presented an advanced Memory Management presentation at various Code Camps.

In the November 2007 issue of [MSDN Magazine](http://msdn.microsoft.com/msdnmag), [Stephen Toub](http://msdn.microsoft.com/msdnmag/find/?type=Au&phrase=Stephen%20Toub&words=exact) presents a solution in [.NET Matters](http://msdn.microsoft.com/msdnmag/issues/07/11/NETMatters/) that solves the problem of making sure that other developers using your custom type dispose of it properly. Stephen mentions that Visual Studio and FxCop can help with this by performing static analysis on the code. Rule [CA2000 (Dispose objects before losing scope)](http://msdn2.microsoft.com/ms182289) checks to see if any local IDisposable objects are created and then not disposed of before all references to the object are out of scope.

This rule can only do so much. In an effort to help complete the solution, Stephen presents a method that will warn developers when your type is garbage collected without having been disposed by using a debugging finalizer.

This is a very unique way of using a finalizer because it will only be present in debug builds of your code, so it alleviates the runtime performance costs associated with having a finalizer. This is a very well thought out generic solution to a fairly common problem. I highly recommend checking it out and if you write custom types that implement IDisposable you should consider implementing this solution.

*<small>[Update, 22-Jan-2008: Updated the article link for Code Project.]</small>*
