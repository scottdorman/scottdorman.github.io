---
layout: post
title: Using Garbage Collection in .NET
date: 7/21/2007 7:06:38 PM
---

Garbage collection is one of the most fundamental aspects of the .NET Common Language Runtime (CLR) and is available to all .NET programming languages. Unfortunately, it also seems to be one of the more difficult concepts to understand correctly, both how it works and how to use it.

Understanding how the garbage collection system in .NET works is important, but it isn't as important as understanding how to use it correctly. Think about your car...we generally don't have intimate knowledge of how the engine works and all of the other systems in the car tie together, but we do need to know how to operate it correctly. For instance, we need to know that it isn't safe to open the door while driving or that it is recommended to change the oil every 3000 miles (or if you have one of the newer cars, every 6000 miles).

That sounds vaguely important, so let me say it again: 

> It is more important to understand how to use the garbage collection system in .NET than it is to understand how it works.

Knowing how the garbage collection system works is important, especially if you are writing your own class libraries or working with a lot of unmanaged code. In that case, you also need to know how to [Implement IDisposable and the Dispose Pattern properly](http://www.codeproject.com/KB/dotnet/idisposable.aspx "Implementing IDisposable and the Dispose Pattern Properly").

However, knowing how to properly use the garbage collection system is more important. Using the garbage collection system correctly is critical to ensure the proper, timely cleanup of resources. Unfortunately, there is nothing in .NET that forces you to call **Dispose** when you are done using a class instance and nothing that forces you to use proper exception handling to make sure that **Dispose** is called even when an exception is thrown.

Just because the language runtime doesn't force a usage pattern on you doesn't mean it isn't important. If the object you are using implements **IDisposable** (or even just a public **Dispose** method), you should properly scope the code and then dispose of the resource in a **try/finally** block. Without the **try/finally** block, the call to **Dispose** will never be reached if the calling methods cause an exception.

How do you tell if the object you're using implements **IDisposable**? If it's a Base Class Library (BCL) class, you can look at the documentation on MSDN. You can also look at the source code using a tool like [Reflector](http://www.aisto.com/roeder/dotnet), or the [Koders.com](http://koders.com/) search engine.

Looking at the documentation isn't always straight forward, however. The class may implement **IDisposable** as a result of another class in it's inheritance chain. Look at [**SqlConnection**](http://msdn2.microsoft.com/en-us/library/system.data.sqlclient.sqlconnection(vs.80).aspx), for example. It implements **IDisposable**, but only because it's parent [**DbConnection**](http://msdn2.microsoft.com/en-us/library/system.data.common.dbconnection(VS.80).aspx) does.

Generally, if the class exposes a public **Dispose** method, it is a safe bet that it implements the **IDisposable** interface. In addition, some classes implement a public **Close** method instead of **Dispose**, and some implement both. In these cases, it is important to look at the documentation to determine what the **Close** method and/or the **Dispose** method do. In the case of **SqlConnection**, the **Close** and **Dispose** methods are functionally equivalent.

Now that we have some ideas of how to identify a class that implements **IDisposable**, what do we do with it? In other words, how do we write code that will make sure that **Dispose** is called?

If you are using C# or VB, you get a little extra help here. Both of these .NET languages implement a language keyword named **using**. (For C# developers, this is the **using** *statement*, not the **using** *directive*.) The **using** statement provides a syntax shortcut for declaring a **try/finally** block. The statement can be exited when the end of the code block is reached or an exception is thrown and control leaves the block before the end of the statement. The object provided to the **using** statement must implement **IDisposable**. 

For example, the following C# code

<div style="BORDER-RIGHT: gray 1px solid; PADDING-RIGHT: 4px; BORDER-TOP: gray 1px solid; PADDING-LEFT: 4px; FONT-SIZE: 8pt; PADDING-BOTTOM: 4px; MARGIN: 20px 0px 10px; OVERFLOW: auto; BORDER-LEFT: gray 1px solid; WIDTH: 97.5%; CURSOR: text; MAX-HEIGHT: 200px; LINE-HEIGHT: 12pt; PADDING-TOP: 4px; BORDER-BOTTOM: gray 1px solid; FONT-FAMILY: consolas, 'Courier New', courier, monospace; BACKGROUND-COLOR: #f4f4f4">
<div style="PADDING-RIGHT: 0px; PADDING-LEFT: 0px; FONT-SIZE: 8pt; PADDING-BOTTOM: 0px; OVERFLOW: visible; WIDTH: 100%; COLOR: black; BORDER-TOP-STYLE: none; LINE-HEIGHT: 12pt; PADDING-TOP: 0px; FONT-FAMILY: consolas, 'Courier New', courier, monospace; BORDER-RIGHT-STYLE: none; BORDER-LEFT-STYLE: none; BACKGROUND-COLOR: #f4f4f4; BORDER-BOTTOM-STYLE: none">


<span style="COLOR: #606060">   1:</span> <span style="COLOR: #0000ff">public</span> <span style="COLOR: #0000ff">void</span> DoWork()

<span style="COLOR: #606060">   2:</span> {

<span style="COLOR: #606060">   3:</span>     <span style="COLOR: #0000ff">using</span> (MyClass myClass = <span style="COLOR: #0000ff">new</span> MyClass())

<span style="COLOR: #606060">   4:</span>     {

<span style="COLOR: #606060">   5:</span>         myClass.SomeMethod();

<span style="COLOR: #606060">   6:</span>     }

<span style="COLOR: #606060">   7:</span> }

</div>
</div>


is automatically translated by the compiler to

<div style="BORDER-RIGHT: gray 1px solid; PADDING-RIGHT: 4px; BORDER-TOP: gray 1px solid; PADDING-LEFT: 4px; FONT-SIZE: 8pt; PADDING-BOTTOM: 4px; MARGIN: 20px 0px 10px; OVERFLOW: auto; BORDER-LEFT: gray 1px solid; WIDTH: 97.5%; CURSOR: text; MAX-HEIGHT: 300px; LINE-HEIGHT: 12pt; PADDING-TOP: 4px; BORDER-BOTTOM: gray 1px solid; FONT-FAMILY: consolas, 'Courier New', courier, monospace; HEIGHT: 289px; BACKGROUND-COLOR: #f4f4f4">
<div style="PADDING-RIGHT: 0px; PADDING-LEFT: 0px; FONT-SIZE: 8pt; PADDING-BOTTOM: 0px; OVERFLOW: visible; WIDTH: 100%; COLOR: black; BORDER-TOP-STYLE: none; LINE-HEIGHT: 12pt; PADDING-TOP: 0px; FONT-FAMILY: consolas, 'Courier New', courier, monospace; BORDER-RIGHT-STYLE: none; BORDER-LEFT-STYLE: none; BACKGROUND-COLOR: #f4f4f4; BORDER-BOTTOM-STYLE: none">


<span style="COLOR: #606060">   1:</span> <span style="COLOR: #0000ff">public</span> <span style="COLOR: #0000ff">void</span> DoWork()

<span style="COLOR: #606060">   2:</span> {

<span style="COLOR: #606060">   3:</span>     MyClass myClass = <span style="COLOR: #0000ff">new</span> MyClass(); 

<span style="COLOR: #606060">   4:</span>  

<span style="COLOR: #606060">   5:</span>     <span style="COLOR: #0000ff">try</span>

<span style="COLOR: #606060">   6:</span>     {

<span style="COLOR: #606060">   7:</span>         myClass.SomeMethod();

<span style="COLOR: #606060">   8:</span>     }

<span style="COLOR: #606060">   9:</span>     <span style="COLOR: #0000ff">finally</span>

<span style="COLOR: #606060">  10:</span>     {

<span style="COLOR: #606060">  11:</span>         <span style="COLOR: #0000ff">if</span> (myClass != <span style="COLOR: #0000ff">null</span>)

<span style="COLOR: #606060">  12:</span>         {

<span style="COLOR: #606060">  13:</span>             IDisposable disposable = myClass;

<span style="COLOR: #606060">  14:</span>             disposable.Dispose();

<span style="COLOR: #606060">  15:</span>         }

<span style="COLOR: #606060">  16:</span>     }

<span style="COLOR: #606060">  17:</span>  }

</div>
</div>


The bottom line is this:

> If the class implements **IDisposable**, there's a reason for it and any instances should have their lifetime properly scoped to help the garbage collector do it's job. Unless there is a **very** compelling reason not to, you should call **Dispose** as early as possible and ensure that it will be called even if there are exceptions.

If you want to understand the internals of how garbage collection works, there are numerous resources available, including two articles written by Jeffery Richter for MSDN Magazine, that do an excellent job. If you want more information on how to implement the **IDisposable** pattern, look at my [article](http://www.codeproject.com/KB/dotnet/idisposable.aspx "Implementing IDisposable and the Dispose Pattern Properly"), [Joe Duffy's blog post](http://www.bluebytesoftware.com/blog/PermaLink,guid,88e62cdf-5919-4ac7-bc33-20c06ae539ae.aspx), or the *[Framework Design Guidelines](http://www.amazon.com/gp/redirect.html?ie=UTF8&location=http%3A%2F%2Fwww.amazon.com%2FFramework-Design-Guidelines-Conventions-Development%2Fdp%2F0321246756%3Fie%3DUTF8%26s%3Dbooks%26qid%3D1185056635%26sr%3D1-1&tag=scotdorm-20&linkCode=ur2&camp=1789&creative=9325 "Framework Design Guidelines")*.

Here is a partial list of references:

<li>Ben Albahari, Peter Drayton, and Brad Merrill. [*C# Essentials (2nd Edition)*](http://www.amazon.com/gp/redirect.html?ie=UTF8&location=http%3A%2F%2Fwww.amazon.com%2FC-Essentials-2nd-Ben-Albahari%2Fdp%2F0596003153%3Fie%3DUTF8%26s%3Dbooks%26qid%3D1185053097%26sr%3D8-1&tag=scotdorm-20&linkCode=ur2&camp=1789&creative=9325 "C# Essentials (2nd Edition)").O'Rielly Media, Inc., Sebastopol, CA, 2001. </li>
<li>Thuan Thai and Hoang Q. Lam. *[.NET Framework Essentials (2nd Edition)](http://www.amazon.com/gp/redirect.html?ie=UTF8&location=http%3A%2F%2Fwww.amazon.com%2FNET-Framework-Essentials-Thuan-Thai%2Fdp%2F0596003021%3Fie%3DUTF8%26s%3Dbooks%26qid%3D1185056424%26sr%3D1-2&tag=scotdorm-20&linkCode=ur2&camp=1789&creative=9325 ".NET Framework Essentials (2nd Edition)")*. O'Rielly Media, Inc., Sebastopol, CA, 2003. </li>
<li>Venkat Subramaniam. *[.NET Gotchas](http://www.amazon.com/gp/redirect.html?ie=UTF8&location=http%3A%2F%2Fwww.amazon.com%2FNET-Gotchas-Venkat-Subramaniam%2Fdp%2F0596009097%3Fie%3DUTF8%26s%3Dbooks%26qid%3D1185056546%26sr%3D1-1&tag=scotdorm-20&linkCode=ur2&camp=1789&creative=9325 ".NET Gotchas")*. O'Rielly Media, Inc., Sebastopol, CA, 2005. </li>
<li>Juval Löwy. *[Programming .NET Components, Second Edition](http://www.amazon.com/gp/redirect.html?ie=UTF8&location=http%3A%2F%2Fwww.amazon.com%2FProgramming-NET-Components-Second-Juval%2Fdp%2F0596007620%3Fie%3DUTF8%26s%3Dbooks%26qid%3D1185056579%26sr%3D1-1&tag=scotdorm-20&linkCode=ur2&camp=1789&creative=9325 "Programming .NET Components, Second Edition")*. O'Reilly Media, Inc., Sebastopol, CA, 2005. </li>
<li>Krzysztof Cwalina and Brad Abrams. *[Framework Design Guidelines](http://www.amazon.com/gp/redirect.html?ie=UTF8&location=http%3A%2F%2Fwww.amazon.com%2FFramework-Design-Guidelines-Conventions-Development%2Fdp%2F0321246756%3Fie%3DUTF8%26s%3Dbooks%26qid%3D1185056635%26sr%3D1-1&tag=scotdorm-20&linkCode=ur2&camp=1789&creative=9325 "Framework Design Guidelines")*. Addison Wesley, Upper Saddle River, NJ, 2005. </li>
<li>Jeffery Richter. [Garbage Collection: Automatic Memory Management in the Microsoft .NET Framework"](http://msdn.microsoft.com/msdnmag/issues/1100/GCI/). *MSDN Magazine, November 2000*. </li>
<li>Jeffery Richter. [Garbage Collection - Part 2: Automatic Memory Management in the Microsoft .NET Framework"](http://msdn.microsoft.com/msdnmag/issues/1200/GCI2/). *MSDN Magazine, December 2000*. </li>
<li>Jeffery Richter. [*CLR via C#, Second Edition*](http://www.amazon.com/gp/redirect.html?ie=UTF8&location=http%3A%2F%2Fwww.amazon.com%2FCLR-via-Second-Pro-Developer%2Fdp%2F0735621632%3Fie%3DUTF8%26s%3Dbooks%26qid%3D1185058872%26sr%3D1-1&tag=scotdorm-20&linkCode=ur2&camp=1789&creative=9325 "CLR via C#, Second Edition"). Microsoft Press. 2006. </li>
<li>[DG Update: Dispose, Finalization, and Resource Management](http://www.bluebytesoftware.com/blog/PermaLink,guid,88e62cdf-5919-4ac7-bc33-20c06ae539ae.aspx) (Joe Duffy's Weblog, April 8, 2005) </li>
<li>Scott Dorman. [Implementing IDisposable and the Dispose Pattern properly](http://www.codeproject.com/KB/dotnet/idisposable.aspx "Implementing IDisposable and the Dispose Pattern Properly"). *The Code Project, August 2006.*


*<font size="1">[Update, 22-Jan-2008: Updated the article link for Code Project.]</font>*

</li>
