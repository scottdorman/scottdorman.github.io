---
layout: post
title: Using Garbage Collection in .NET
date: '2007-07-21 19:06:38 -05:00'
---

Garbage collection is one of the most fundamental aspects of the .NET Common Language Runtime (CLR) and is available to all .NET programming languages. Unfortunately, it also seems to be one of the more difficult concepts to understand correctly, both how it works and how to use it.

Understanding how the garbage collection system in .NET works is important, but it isn't as important as understanding how to use it correctly. Think about your car...we generally don't have intimate knowledge of how the engine works and all of the other systems in the car tie together, but we do need to know how to operate it correctly. For instance, we need to know that it isn't safe to open the door while driving or that it is recommended to change the oil every 3000 miles (or if you have one of the newer cars, every 6000 miles).

That sounds vaguely important, so let me say it again: 

> It is more important to understand how to use the garbage collection system in .NET than it is to understand how it works.

Knowing how the garbage collection system works is important, especially if you are writing your own class libraries or working with a lot of unmanaged code. In that case, you also need to know how to [Implement IDisposable and the Dispose Pattern properly](http://www.codeproject.com/KB/dotnet/idisposable.aspx).

However, knowing how to properly use the garbage collection system is more important. Using the garbage collection system correctly is critical to ensure the proper, timely cleanup of resources. Unfortunately, there is nothing in .NET that forces you to call **Dispose** when you are done using a class instance and nothing that forces you to use proper exception handling to make sure that **Dispose** is called even when an exception is thrown.

Just because the language runtime doesn't force a usage pattern on you doesn't mean it isn't important. If the object you are using implements **IDisposable** (or even just a public **Dispose** method), you should properly scope the code and then dispose of the resource in a **try/finally** block. Without the **try/finally** block, the call to **Dispose** will never be reached if the calling methods cause an exception.

How do you tell if the object you're using implements **IDisposable**? If it's a Base Class Library (BCL) class, you can look at the documentation on MSDN. You can also look at the source code using a tool like [Reflector](http://www.aisto.com/roeder/dotnet), or the [Koders.com](http://koders.com/) search engine.

Looking at the documentation isn't always straight forward, however. The class may implement **IDisposable** as a result of another class in it's inheritance chain. Look at [**SqlConnection**](http://msdn2.microsoft.com/en-us/library/system.data.sqlclient.sqlconnection(vs.80).aspx), for example. It implements **IDisposable**, but only because it's parent [**DbConnection**](http://msdn2.microsoft.com/en-us/library/system.data.common.dbconnection(VS.80).aspx) does.

Generally, if the class exposes a public **Dispose** method, it is a safe bet that it implements the **IDisposable** interface. In addition, some classes implement a public **Close** method instead of **Dispose**, and some implement both. In these cases, it is important to look at the documentation to determine what the **Close** method and/or the **Dispose** method do. In the case of **SqlConnection**, the **Close** and **Dispose** methods are functionally equivalent.

Now that we have some ideas of how to identify a class that implements **IDisposable**, what do we do with it? In other words, how do we write code that will make sure that **Dispose** is called?

If you are using C# or VB, you get a little extra help here. Both of these .NET languages implement a language keyword named **using**. (For C# developers, this is the **using** *statement*, not the **using** *directive*.) The **using** statement provides a syntax shortcut for declaring a **try/finally** block. The statement can be exited when the end of the code block is reached or an exception is thrown and control leaves the block before the end of the statement. The object provided to the **using** statement must implement **IDisposable**. 

For example, the following C# code

```csharp
public void DoWork()
{
   using (MyClass myClass = new MyClass())
   {
      myClass.SomeMethod();
   }
}
```

is automatically translated by the compiler to

```csharp
public void DoWork()
{
   MyClass myClass = new MyClass();
   try
   {
      myClass.SomeMethod();
   }
   finally
   {
      if (myClass != null)
      {
         IDisposable disposable = myClass;
         disposable.Dispose();
      }
   }
}
```

The bottom line is this:

> If the class implements **IDisposable**, there's a reason for it and any instances should have their lifetime properly scoped to help the garbage collector do it's job. Unless there is a **very** compelling reason not to, you should call **Dispose** as early as possible and ensure that it will be called even if there are exceptions.

If you want to understand the internals of how garbage collection works, there are numerous resources available, including two articles written by Jeffery Richter for MSDN Magazine, that do an excellent job. If you want more information on how to implement the **IDisposable** pattern, look at my [article](http://www.codeproject.com/KB/dotnet/idisposable.aspx), [Joe Duffy's blog post](http://www.bluebytesoftware.com/blog/PermaLink,guid,88e62cdf-5919-4ac7-bc33-20c06ae539ae.aspx), or the *[Framework Design Guidelines](http://amzn.to/28JOJA1)*.

Here is a partial list of references:

* [C# Essentials](http://amzn.to/28M3fX6)
* [.NET Framework Essentials](http://amzn.to/28IJrmC)
* [.NET Gotchas](http://amzn.to/28JRVvj)
* [Programming .NET Components](http://amzn.to/28JudAR)
* [Framework Design Guidelines](http://amzn.to/28JOJA1)
* [Garbage Collection: Automatic Memory Management in the Microsoft .NET Framework](http://msdn.microsoft.com/msdnmag/issues/1100/GCI/)
* [Garbage Collection - Part 2: Automatic Memory Management in the Microsoft .NET Framework](http://msdn.microsoft.com/msdnmag/issues/1200/GCI2/)
* [CLR via C#](http://amzn.to/28JSmWn)
* [DG Update: Dispose, Finalization, and Resource Management](http://www.bluebytesoftware.com/blog/PermaLink,guid,88e62cdf-5919-4ac7-bc33-20c06ae539ae.aspx)
* [Implementing IDisposable and the Dispose Pattern properly](http://www.codeproject.com/KB/dotnet/idisposable.aspx)

*<small>[Update, 22-Jan-2008: Updated the article link for Code Project.]</small>*