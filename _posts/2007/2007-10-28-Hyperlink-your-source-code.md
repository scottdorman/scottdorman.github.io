---
layout: post
title: Hyperlink your source code
date: '2007-10-28 14:08:52 -05:00'
---

If you're diligent about putting meaningful comments in your source code (and if you're not, you should be!) you have probably wanted the ability to have a comment link to another method or another area of code. Using XML comments, it is relatively easy to link to other code elements using the <see> or <seealso> tags.

However, if you want to have this same ability in normal comments, you were out of luck. However, a new [Visual Studio Add In](http://www.codeplex.com/hyperAddin/) available on CodePlex is changing that. This add in is called [HyperAddIn](http://www.codeplex.com/hyperAddin/), and it makes creating and following hyper-links in your code trivial.

The main features of the add in are:

*   **Anchors and Hyperlinks in your code comments.** Quickly navigate to related parts of your code by simply clicking on a hyperlink in your comments.  
*   **'GoOut' Navigation.** Quickly find the method, class, and top of the file of the method you are currently in. These places are where you should be put  interesting comments about the 'big picture' comments about the design of the code.  
*   **Word wrapping in comments.**Form nicely justified paragraphs in your comments with one click of the mouse.  
*   Supports both C#, C++, JScript and VB style comments.  

For a full description of these features and all of the other features supported by the add in, take a look at the [help page](http://www.codeplex.com/hyperAddin/Project/Download/FileDownload.aspx?DownloadId=18139).

There is also an effort to get this feature added to the next release of Visual Studio, so be sure to vote for it on [Connect](https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=296795). (You will need to sign in first, and then simply click on the number of stars that indicate it's value to you.)

The ability to have hyperlinks in your source code is one of those features that you will wonder how you got by without it.
