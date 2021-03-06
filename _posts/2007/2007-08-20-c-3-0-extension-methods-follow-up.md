---
layout: post
title: C# 3.0 Extension Methods Follow Up
date: '2007-08-20 12:05:15 -05:00'
---

As I mentioned in my [previous post]({% post_url /2007/2007-08-19-c-3-0-extension-methods %}), if you create an extension method with the exact same signature as an existing method your extension will be ignored. However, one thing that I didn't mention is that if the extension method has a different signature, it will show up in that methods overload list.

To make this a little bit clearer, if you create the following extension method

```csharp
   1: namespace DataValidationHelpers
   2: {
   3:     public static class DataValidation
   4:     {
   5:         public static string ToString(this string source, IFormatProvider provider)
   6:         {
   7:             return source.ToString(provider);
   8:         }
   9:     }
  10: }
```

You will not see this as an overload on `ToString`. The reason for this is that the compiler can't disambiguate the two calls, so it doesn't even try and just ignores your extension. You can still write the extension method and still call it, but you would need to use the more "traditional" syntax of calling it through the helper class:

```csharp
   1: string testValue = "abcdefg";
   2: DataValidation.ToString(testValue, CultureInfo.CurrentUICulture);
```

I think this is the best approach. If extension methods were allowed to override an existing method and change it's functionality we would see a huge number of problems cropping up. For better or worse, we are stuck with the functionality  provided by the original designers of the object you are extending. If you want to change that functionality, you can still do so but you are forced to use a more explicit style both for writing the extension and for calling it.

However, if you wrote this extension method

```csharp
namespace DataValidationHelpers
{
    public static class DataValidation
    {
        public static string ToString(this string source, IFormatProvider provider, bool test)
        {
            if (test)
            {
                return source.ToString(provider);
            }
            else
            {
                return source.ToString();
            }
        }
    }
}
```

You are adding new functionality to the `ToString` methods that didn't previously exist. (Granted, the example I used above is completely arbitrary and doesn't provide any real value; it's just for demonstration purposes.) In this case, you want it to show up as an overloaded method on ToString, which is exactly what happens:

{% include post/image.html image-file="image-1.png" alt="image" %}
