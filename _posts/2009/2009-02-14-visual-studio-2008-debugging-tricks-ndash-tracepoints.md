---
layout: post
title: Visual Studio 2008 Debugging Tricks &ndash; Tracepoints
date: 2009-02-14 16:17:12 -05:00
---

We have talked about the [Location, Condition, Hit Count]({% post_url 2009/2009-02-14-visual-studio-2008-debugging-tricks-ndash-advanced-breakpoints %}), and [Filter]({% post_url 2009/2009-02-14-visual-studio-2008-debugging-tricks-ndash-multi-threaded-debugging %}) modifiers for breakpoints which only leaves the When Hit modifier. Using the When Hit modifier allows you to change your breakpoint to a tracepoint.

What is a tracepoint? Simply put, it is a breakpoint that continues execution. Why would this be interesting or even important? Tracepoints are great when you want to trace a particular path of execution, such as OnDeserialized events in your WCF DataContract classes. You are interested in watching the order your objects are deserialized to ensure that everything is happening when you expected it to occur. 

In this scenario, you aren’t really interested in stopping the execution. Ordinarily you could achieve this by inserting Trace.WriteLine (or even Console.WriteLine or Debug.WriteLine) calls throughout your code. While this would work it means that you are adding lines of code just for debugging purposes (so hopefully they would only be needed temporarily) which means you need to remember to remove them when you are done debugging. Wouldn’t it be great if you could simply set a breakpoint to execute Console.WriteLine (or some equivalent) to display a message in our Output window?

That’s exactly what a tracepoint does, but it can do a lot more than just that.  

   ![image](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/VisualStudio2008DebuggingTricksTracepoin_E1A7/image_3.png "image")  

The When Breakpoint Is Hit dialog allows you to simply print a message, but that message can contain special keywords and can also evaluate methods and properties of any object that is in scope when the tracepoint is hit. In addition to printing a message,  you can also run a macro. By default a tracepoint is intended to continue execution, but you can change that as well which will effectively give you a breakpoint which will print a message and/or execute a macro before breaking.
  <div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:47dd9e17-5935-4891-a6be-aeae9689a30c" class="wlWriterSmartContent">*Technorati Tags: [Visual Studio](http://technorati.com/tags/Visual+Studio), [Advanced](http://technorati.com/tags/Advanced), [Debugging](http://technorati.com/tags/Debugging)*</div><div class="wlWriterHeaderFooter" style="text-align:left; margin:0px; padding:4px 4px 4px 4px;">[![DotNetKicks Image](http://www.dotnetkicks.com/Services/Images/KickItImageGenerator.ashx?url=http://geekswithblogs.net/sdorman/archive/2009/02/14/visual-studio-2008-debugging-tricks-ndash-tracepoints.aspx&bgcolor=0080C0&fgcolor=FFFFFF&border=000000&cbgcolor=D4E1ED&cfgcolor=000000)]({% post_url 2009/2009-02-14-visual-studio-2008-debugging-tricks-ndash-tracepoints %})</div>
