---
layout: post
title: When Should You Use WPF?
date: '2008-07-20 13:52:15 -05:00'
tags: wpf
---

It's pretty clear that Windows Presentation Foundation (WPF) is here to stay. In fact, use of WPF is becoming more popular and frequent, particularly now that Silverlight 2.0 is on the horizon. The problem is that there has been very little guidance available to help you decide when to use the various UI technologies available. There is however, some unofficial help in the form of this [blog post](http://blogs.msdn.com/synergist/archive/2007/07/10/when-to-use-which-microsoft-presentation-technology.aspx) and this [white paper](http://www.davidchappell.com/articles/white_papers/Introducing_WCF_in_.NET_Framework_3.5_v1.0.docx).

Here is the comparison matrix from Michael's blog post:

|    |     |   |    |    |
|----|-----|---|----|----|
||**[WPF](http://wpf.netfx3.com/)**|**[WPF XBAP](http://www.xbap.org/index.html)**|**[Silverlight](http://www.microsoft.com/silverlight/)**|**[ASP.Net + AJAX](http://ajax.asp.net/)**|
|**Client**|Windows XP SP2 (With [.Net 3.0](http://www.microsoft.com/downloads/details.aspx?familyid=10cc340b-f857-4a14-83f5-25634c3bf043&displaylang=en)) & Vista|Internet Explorer + Windows XP SP2 (with .[Net 3.0](http://www.microsoft.com/downloads/details.aspx?familyid=10cc340b-f857-4a14-83f5-25634c3bf043&displaylang=en)) & Vista|FireFox, Mac Safari, Internet Explorer|Any Web Browser|
|**Deployment**|Downloadable Installer or [ClickOnce](http://msdn2.microsoft.com/en-US/library/142dbbz4(VS.80).aspx)|Runs in Internet Explorer secure sandbox|One-time install of Silverlight plug-in|Web Page|
|**When to use**|Programs that need access to Windows desktop files.|Intranet applications for Windows-oriented companies.|Rich Internet Applications for public-facing web sites|General-purpose public-facing web sites|
