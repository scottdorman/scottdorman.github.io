---
layout: post
title: Generic Enum Parsing with Extension Methods
date: 2007-09-25 15:32:44 -04:00
---

Not too long ago, I talked about [Extension Methods]({% post_url 2007/2007-08-19-C-3.0-Extension-Methods %} "Click To View Entry") in .NET 3.5 and also about a way to provide [data binding an enum type with descriptions](http://www.codeproject.com/useritems/enumdatabinding.asp). Today, [Simo](http://codeclimber.net.nz/archive/2007/09/25/String-to-Enum.aspx) talked about how often he forgets the syntax of parsing a string value to it's Enum value. In his post, he refers to a generic Enum parse method that [Scott Watermasysk](http://scottwater.com/blog/archive/Generic-Enum-Parse/) created just over a year ago (in 2006). In Scott's post, [Kenny Kerr](http://weblogs.asp.net/kennykerr/archive/2005/05/16/The-Case-of-the-Missing-Generic-_2800_Parse-Method_2900_.aspx) points back to his article (from 2005) about how to create a generic parse method in C++/CLI.  

Reading through all of these posts started me thinking about the EnumHelper class in my [article](http://www.codeproject.com/useritems/enumdatabinding.asp) and how nice it would be to provide an EnumParse method as part of any String value. This is where the simplicity of extension methods really starts to show.  

Taking the functions created by both Scott and Kenny, I created a derivative of them as an extension method on the String class. These functions look like
 <div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 1200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 488px; background-color: #f4f4f4"> <div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">

<span style="color: #606060">   1:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> T EnumParse<T>(<span style="color: #0000ff">this</span> <span style="color: #0000ff">string</span> <span style="color: #0000ff">value</span>)

<span style="color: #606060">   2:</span> {

<span style="color: #606060">   3:</span>     <span style="color: #0000ff">return</span> EnumHelper.EnumParse<T>(<span style="color: #0000ff">value</span>, <span style="color: #0000ff">false</span>);

<span style="color: #606060">   4:</span> }

<span style="color: #606060">   5:</span>  

<span style="color: #606060">   6:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> T EnumParse<T>(<span style="color: #0000ff">this</span> <span style="color: #0000ff">string</span> <span style="color: #0000ff">value</span>, <span style="color: #0000ff">bool</span> ignoreCase)

<span style="color: #606060">   7:</span> {

<span style="color: #606060">   8:</span>     <span style="color: #0000ff">if</span> (<span style="color: #0000ff">value</span> == <span style="color: #0000ff">null</span>)

<span style="color: #606060">   9:</span>     {

<span style="color: #606060">  10:</span>         <span style="color: #0000ff">throw</span> <span style="color: #0000ff">new</span> ArgumentNullException(<span style="color: #006080">"value"</span>);

<span style="color: #606060">  11:</span>     }

<span style="color: #606060">  12:</span>  

<span style="color: #606060">  13:</span>     <span style="color: #0000ff">value</span> = <span style="color: #0000ff">value</span>.Trim();

<span style="color: #606060">  14:</span>  

<span style="color: #606060">  15:</span>     <span style="color: #0000ff">if</span> (<span style="color: #0000ff">value</span>.Length == 0)

<span style="color: #606060">  16:</span>     {

<span style="color: #606060">  17:</span>         <span style="color: #0000ff">throw</span> <span style="color: #0000ff">new</span> ArgumentException(<span style="color: #006080">"Must specify valid information for parsing in the string."</span>, <span style="color: #006080">"value"</span>);

<span style="color: #606060">  18:</span>     }

<span style="color: #606060">  19:</span>  

<span style="color: #606060">  20:</span>     Type t = <span style="color: #0000ff">typeof</span>(T);

<span style="color: #606060">  21:</span>  

<span style="color: #606060">  22:</span>     <span style="color: #0000ff">if</span> (!t.IsEnum)

<span style="color: #606060">  23:</span>     {

<span style="color: #606060">  24:</span>         <span style="color: #0000ff">throw</span> <span style="color: #0000ff">new</span> ArgumentException(<span style="color: #006080">"Type provided must be an Enum."</span>, <span style="color: #006080">"T"</span>);

<span style="color: #606060">  25:</span>     }

<span style="color: #606060">  26:</span>  

<span style="color: #606060">  27:</span>     T enumType = (T)Enum.Parse(t, <span style="color: #0000ff">value</span>, ignoreCase);

<span style="color: #606060">  28:</span>     <span style="color: #0000ff">return</span> enumType;

<span style="color: #606060">  29:</span> }
</div></div>


I think the extension method version provides a lot of benefits over the versions proposed by Scott W. and Kenny, namely by providing a natural extension to the String class and simplifying the calling syntax.

In order to use either of these functions, you can simply do this:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">
<div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">

<span style="color: #606060">   1:</span> <span style="color: #0000ff">string</span> stringValue = <span style="color: #006080">"Last14"</span>;

<span style="color: #606060">   2:</span>  

<span style="color: #606060">   3:</span> <span style="color: #008000">// Using the .NET 3.5 extension methods syntax</span>

<span style="color: #606060">   4:</span> SimpleEnum enumVal2 = stringValue.EnumParse<SimpleEnum>(<span style="color: #0000ff">true</span>);

<span style="color: #606060">   5:</span>  

<span style="color: #606060">   6:</span> <span style="color: #008000">// Exact same function, but using the older "helper class" style</span>

<span style="color: #606060">   7:</span> SimpleEnum enumVal3 = EnumHelper.EnumParse<SimpleEnum>(stringValue, <span style="color: #0000ff">true</span>);

<span style="color: #606060">   8:</span>  

<span style="color: #606060">   9:</span> <span style="color: #008000">// Using the standard Enum.Parse method</span>

<span style="color: #606060">  10:</span> SimpleEnum enumVal = (SimpleEnum)Enum.Parse(<span style="color: #0000ff">typeof</span>(SimpleEnum), stringValue);
</div></div>


As you can see, using the extension methods syntax greatly simplifies the calling code and provides the method on the String itself. Using the older "helper class" style of calling syntax is exactly the same as what Scott W. and Kenny provide, and is still easier than using the standard Enum.Parse method.

While this solution doesn't provide the ultimate syntax, which would simply be:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">
<div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">

<span style="color: #606060">   1:</span> SimpleEnum enumVal = Enum.Parse<SimpleEnum>(stringValue);
</div></div>


It does provide an alternative that is almost as easy.

(This example assumes the static class is named EnumHelper and uses the SimpleEnum type defined in both my [article](http://www.codeproject.com/useritems/enumdatabinding.asp) and blog [post]({% post_url 2007/2007-08-02-Data-Binding-an-Enum-with-Descriptions %}).)
