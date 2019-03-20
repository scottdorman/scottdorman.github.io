---
layout: post
title: "CLR 4.0: Managed Languages"
date: '2008-11-10 10:26:58 -05:00'
tags: .net
---

Over the years .NET has been a great platform for multiple languages, and actually launched with support for 16 different languages. Up until recently, however, it has been difficult (but not impossible) to create functional and dynamic languages for .NET.

With the release of CLR 4.0, Microsoft is officially releasing IronPython, IronRuby, F#, and several other functional or dynamic languages. In order to do this, the CLR is gaining support for a few language features that are common in these types of languages, specifically support for:

*   Big Integers
*   Tuples
*   Tail Recursion  

Big Integer support was a request from both the F# and Python languages and was co-implemented with the Microsoft Optima team. (This is the team that works on the [Microsoft Solver Foundation](http://code.msdn.microsoft.com/solverfoundation), which is a brand new framework and managed code runtime for mathematical programming, modeling, and optimization.)

Tuples were also a request from both the F# and Python languages and provide the ability to create classes on the fly. The real benefit, especially to C# and VB developers is that now there is a built-in data type which will allow multiple return values.
 
```csharp
public Tuple<Int32, Int32> DivAndRemainder(Int32 i, Int32 j) 
{
    return new Tuple.Create(i/j, i%j);
}

// Accessing items in a tuple.  
for (Int16 i = 0; i <= 25; i++)
{
    for (Int16 j = 1; j <= 5; j++) 
    {
        var tuple = DivAndRemainder(i,j);
        Console.WriteLine("{0}\t{1}\t{2}\t{3}\n", i, j, tuple.item1, tuple.item2);
    }
}
```

Tuples are implemented as a generic class, in a very similar fashion to the Func<T> and Action<T> classes. C# and VB.NET don't get the same syntax support in the language (in F# or Python you create a tuple with syntax like* (4, "Hello World")* which is very concise), but this is almost as easy (and there may possibly be some syntax support in C# 5.0).

Also requested by the F# team is support for tail recursion. Tail recursion is relatively rare in C# and other procedural languages so this is more important for the functional languages that will be supported.
