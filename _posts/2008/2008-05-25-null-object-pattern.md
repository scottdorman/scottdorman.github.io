---
layout: post
title: Null Object pattern
date: 2008-05-25 18:28:23 -05:00
---

I've been trying to catch up on my reading and came across this [post](http://weblogs.asp.net/fredriknormen/archive/2008/05/22/avoid-returning-quot-null-quot-and-use-the-null-object-pattern.aspx "Avoid returning ") by [Fredrik Normén](http://weblogs.asp.net/fredriknormen/default.aspx) where he raises the question about returning null or using the [Null Object pattern](http://en.wikipedia.org/wiki/Null_object_pattern). Interestingly enough, last month while I was in Seattle for the 2008 MVP Summit I had a very similar discussion. The end result of that discussion was that null objects, and nullability in general, ideally should be treated as a "first-class" citizen in the CLR. This means that if you try to execute a method on a null object you get a null back in return rather than a [NullReferenceException](http://msdn.microsoft.com/library/system.nullreferenceexception.aspx).

I tend to follow a very similar philosophy as Fredrik in that I return null in some circumstances and empty collections (or other appropriate defaults) in others. I think this style has grown from the fact that nullability has never been a first class citizen in most programming languages.

A few of the comments suggested the use of an extension method to accomplish Fredrik's idea of an "IsNull" property. Since we only have the ability to create extension methods, I created an extension method called IsNull that extends [Object Class (System)](http://msdn.microsoft.com/library/system.object.aspx) to see if this would work. 

This is, perhaps, the simplest extension method I've seen and worked with. The extension method is:
  <div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 134px; background-color: #f4f4f4">   <div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">     

<span style="color: #606060">   1:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">class</span> NullObjectExtenstions

<span style="color: #606060">   2:</span> {

<span style="color: #606060">   3:</span>     <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">bool</span> IsNull(<span style="color: #0000ff">this</span> <span style="color: #0000ff">object</span> source)

<span style="color: #606060">   4:</span>     {

<span style="color: #606060">   5:</span>         <span style="color: #0000ff">return</span> (source == <span style="color: #0000ff">null</span>);

<span style="color: #606060">   6:</span>     }

<span style="color: #606060">   7:</span> }

  </div>
</div>



Using this extension method is also just as easy. Here is a simple console application I wrote to verify that this does indeed work:


<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 400px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 325px; background-color: #f4f4f4">
  <div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">
    

<span style="color: #606060">   1:</span> <span style="color: #0000ff">class</span> Program

<span style="color: #606060">   2:</span> {

<span style="color: #606060">   3:</span>     <span style="color: #0000ff">static</span> <span style="color: #0000ff">void</span> Main(<span style="color: #0000ff">string</span>[] args)

<span style="color: #606060">   4:</span>     {

<span style="color: #606060">   5:</span>         <span style="color: #0000ff">string</span> x = <span style="color: #0000ff">null</span>;

<span style="color: #606060">   6:</span>         List<<span style="color: #0000ff">string</span>> y = <span style="color: #0000ff">null</span>;

<span style="color: #606060">   7:</span>         CultureInfo culture = <span style="color: #0000ff">null</span>;

<span style="color: #606060">   8:</span>  

<span style="color: #606060">   9:</span>  

<span style="color: #606060">  10:</span>         Debug.WriteLine(x.IsNull());

<span style="color: #606060">  11:</span>         Debug.WriteLine(y.IsNull());

<span style="color: #606060">  12:</span>         Debug.WriteLine(culture.IsNull());

<span style="color: #606060">  13:</span>  

<span style="color: #606060">  14:</span>         <span style="color: #0000ff">if</span> (!culture.IsNull())

<span style="color: #606060">  15:</span>         {

<span style="color: #606060">  16:</span>             Debug.WriteLine(culture.DisplayName);

<span style="color: #606060">  17:</span>         }

<span style="color: #606060">  18:</span>     }

<span style="color: #606060">  19:</span> }

  </div>
</div>



The output of this application is:


<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 74px; background-color: #f4f4f4">
  

```
True
True
True
```

</div>



The last call to *<font face="Consolas">Debug.WriteLine(culture.DisplayName)</font>* is never executed since *<font face="Consolas">culture.IsNull()</font>* returns true so we don't hit the [NullReferenceException](http://msdn.microsoft.com/library/system.nullreferenceexception.aspx).
