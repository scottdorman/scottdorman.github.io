---
layout: post
title: Using vs. Using
date: '2007-08-28 18:59:26 -05:00'
---

"Deuces you say", there is no difference...right? Wrong!

In the C# language, using is a [keyword](http://msdn2.microsoft.com/library/zhdeatwt(VS.80).aspx). Unfortunately, this is one of those times that a single keyword has multiple uses:

*   As a preprocessor **directive** used to create an alias for a namespace or to import types defined in other namespaces.  
*   As a **statement** used to define a scope at the end of which an object will be disposed. 

It's unfortunate that Microsoft chose to attach multiple meanings to this keyword as it tends to cause a lot of confusion for newer developers. I think it's time to try clear up some of that confusion. (This  issue only affects C#. The other .NET languages do use a different keyword for the directive and the statement forms.)

# The Using Directive

The [using Directive (C#)](http://msdn2.microsoft.com/library/sf0df423(VS.80).aspx) actually has two uses:

1.  To allow the use of types in a namespace without needing to fully qualify that type.  
2.  To create an alias for a namespace or a type. 

In both of these scenarios, the using directive must appear at the beginning of the file and it's scope is limited to the file in which it appears. If you are referencing a namespace in a different assembly, that assembly must be included in your project references. Also, there is no harm in having "unused" using directives. These are namespaces or types that are referenced by a using directive that aren't actually needed by the code. (If you're using Visual Studio 2008, there is a new [context menu]({% post_url /2007/2007-08-08-visual-studio-2008-code-editor-improvements %}) that allows you to clean these up.)

Here are some examples of the using directive. These examples are taken from the [MSDN documentation](http://msdn2.microsoft.com/library/sf0df423(VS.80).aspx), so there is nothing "magic" about them.

Example 1: Define and use a **using** alias for a namespace.

```csharp
namespace PC
{
    // Define an alias for the nested namespace.
    using Project = PC.MyCompany.Project;
    class A 
    {
        void M()
        {
            // Use the alias
            Project.MyClass mc = new Project.MyClass();
        }
    }
    namespace MyCompany
    {
        namespace Project
        {
            public class MyClass{}
        }
    }
}
```

Example 2: Define a **using** directive and a **using** alias for a class.

```csharp
// Using directive.
using System;   

// Using alias for a class.
using AliasToMyClass = NameSpace1.MyClass;   

namespace NameSpace1 
{
    public class MyClass 
    {
        public override string ToString() 
        {
            return "You are in NameSpace1.MyClass";
        }
    }
}

namespace NameSpace2 
{
    class MyClass 
    {
    }
}

namespace NameSpace3 
{
    // Using directive:
    using NameSpace1;
    // Using directive:
    using NameSpace2;

    class MainClass
    {
        static void Main() 
        {
            AliasToMyClass somevar = new AliasToMyClass();
            Console.WriteLine(somevar);
        }
    }
}
```

# The Using Statement

The [using Statement (C#)](http://msdn2.microsoft.com/library/yh598w02(VS.80).aspx) allows programmers to specify when an object (or objects) that use resources should release them. The object provided to the using statement must implement the [IDisposable Interface (System)](http://msdn2.microsoft.com/library/system.idisposable(VS.80).aspx). A using statement is exited when the end of the statement is reached or an exception is thrown and control leaves the statement block early. This is a compile time "[translation]({% post_url /2007/2007-07-21-using-garbage-collection-in-net %})" that occurs where the compiler actually translates this to a try/finally block. 

The using statement can be declared in different ways:

```csharp
// Object declared in the using statement
using (Font font1 = new Font("Arial", 10.0f))
{
}

// Object declared outside (before) the using statement
Font font2 = new Font("Arial", 10.0f);
using (font2)
{
}

// Multiple objects (must be declared inside the using statement, and must
// all be of the same type)
using (Font font3 = new Font("Arial", 10.0f), font4 = new Font("Arial", 10.0f))
{
}
```
