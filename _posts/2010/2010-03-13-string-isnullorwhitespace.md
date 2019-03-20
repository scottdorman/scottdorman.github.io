---
layout: post
title: String.IsNullOrWhiteSpace
date: '2010-03-13 13:10:11 -05:00'
tags: .net c# coding-style code-standards
---

An empty string is different than an unassigned string variable (which is null), and is a string containing no characters between the quotes (""). The .NET Framework provides `String.Empty` to represent an empty string, and there is no practical difference between ("") and `String.Empty`.

One of the most common string comparisons to perform is to determine if a string variable is equal to an empty string. The fastest and simplest way to determine if a string is empty is to test if the Length property is equal to 0. However, since strings are reference types it is possible for a string variable to be null, which would result in a runtime error when you tried to access the Length property. 

Since testing to determine if a string is empty is such a common occurrence, the .NET Framework provides the static method `String.IsNullOrEmpty` method:

```csharp
public static bool IsNullOrEmpty(string value)
{
    if (value != null)
    {
        return (value.Length == 0);
    }
    
    return true;
}
```
It is also very common to determine if a string is empty and contains more than just whitespace characters. For example, `String.IsNullOrEmpty`("   ") would return false, since this string is actually made up of three whitespace characters. In some cases, this may be acceptable, but in many others it is not. To help simplify testing this scenario, the .NET Framework 4 introduces the `String.IsNullOrWhiteSpace` method:

```csharp
public static bool IsNullOrWhiteSpace(string value)
{
    if (value != null)
    {
        for (int i = 0; i < value.Length; i++)
        {
            if (!char.IsWhiteSpace(value[i]))
            {
                return false;
            }
        }
    }

    return true;
}
```
Using either `String.IsNullOrEmpty` or `String.IsNullOrWhiteSpace` helps ensure correctness, readability, and consistency, so they should be used in all situations where you need to determine if a string is null, empty, or contains only whitespace characters.
