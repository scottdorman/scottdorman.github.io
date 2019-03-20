---
layout: post
title: "CLR 4.0: Code Contracts"
date: '2008-11-07 14:58:51 -05:00'
tags: .net
---

If anyone is familiar with the Microsoft Research (MSR) project [Spec#](http://research.microsoft.com/SpecSharp/) you will be familiar with the idea of contract based programming. CLR 4.0 takes the idea of contract based programming (and more specifically code contracts to ensure code validity) from Spec# and adds it to the CLR. This now means that code contracts are available to any .NET language.

The premise behind code contracts is that you (the programmer) know a lot about your code, including when input arguments should and shouldn't be null (or other bad inputs) and what the return value properties of a method should be.

Before code contracts there were very few ways to tell the compiler or runtime about this metadata and have it help look for errors. With code contracts in CLR 4.0, you now have this ability.

```csharp
public void BuyMoreStuff(Item[] cart, ref Decimal totalCost, Item i)
{       
    CodeContract.Requires(totalCost >=0);
    CodeContract.Requires(cart != null);
    CodeContract.Requires(CodeContract.ForAll(cart, s => s != i));

    CodeContract.Ensures(CodeContract.Exists(cart, s => s == i);
    CodeContract.Ensures(totalCost >= CodeContract.OldValue(totalCost));
    CodeContract.EnsuresOnThrow<IOException>(totalCost == CodeContract.OldValue(totalCost));

    // Do some stuff
    ...
}
```

As you can see, there is a new static class `CodeContract` that makes the contracts available. This allows you to go way beyond simple Assert statements and will actually allow you to (almost) declaratively specify certain rules about your method inputs and outputs.

Code contracts are split into two different categories: pre-conditions (which are very much like Asserts) and post-conditions. The pre-conditions (like Requires) are actually translated by the compiler to the correct code for you while the post-conditions are handled by a postprocessor (essentially an IL rewriter) to insert the appropriate code before each return statement in the function.

It's probably a safe bet that C# 5.0 will include some simplified syntax sugar to make using contracts even easier, and possibly some attributes to handle this as well.
