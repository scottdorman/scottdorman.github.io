---
layout: post
title: Generic Enum Parsing with Extension Methods
date: 2007-09-25 15:32:44 -05:00
---

Not too long ago, I talked about [Extension Methods]({% post_url /2007/2007-08-19-C-3.0-Extension-Methods %} "Click To View Entry") in .NET 3.5 and also about a way to provide [data binding an enum type with descriptions](http://www.codeproject.com/useritems/enumdatabinding.asp). Today, [Simo](http://codeclimber.net.nz/archive/2007/09/25/String-to-Enum.aspx) talked about how often he forgets the syntax of parsing a string value to it's Enum value. In his post, he refers to a generic Enum parse method that [Scott Watermasysk](http://scottwater.com/blog/archive/Generic-Enum-Parse/) created just over a year ago (in 2006). In Scott's post, [Kenny Kerr](http://weblogs.asp.net/kennykerr/archive/2005/05/16/The-Case-of-the-Missing-Generic-_2800_Parse-Method_2900_.aspx) points back to his article (from 2005) about how to create a generic parse method in C++/CLI.  

Reading through all of these posts started me thinking about the EnumHelper class in my [article](http://www.codeproject.com/useritems/enumdatabinding.asp) and how nice it would be to provide an EnumParse method as part of any String value. This is where the simplicity of extension methods really starts to show.  

Taking the functions created by both Scott and Kenny, I created a derivative of them as an extension method on the String class. These functions look like

```csharp
public static T EnumParse<T>(this string value)
{
    return EnumHelper.EnumParse<T>(value, false);
}
 
public static T EnumParse<T>(this string value, bool ignoreCase)
{
    if (value == null)
    {
        throw new ArgumentNullException("value");
    }
 
    value = value.Trim();
 
    if (value.Length == 0)
    {
        throw new ArgumentException("Must specify valid information for parsing in the string.", "value");
    }
 
    Type t = typeof(T);
 
    if (!t.IsEnum)
    {
        throw new ArgumentException("Type provided must be an Enum.", "T");
    }
 
    T enumType = (T)Enum.Parse(t, value, ignoreCase);
    return enumType;
}
```

I think the extension method version provides a lot of benefits over the versions proposed by Scott W. and Kenny, namely by providing a natural extension to the String class and simplifying the calling syntax.

In order to use either of these functions, you can simply do this:

```csharp
string stringValue = "Last14";
 
// Using the .NET 3.5 extension methods syntax
SimpleEnum enumVal2 = stringValue.EnumParse<SimpleEnum>(true);
 
// Exact same function, but using the older "helper class" style
SimpleEnum enumVal3 = EnumHelper.EnumParse<SimpleEnum>(stringValue, true);
 
// Using the standard Enum.Parse method
SimpleEnum enumVal = (SimpleEnum)Enum.Parse(typeof(SimpleEnum), stringValue);
```

As you can see, using the extension methods syntax greatly simplifies the calling code and provides the method on the String itself. Using the older "helper class" style of calling syntax is exactly the same as what Scott W. and Kenny provide, and is still easier than using the standard Enum.Parse method.

While this solution doesn't provide the ultimate syntax, which would simply be:

```csharp
SimpleEnum enumVal = Enum.Parse<SimpleEnum>(stringValue);
```

It does provide an alternative that is almost as easy.

(This example assumes the static class is named EnumHelper and uses the SimpleEnum type defined in both my [article](http://www.codeproject.com/useritems/enumdatabinding.asp) and blog [post]({% post_url /2007/2007-08-02-Data-Binding-an-Enum-with-Descriptions %}).)
