---
layout: post
title: StyleCop 4.3 Released
date: '2008-08-19 10:25:15 -05:00'
tags: coding-style code-standards
---

A while ago I [talked]({% post_url /2008/2008-05-25-source-analysis %}) about a new tool from Microsoft called [StyleCop](http://code.msdn.microsoft.com/sourceanalysis). Since then, there was a lot of confusion surrounding the tool and it has undergone a lot of changes both internally and externally.

Both [Jason](http://blogs.msdn.com/sourceanalysis/archive/2008/07/20/clearing-up-confusion.aspx) and [Brian](http://blogs.msdn.com/bharry/archive/2008/07/19/clearing-up-confusion.aspx) do an excellent job explaining the context behind some of the discussions and decisions leading up to these changes, but the biggest one is that the tool has been officially renamed as "StyleCop" to prevent any confusion with the built-in Visual Studio Code Analysis packages. 

I'm not sure I agree 100% with the reasoning behind the name reversion, but I'm glad it went back to the StyleCop name. As I mentioned, Microsoft needs to choose one umbrella name for both [FxCop](http://msdn.microsoft.com/en-us/library/bb429476(VS.80).aspx) and StyleCop as the name for the overall technology/process concept. The industry term (at least the one I'm familiar with) for the type of activities/analysis both of these tools perform is generally called "Code Analysis". Call it that as a technology "suite" that has two tools: FxCop for static analysis and StyleCop for source code style analysis.

I'm happy to say that the newest release of StyleCop shows the direction StyleCop seems to be heading...and it's a good direction. The new release includes various bug fixes and better Visual Studio integration, new rules documentation (which is also integrated into Visual Studio) and new rules. See Jason's [post](http://blogs.msdn.com/sourceanalysis/archive/2008/08/19/stylecop-4-3-is-released.aspx) for the full list of rules added.

A StyleCop SDK is also undergoing final review which will allow custom rules to be created, similar to FxCop.
