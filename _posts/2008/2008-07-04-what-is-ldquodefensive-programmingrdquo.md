---
layout: post
title: What is &ldquo;Defensive Programming&rdquo;?
date: 2008-07-04 09:26:10 -04:00
---

My post on the [Null Object pattern](http://geekswithblogs.net/sdorman/archive/2008/05/25/null-object-pattern.aspx "Null Object pattern") has generated some interesting dialog. One of the trends that I have seen is the idea that defensive programming means your code should fail as early as possible. I couldn’t agree less.

According to Wikipedia,

> **[Defensive programming](http://en.wikipedia.org/wiki/Defensive_programming)** is a form of [defensive design](http://en.wikipedia.org/wiki/Defensive_design) intended to ensure the continuing function of a piece of [software](http://en.wikipedia.org/wiki/Software) in spite of unforeseeable usage of said software. The idea can be viewed as reducing or eliminating the prospect of [Murphy's Law](http://en.wikipedia.org/wiki/Murphy%27s_Law) having effect. Defensive programming techniques are used especially when a piece of software could be misused mischievously or inadvertently to catastrophic effect.

While this is a good definition, I think it still leaves much to be desired. The Wikipedia entry goes on to say that defensive programming is one approach to improving software quality by “Making the software behave in a predictable manner despite unexpected input or user actions.”

I think this is the closest definition that actually conveys what defensive programming is all about. The idea behind defensive programming is that the application should behave in a consistent and predictable manner even in the case of unexpected conditions.

There are a lot of different ways to achieve this and they are all different depending on what you are trying to accomplish with the code, the programming language, and the control structures being used. For example, considering a switch statement:
  <div style="border-right: gray 1px solid; padding-right: 4px; padding-left: 4px; font-size: 8pt; border-top: gray 1px solid; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">   

```
<span style="color: #0000ff">switch</span> (Orientation)
{
   <span style="color: #0000ff">case</span> Orientation.Horizontal:
      <span style="color: #0000ff">break</span>;

   <span style="color: #0000ff">case</span> Orientation.Vertical:
      <span style="color: #0000ff">break</span>;
}
```

</div>



This is perfectly acceptable code, right? Remembering that enumerations are simply numeric (generally integer) values, it is entirely possible for this switch to get passed a numeric value that doesn’t correspond to either Horizontal or Vertical. In that case, there is the possibility of the switch, or code following the switch, to crash. One option to handle this would be to add a default case to the switch:


<div style="border-right: gray 1px solid; padding-right: 4px; padding-left: 4px; font-size: 8pt; border-top: gray 1px solid; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">
  

```
<span style="color: #0000ff">switch</span> (Orientation)
{
    <span style="color: #0000ff">case</span> Orientation.Horizontal:
        <span style="color: #0000ff">break</span>;

    <span style="color: #0000ff">case</span> Orientation.Vertical:
        <span style="color: #0000ff">break</span>;

    <span style="color: #0000ff">default</span>:
        <span style="color: #0000ff">break</span>;
}
```

</div>



In the default case you could throw an exception (if that’s the appropriate behavior) or, more likely, you take some action that ensures either the remaining code doesn’t execute or at least doesn’t crash.

Looking at another example, this time casting, shows some other ways to program defensively. A common scenario for casting is in UI programming and handling events.


<div style="border-right: gray 1px solid; padding-right: 4px; padding-left: 4px; font-size: 8pt; border-top: gray 1px solid; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">
  

```
<span style="color: #0000ff">private</span> <span style="color: #0000ff">void</span> button1_Click(<span style="color: #0000ff">object</span> sender, EventArgs e)
{
    ((Button)sender).Text = <span style="color: #006080">"You pressed a button"</span>;
}
```

</div>



Again, this code looks perfectly reasonable and will work just fine until someone accidentally assigns this event handler to something other than a button. Once that happens, the code will crash since sender won’t be castable to a Button. There are several different ways to handle this but the simplest (at least in my opinion) is


<div style="border-right: gray 1px solid; padding-right: 4px; padding-left: 4px; font-size: 8pt; border-top: gray 1px solid; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">
  

```
<span style="color: #0000ff">private</span> <span style="color: #0000ff">void</span> button1_Click(<span style="color: #0000ff">object</span> sender, EventArgs e)
{
    Button button = sender <span style="color: #0000ff">as</span> Button;
    <span style="color: #0000ff">if</span> (button != <span style="color: #0000ff">null</span>)
    {
        button.Text = <span style="color: #006080">"You pressed a button"</span>;
    }
}
```

</div>



Yes, it is a bit more code but it also guarantees that no matter what happens if the object that raised the event is not a Button, the code won’t crash. You could have chosen to throw an exception (or just let the exception generated by the runtime bubble up the call stack until it’s handled, but that may not be desirable depending on what you are doing.

The bottom line is that catching exceptions (not throwing them, but catching them…and all exceptions will eventually be caught, but possibly not in a way you intended) is expensive and if there are techniques that allow your program to continue functioning properly or otherwise gracefully handle exceptional conditions, known as “defensive programming”, you should opt for that approach.



<div style="padding-right: 0px; padding-left: 0px; float: none; padding-bottom: 0px; margin: 0px; padding-top: 0px; display: inline" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:517fb5fe-e548-43be-9602-2dea0d3d5c4f" class="wlWriterSmartContent">Technorati Tags: [.NET](http://technorati.com/tags/.NET), [CSharp](http://technorati.com/tags/CSharp)</div>
