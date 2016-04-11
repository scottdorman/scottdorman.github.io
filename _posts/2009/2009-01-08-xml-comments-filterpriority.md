---
layout: post
title: "XML Comments: filterpriority"
date: 2009-01-08 20:55:15 -0500
---

I am a big fan of using XML comments in code and actually have a few Visual Studio macros which allow me to “inherit” the documentation from an overridden member. Every once in a while, I end up pulling in a comment with a *filterpriority* XML tag. This tag is very prevalent in the BCL but I have never been able to find documentation on what it actually means.

To see what I mean, let’s take a look at part of the definition for `System.Object`. In the XML comments, you will see that the class itself has a **`<filterpriority>1</filterpriority>`** and that the Equals method has a **`<filterpriority>2</filterpriority>`**.

```csharp
namespace System   
{
  /// <summary>
  /// Supports all classes in the .NET Framework class hierarchy and provides
  /// low-level services to derived classes. This is the ultimate base class
  /// of all classes in the .NET Framework; it is the root of the type hierarchy.
  /// </summary>
  /// <filterpriority>1</filterpriority>
  [System.Runtime.InteropServices.ClassInterfaceAttribute(2)]
  public Object    
  {    
    /// <summary>
    /// Determines whether the specified <see cref="T:System.Object" /> instances
    /// are considered equal.
    /// </summary>
    /// <returns>true if objA is the same instance as objB or if both are null 
    /// references or if objA.Equals(objB) returns true; otherwise, false.</returns>
    /// <param name="objB">The second <see cref="T:System.Object" /> to compare.</param>
    /// <param name="objA">The first <see cref="T:System.Object" /> to compare.</param>
    /// <filterpriority>2</filterpriority>
    public static bool  Equals(object objA, object objB);
  }
}
```
The only real mention I was able to find was this [blog post](http://blogs.msdn.com/mitchw/archive/2004/07/03/172689.aspx), which is actually talking about the "Go to definition" feature of Visual Studio. One of the comments asks about the `<filterpriority>` tag. Unfortunately, when I saw this blog post and the comments, I misread the second comment and thought that it applied to the first comment about the `<filterpriority>`. As it turns out, the comment was talking about the "Go to definition" feature itself.

Since I wanted to know the answer, I posted a [question](http://stackoverflow.com/questions/281355/what-does-the-filterpriority-tag-in-an-xml-comment-do) on StackOverflow. The first answer seemed to indicate that this applied to the "All" and "Common" tabs in the VB.NET editors intellisense implementation, but (due to having misread the blog post comments) I dismissed that thinking this was a C# feature. A second answer just a few days ago said that this was somehow tied to the `EditorBrowsableAttribute` (and more specifically the values of the `EditorBrowsableState` enum. I couldn’t see how an XML comment could be the same as decorating the member with the attribute.

As a result, I started doing some more digging and came across a self-published book titled [XML Document Guide](http://issuu.com/pchew/docs/xml_document_guide/31), which actually documented the `<filterpriority>` tag (page 30). According to that book, the value of this tag is:

> Used by the Visual Basic editor in order to determine whether a member should appear on the Common or All tab when the completion list is shown.

That led me to start doing some testing of my own to verify things. 

The first thing I discovered is that it appears to have no effect on classes. This is contrary to what I would have thought since Microsoft places filterpriority tags on classes. Getting past that discrepancy, it became very clear that the filterpriority tag controls the IntelliSense visibility for both methods and properties whether they are instance members or static members. Testing on Visual Studio 2008 RTM provided the following results:

<table border="1" cellspacing="0" cellpadding="2">
    <tr>
      <th>Filter Priority value</th>
      <th colspan="2">Method</th>
      <th colspan="2">Property</th>
    </tr>
    <tr>
      <th></th>
      <th>Instance</th>
      <th>Static</th>
      <th>Instance</th>
      <th>Static</th>
    </tr>
    <tr>
      <td><em>missing</em></td>
      <td>Common</td>
      <td>Common</td>
      <td>Common</td>
      <td>Common</td>
    </tr>
    <tr>
      <td>0</td>
      <td>Common</td>
      <td>Common</td>
      <td>Common</td>
      <td>Common</td>
    </tr>
    <tr>
      <td>1</td>
      <td>Common</td>
      <td>Common</td>
      <td>Common</td>
      <td>Common</td>
    </tr>
    <tr>
      <td>2</td>
      <td>All</td>
      <td>All</td>
      <td>All</td>
      <td>All</td>
    </tr>
    <tr>
      <td>3</td>
      <td><em>Hidden</em>*</td>
      <td><em>Hidden</em></td>
      <td><em>Hidden</em></td>
      <td><em>Hidden</em></td>
    </tr>
</table>

\* Initial testing on VS2008 SP1 showed this method available on the All tab.

Where things start to become really interesting is when you combine the filterpriority tag with the [`EditorBrowsableAttribute`](http://msdn2.microsoft.com/8a045wyx.aspx "EditorBrowsableAttribute Class"). This attribute specifies if a method or property is viewable in an editor and allows you to specify a state of Always, Advanced, or Never. At first glance this appears to cause the same behavior as the filterpriority tag with the benefit that any language editor will respect the attribute.

But what happens if you specify both the filterpriority tag and the `EditorBrowsableAttribute`? When tested on VS2008 RTM, the filterpriority tag took precedence over the `EditorBrowsableAttribute` and the results were exactly the same as if the attribute were not present. However, when using `EditorBrowsableState.Never`, the attribute took precedence over the filterpriority tag and none of the methods displayed in the IntelliSense list.

I did notice that the results did not seem 100% repeatable so, for now I would be a bit cautious relying on the filterpriority tag. I’m going to see if I can get someone from either the VB or Visual Studio teams to comment and provide some definitive information on how this tag behaves, but until then the only certainty is that it does control whether a member appears on the Common or All tab for the Visual Basic IntelliSense list.
