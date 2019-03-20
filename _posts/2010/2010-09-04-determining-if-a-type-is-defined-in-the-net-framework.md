---
layout: post
title: Determining if a type is defined in the .NET Framework
date: '2010-09-04 22:24:51 -05:00'
tags: .net c#
---

There have been several questions on StackOverflow about how to determine if a type is defined in the .NET Framework or is a third-party or custom type. Based on the answers provided to these questions, this can be accomplished using some reflection to retrieve the public key token of the assembly in which the type is defined and compare it to a public key token known to be used by Microsoft to sign the .NET Framework assemblies.

*Update: Based on some additional research and a Twitter conversation with @blowdart, it turns out that what I have actually written is an extension method that determines if the type was provided by Microsoft, since there are other assemblies outside of the .NET Framework (such as most of the Visual Studio 2010 assemblies) are also signed with the same public key tokens. This list of public key tokens is not exhaustive as Visual Studio 2010 assemblies actually use 9 different public key tokens. For the majority of cases, I think this method will work and given a custom type defined in the .NET Framework (and not provided by Microsoft) should reliably return false. I'm investigating some additional ways to more reliably determine if the type is defined in the Framework as opposed to being provided by Microsoft.*

To do this, you can make use of the following extension method:

```csharp  
public static class TypeExtensions
{
    private static List<byte[]> tokens = new List<byte[]>()  
    { 
        new byte[] {0xb7, 0x7a, 0x5c, 0x56, 0x19, 0x34, 0xe0, 0x89}, 
        new byte[] {0x31, 0xbf, 0x38, 0x56, 0xad, 0x36, 0x4e, 0x35}, 
        new byte[] {0xb0, 0x3f, 0x5f, 0x7f, 0x11, 0xd5, 0x0a, 0x3a} 
    };

    public static bool IsFrameworkType(this Type type)
    {
        if (type == null) { throw new ArgumentNullException(<span style="color: rgb(0, 96, 128);">"type"); }
        byte[] publicKeyToken = type.Assembly.GetName().GetPublicKeyToken();
        return publicKeyToken != null
            && tokens.Contains(publicKeyToken, new ByteArrayEqualityComparer());
    }
}
```

The set of public key tokens are valid for all versions of the .NET Framework starting with .NET Framework 2.0. The ByteArrayEqualityComparer class looks like:


```csharp
public class ByteArrayEqualityComparer : EqualityComparer<byte[]>
{
    public override bool Equals(byte[] x, byte[] y)
    {
        return x != null && y != null && x.SequenceEqual(y);
    }

    public override int GetHashCode(byte[] obj)
    {
        return obj.GetHashCode();
    }
}
```

(Update: Based on some reader comments, the ByteArrayEqualityComparer class has been changed to use the [SequenceEquals](http://msdn.microsoft.com/en-us/library/bb348567.aspx) LINQ extension.)

You would then use this extension method like:

```csharp
Debug.WriteLine(<span style="color: rgb(0, 96, 128);">"Is type `string` a .NET Framework type? {0}", typeof(string).IsFrameworkType()); 
```
