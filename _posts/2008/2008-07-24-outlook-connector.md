---
layout: post
title: Outlook Connector
date: '2008-07-24 20:38:03 -05:00'
---

The last time I [wrote]({% post_url /2008/2008-02-24-outlook-connector-calendar-sync %}) about the Outlook Connector it was to talk about the lack of Calendar synchronization and the fact that a new version of the connector was in internal Microsoft testing. 

I am happy to announce that the new version is out of internal testing and is available as a [public beta](http://www.microsoft.com/downloads/details.aspx?FamilyID=9A2279B1-DF0A-46E1-AA93-7D4870871ECF&displaylang=en). This new version synchronizes with your Windows Live Hotmail or Microsoft Office Live Mail accounts, including e-mail, contacts **and calendars**.

I installed the new version and so far it works great. It remembered all of my previous account settings and synchronized my email and calendar the next time I started Outlook.

What I'm not happy about is the way the new version was announced...that is to say, it really wasn't. Over the last few days you may have noticed that the old version of the Outlook Connector quietly stopped synchronizing. You could still send email, but it wouldn't download new messages. There were no error messages indicating a problem, it just wouldn't do anything. The apparent problem is that something must have changed on the Live side which prevented the old version from working correctly. Installing the 12.1 Beta (the new version) seems to correct the problem.

While I'm glad to have access to my calendar, I think Microsoft could have done a much better job letting people know a new version was available. Making the update available as an optional download with Windows or Office Update would have been really nice, at least a message in the synchronization log would have been helpful.
