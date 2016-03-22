---
layout: post
title: Null Object pattern follow up
date: 2008-07-04 09:51:08 -04:00
---

My earlier post on the [Null Object pattern]({% post_url 2008/2008-05-25-null-object-pattern %}) led to a few critiques about the fact that I was presenting an extension method to do what is essentially a very simple logical test, and, as a result, doesn’t provide much value.

For reference, here is the original extension method from that post
  <div style="border-right: gray 1px solid; padding-right: 4px; padding-left: 4px; font-size: 8pt; border-top: gray 1px solid; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">   

```
<span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">class</span> NullObjectExtenstions
{
    <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">bool</span> IsNull(<span style="color: #0000ff">this</span> <span style="color: #0000ff">object</span> source)
    {
        <span style="color: #0000ff">return</span> (source == <span style="color: #0000ff">null</span>);
    }
}
```

</div>



Yes, this is an extremely simple method and performs a very basic logical test. However, consider the static IsNullOrEmtpy function on String (taken from [Reflector](http://www.aisto.com/roeder/dotnet/)):


<div style="border-right: gray 1px solid; padding-right: 4px; padding-left: 4px; font-size: 8pt; border-top: gray 1px solid; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">
  

```
<span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">bool</span> IsNullOrEmpty(<span style="color: #0000ff">string</span> <span style="color: #0000ff">value</span>)
{
    <span style="color: #0000ff">if</span> (<span style="color: #0000ff">value</span> != <span style="color: #0000ff">null</span>)
    {
        <span style="color: #0000ff">return</span> (<span style="color: #0000ff">value</span>.Length == 0);
    }
    <span style="color: #0000ff">return</span> <span style="color: #0000ff">true</span>;
}
```

</div>



I would argue that this is a relatively simple method and performs two very basic logical tests. What is the benefit to using IsNullOrEmpty? In a word, **<u>consistency</u>**. By using IsNullOrEmpty, I know that every time I need to perform this test it is executing the exact same code in the same order. I don’t have to worry about someone accidentally testing “Length == 0” before the “!= null” and causing a NullReferenceExcpetion.

This same benefit applies to the IsNull extension method. It introduces that consistency (although I agree this test is still very trivial) for testing nullability. As I mentioned in my comments, the better choice for the extension method would probably have been an IsNotNull method. Here is a more complete NullObjectExtensions class:


<div style="border-right: gray 1px solid; padding-right: 4px; padding-left: 4px; font-size: 8pt; border-top: gray 1px solid; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 246px; background-color: #f4f4f4">
  

```
<span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">class</span> NullObjectExtenstions
{
    <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">bool</span> IsNull<T>(<span style="color: #0000ff">this</span> T source) <span style="color: #0000ff">where</span> T : <span style="color: #0000ff">class</span>
    {
        <span style="color: #0000ff">return</span> (source == <span style="color: #0000ff">null</span>);
    }

    <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">bool</span> IsNotNull<T>(<span style="color: #0000ff">this</span> T source) <span style="color: #0000ff">where</span> T : <span style="color: #0000ff">class</span>
    {
        <span style="color: #0000ff">return</span> (source != <span style="color: #0000ff">null</span>);
    }
}
```

</div>

<div style="padding-right: 0px; padding-left: 0px; float: none; padding-bottom: 0px; margin: 0px; padding-top: 0px; display: inline" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:5188f4ff-65a3-4195-a276-e38d14fbd477" class="wlWriterSmartContent">Technorati Tags: [CSharp](http://technorati.com/tags/CSharp), [.NET](http://technorati.com/tags/.NET)</div>
