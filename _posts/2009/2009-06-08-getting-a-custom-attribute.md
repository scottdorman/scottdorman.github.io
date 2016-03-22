---
layout: post
title: Getting a custom attribute
date: 2009-06-08 13:31:58 -04:00
---

<div id="codeSnippetWrapper">Attribute programming has a lot of benefits and, when done correctly, can greatly simplify the amount of code that you need to write. One drawback to using attributes is that the code required to retrieve a custom attribute from a type is a bit cumbersome and is very repetitious.</div>  

Given a type, the simplest way to retrieve a custom attribute is code like
  <div id="codeSnippetWrapper" style="margin: 20px 0px 10px; padding: 4px; border: 1px solid silver; width: 97.5%; text-align: left; line-height: 12pt; overflow: auto; font-family: "Courier New", courier, monospace; font-size: 8pt; cursor: text; direction: ltr; max-height: 200px; background-color: rgb(244, 244, 244);">   

CustomAttribute attribute = Attribute.GetCustomAttribute(customType.GetType(), <span style="color: rgb(0, 0, 255);">typeof</span>(CustomAttribute), <span style="color: rgb(0, 0, 255);">true</span>) <span style="color: rgb(0, 0, 255);">as</span> CustomAttribute;

</div>



While this is simple code, it doesn’t handle any error conditions and requires that you always remember to perform the cast. A more complete method would look like


<div id="codeSnippetWrapper" style="margin: 20px 0px 10px; padding: 4px; border: 1px solid silver; width: 97.5%; height: 275px; text-align: left; line-height: 12pt; overflow: auto; font-family: "Courier New", courier, monospace; font-size: 8pt; cursor: text; direction: ltr; max-height: 400px; background-color: rgb(244, 244, 244);">
  

```
<span style="color: rgb(0, 0, 255);">public</span> <span style="color: rgb(0, 0, 255);">static</span> CustomAttribute GetAttribute(MemberInfo element)  
{  
    CustomAttribute attribute = <span style="color: rgb(0, 0, 255);">null</span>;  

    <span style="color: rgb(0, 0, 255);">try</span>  
    {  
        attribute = Attribute.GetCustomAttribute(element, <span style="color: rgb(0, 0, 255);">typeof</span>(CustomAttribute), <span style="color: rgb(0, 0, 255);">true</span>) <span style="color: rgb(0, 0, 255);">as</span> CustomAttribute;  
    }  
    <span style="color: rgb(0, 0, 255);">catch</span>  
    {  
        <span style="color: rgb(0, 128, 0);">// We aren't really interested in the exceptions here, but if we do get an exception</span>  
        <span style="color: rgb(0, 128, 0);">// just return null;</span>  
        attribute = <span style="color: rgb(0, 0, 255);">null</span>;  
    }  

    <span style="color: rgb(0, 0, 255);">return</span> attribute;  
}
```

</div>

<div>This nicely encapsulates the error handling and casting, but introduces another drawback. In order to make use of this method you would need to include it on every custom attribute you create, being sure to change the types appropriately.</div>

<div> </div>

<div>We can make this more practical by changing to a generic extension method with very little effort</div>

<div id="codeSnippetWrapper" style="margin: 20px 0px 10px; padding: 4px; border: 1px solid silver; width: 97.5%; height: 336px; text-align: left; line-height: 12pt; overflow: auto; font-family: "Courier New", courier, monospace; font-size: 8pt; cursor: text; direction: ltr; max-height: 400px; background-color: rgb(244, 244, 244);">
  

```
<span style="color: rgb(0, 0, 255);">public</span> <span style="color: rgb(0, 0, 255);">static</span> T GetAttribute<T>(<span style="color: rgb(0, 0, 255);">this</span> MemberInfo element) <span style="color: rgb(0, 0, 255);">where</span> T: Attribute  
{  
    T attribute = <span style="color: rgb(0, 0, 255);">null</span>;  

    <span style="color: rgb(0, 0, 255);">if</span> (element != <span style="color: rgb(0, 0, 255);">null</span>)  
    {  
        <span style="color: rgb(0, 0, 255);">try</span>  
        {  
            attribute = Attribute.GetCustomAttribute(element, <span style="color: rgb(0, 0, 255);">typeof</span>(T), <span style="color: rgb(0, 0, 255);">true</span>) <span style="color: rgb(0, 0, 255);">as</span> T;  
        }  
        <span style="color: rgb(0, 0, 255);">catch</span>  
        {  
            <span style="color: rgb(0, 128, 0);">// We aren't really interested in the exceptions here, but if we do get an exception</span>  
            <span style="color: rgb(0, 128, 0);">// just return null;</span>  
            attribute = <span style="color: rgb(0, 0, 255);">null</span>;  
        }  
    }  

    <span style="color: rgb(0, 0, 255);">return</span> attribute;  
}
```

</div>

<div>The benefit here is that, because this is implemented as an extension method it is available as if it were a real method call on any class derived from MemberInfo, which happens to be the base class for all of the Type classes.</div>

<div> </div>

<div>Now, we can define our custom attributes without any special consideration to providing a strongly typed GetAttribute method and when we want to retrieve a custom attribute, we can use code that now looks like</div>

<div id="codeSnippetWrapper" style="margin: 20px 0px 10px; padding: 4px; border: 1px solid silver; width: 97.5%; text-align: left; line-height: 12pt; overflow: auto; font-family: "Courier New", courier, monospace; font-size: 8pt; cursor: text; direction: ltr; max-height: 200px; background-color: rgb(244, 244, 244);">
  

CustomAttribute attribute = customType.GetType().GetAttribute<CustomAttribute>();

</div>

<div>It might not look like a major change in the calling site, but we are now able to quickly and easily get a strongly typed attribute given an instance type. 
    
</div>





<div class="wlWriterSmartContent" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:271cffa5-0f80-4f36-b0e8-4e4f9d76b7a6" style="margin: 0px; padding: 0px; float: none; display: inline;">Technorati Tags: [C#](http://technorati.com/tags/C%23),[Attributes](http://technorati.com/tags/Attributes)</div><div class="wlWriterHeaderFooter" style="margin: 0px; padding: 4px 0px; text-align: right;">[![Digg This](http://digg.com/img/badges/100x20-digg-button.png "Digg This")](http://digg.com/submit?url=http%3a%2f%2fgeekswithblogs.net%2fsdorman%2farchive%2f2009%2f06%2f08%2fgetting-a-custom-attribute.aspx&title=Getting+a+custom+attribute)</div>
