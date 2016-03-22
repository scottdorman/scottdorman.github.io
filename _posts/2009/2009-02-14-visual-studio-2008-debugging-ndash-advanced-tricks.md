---
layout: post
title: Visual Studio 2008 Debugging &ndash; Advanced Tricks
date: 2009-02-14 18:45:40 -05:00
---

We previously talked about the [Location, Condition, Hit Count]({% post_url /2009/2009-02-14-visual-studio-2008-debugging-tricks-ndash-advanced-breakpoints %}), [Filter]({% post_url /2009/2009-02-14-visual-studio-2008-debugging-tricks-ndash-multi-threaded-debugging %}), and [When Hit]({% post_url /2009/2009-02-14-visual-studio-2008-debugging-tricks-ndash-tracepoints %}) modifiers for breakpoints. These are great advanced breakpoints that will really make your debug sessions much more useful, but there are also some other advances in Visual Studio that go beyond these breakpoint modifiers.

The first advance is the idea of advanced location breakpoints. How many times have you been debugging an issue and as you’re looking at the call stack you realize that you want to set a breakpoint somewhere higher up in the call stack? This is really useful when you want to let execution continue but want to stop part way through the return sequence from some lower-level function.

In order to accomplish this you would ordinarily have to find the source file in the solution explorer, then find the function you are interested in and set your breakpoint. Yes, you can simplify this by double-clicking the line in the call stack, which will take you to that line in the source code but then you loose the context of your current location.

![](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/VisualStudio2008DebuggingAdvancedTricks_E730/image_3.png) 

Well, Visual Studio allows you to select the line in the call stack and press F9 (on the default keyboard, this is the keyboard shortcut to insert a breakpoint) and a breakpoint will be inserted at the appropriate location in code. You can also right click on the stack item and choose Run to Cursor.

This is great, but what about trying to set a breakpoint on a line that contains sub expressions, such as a foreach loop. A foreac loop is actually comprised of 3 sub expressions. If you click the gutter to set a breakpoint it sets it on the first sub expression on the line. 

![](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/VisualStudio2008DebuggingAdvancedTricks_E730/image_6.png)

How do you set a breakpoint on another sub expression? For instance, if I wanted to set a breakpoint on the workerSettings.Tasks property in the foreach statement. By selecting the sub expression (or simply putting your cursor anywhere in that sub expression) and pressing F9 you will set a breakpoint only on that sub expression. 

![image](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/VisualStudio2008DebuggingAdvancedTricks_E730/image_9.png "image") 

Let’s now look at a concept that can only be called dynamic assertions. Hopefully you are familiar with the Debug.Assert and Trace.Assert methods which allow you to halt program execution given a specific Boolean condition. While these are useful they aren’t very dynamic and can’t be very complex. But what happens if you want to hit a breakpoint when an error condition occurs in your application that needs to take in to account multiple factors?

If you remember from our discussion on the [Condition]({% post_url /2009/2009-02-14-visual-studio-2008-debugging-tricks-ndash-advanced-breakpoints %}) modifier you can set the condition expression to any any valid Boolean expression. This means that you can also set the condition to be the result of a method call, as long as that method returns a Boolean value. In order to do this, you need to add a method that returns a Boolean. This method should return true if an error condition exists. (Basically, it should return true when you want the breakpoint to hit.) 
  <div style="border-bottom: silver 1px solid; border-left: silver 1px solid; padding-bottom: 4px; line-height: 12pt; background-color: #f4f4f4; margin: 20px 0px 10px; padding-left: 4px; width: 97.5%; padding-right: 4px; font-family: 'Courier New', courier, monospace; max-height: 200px; font-size: 8pt; overflow: auto; border-top: silver 1px solid; cursor: text; border-right: silver 1px solid; padding-top: 4px" id="codeSnippetWrapper">   <div style="border-bottom-style: none; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; padding-left: 0px; width: 100%; padding-right: 0px; font-family: 'Courier New', courier, monospace; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px" id="codeSnippet">     

<span style="color: #606060" id="lnum1">   1:</span> <span style="color: #cc6633">#if</span> DEBUG

<span style="color: #606060" id="lnum2">   2:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">bool</span> CheckName()

<span style="color: #606060" id="lnum3">   3:</span> {

<span style="color: #606060" id="lnum4">   4:</span>    <span style="color: #0000ff">if</span> (<span style="color: #0000ff">this</span>.name == <span style="color: #0000ff">null</span>)

<span style="color: #606060" id="lnum5">   5:</span>    {

<span style="color: #606060" id="lnum6">   6:</span>       <span style="color: #0000ff">return</span> <span style="color: #0000ff">true</span>;

<span style="color: #606060" id="lnum7">   7:</span>    }

<span style="color: #606060" id="lnum8">   8:</span>  

<span style="color: #606060" id="lnum9">   9:</span>    <span style="color: #0000ff">return</span> <span style="color: #0000ff">false</span>;

<span style="color: #606060" id="lnum10">  10:</span> }

<span style="color: #606060" id="lnum11">  11:</span> <span style="color: #cc6633">#endif</span>

</div>
</div>



Notice that I didn’t use the ConditionalAttribute(“DEBUG”) syntax here. The reason for this is that this attribute only works for void return types. Now that we have this method defined, you can use it as the condition expression

![](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/VisualStudio2008DebuggingAdvancedTricks_E730/image_12.png) 

You also get some IntelliSense help showing that this is the correct method and you can verify that the condition is set correctly by looking at the Breakpoints window

![image](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/VisualStudio2008DebuggingAdvancedTricks_E730/image_17.png "image") 

Now, whenever the result of CheckName() is true, the breakpoint will be hit. This allows you to create some really complex and powerful debug conditions for your breakpoints.

Finally, we need to take a look at the New Breakpoint dialog. This is probably the most powerful and underutilized feature of the debugging system. Most of the developers that I know open files and scroll around until they find the line of code that should contain a breakpoint. In at least half of those times (if not more) they already know the function that should contain the breakpoint and generally want to set the breakpoint at the start of the function. This is where the New Breakpoint dialog can really help.

![](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/VisualStudio2008DebuggingAdvancedTricks_E730/image_20.png) 

As you can see from the dialog, you can simply type the name of the function (this can be either a method or a property) which will contain your breakpoint. Unfortunately you don’t get any IntelliSense help while typing the function (like you do in the Breakpoint Condition dialog) but if you leave the “Use IntelliSense to verify the function name” checkbox checked it will display a warning message if you get the name wrong.

![](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/VisualStudio2008DebuggingAdvancedTricks_E730/image_23.png) 

While this can save a lot of scrolling through files to find the right function, it does require you to know the fully qualified method name, which means you must know both the class and method name. What happens if you don’t know what class the method is in or you have multiple methods of the same name where you want to set breakpoints? As long as you have a project loaded, you can simply type the function name and a Choose Breakpoints dialog will display.

![](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/VisualStudio2008DebuggingAdvancedTricks_E730/image_26.png) 

From this dialog, you can see all of the functions that match the name from all classes.

<div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:3235025c-6167-4d4a-b1e8-b737a2c71f22" class="wlWriterSmartContent">*Technorati Tags: [Visual Studio](http://technorati.com/tags/Visual+Studio), [Advanced](http://technorati.com/tags/Advanced), [Debugging](http://technorati.com/tags/Debugging)*</div><div class="wlWriterHeaderFooter" style="text-align:left; margin:0px; padding:4px 4px 4px 4px;">[![DotNetKicks Image](http://www.dotnetkicks.com/Services/Images/KickItImageGenerator.ashx?url=http://geekswithblogs.net/sdorman/archive/2009/02/14/visual-studio-2008-debugging-ndash-advanced-tricks.aspx&bgcolor=0080C0&fgcolor=FFFFFF&border=000000&cbgcolor=D4E1ED&cfgcolor=000000)]({% post_url /2009/2009-02-14-visual-studio-2008-debugging-ndash-advanced-tricks %})</div>
