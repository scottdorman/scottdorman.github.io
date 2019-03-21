---
layout: post
title: "C# 4.0: Dynamic Programming"
date: '2008-11-16 10:11:44 -05:00'
tags: c#
---

If C# 3.0 was all about Language Integrated Query (LINQ), then C# 4.0 is all about dynamic programming. What exactly does that mean? It means that C# 4.0 brings some of flexibility and declarative style of programming to C#.

{% include post/image.html image-file="image-3.png" alt="" %} 

But what does that really mean?

To sum it up in one keyword: dynamic.

C# 4.0 is adding a new `dynamic` keyword which is used as a data type in much the same way the `var` keyword is used. Why is this important? The biggest reason is that it allows a C# program to use dynamic dispatch to more naturally create objects coming from a dynamic language.

For example, suppose you have a Calculator object declared in C#, meaning it is statically typed. You interact with your object like this:

```csharp
Calculator calc = GetCalculator();
int sum = calc.Add(10, 20);
```

That's pretty simple and straight forward. Now suppose the Calculator is not a statically typed .NET class (or it is a .NET class but you don't know the specific type of class), you must do something like this:

```csharp
object calc = GetCalculator();
Type calcType = calc.GetType();
object res = calcType.InvokeMember("Add",
    BindingFlags.InvokeMethod, null,
    new object[] { 10, 20 });
int sum = Convert.ToInt32(res);
```

That's not nearly as simple. In fact, it's downright ugly. There is a lot of non-type-safe calls and reflection going on here that you really shouldn't have to see. 

To take this a step further, if we knew that Calculator was a JavaScript class, you must use similar (but still significantly different) code:

```csharp
ScriptObject calc = GetCalculator();
object res = calc.Invoke("Add", 10, 20);
int sum = Convert.ToInt32(res);
```

The reason for the differences in syntax is that there is no unification between the two APIs.

In C# 4.0, you can now use the following syntax:

```csharp
dynamic calc = GetCalculator();
int sum = calc.Add(10, 20);
```

If you look at this syntax and the earlier statically typed call, you should notice that the only difference is that in C# we are declaring the data type to be dynamic.

{% include post/image.html image-file="image-6.png" alt="" %} 

Does this mean that C# is loosing it's roots as a statically typed language or that we should all start moving towards dynamic languages? Absolutely not. What is means is that it is now easier for you to write C# code that talks to objects (or APIs) written in dynamically typed languages. It also means that there is a unified API to talk to any dynamic language. You no longer need to worry about what language you are interoperating with to determine which C# code you must write.

So how does the dynamic keyword work? As I mentioned, it's a keyword in a similar fashion to var. You declare at compile-time the type to be dynamic, but at run-time you get a strongly typed object.

{% include post/image.html image-file="image-9.png " alt="" %} 

The dynamic keyword is great for writing C# code that consumes a dynamic object, but what about going the other direction and writing C# code that can be called from a dynamic language? You do this by implementing the `IDynamicObject` interface (or more simply, inheriting from the abstract `DynamicObject` class) and providing your own implementation for the member lookup and invocation.

Using the features and capabilities of the new dynamic keyword, the `IDynamicObject` interface, and the fact that the dynamic dispatch can dispatch to both dynamic and static types, C# effectively gets support for duck-typing.
