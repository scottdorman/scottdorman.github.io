---
layout: post
title: Folder Size for Windows Explorer
date: 2007-03-04 11:49:00 -05:00
---

![](/img/posts/{% page.id %}/o_foldersize.jpg) 

If you have ever wanted to know how big a folder was, you had two options:

1. Open a dos prompt and get a directory listing 
2. Open the properties for the folder

Wouldn't it be great if the folder size could be displayed right in Windows Explorer, just like it does for file size? Well, thanks to this [post](http://blogs.msdn.com/noahc/archive/2007/02/26/folder-size-for-windows-explorer.aspx) on [Noah's](http://blogs.msdn.com/noahc/default.aspx) blog, it is now possible! 

This is an open source project available on SourceForge at:

[http://foldersize.sourceforge.net/](http://foldersize.sourceforge.net/)

Of course, this information is only available in Details view, but if you are looking for this type of information you probably are already in that view.

It works by adding a new "Folder Size" column that can list the size of the folder. It keeps track of which folders you view and scans them in the background using an intelligent scanner service that monitors the average length of the disk requests queue. 

You can also pause the service through the Folder Size Control Panel, which will keep it running and updating, but disable the background scanner. 

If you don't display the Folder Size column, the background scanner doesn't stay active, so it won't take up CPU time.

There are some [known issues](http://foldersize.sourceforge.net/support.html), most of which deal with substituted dries and Samba shares.  

Folder size runs on Windows 2000 and higher except Vista, but only on 32-bit versions of Windows XP.
