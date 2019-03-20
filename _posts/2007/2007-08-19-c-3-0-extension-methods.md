---
layout: post
title: C# 3.0 Extension Methods
date: '2007-08-19 01:06:42 -05:00'
---

At one time or another most of us have wished we could add functions to one of the intrinsic .NET classes. The solution has always been to either create a static (or sealed) class that contains these "helper" functions or derive a new class that adds the desired functionality.

A good example of this is testing a string to see if it contains only alphanumeric characters. In order to do this, we need to define a helper class:

```csharp
namespace DataValidationHelpers
{
    public static class DataValidation
    {
        public static bool IsAlphanumeric(string expression) 
        {
            if (expression == null)
            {
                throw new ArgumentNullException("expression");
            }

            bool success = true;

            for (int i = 0; i < expression.Length; i++)
            {
                if (!(Char.IsLetter(expression, i) || Char.IsNumber(expression, i) || Char.IsPunctuation(expression, i)
                     || Char.GetUnicodeCategory(expression, i) == UnicodeCategory.SpaceSeparator))
                {
                    success = false;
                    break;
                }
            }
            return success;
            }
    }
}
```

In order to use this method, we need to write code like

```csharp
string test = "Abc123";
bool isAlphanumeric = DataValidationHelpers.DataValidation.IsAlphanumeric(test);
```

While this solution works, it always felt kludgy or incomplete. There had to be a better way, right? What we really wanted to be able to write was code like

```csharp
string test = "Abc123";
bool isAlphanumeric = test.IsAlphanumeric();
```

Unfortunately, we weren't able to. That is, until .NET 3.5 and extension methods.

Extension methods allow a developer to add new methods to the public interface of an existing CLR type without deriving a new class or recompiling the original type. The decision to name this new class of function "extension methods" was a good choice as the name very clearly describes what these functions do. They "extend" an existing type by providing new functions that operate on that type without the need to recompile the original type, derive a new type, and allow extensions to types that are sealed which provides a natural syntax for making use of these extensions. Extension methods benefit from all of the compile-time checking you expect and also show up in the intellisense list:

![image](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image-thumb.png) 

In order to change this to an extension method, we need to make one change. That's right, one change. For C#, we need to add the "this" keyword before the first parameter. The "this" keyword in the function declaration instructs the compiler that the function extends the data type that immediately follows it. In our IsAlphanumeric function, we are telling the compiler that we are extending the String data type.

```csharp
namespace DataValidationHelpers
{
    public static class DataValidation
    {
        public static bool IsAlphanumeric(this string expression) 
        {
            if (expression == null)
            {
                throw new ArgumentNullException("expression");
            }

            bool success = true;

            for (int i = 0; i < expression.Length; i++)
            {
                if (!(Char.IsLetter(expression, i) || Char.IsNumber(expression, i) || Char.IsPunctuation(expression, i) 
                    || Char.GetUnicodeCategory(expression, i) == UnicodeCategory.SpaceSeparator))
                {
                    success = false;
                    break;
                }
            }
            return success;
            }
    }
}
```

For VB, we add an Extension attribute to the method:

```vb
Namespace DataValidationHelpers
    Public Module DataValidation
        <Extension()> _
        Public Function IsAlphanumeric(ByVal expression As String) As Boolean
            ' implementation
        End Function
    End Module
End Namesapce
```

An interesting side effect is that we actually have two ways to call the same method:

```csharp
string test="Abc123";
bool b1 = test.IsAphanumeric();
bool b2 = DataValidation.IsAlphanumeric(test);
```

In fact, the IL code generated for either line is actually the same:

```il
L_0000: ldstr "Abc123"
L_0005: stloc.0 
L_0006: ldloc.0 
L_0007: call bool [Campari.Software.Core]Campari.Software.Text.DataValidation::IsAlphanumeric(string)
L_000c: pop 
L_000d: ldloc.0 
L_000e: call bool [Campari.Software.Core]Campari.Software.Text.DataValidation::IsAlphanumeric(string)
L_0013: pop 
L_0014: ret 
```

There are only a few things to keep in mind when writing extension methods.

1.  The only places you can define extension methods are a static class (C#) or a module (VB). 
2.  You aren't actually adding methods to the class, you can only access the public members from your extension method. Logically, any extension methods that are defined on a type are available to any subclasses of that type. 
3.  For the extension method to be available, you must include the namespace containing the extension. 
4.  If the type you are extending has a real method that has the same name as the extension method, the extension method is ignored. This is important as it has comparability implications. 
5.  Extension methods for properties are not possible. 
6.  Extension properties are not possible.

Finally, even though there is no magic happening with extension methods, they do require the .NET Framework 3.5 in order to compile. You need to include a reference to System.Core (you will get a compiler error if you try to compile an extension method without including this reference), which is only available in the .NET Framework 3.5.

Extension methods help provide the power and flexibility of Linq and will provide a very significant shift in how we develop "helper" functions.
