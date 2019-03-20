---
layout: post
title: Catching (Handling) Exceptions in .NET
date: '2007-09-26 17:42:57 -05:00'
---

It seems there is a lot of confusion on how to properly catch exceptions in .NET, especially among newer developers. There are a lot of good references available on MSDN and on the web, but a lot of these are either very advanced or just hard to follow.

I'm not going to discuss the CLR exception classes and go into the internals of how the .NET runtime generates exceptions. I don't want to discount this information, as it is helpful to know, but it isn't essential to understanding how to properly handle exceptions.

The most important thing to understand when handling exceptions is the concept of the [Try/Catch/Finally](http://msdn2.microsoft.com/en-us/library/xtd0s8kd(VS.80).aspx) block. This is a special section of code that is designed to allow you to work with exceptions. (This is a bit of a simplification, but that's the general idea.) Almost any line of code can cause an exception, but most applications don't actually need to deal with these exceptions. You should only handle an exception if there is something meaningful you can do as a result.

There are three ways you can specify a Try/Catch/Finally block:

1.  Try/Catch  
2.  Try/Finally  
3.  Try/Catch/Finally 

In order to understand the differences, it is important to first understand what the different sections are responsible for.

*   The Try block contains sections of code that might throw an exception. 
*   The Catch block contains the code that should run when an exception is encountered. 
*   The Finally block contains code that should always run, even if an exception was encountered. 

The syntax for a Try/Catch/Finally block looks like this:

```csharp
int[] array1={0,0};
int[] array2={0,0};

 try
 {
     Array.Copy(array1,array2,-1);
 }
 catch (ArgumentOutOfRangeException e)
 {
     Console.WriteLine("Error: {0}", e);
 }
 finally
 {
     Console.WriteLine("This statement is always executed.");
 }
```

The part that tends to cause problems is the Catch handlers. 

When an exception occurs, each catch block in the calling stack is given the opportunity to handle it. The proper catch block is determined by matching the type of the exception to the type of exception specified in the catch block.

A catch handler that only catches [`System.Exception`](http://msdn2.microsoft.com/en-us/library/system.exception(VS.80).aspx) or [`System.SystemException`](http://msdn2.microsoft.com/en-us/library/system.systemexception(VS.80).aspx) is called a general catch handler and should be avoided whenever possible as it can hide run-time problems and complicate debugging.

Since all exceptions in .NET inherit from `System.Exception`, this type of catch block will always match for any exception. If you think of catch blocks being evaluated in a "top down" approach, the first catch block that matches will be the one used. This means that if you put a general catch block first, none of the other catch blocks will be evaluated.

```csharp
try
 {
     //some operation that results in InvalidCastException
 }
 catch (InvalidCastException e)
 {
     Console.WriteLine("Invalid cast occurred.");
 }
 catch (Exception e)
 {
     Console.WriteLine("General catch handler.");
 }
```

In the example above, the output would be "Invalid cast occurred." However, if the catch blocks were reversed, the output would be "General catch handler."

Another common mistake is to use an empty catch handler. This is a catch handler that doesn't  specify any exceptions and just uses the Catch keyword and is a result of legacy programming habits from the .NET Framework 1.0 and 1.1 releases. 

In the .NET Framework 1.0 and 1.1 releases, there were situations where unmanaged code would throw an exception that wasn't properly handled by the runtime. As a result, it wasn't wrapped in a `System.Exception` derived exception and couldn't be caught by anything other than an empty catch block. This issue was corrected in .NET 2.0 and now these exceptions are wrapped in a `System.Runtime.CompilerServices.RuntimeWrappedException` (which inherits from System.Exception), so there is no longer a need for this empty catch block.

It is also common for people to write catch blocks that do nothing more than log the error. While this is sometimes important, it can usually be done by the top level caller and does not need to performed for each and every function. The best way to look at this situation is that you should only catch an exception if you have meaningful cleanup work that needs to be done as a result of the exception (like closing files or database connections). 

This leads to a problem known as "swallowing exceptions", and occurs when you catch an exception and either do nothing with it or don't allow it to pass up the chain. This can also lead to problems because you are effectively hiding the exception and not doing anything with it, which can lead to intermittent problems that will be very hard to track down.

While we're talking about exception swallowing, there is a similar problem known as "breaking the stack". I talk about this in detail in [another post]({% post_url /2007/2007-08-20-Difference-between-quotthrowquot-and-quotthrow-exquot-in-.NET %}), but it boils down to the fact that when you rethrow an exception you should almost always use the "throw" syntax.

Finally, if you are using a class that implements the [`System.IDisposable`](http://msdn2.microsoft.com/aax125c9.aspx) interface you can make use of the [`using` Statement (C#)](http://msdn2.microsoft.com/library/yh598w02(VS.80).aspx) to simplify the code you need to write. I talk more about the using statement in [this]({% post_url /2007/2007-08-28-Using-vs.-Using %}) post.

## References

*   [Exception Handling Fundamentals](http://msdn2.microsoft.com/en-us/library/2w8f0bss(VS.80).aspx)
*   [Exception Handling Best Practices in .NET](http://www.codeproject.com/dotnet/exceptionbestpractices.asp)
*   [How to use structured exception handling in Visual C# .NET and in Visual C# 2005](http://support.microsoft.com/default.aspx/kb/816157)
*   [Using vs. Using]({% post_url /2007/2007-08-28-Using-vs.-Using %} "Using vs. Using")
*   [Difference between "throw" and "throw ex" in .NET]({% post_url /2007/2007-08-20-Difference-between-quotthrowquot-and-quotthrow-exquot-in-.NET %})
