---
layout: post
title: Visual Studio user settings per project/solution
date: 2007-04-23 11:12:58 -04:00
---

In a recent email discussion between a few of the Subtext developers and myself, we talked about the need to have the Visual Studio editor settings (like tab size, curly brace location, etc.) stored with each solution as well as globally.

The problem here is that many of us use the same development machine for our "real work" and our personal or open source projects. For some people this might not be a problem, but for most of us, it is. The real issue comes about when one client mandates a certain style that is different from either your personal preferences or from any other projects you work on. In order to accomodate these differences, you end up creating multiple Visual Studio settings files, one for each client or project you work on that has different settings. That's the realtively easy part. The hard part comes when you have to constantly remember to switch settings files and remember which file belongs to which client or project.

The solution that we discussed is that these settings should be stored at the solution level, most likely in a separate settings file (like <solutionname>.settings). There should be an easy way to set these options, and possibly apply them globally as well. If the settings file doesn't exist, then the global settings should be used.

The benefits are:

1.  The settings can be managed and placed under source control.
2.  The settings travel with the solution, so new developers automatically pick up the desired settings.
3.  The developer no longer has to create multiple settings files and switch between them each time he/she changes projects.


The settings file could even be pushed in to TFS in the same way the code analysis settings can be migrated to the solution.

This request has been submitted to  Microsoft Connect, and can be viewed here:

[https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=272773](https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=272773)
