---
layout: post
title: More on .NET 4.0 Code Contracts
date: '2008-12-10 13:36:25 -05:00'
tags: c#
---

Last month I [talked]({% post_url /2008/2008-11-07-clr-4.0-code-contracts %}) about Code Contracts, which are one of the new features in .NET 4.0. Earlier today I was digging around in [.NET Reflector](http://www.red-gate.com/products/reflector/) looking for something totally unrelated when I came across the Microsoft.Contracts namespace in System.Core.

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image_4.png) 

Looking at the [Contract](code://System.Core:3.5.0.0:b77a5c561934e089/Microsoft.Contracts.Contract) class reveals some custom exception types and a bunch of static methods that look surprisingly similar to what will be available in the CodeContract class in .NET 4.0.

What does this mean? It means that Microsoft internally was already using code contracts in .NET 3.5 but they weren't available to the rest of us. 

If you recall from my previous post, I mentioned that the CodeContract support in .NET 4.0 was based on the work done in [Spec#](http://research.microsoft.com/SpecSharp/). Looking at the disassembly of the Contracts class, specifically any of the methods that represent a post-condition evaluation, reveals a [System.Diagnostics.ConditionalAttribute](http://msdn2.microsoft.com/y5dw26w3.aspx) declaration with a value of "USE_SPECSHARP_ASSEMBLY_REWRITER". 

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image_6.png) 

This attribute very clearly indicates that the code contract portions of Spec# had already made their way in to the .NET Framework with version 3.5. Not only that, but using the analyzer capabilities of [Reflector](http://www.red-gate.com/products/reflector/) show that the Contract class is being used by some of the Microsoft.Win32.SafeHandles and System.Security.Cryptography classes. 

Running [Reflector](http://www.aisto.com/roeder/dotnet/) against the .NET 4.0 CTP reveals that the CodeContract class is very similar to the Contract class. It turns out that not only do all of the places that previously used the internal Contract class now use the new CodeContract class but a lot of new classes use it as well (including System.AddIn). The old Contract class is still present, but no longer used.

A few differences are that the new CodeContract class has more methods available and the Conditional attribute appears to have changed from USE_SPECSHARP_ASSEMBLY_REWRITER to CONTRACTS_PRECONDITIONS and CONTRACTS_FULL Conditional attributes. 

The other important thing to realize is that the Assert and Assume methods are also marked with a DEBUG conditional which means that they will only appear in debug builds.
