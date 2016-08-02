---
layout: post
title: Microsoft and monetizing developer products
date: 2008-07-13 09:38:32 -05:00
---

I'm catching up on blog posts and saw this [one](http://blogs.msdn.com/bharry/archive/2008/07/05/power-tools-and-software-assurance.aspx) from Brian Harry about the [TFS Power Tools](http://msdn.microsoft.com/en-us/vs2005/aa718351.aspx) and Software Assurance. In that post he asks "How are Power Tools monetized?" and goes on to mention that there is a possibility that the power tools will become a paid feature and part of the Software Assurance (SA) program.

My response (which I tried to post as a comment, but since it didn't save I'm turning it into this blog post instead) is this:

**Absolutely not!** While I understand the desire to monetize every "product" coming out of Microsoft, it sometimes ends up hurting the community as a whole. The Power Tools are a great set of extensions to Visual Studio and TFS and should continue to be available to anyone who needs them, regardless as to whether they have purchased SA or not. 

By making these a purchased product, you end up in a situation like we currently have with [FxCop](http://msdn.microsoft.com/en-us/library/bb429476(VS.80).aspx)/VS Code Analysis, [StyleCop](http://code.msdn.microsoft.com/sourceanalysis), and MSTest. FxCop is free but doesn't include all of the features of VS Code Analysis, which only comes with the Team System SKUs of Visual Studio. Likewise, StyleCop is free and doesn't have an equivalent in Visual Studio while MSTest only comes with Team System SKUs and isn't as widely used as it might be if it were more available. 

The other problem is that you then start sending mixed signals to the community. On one hand you say that running static code analysis is a best practice but you then restrict that capability to companies/developers willing to spend $10K+ on a Team System SKU. This makes it hard for the community to recognize the real value since it becomes seen as a restricted/elite/enterprise-only feature. 

It also makes it harder for us to talk about things...it's difficult to tell a group of people at a code camp "Yes, code analysis is important and it's part of Visual Studio, but you can't download VS Express and use it, if you have VS Standard or even Pro you can't use it. You can only use it if you're lucky enough to have the most expensive version of Visual Studio." 

**There was a time when Microsoft was much less concerned about monetizing their developer products and instead concerned with creating solid developer tools that continually attract new developers (and retain existing ones) to the Windows/Microsoft platform. Moving away from that model isn't necessarily a good thing for the community or for Microsoft.**
