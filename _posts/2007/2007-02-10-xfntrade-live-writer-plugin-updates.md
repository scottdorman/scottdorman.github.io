---
layout: post
title: XFN&trade; Live Writer Plugin Updates
date: 2007-02-10 04:25:00 -05:00
---

I know it's only been a couple of days, but there were a few things that were bothering me about my XFN™ plugin for ![](/img/posts/{ page.id }/o_sshot-4.jpg)Live Writer. The biggest issue (and really the one that everything else centered around) was that once a link was inserted, you couldn't edit it again without recreating it. I doubt anyone would have really felt this was a problem, but it was annoying enough to me that I decided to do something about it.

The changes centered around making the plugin a SmartContentSource rather than just a ContentSource ![](/img/posts/{ page.id }/o_sshot-2.jpg). This change allows the plugin to be listed in the "Insert" group that displays as part of the Sidebar and also allows an XFN link to be viewed and editing using the Sidebar. 

When an XFN link is inserted, it is treated as a single element, so when it is selected, you see a "hash outline" around the content. This only displays when you are editing and only when that element has the focus. When the XFN Link has the focus, the Sidebar displays the XFN Link Properties, which allows you to edit the actual hyperlink, the relationships, and also see the current relationships.

The Edit Hyperlink and Edit Relationships links display the appropriate editor. These editors are a subset of the main dialog that is used to insert a link, and allow you to focus on just the part of the link that needs changing.

Since Windows Live Gallery still hasn't approved the first version I submitted, I am going to cancel that one and resubmit the update. Just in case there are any problems, the latest version is 1.0.2597. If you want an "early" copy, send me an email through the [contact](/sdorman/contact.aspx "http://geekswithblogs.net/sdorman/contact.aspx") page and I will send you a copy of the installer.

Once the new version is approved on Windows Live Gallery, it will be in the Miscellaneous category title "XFN Link Editor".
