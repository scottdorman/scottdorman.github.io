---
layout: post
title: Ignore spaces in declaration statements
date: 2007-09-26 12:28:11 -05:00
---

One of the new features coming up in Visual Studio 2008, is the ability to ignore spaces in declaration statements. This was a [bug](http://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=93488) opened on the Microsoft Connect site a long time ago and it is finally getting some work done to fix it.

Unfortunately, even in Visual Studio 2008, we won't have full alignment options like the ability to control how individual symbols are aligned in the editor, but there will be some help for aligning declaration statements. This isn't in the Beta 2 release, but it will be in the final release (and any other Beta or RC releases).

According to [Karen Liu](http://blogs.msdn.com/karenliu/archive/2007/09/24/auto-formatting-removes-tabs.aspx?CommentPosted=true#commentmessage), there is a new option added to the Tools | Options | Text Editor | C# | Formatting | Spacing | Set other spacing options. This new option is a check box titled "Ignore spaces in declaration statements" and applies to:

*   Constants and Fields  
*   Local variables  

The option will apply for every location that a field or local variable is valid, including:  

*   Block  
*   For-statement  
*   Foreach-statement  
*   Using-statement  

If the option is on, spaces **around** attributes, modifiers, type, identifier, and the binary operator will be retained but the spacing **within** the right-hand-side expression will continue to be formatted. Spacing between multiple statements will continue to be removed and it will continue to not format around comments. 

I'm not entirely clear yet how the end result of this will actually work in practice since I don't have a version of Visual Studio 2008 that contains this feature. I like the fact that it will allow me to align declaration statements, but I'm not sold on the idea of applying this to for, foreach, and using statements.
