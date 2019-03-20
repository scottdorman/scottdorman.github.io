---
layout: post
title: Getting a custom attribute
date: '2009-06-08 13:31:58 -05:00'
tags: c#
---

Attribute programming has a lot of benefits and, when done correctly, can greatly simplify the amount of code that you need to write. One drawback to using attributes is that the code required to retrieve a custom attribute from a type is a bit cumbersome and is very repetitious.

Given a type, the simplest way to retrieve a custom attribute is code like
 
```csharp
CustomAttribute attribute = Attribute.GetCustomAttribute(customType.GetType(), typeof(CustomAttribute), true) as CustomAttribute;
```

While this is simple code, it doesn't handle any error conditions and requires that you always remember to perform the cast. A more complete method would look like

```csharp
public static CustomAttribute GetAttribute(MemberInfo element)  
{  
    CustomAttribute attribute = null;  

    try  
    {  
        attribute = Attribute.GetCustomAttribute(element, typeof(CustomAttribute), true) as CustomAttribute;  
    }  
    catch  
    {  
        // We aren't really interested in the exceptions here, but if we do get an exception  
        // just return null;  
        attribute = null;  
    }  

    return attribute;  
}
```

This nicely encapsulates the error handling and casting, but introduces another drawback. In order to make use of this method you would need to include it on every custom attribute you create, being sure to change the types appropriately.

We can make this more practical by changing to a generic extension method with very little effort

```csharp
public static T GetAttribute<T>(this MemberInfo element) where T: Attribute  
{  
    T attribute = null;  

    if (element != null)  
    {  
        try  
        {  
            attribute = Attribute.GetCustomAttribute(element, typeof(T), true) as T;  
        }  
        catch  
        {  
            // We aren't really interested in the exceptions here, but if we do get an exception  
            // just return null;  
            attribute = null;  
        }  
    }  

    return attribute;  
}
```

The benefit here is that, because this is implemented as an extension method it is available as if it were a real method call on any class derived from `MemberInfo`, which happens to be the base class for all of the `Type` classes.

Now, we can define our custom attributes without any special consideration to providing a strongly typed `GetAttribute` method and when we want to retrieve a custom attribute, we can use code that now looks like

```csharp
CustomAttribute attribute = customType.GetType().GetAttribute<CustomAttribute>();
```

It might not look like a major change in the calling site, but we are now able to quickly and easily get a strongly typed attribute given an instance type.
