---
layout: post
title: C# 3.0 Type Inference
date: 4/6/2007 12:32:00 PM
---

One of the new language features of the C# 3.0 language release is type inference. Wikipedia has an excellent [discussion](http://en.wikipedia.org/wiki/Type_inference) on type inference, including a non-technical and technical explanation.

C# 3.0 introduces the concept of type inference with the <font face="Courier New" color="#000080">var</font> keyword. At first glance, this looks a lot like the old <font face="Courier New" color="#000080">Variant</font> keyword of Visual Basic. **It isn't!**

One of the compelling features of C# is that it is a strongly typed language whose variables are statically typed. The <font face="Courier New" color="#000080">var</font> keyword doesn't change this; it simply lets the compiler infer the variables data type from its context. To help clear this mystery up, lets look at an example:

In C# 2.0, you can write:

> <font face="Courier New" color="#000080">int i;
> i = 1;</font>

or simply:  

> <font face="Courier New" color="#000080">int i = 1; </font>

In C# 3.0, you can also write this as:  

> <font face="Courier New" color="#000080">var i = 1;</font>

What this actually means to the compiler is that the variable ***i*** is of the same data type as it's initializer. In this case, ***i*** would end up being compiled as an <font face="Courier New" color="#000080">int.</font> The key here is that ***i*** is still strongly typed. The other thing to realize is that the <font face="Courier New" color="#000080">var</font> keyword is only valid within the body of a method. You can't use it define class-wide variables that have an inferred type.  

The <font face="Courier New" color="#000080">var</font> keyword was added to support anonymous types, another new feature in C# 3.0. Without this keyword, you wouldn't be able to create a variable of an anonymous type if you always needed to specify the type. An interesting side-effect of the <font face="Courier New" color="#000080">var</font> keyword is that you no longer have to specify the type name twice when you declare a variable.  

> <font face="Courier New" color="#000080">List<string> list = new List<string>();</font>
> 
> <font face="Courier New" color="#000080">var list = new List<string>();</font>

The most important things to remember are:  

1.  1.  <font face="Courier New" color="#000080">var != object != Variant</font>  You can only use the <font face="Courier New" color="#000080">var</font> keyword inside a method body.
