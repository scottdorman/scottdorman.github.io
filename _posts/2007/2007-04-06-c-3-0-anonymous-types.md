---
layout: post
title: C# 3.0 Anonymous Types
date: '2007-04-06 13:29:00 -05:00'
---

Anonymous types are a new language feature introduced in the C# 3.0 release. For those that remember your set theory, an anonymous type is described as a tuple type that is automatically inferred and created from its object initializer. An object initializer specifies the values from one or more fields (or properties) of an object. Another way to look at this is that the object initializer specifies the named parameters that passed to an object.

All of this happens at compile time, so anonymous types are still strongly typed. In reality, the compiler automatically creates a class that represents the anonymous type. For example, 

```
var product = new {Name = "C# Rocks!", Price = 3};
```

automatically gets translated by the compiler to something that looks like this:

```
<class __Anonymous1
{
   private string name;
   private int price;

   public string Name
   {
      get { return name; }
      set { name = value; }
   }

   public int Price
   {
      get { return price; }
      set { price = value; }
   }
}

__Anonymous1 product = new __Anonymous1();
product.Name = "C# Rocks!";
product.Price = 3;</font>
```

While anonymous types might not seem all that useful on the surface, they are the cornerstone for LINQ. Without anonymous types, LINQ would not be able to create types dynamically. This is what allows LINQ to query for an arbitrary set of data, without first having the structure declared.
