---
layout: post
title: "Windows Vista: Kernel Changes - Wakeup, wakeup, wakeup!"
date: 2006-06-18 13:24:00 -05:00
---

Up until Vista, an application or a driver could prevent the system from entering a sleep mode (standby or hibernate) and was often caused by a bug or an overly aggressive power management policy. The problem with this was that the user might not know the system hasn't entered the appropriate sleep stat and eventually loose data.

Vista no longer queries processes when entering sleep states like previous versions of Windows and has reduced the timeout for user-mode notifications to 2 seconds (down from 20 seconds). In addition, drivers can not veto the transition into a sleep state.

Hopefully, these changes will make going to sleep a lot more peaceful.
