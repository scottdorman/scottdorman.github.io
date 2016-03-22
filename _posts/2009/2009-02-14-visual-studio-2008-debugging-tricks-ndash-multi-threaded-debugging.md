---
layout: post
title: Visual Studio 2008 Debugging Tricks &ndash; Multi-Threaded Debugging
date: 2009-02-14 16:16:53 -05:00
---

We previously talked about the [Location, Condition and Hit Count]({% post_url /2009/2009-02-14-visual-studio-2008-debugging-tricks-ndash-advanced-breakpoints %}) modifiers for advanced breakpoints. These are great for a lot of different debugging scenarios, but what about tricks specifically for debugging multi-threaded applications. If you have ever tried to debug a multi-threaded application you know that it isn’t always the easiest experience. 

Hopefully everyone is already familiar with the Treads window. If you aren’t, it is accessed through the Debug|Windows|Threads menu or the Ctrl+D, T keyboard shortcut. The threads window is only available when you are actively in a debug session.

[![image](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/VisualStudio2008DebuggingTricksMultiThre_D278/image_thumb.png "image")](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/VisualStudio2008DebuggingTricksMultiThre_D278/image_2.png)The Threads window provides a few useful tricks of it’s own that you might not be aware of. The first three tricks are available from the context menu.

You can freeze threads to avoid bouncing around when single stepping and you can switch to a specific thread.

Giving threads meaningful names is very helpful in helping to identify your threads and not all threads have a meaningful name (or in some cases, they don’t have a name at all). Fortunately, you can rename threads directly from the Threads window as well. You can do this using either the Rename context menu or simply clicking in the Name column and typing.

![](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/VisualStudio2008DebuggingTricksMultiThre_D278/080107_2004_NeatNewMult2_3.png)  

The Threads window also makes it easier to identify the main and worker threads by using the green and yellow color squares. Perhaps the most interesting new feature is the ability to flag threads. Once a thread is flagged, you can use use the Debug Location toolbar to only display those flagged threads. This is a great simplifying option for applications that have a lot of threads.

![](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/VisualStudio2008DebuggingTricksMultiThre_D278/image_5.png) 

One other benefit of the Threads window is that by hovering the mouse over the Location column (or the current thread indicator, which is the yellow arrow) you can see the call stack for that thread. This is really useful if you just need to check the call stack quickly and don’t actually want to switch to that thread.

One last trick to mention is the Show Threads in Source option. [![image_thumb[58]](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/VisualStudio2008DebuggingTricksMultiThre_D278/image_thumb58_24496d81-8735-4631-b8b0-198b3a3fa12d.png "image_thumb[58]")](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/VisualStudio2008DebuggingTricksMultiThre_D278/image142.png)This is available from the Threads window context menu and also the Debug toolbar. 

When this option is turned on you get some very nice visual indicators to show information about your threads. If you look carefully, you will see that the breakpoint symbol actually has a red and blue squiggly line through it and, just below that you see a similar marker. If you hover the mouse over the threads marker you will see a debug tool tip that shows you all of the threads that are executing at that location. If you notice there are also some source code lines shaded in grey, which indicates that another thread is executing at the same location. 

![](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/VisualStudio2008DebuggingTricksMultiThre_D278/080107_2004_NeatNewMult1_3.png) 

One word of caution with the Show Threads In Source option: You must have this option enabled before your debug session begins in order for it to behave correctly.

Now, let’s take a look now at the Filter modifier. This is used to restrict the breakpoint to only being set in certain processes and/or threads. When you choose the filter modifier, the Breakpoint Filter dialog is displayed

![](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/VisualStudio2008DebuggingTricksMultiThre_D278/image140_3.png)

which allows you to specify the machine name, process id (or name), and/or the thread id (or name). Using the threads shown earlier, if we wanted to restrict a breakpoint to only being set in Thread 3 we could set the filter to either of these expressions:

*   ThreadId = 2020 
*   ThreadName = "Thread 3"   

Two important things to be aware of here are that the machine/process/thread keywords are case insensitive and that the “==” operator is supported.
  <div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:e5ff7221-12bf-4fbe-b949-54497c96a9d7" class="wlWriterSmartContent">*Technorati Tags: [Visual Studio](http://technorati.com/tags/Visual+Studio), [Advanced](http://technorati.com/tags/Advanced), [Debugging](http://technorati.com/tags/Debugging)*</div><div class="wlWriterHeaderFooter" style="text-align:left; margin:0px; padding:4px 4px 4px 4px;">[![DotNetKicks Image](http://www.dotnetkicks.com/Services/Images/KickItImageGenerator.ashx?url=http://geekswithblogs.net/sdorman/archive/2009/02/14/visual-studio-2008-debugging-tricks-ndash-multi-threaded-debugging.aspx&bgcolor=0080C0&fgcolor=FFFFFF&border=000000&cbgcolor=D4E1ED&cfgcolor=000000)]({% post_url /2009/2009-02-14-visual-studio-2008-debugging-tricks-ndash-multi-threaded-debugging %})</div>
