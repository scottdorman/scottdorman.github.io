---
layout: post
title: Determining if a type is defined in the .NET Framework
date: 2010-09-04 22:24:51 -04:00
---

There have been several questions on StackOverflow about how to determine if a type is defined in the .NET Framework or is a third-party or custom type. Based on the answers provided to these questions, this can be accomplished using some reflection to retrieve the public key token of the assembly in which the type is defined and compare it to a public key token known to be used by Microsoft to sign the .NET Framework assemblies.

*Update: Based on some additional research and a Twitter conversation with @blowdart, it turns out that what I have actually written is an extension method that determines if the type was provided by Microsoft, since there are other assemblies outside of the .NET Framework (such as most of the Visual Studio 2010 assemblies) are also signed with the same public key tokens. This list of public key tokens is not exhaustive as Visual Studio 2010 assemblies actually use 9 different public key tokens. For the majority of cases, I think this method will work and given a custom type defined in the .NET Framework (and not provided by Microsoft) should reliably return false. I’m investigating some additional ways to more reliably determine if the type is defined in the Framework as opposed to being provided by Microsoft.*

To do this, you can make use of the following extension method:
  <div id="codeSnippetWrapper" style="margin: 20px 0px 10px; padding: 4px; border: 1px solid silver; width: 97.5%; text-align: left; line-height: 12pt; overflow: auto; font-family: "Courier New", courier, monospace; font-size: 8pt; cursor: text; direction: ltr; max-height: 200px; background-color: rgb(244, 244, 244);">   <div id="codeSnippet" style="padding: 0px; width: 100%; text-align: left; color: black; line-height: 12pt; overflow: visible; font-family: "Courier New", courier, monospace; font-size: 8pt; direction: ltr; background-color: rgb(244, 244, 244);">     

<span style="color: rgb(0, 0, 255);">public</span> <span style="color: rgb(0, 0, 255);">static</span> <span style="color: rgb(0, 0, 255);">class</span> TypeExtensions

{

    <span style="color: rgb(0, 0, 255);">private</span> <span style="color: rgb(0, 0, 255);">static</span> List<<span style="color: rgb(0, 0, 255);">byte</span>[]> tokens = <span style="color: rgb(0, 0, 255);">new</span> List<<span style="color: rgb(0, 0, 255);">byte</span>[]>()  

    { 

        <span style="color: rgb(0, 0, 255);">new</span> <span style="color: rgb(0, 0, 255);">byte</span>[] {0xb7, 0x7a, 0x5c, 0x56, 0x19, 0x34, 0xe0, 0x89}, 

        <span style="color: rgb(0, 0, 255);">new</span> <span style="color: rgb(0, 0, 255);">byte</span>[] {0x31, 0xbf, 0x38, 0x56, 0xad, 0x36, 0x4e, 0x35}, 

        <span style="color: rgb(0, 0, 255);">new</span> <span style="color: rgb(0, 0, 255);">byte</span>[] {0xb0, 0x3f, 0x5f, 0x7f, 0x11, 0xd5, 0x0a, 0x3a} 

    };

    <span style="color: rgb(0, 0, 255);">public</span> <span style="color: rgb(0, 0, 255);">static</span> <span style="color: rgb(0, 0, 255);">bool</span> IsFrameworkType(<span style="color: rgb(0, 0, 255);">this</span> Type type)

    {

        <span style="color: rgb(0, 0, 255);">if</span> (type == <span style="color: rgb(0, 0, 255);">null</span>) { <span style="color: rgb(0, 0, 255);">throw</span> <span style="color: rgb(0, 0, 255);">new</span> ArgumentNullException(<span style="color: rgb(0, 96, 128);">"type"</span>); }

        <span style="color: rgb(0, 0, 255);">byte</span>[] publicKeyToken = type.Assembly.GetName().GetPublicKeyToken();

        <span style="color: rgb(0, 0, 255);">return</span> publicKeyToken != <span style="color: rgb(0, 0, 255);">null</span>

            && tokens.Contains(publicKeyToken, <span style="color: rgb(0, 0, 255);">new</span> ByteArrayEqualityComparer());

    }

}

</div>
</div>



The set of public key tokens are valid for all versions of the .NET Framework starting with .NET Framework 2.0. The ByteArrayEqualityComparer class looks like:


<div id="codeSnippetWrapper" style="margin: 20px 0px 10px; padding: 4px; border: 1px solid silver; width: 97.5%; text-align: left; line-height: 12pt; overflow: auto; font-family: "Courier New", courier, monospace; font-size: 8pt; cursor: text; direction: ltr; max-height: 200px; background-color: rgb(244, 244, 244);">
  <div id="codeSnippet" style="padding: 0px; width: 100%; text-align: left; color: black; line-height: 12pt; overflow: visible; font-family: "Courier New", courier, monospace; font-size: 8pt; direction: ltr; background-color: rgb(244, 244, 244);">
    

<span style="color: rgb(0, 0, 255);">public</span> <span style="color: rgb(0, 0, 255);">class</span> ByteArrayEqualityComparer : EqualityComparer<<span style="color: rgb(0, 0, 255);">byte</span>[]>

{

    <span style="color: rgb(0, 0, 255);">public</span> <span style="color: rgb(0, 0, 255);">override</span> <span style="color: rgb(0, 0, 255);">bool</span> Equals(<span style="color: rgb(0, 0, 255);">byte</span>[] x, <span style="color: rgb(0, 0, 255);">byte</span>[] y)

    {

        <span style="color: rgb(0, 0, 255);">return</span> x != <span style="color: rgb(0, 0, 255);">null</span> && y != <span style="color: rgb(0, 0, 255);">null</span> && x.SequenceEqual(y);

    }

    <span style="color: rgb(0, 0, 255);">public</span> <span style="color: rgb(0, 0, 255);">override</span> <span style="color: rgb(0, 0, 255);">int</span> GetHashCode(<span style="color: rgb(0, 0, 255);">byte</span>[] obj)

    {

        <span style="color: rgb(0, 0, 255);">return</span> obj.GetHashCode();

    }

}

</div>
</div>



(Update: Based on some reader comments, the ByteArrayEqualityComparer class has been changed to use the [SequenceEquals](http://msdn.microsoft.com/en-us/library/bb348567.aspx) LINQ extension.)

You would then use this extension method like:


<div id="codeSnippetWrapper" style="margin: 20px 0px 10px; padding: 4px; border: 1px solid silver; width: 97.5%; text-align: left; line-height: 12pt; overflow: auto; font-family: "Courier New", courier, monospace; font-size: 8pt; cursor: text; direction: ltr; max-height: 200px; background-color: rgb(244, 244, 244);">
  <div id="codeSnippet" style="padding: 0px; width: 100%; text-align: left; color: black; line-height: 12pt; overflow: visible; font-family: "Courier New", courier, monospace; font-size: 8pt; direction: ltr; background-color: rgb(244, 244, 244);">
    

Debug.WriteLine(<span style="color: rgb(0, 96, 128);">"Is type `string` a .NET Framework type? {0}"</span>, 

   <span style="color: rgb(0, 0, 255);">typeof</span>(<span style="color: rgb(0, 0, 255);">string</span>).IsFrameworkType()); 

</div>
</div>
