---
layout: post
title: The Dispose Pattern (and FxCop warnings)
date: 2010-05-25 10:40:09 -05:00
---

*[This is actually a response to *[*Bill’s blog post*](http://srtsolutions.com/public/item/254680)*, but since it isn’t possible to leave this as a comment on his blog it’s a post here.]*

There are many different ways to implement the Dispose pattern correctly. Some are (in my opinion) better than others. In Bill’s blog post he presents a particular pattern, which is an excerpt from his book ([Effective C#](http://www.amazon.com/Effective-Covers-4-0-Specific-Development/dp/0321658701%3FSubscriptionId%3D0JTCV5ZMHMF7ZYTXGFR2%26tag%3Dscotdorm-20%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D0321658701)). The issue centers around the fact that a reader took the code sample presented in the book and ran FxCop (Code Analysis) on it, which generated a warning: “Ensure that base.Dispose() is always called.” The “lesson learned” that Bill presents is that “tools are there to help us, not control us.”

While I completely agree with the belief that tools are there to help us, I think it’s important to understand *why* FxCop is raising this particular warning. The code presented in Bill’s book looks like:
  <div style="border-bottom: silver 1px solid; text-align: left; border-left: silver 1px solid; padding-bottom: 4px; line-height: 12pt; background-color: #f4f4f4; margin: 20px 0px 10px; padding-left: 4px; width: 97.5%; padding-right: 4px; font-family: 'Courier New', courier, monospace; direction: ltr; max-height: 200px; font-size: 8pt; overflow: auto; border-top: silver 1px solid; cursor: text; border-right: silver 1px solid; padding-top: 4px" id="codeSnippetWrapper">   

```
<span style="color: #008000">// Have its own disposed flag.</span>  
<span style="color: #0000ff">private</span> <span style="color: #0000ff">bool</span> disposed = <span style="color: #0000ff">false</span>;  
<span style="color: #0000ff">protected</span> <span style="color: #0000ff">override</span> <span style="color: #0000ff">void</span> Dispose(<span style="color: #0000ff">bool</span> isDisposing)  
{  
    <span style="color: #008000">// Don't dispose more than once.</span>  
    <span style="color: #0000ff">if</span> (disposed)  
        <span style="color: #0000ff">return</span>;  
    <span style="color: #0000ff">if</span> (isDisposing)  
    {  
        <span style="color: #008000">// TODO: free managed resources here.</span>  
    }  
    <span style="color: #008000">// TODO: free unmanaged resources here.</span>  
    <span style="color: #008000">// Let the base class free its resources.</span>  
    <span style="color: #008000">// Base class is responsible for calling</span>  
    <span style="color: #008000">// GC.SuppressFinalize( )</span>  
    <span style="color: #0000ff">base</span>.Dispose(isDisposing);  
    <span style="color: #008000">// Set derived class disposed flag:</span>  
    disposed = <span style="color: #0000ff">true</span>;  
}
```

</div>
This code does follow all of the guidelines for implementing the Dispose pattern. In this case, it’s presumably part of a larger example showing how to implement the pattern as part of a base class. The reason FxCop is warning you about this code is the first if statement in the Dispose method, which will cause the method to exit if disposed is true.



The problem here is that there is the possibility that if the disposed flag is true, the call to base.Dispose() will never be executed. As Bill points out, it is possible for some other code elsewhere in the class to set this flag. He states that this is an “unlikely occurrence.” While that is probably true, it can be a potentially dangerous assumption to make and is one that can be easily corrected. By changing the code slightly you can remove this assumption and correct the FxCop violation.


<div style="border-bottom: silver 1px solid; text-align: left; border-left: silver 1px solid; padding-bottom: 4px; line-height: 12pt; background-color: #f4f4f4; margin: 20px 0px 10px; padding-left: 4px; width: 97.5%; padding-right: 4px; font-family: 'Courier New', courier, monospace; direction: ltr; max-height: 200px; font-size: 8pt; overflow: auto; border-top: silver 1px solid; cursor: text; border-right: silver 1px solid; padding-top: 4px" id="codeSnippetWrapper">
  

```
<span style="color: #0000ff">private</span> <span style="color: #0000ff">bool</span> disposed = <span style="color: #0000ff">false</span>;  

<span style="color: #0000ff">protected</span> <span style="color: #0000ff">override</span> <span style="color: #0000ff">void</span> Dispose(<span style="color: #0000ff">bool</span> disposing)  
{  
   <span style="color: #0000ff">if</span> (!disposed)  
   {  
        <span style="color: #0000ff">if</span> (disposing)  
        {  
            <span style="color: #008000">// Dispose managed resources.</span>  
        }  

        <span style="color: #008000">// Dispose unmanaged resources.</span>  

        disposed = <span style="color: #0000ff">true</span>;  
    }  

    <span style="color: #0000ff">base</span>.Dispose(disposing);  
}  

```

</div>



Using this implementation allows the call to base.Dispose() to always occur, which ensures that the the disposal chain is always properly followed.


<div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:bc832855-e6a1-4f9b-b37e-61375da908c7" class="wlWriterSmartContent">Technorati Tags: [.NET](http://technorati.com/tags/.NET),[C#](http://technorati.com/tags/C%23),[Dispose Pattern](http://technorati.com/tags/Dispose+Pattern)</div><div class="wlWriterHeaderFooter" style="text-align:right; margin:0px; padding:4px 0px 4px 0px;">[![Digg This](http://digg.com/img/badges/100x20-digg-button.png "Digg This")](http://digg.com/submit?url=http%3a%2f%2fgeekswithblogs.net%2fsdorman%2farchive%2f2010%2f05%2f25%2fthe-dispose-pattern-and-fxcop-warnings.aspx&title=The+Dispose+Pattern+(and+FxCop+warnings))</div>
