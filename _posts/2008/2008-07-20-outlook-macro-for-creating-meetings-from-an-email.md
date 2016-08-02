---
layout: post
title: Outlook Macro for Creating Meetings from an Email
date: 2008-07-20 12:07:41 -05:00
---

I just came across a post by [Michael S. Scherotter](http://blogs.msdn.com/synergist) about his Outlook macro to create an Outlook appointment from an email message. This is a feature that Outlook really should have, and this macro fills that gap very nicely. I cleaned up the code a bit and made some improvements to Michael's original version:

*   The appointment type is now set to "Meeting" by default so it shows the participants.
*   The Importance and Sensitivity are now set based on the corresponding property in the email.
*   The Busy Status is set to "Busy" by default and a reminder is set for 5 minutes before the start of the meeting.  

The macro is [available](http://cid-93d618d639ec9651.skydrive.live.com/self.aspx/Public/Office%202007%20Macros/OutlookMacros.bas) on my SkyDrive account. For details on how to add a VBA Macro to Outlook, check out Michael's [instructions](http://blogs.msdn.com/synergist/archive/2007/05/23/adding-a-vba-macro-to-outlook.aspx).

I make no guarantees or warranties on this macro. I have tested it on several different email messages and other Outlook items and it seems to work and not cause any problems, but, as always, use with caution. Since it is a macro, you have the full source code available to investigate and see what it's actually doing. If you find any bugs or make any useful changes, please let me know and I'll update the macro.
