---
layout: post
title: Windows Vista UX Guidelines and Visual Studio
date: 2008-07-25 09:50:23 -05:00
---

Whether you like Vista or not, the user interface aspects of the operating system are here to stay. Overall, I think Microsoft did a good job with the core interface guidelines, as presented in the [Windows Vista User Experience Guidelines](http://msdn.microsoft.com/library/aa511258.aspx).

From the guidelines, 

> The goals for these official Windows Vista® User Experience Guidelines (or "UX Guide" for short) are to:
> 
> *   Establish a high quality and consistency baseline for all Windows Vista-based applications.
> *   Answer your specific user experience questions.
> *   Make your job easier!

The UX Guide is one of the most comprehensive UI guidelines I've seen published from Microsoft since the Windows 3.1 UI Guidelines book.

The problem is that the Visual Studio Windows Forms designer doesn't follow all of the guidelines, specifically the [layout guidelines](http://msdn.microsoft.com/en-us/library/aa511279.aspx#sizingspacing ). There is a bug entered at [Microsoft Connect](https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=357125) about this issue, but after 4 days Microsoft closed the issue saying it won't be fixed because it's too big of a change to the .NET Framework.

The problem with that is that this issue has absolutely nothing to do with the .NET Framework. It is purely an issue that exists within the Visual Studio Windows Forms designer. By not fixing this issue, Microsoft is making it virtually impossible for developers to create applications that run on Vista which also follow the Vista UX Guidelines...at least using Visual Studio. 

As I have mentioned [previously]({% post_url /2008/2008-07-13-microsoft-and-monetizing-developer-products %}), there was a time when Microsoft was primarily concerned with creating solid developer tools and ensuring that developers were able to create applications that followed all of their UX guidelines for the current operating system. By not continuing this trend, Microsoft is sending mixed signals to the developer community...you should follow the Vista UX Guidelines but you can't use Visual Studio to do it.

Discussing this in the forums isn't really going to be of much help as there really is no workaround to resolve this issue and there really isn't much to discuss about it anyway...the Windows Forms designer simply doesn't follow the new UX Guidelines.

Be sure to [vote on this issue](https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=357125) so Microsoft continues to be aware of the problem and how the developer community see it.
