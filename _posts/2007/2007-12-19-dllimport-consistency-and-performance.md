---
layout: post
title: DLLImport Consistency and Performance
date: 12/19/2007 8:53:51 PM
---

[Daniel Moth](http://www.danielmoth.com/Blog/index.htm) has an interesting post that talks about performance and the [DllImport](http://msdn2.microsoft.com/library/system.runtime.interopservices.dllimportattribute.aspx) attribute. The underlying theme to his post is that you should define a convention for how the DLL name is specified in the attribute. This actually has a significant enough impact that it really should become one of the rules in your coding standards documents.

If we take an example, all of the following are valid and will work at runtime without any problems:
  <div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 300px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 248px; background-color: #f4f4f4">   <div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">     

<span style="color: #606060">   1:</span> [DllImport(<span style="color: #006080">"kernel32.dll"</span>)]

<span style="color: #606060">   2:</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">extern</span> ...;

<span style="color: #606060">   3:</span>  

<span style="color: #606060">   4:</span> [DllImport(<span style="color: #006080">"kernel32"</span>)]

<span style="color: #606060">   5:</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">extern</span> ...;

<span style="color: #606060">   6:</span>  

<span style="color: #606060">   7:</span> [DllImport(<span style="color: #006080">"Kernel32.DLL"</span>)]

<span style="color: #606060">   8:</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">extern</span> ...;

<span style="color: #606060">   9:</span>  

<span style="color: #606060">  10:</span> [DllImport(<span style="color: #006080">"KERNEL32"</span>)]

<span style="color: #606060">  11:</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">extern</span> ...;

<span style="color: #606060">  12:</span>  

<span style="color: #606060">  13:</span> [DllImport(<span style="color: #006080">"KeRnEl32.DlL"</span>)]

<span style="color: #606060">  14:</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">extern</span> ...;

  </div>
</div>



At first glance, this probably doesn't look like it should be a big issue. It does show a lack of consistency by the developer, but other than that these attributes still import functions from kernel32.dll.

Looking at the results in both Reflector and ILDASM, you start to see the problem this lack of consistency causes.

![](http://www.danielmoth.com/Blog/dirtyKernel32References.png)

If you're still thinking that this isn't a problem because the loader is smart enough to only load one kernel32 instance into your process, you're only partly correct. The loader will only load one instance, but there is still a performance penalty because each string is treated as a separate module. At this point, you should start to see the problem. The more variations you have the more modules get processed by the loader.

Daniel recommends using all lowercase for the library name and always including the ".dll" extension, a recommendation that I agree with completely.
