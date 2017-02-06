---
layout: post
title: Null Object pattern follow up
date: '2008-07-04 09:51:08 -05:00'
---

My earlier post on the [Null Object pattern]({% post_url 2008-05-25-null-object-pattern %}) led to a few critiques about the fact that I was presenting an extension method to do what is essentially a very simple logical test, and, as a result, doesn't provide much value.

For reference, here is the original extension method from that post


```csharp
public static class NullObjectExtenstions
{
    public static bool IsNull(this object source)
    {
        return (source == null);
    }
}
```

Yes, this is an extremely simple method and performs a very basic logical test. However, consider the static IsNullOrEmtpy function on String (taken from [Reflector](http://www.aisto.com/roeder/dotnet/)):

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

I would argue that this is a relatively simple method and performs two very basic logical tests. What is the benefit to using IsNullOrEmpty? In a word, **<u>consistency</u>**. By using IsNullOrEmpty, I know that every time I need to perform this test it is executing the exact same code in the same order. I don't have to worry about someone accidentally testing "Length == 0" before the "!= null" and causing a NullReferenceExcpetion.

This same benefit applies to the IsNull extension method. It introduces that consistency (although I agree this test is still very trivial) for testing nullability. As I mentioned in my comments, the better choice for the extension method would probably have been an IsNotNull method. Here is a more complete NullObjectExtensions class:

```csharp
public static class NullObjectExtenstions
{
    public static bool IsNull<T>(this T source) where T : class
    {
        return (source == null);
    }

    public static bool IsNotNull<T>(this T source) where T : class
    {
        return (source != null);
    }
}
```
