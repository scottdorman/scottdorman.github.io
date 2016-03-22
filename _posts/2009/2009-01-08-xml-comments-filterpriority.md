---
layout: post
title: "XML Comments: filterpriority"
date: 2009-01-08 20:55:15 -05:00
---

I am a big fan of using XML comments in code and actually have a few Visual Studio macros which allow me to “inherit” the documentation from an overridden member. Every once in a while, I end up pulling in a comment with a *filterpriority* XML tag. This tag is very prevalent in the BCL but I have never been able to find documentation on what it actually means.

To see what I mean, let’s take a look at part of the definition for System.Object. In the XML comments, you will see that the class itself has a <span style="color: #008000">**<filterpriority>1</filterpriority>**</span> and that the Equals method has a <span style="color: #008000">**<filterpriority>2</filterpriority>**</span>.
  <div style="border-bottom: gray 1px solid; border-left: gray 1px solid; padding-bottom: 4px; line-height: 12pt; background-color: #f4f4f4; margin: 20px 0px 10px; padding-left: 4px; width: 97.5%; padding-right: 4px; font-family: consolas, 'Courier New', courier, monospace; height: 402px; max-height: 400px; font-size: 8pt; overflow: auto; border-top: gray 1px solid; cursor: text; border-right: gray 1px solid; padding-top: 4px">   <div style="border-bottom-style: none; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; padding-left: 0px; width: 100%; padding-right: 0px; font-family: consolas, 'Courier New', courier, monospace; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">     

<span style="color: #606060">   1:</span> <span style="color: #0000ff">namespace</span> System   

<span style="color: #606060">   2:</span>  {

<span style="color: #606060">   3:</span>      <span style="color: #008000">/// <summary>Supports all classes in the .NET Framework class hierarchy </span>

<span style="color: #606060">   4:</span>      <span style="color: #008000">/// and provides low-level services to derived classes. This is the </span>

<span style="color: #606060">   5:</span>      <span style="color: #008000">/// ultimate base class of all classes in the .NET Framework; it is the</span>

<span style="color: #606060">   6:</span>      <span style="color: #008000">/// root of the type hierarchy.</summary></span>

<span style="color: #606060">   7:</span>      <span style="color: #008000">**/// <filterpriority>1</filterpriority> **</span>

<span style="color: #606060">   8:</span>      [System.Runtime.InteropServices.ClassInterfaceAttribute(2)]

<span style="color: #606060">   9:</span>      <span style="color: #0000ff">public</span> <span style="color: #0000ff">class</span> Object    

<span style="color: #606060">  10:</span>      {    

<span style="color: #606060">  11:</span>          <span style="color: #008000">/// <summary>Determines whether the specified </span>

<span style="color: #606060">  12:</span>          <span style="color: #008000">/// <see cref="T:System.Object" /> </span>

<span style="color: #606060">  13:</span>          <span style="color: #008000">/// instances are considered equal.</summary>  </span>

<span style="color: #606060">  14:</span>          <span style="color: #008000">/// <returns>true if objA is the same instance as objB or</span>

<span style="color: #606060">  15:</span>          <span style="color: #008000">/// if both are null</span>

<span style="color: #606060">  16:</span>          <span style="color: #008000">/// references or if objA.Equals(objB) returns true; </span>

<span style="color: #606060">  17:</span>          <span style="color: #008000">/// otherwise, false.</returns></span>

<span style="color: #606060">  18:</span>          <span style="color: #008000">/// <param name="objB">The second <see cref="T:System.Object" /> </span>

<span style="color: #606060">  19:</span>          <span style="color: #008000">/// to compare. </param></span>

<span style="color: #606060">  20:</span>          <span style="color: #008000">/// <param name="objA">The first <see cref="T:System.Object" /> </span>

<span style="color: #606060">  21:</span>          <span style="color: #008000">/// to compare. </param></span>

<span style="color: #606060">  22:</span>          <span style="color: #008000">**/// <filterpriority>2</filterpriority>**</span>

<span style="color: #606060">  23:</span>          <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">bool</span> Equals(<span style="color: #0000ff">object</span> objA, <span style="color: #0000ff">object</span> objB);

<span style="color: #606060">  24:</span>       }

<span style="color: #606060">  25:</span>   }

  </div>
</div>



The only real mention I was able to find was this [blog post](http://blogs.msdn.com/mitchw/archive/2004/07/03/172689.aspx), which is actually talking about the “Go to definition” feature of Visual Studio. One of the comments asks about the <filterpriority> tag. Unfortunately, when I saw this blog post and the comments, I misread the second comment and thought that it applied to the first comment about the <filterpriority>. As it turns out, the comment was talking about the “Go to definition” feature itself.

Since I wanted to know the answer, I posted a [question](http://stackoverflow.com/questions/281355/what-does-the-filterpriority-tag-in-an-xml-comment-do) on StackOverflow. The first answer seemed to indicate that this applied to the “All” and “Common” tabs in the VB.NET editors intellisense implementation, but (due to having misread the blog post comments) I dismissed that thinking this was a C# feature. A second answer just a few days ago said that this was somehow tied to the EditorBrowsableAttribute (and more specifically the values of the EditorBrowsableState enum. I couldn’t see how an XML comment could be the same as decorating the member with the attribute.

As a result, I started doing some more digging and came across a self-published book titled [XML Document Guide](http://issuu.com/pchew/docs/xml_document_guide/31), which actually documented the <filterpriority> tag (page 30). According to that book, the value of this tag is:

> Used by the Visual Basic editor in order to determine whether a member should appear on the Common or All tab when the completion list is shown.

That led me to start doing some testing of my own to verify things. 

The first thing I discovered is that it appears to have no effect on classes. This is contrary to what I would have thought since Microsoft places filterpriority tags on classes. Getting past that discrepancy, it became very clear that the filterpriority tag controls the IntelliSense visibility for both methods and properties whether they are instance members or static members. Testing on Visual Studio 2008 RTM provided the following results:



<table border="1" cellspacing="0" cellpadding="2"><tbody>
    <tr>
      <td valign="top">
        

**Filter Priority value**

      </td>

      <td valign="top" width="215" colspan="2">
        

**Method**

      </td>

      <td valign="top" rowspan="7"> </td>

      <td valign="top" width="215" colspan="2">
        

**Property**

      </td>
    </tr>

    <tr>
      <td valign="top"> </td>

      <td valign="top">
        

**Instance**

      </td>

      <td valign="top">
        

 **Static**

      </td>

      <td valign="top">
        

**Instance**

      </td>

      <td valign="top">
        

 **Static**

      </td>
    </tr>

    <tr>
      <td valign="top">*missing*</td>

      <td valign="top">Common</td>

      <td valign="top">Common</td>

      <td valign="top">Common</td>

      <td valign="top">Common</td>
    </tr>

    <tr>
      <td valign="top">0</td>

      <td valign="top">Common</td>

      <td valign="top">Common</td>

      <td valign="top">Common</td>

      <td valign="top">Common</td>
    </tr>

    <tr>
      <td valign="top">1</td>

      <td valign="top">Common</td>

      <td valign="top">Common</td>

      <td valign="top">Common</td>

      <td valign="top">Common</td>
    </tr>

    <tr>
      <td valign="top">2</td>

      <td valign="top">All</td>

      <td valign="top">All</td>

      <td valign="top">All</td>

      <td valign="top">All</td>
    </tr>

    <tr>
      <td valign="top">3</td>

      <td valign="top">*Hidden**</td>

      <td valign="top"> *Hidden*</td>

      <td valign="top">*Hidden*</td>

      <td valign="top">*Hidden*</td>
    </tr>
  </tbody></table>



* Initial testing on VS2008 SP1 showed this method available on the All tab.

Where things start to become really interesting is when you combine the filterpriority tag with the [EditorBrowsableAttribute](http://msdn2.microsoft.com/8a045wyx.aspx "EditorBrowsableAttribute Class"). This attribute specifies if a method or property is viewable in an editor and allows you to specify a state of Always, Advanced, or Never. At first glance this appears to cause the same behavior as the filterpriority tag with the benefit that any language editor will respect the attribute.

But what happens if you specify both the filterpriority tag and the EditorBrowsableAttribute? When tested on VS2008 RTM, the filterpriority tag took precedence over the EditorBrowsableAttribute and the results were exactly the same as if the attribute were not present. However, when using EditorBrowsableState.Never, the attribute took precedence over the filterpriority tag and none of the methods displayed in the IntelliSense list.

I did notice that the results did not seem 100% repeatable so, for now I would be a bit cautious relying on the filterpriority tag. I’m going to see if I can get someone from either the VB or Visual Studio teams to comment and provide some definitive information on how this tag behaves, but until then the only certainty is that it does control whether a member appears on the Common or All tab for the Visual Basic IntelliSense list.
<div class="wlWriterHeaderFooter" style="text-align:left; margin:0px; padding:4px 4px 4px 4px;">[![DotNetKicks Image](http://www.dotnetkicks.com/Services/Images/KickItImageGenerator.ashx?url=http://geekswithblogs.net/sdorman/archive/2009/01/08/xml-comments-filterpriority.aspx&bgcolor=0080C0&fgcolor=FFFFFF&border=000000&cbgcolor=D4E1ED&cfgcolor=000000)]({% post_url /2009/2009-01-08-xml-comments-filterpriority %})</div>
