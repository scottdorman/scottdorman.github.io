---
layout: post
title: Multi-Targeting FxCop Rules
date: 2007-10-05 01:32:32 -05:00
---

Last month, I [talked]({% post_url 2007-09-30-Visual-Studio-2008-Multi-targeting %}) about multi-targeting, one of the new features in Visual Studio 2008. According to [Krzysztof](http://blogs.msdn.com/kcwalina/archive/2007/10/02/Multi_2D00_TargetingAndFxCop.aspx), the idea of [Red and Green bits](http://www.danielmoth.com/Blog/2007/06/net-framework-35.html) made this possible. Everything sounds good, so far. However, there is a very limited number of APIs that have been added to the Red bits that the multi-targeting system isn't able to detect. What this means is that if you set the target to the .NET Framework 2.0 and use one of these new changes, the compiler will not issue a warning or an error. The application will compile just fine, but will fail at runtime.

![image](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image_2.png) 

In order to help deal with this issue, Krzysztof has written a custom [FxCop](http://www.gotdotnet.com/Team/FxCop/) rule that can analyze an assembly targets at the .NET Framework 2.0 and warn you about calls to members that aren't present in the 2.0 RTM. This is a [sample project](http://blogs.msdn.com/kcwalina/attachment/5249710.ashx), and is provided without any guarantees. Hopefully, it will get some more polish and make it's way into either the VS2008 RTM release or an update to FxCop. To install the rule, build the sample project and copy the rules to the FxCop directory.
