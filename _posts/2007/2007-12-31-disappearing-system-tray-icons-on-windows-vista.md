---
layout: post
title: Disappearing System Tray Icons on Windows Vista
date: 2007-12-31 01:51:20 -05:00
---

I've been running Vista on my work laptop since the first quarter of this year and on my development system at home since August. So far, I haven't had too many problems with it. Actually, on my home system I've had almost no problems. My laptop, on the other hand, routinely has issues.

One of the more annoying issues is that my wireless network connection periodically and randomly dies. It comes back to life after about 30 seconds to a minute, but it's still pretty frustrating. (Yes, I know I need to tell the IT department that I need a new laptop; I just don't want to deal with the downtime of reinstalling all of my programs.)

What does this have to do with the title of the post? Everything, actually. One of the ways I know when my network connection has died is by looking at the "network lights" icon in my system tray. It's a great indicator to show if I have a working connection.

The problem is that every so often the icon disappears. On Windows versions prior to Vista, this icon was controlled by the lights.exe application. However, Windows Vista incorporated this capability directly into the OS and is controlled by the Taskbar and Start Menu Properties dialog.

[![image](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/DisappearingSystemTrayIconsonWindowsVist_14CD/image_thumb.png)](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/DisappearingSystemTrayIconsonWindowsVist_14CD/image_2.png) 

This is great, except for the fact that when the icon disappears from the notification area, the checkbox becomes disabled on the property dialog. This tends to make it a bit difficult to re-enable.

Fortunately the work-around until this problem actually gets fixed is relatively simple. (If you experience this problem, be sure to [vote](https://connect.microsoft.com/feedback/ViewFeedback.aspx?FeedbackID=320435&SiteID=480) for the bug on Microsoft Connect.)

Vista keeps a cache of the recently used icons in the registry under the HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\Windows\CurrentVersion\TrayNotify key.

![](http://www.colincochrane.com/image.axd?picture=registry-location.JPG)

Under this key, you will find two REG_BINARY values:

![](http://www.colincochrane.com/image.axd?picture=registry-values.JPG)

To restore your task tray icons, simply delete both of these keys and restart the explorer.exe process. You can restart the process by rebooting or by ending the process from Task Manager and starting a new instance of it.
