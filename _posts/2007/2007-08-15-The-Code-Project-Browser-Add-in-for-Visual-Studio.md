---
layout: post
title: The Code Project Browser Add-in for Visual Studio
date: 2007-08-15 20:29:38 -05:00
---

 ![cpbrowser2[1]](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/TheCodeProjectBrowserAddinforVisualStudi_118BF/cpbrowser21_1.jpg) 

I received an email today through my blog from one of the developers at [SlickEdit](http://www.slickedit.com/component/option,com_frontpage/Itemid,1/), who also happens to be a member of [The Code Project](http://www.codeproject.com/ "The Code Project - Free Source Code and Tutorials") community, letting me know about a new [Visual Studio Add-in](http://www.codeproject.com/csharp/cpbrowser.asp) they have developed. You may remember I blogged about the free [SlickEdit Gadgets]({% post_url 2007-08-15-SlickEdit-Gadgets-for-Visual-Studio-2008 %}), a really great set of Add-ins for Visual Studio.

 Since I am also a member of The Code Project community, I spend a lot of time on the web site answering forum questions and reading the articles posted. I also spend a lot of time in Visual Studio. Thanks to this new Add-in, I can browse The Code Project directly in Visual Studio. I know that I can do this without the Add-in, but the Add-in provides some additional features:

1.  You can download files directly into a "My Documents\My Code Project Samples" directory, where they will be automatically unzipped and loaded into the IDE.  
2.  You can view, reload and delete all of the projects you've downloaded through a sidebar.  
3.  You can keep a list of favorite articles. 

The Add-in currently only installs for Visual Studio 2005, but it will run with Visual Studio 2008 Beta 2. In order to run it, you need to follow these steps:

1.  Install the Add-in using the MSI installer for VS2005.  
2.  Copy the CPBrowser.AddIn file from the `` folder to the `` folder. (You might need to create this directory under the Visual Studio 2008 folder first.)  
3.  Change the following items (in ***bold italics***) in the CPBrowser.AddIn file:  <div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 46%; cursor: text; max-height: 300px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 245px; background-color: #f4f4f4"> <div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">

<span style="color: #606060">   1:</span> <span style="color: #0000ff"><?</span><span style="color: #800000">xml</span> <span style="color: #ff0000">version</span><span style="color: #0000ff">="1.0"</span> <span style="color: #ff0000">encoding</span><span style="color: #0000ff">="UTF-16"</span> <span style="color: #ff0000">standalone</span><span style="color: #0000ff">="no"</span>?<span style="color: #0000ff">></span>

<span style="color: #606060">   2:</span> <span style="color: #0000ff"><</span><span style="color: #800000">Extensibility</span> <span style="color: #ff0000">xmlns</span><span style="color: #0000ff">="http://schemas.microsoft.com/AutomationExtensibility"</span><span style="color: #0000ff">></span>

<span style="color: #606060">   3:</span>     <span style="color: #0000ff"><</span><span style="color: #800000">HostApplication</span><span style="color: #0000ff">></span>

<span style="color: #606060">   4:</span>         <span style="color: #0000ff"><</span><span style="color: #800000">Name</span><span style="color: #0000ff">></span>Microsoft Visual Studio Macros<span style="color: #0000ff"></</span><span style="color: #800000">Name</span><span style="color: #0000ff">></span>

<span style="color: #606060">   5:</span>         ***<span style="color: #0000ff"><</span><span style="color: #800000">Version</span><span style="color: #0000ff">></span>9.0<span style="color: #0000ff"></</span><span style="color: #800000">Version</span><span style="color: #0000ff">></span>***

<span style="color: #606060">   6:</span>     <span style="color: #0000ff"></</span><span style="color: #800000">HostApplication</span><span style="color: #0000ff">></span>

<span style="color: #606060">   7:</span>     <span style="color: #0000ff"><</span><span style="color: #800000">HostApplication</span><span style="color: #0000ff">></span>

<span style="color: #606060">   8:</span>         <span style="color: #0000ff"><</span><span style="color: #800000">Name</span><span style="color: #0000ff">></span>Microsoft Visual Studio<span style="color: #0000ff"></</span><span style="color: #800000">Name</span><span style="color: #0000ff">></span>

<span style="color: #606060">   9:</span>         ***<span style="color: #0000ff"><</span><span style="color: #800000">Version</span><span style="color: #0000ff">></span>9.0<span style="color: #0000ff"></</span><span style="color: #800000">Version</span><span style="color: #0000ff">></span>***

<span style="color: #606060">  10:</span>     <span style="color: #0000ff"></</span><span style="color: #800000">HostApplication</span><span style="color: #0000ff">></span>

<span style="color: #606060">  11:</span>     <span style="color: #0000ff"><</span><span style="color: #800000">Addin</span><span style="color: #0000ff">></span>

<span style="color: #606060">  12:</span>         ***<span style="color: #0000ff"><</span><span style="color: #800000">Assembly</span><span style="color: #0000ff">></span>C:\Program Files\Code Project Browser\VS2008\CPBrowser.dll<span style="color: #0000ff"></</span><span style="color: #800000">Assembly</span><span style="color: #0000ff">></span>***

<span style="color: #606060">  13:</span>     <span style="color: #0000ff"></</span><span style="color: #800000">Addin</span><span style="color: #0000ff">></span>

<span style="color: #606060">  14:</span> <span style="color: #0000ff"></</span><span style="color: #800000">Extensibility</span><span style="color: #0000ff">></span>
</div></div>


They are currently working on an installer for Visual Studio 2008 so you don't have to do the manual steps. They are also looking to add the following features:

*   A URL entry field that allows you to paste the URL of an article and go directly to it. 

*   Linking the Add-in Favorites to the Bookmarks feature of the web site. 

*   A fix for people that don't have the "traditional" C:\Program Files" folder, such as foreign language versions or 64-bit of Windows.


One other feature requested was a progress indicator showing that a page is loading. I'm pretty sure it will be included but as of right now I haven't heard confirmation that it has been added to the list.

If you use The Code Project, this is definitely an Add-in you want to install. You can download the source code and the installer from The Code Project through the article [The Code Project Browser Add-in for VS 2005](http://www.codeproject.com/csharp/cpbrowser.asp).
