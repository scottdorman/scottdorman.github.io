---
layoutpost
titleNull Object pattern
date2008-05-25 18:28:23 -05:00
---

I've been trying to catch up on my reading and came across this [post](http://weblogs.asp.net/fredriknormen/archive/2008/05/22/avoid-returning-quot-null-quot-and-use-the-null-object-pattern.aspx) by [Fredrik Normén](http://weblogs.asp.net/fredriknormen/default.aspx) where he raises the question about returning null or using the [Null Object pattern](http://en.wikipedia.org/wiki/Null_object_pattern). Interestingly enough, last month while I was in Seattle for the 2008 MVP Summit I had a very similar discussion. The end result of that discussion was that null objects, and nullability in general, ideally should be treated as a "first-class" citizen in the CLR. This means that if you try to execute a method on a null object you get a null back in return rather than a [NullReferenceException](http://msdn.microsoft.com/library/system.nullreferenceexception.aspx).

I tend to follow a very similar philosophy as Fredrik in that I return null in some circumstances and empty collections (or other appropriate defaults) in others. I think this style has grown from the fact that nullability has never been a first class citizen in most programming languages.

A few of the comments suggested the use of an extension method to accomplish Fredrik's idea of an "IsNull" property. Since we only have the ability to create extension methods, I created an extension method called IsNull that extends [Object Class (System)](http://msdn.microsoft.com/library/system.object.aspx) to see if this would work. 

This is, perhaps, the simplest extension method I've seen and worked with. The extension method is:

```csharp
public static class NullObjectExtenstions
{
  public static bool IsNull(this object source)
  {
    return (source == null);
  }
}
```


Using this extension method is also just as easy. Here is a simple console application I wrote to verify that this does indeed work:

```csharp
class Program
{
    static void Main(string[] args)
    {
        string x = null;
        List<string> y = null;
        CultureInfo culture = null;

        Debug.WriteLine(x.IsNull());
        Debug.WriteLine(y.IsNull());
        Debug.WriteLine(culture.IsNull());

        if (!culture.IsNull())
        {
            Debug.WriteLine(culture.DisplayName);
        }
    }
}
```

The output of this application is:

```
True
True
True
```

The last call to `Debug.WriteLine(culture.DisplayName)` is never executed since `culture.IsNull()` returns true so we don't hit the [`NullReferenceException`](http://msdn.microsoft.com/library/system.nullreferenceexception.aspx).
