---
layout: post
title: The Code Project Browser Add-in for Visual Studio
date: 2007-08-15 20:29:38 -05:00
---

I received an email today through my blog from one of the developers at [SlickEdit](http://www.slickedit.com/component/option,com_frontpage/Itemid,1/), who also happens to be a member of [The Code Project](http://www.codeproject.com/) community, letting me know about a new [Visual Studio Add-in](http://www.codeproject.com/csharp/cpbrowser.asp) they have developed. You may remember I blogged about the free [SlickEdit Gadgets]({% post_url 2007-08-15-SlickEdit-Gadgets-for-Visual-Studio-2008 %}), a really great set of Add-ins for Visual Studio.

 ![](/img/posts/{% page.id %}/cpbrowser21_1.jpg) 

Since I am also a member of The Code Project community, I spend a lot of time on the web site answering forum questions and reading the articles posted. I also spend a lot of time in Visual Studio. Thanks to this new Add-in, I can browse The Code Project directly in Visual Studio. I know that I can do this without the Add-in, but the Add-in provides some additional features:

1.  You can download files directly into a "My Documents\My Code Project Samples" directory, where they will be automatically unzipped and loaded into the IDE.  
2.  You can view, reload and delete all of the projects you've downloaded through a sidebar.  
3.  You can keep a list of favorite articles. 

The Add-in currently only installs for Visual Studio 2005, but it will run with Visual Studio 2008 Beta 2. In order to run it, you need to follow these steps:

1.  Install the Add-in using the MSI installer for VS2005.  
2.  Copy the CPBrowser.AddIn file from the `` folder to the `` folder. (You might need to create this directory under the Visual Studio 2008 folder first.)  
3.  Change the following items (in ***bold italics***) in the CPBrowser.AddIn file:  
```
<?xml version="1.0" encoding="UTF-16" standalone="no"?>
<Extensibility xmlns="http://schemas.microsoft.com/AutomationExtensibility">
    <HostApplication>
        <Name>Microsoft Visual Studio Macros</Name>
        <Version>9.0</Version>
    </HostApplication>
    <HostApplication>
        <Name>Microsoft Visual Studio</Name>
        <Version>9.0</Version>
    </HostApplication>
    <Addin>
        <Assembly>C:\Program Files\Code Project Browser\VS2008\CPBrowser.dll</Assembly>
    </Addin>
</Extensibility>
```

They are currently working on an installer for Visual Studio 2008 so you don't have to do the manual steps. They are also looking to add the following features:

*   A URL entry field that allows you to paste the URL of an article and go directly to it. 
*   Linking the Add-in Favorites to the Bookmarks feature of the web site. 
*   A fix for people that don't have the "traditional" C:\Program Files" folder, such as foreign language versions or 64-bit of Windows.

One other feature requested was a progress indicator showing that a page is loading. I'm pretty sure it will be included but as of right now I haven't heard confirmation that it has been added to the list.

If you use The Code Project, this is definitely an Add-in you want to install. You can download the source code and the installer from The Code Project through the article [The Code Project Browser Add-in for VS 2005](http://www.codeproject.com/csharp/cpbrowser.asp).
