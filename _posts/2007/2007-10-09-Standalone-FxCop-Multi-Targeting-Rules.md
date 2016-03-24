---
layout: post
title: Standalone FxCop Multi-Targeting Rules
date: 2007-10-09 23:47:56 -05:00
---

Last week, I [talked]({% post_url /2007/2007-10-05-Multi-Targeting-FxCop-Rules %}) about a new [FxCop](http://www.gotdotnet.com/Team/FxCop/) rule that [Krzysztof](http://blogs.msdn.com/kcwalina/archive/2007/10/02/Multi_2D00_TargetingAndFxCop.aspx "Krzysztof") released to help deal with some issues around multi-targeting. In one of the [comments]({% post_url /2007/2007-10-05-Multi-Targeting-FxCop-Rules %}) to this post, I was asked to add this rule to the [Subtext](http://subtextproject.com/) FxCop rule set. As I started working on this, I discovered that the sample project Krzysztof provided was compiled against the .NET Framework 3.5 and would not load with the stand-alone version of FxCop.

I spent a little bit of time reviewing the code in the sample project and, with only a few minor modifications, I was able to get the rule to compile under the .NET Framework 2.0 and load with the stand-alone version of FxCop. I have cleaned up the code a little bit and am making the [sample project](http://cid-93d618d639ec9651.skydrive.live.com/self.aspx/Public/MultitargettingRules.zip) available on my [SkyDrive public folder](http://cid-93d618d639ec9651.skydrive.live.com/self.aspx/Public/).
