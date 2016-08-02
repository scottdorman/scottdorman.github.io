---
layout: post
title: C# 3.0 Type Inference
date: 2007-04-06 12:32:00 -05:00
---

One of the new language features of the C# 3.0 language release is type inference. Wikipedia has an excellent [discussion](http://en.wikipedia.org/wiki/Type_inference) on type inference, including a non-technical and technical explanation.

C# 3.0 introduces the concept of type inference with the `var` keyword. At first glance, this looks a lot like the old `Variant` keyword of Visual Basic. **It isn't!**

One of the compelling features of C# is that it is a strongly typed language whose variables are statically typed. The `var` keyword doesn't change this; it simply lets the compiler infer the variables data type from its context. To help clear this mystery up, lets look at an example:

In C# 2.0, you can write:

```csharp
int i;
i = 1;
```

or simply:  

```csharp
int i = 1; 
```

In C# 3.0, you can also write this as:  

```csharp
var i = 1;
```

What this actually means to the compiler is that the variable ***i*** is of the same data type as it's initializer. In this case, ***i*** would end up being compiled as an int. The key here is that ***i*** is still strongly typed. The other thing to realize is that the var keyword is only valid within the body of a method. You can't use it define class-wide variables that have an inferred type.  

The var keyword was added to support anonymous types, another new feature in C# 3.0. Without this keyword, you wouldn't be able to create a variable of an anonymous type if you always needed to specify the type. An interesting side-effect of the var keyword is that you no longer have to specify the type name twice when you declare a variable.  

```csharp
List<string> list = new List<string>();
var list = new List<string>();
```

The most important things to remember are:  

1. var != object != Variant 
2. You can only use the `var` keyword inside a method body.
