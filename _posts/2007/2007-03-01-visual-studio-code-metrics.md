---
layout: post
title: Visual Studio Code Metrics
date: 2007-03-01 21:47:00 -05:00
---

Visual Studio will finally get built-in support for generating code metrics for project and solutions. Unfortunately, we'll have to wait until Orcas officially ships, but it is part of the latest March CTP release ([Virtual PC image](http://www.microsoft.com/downloads/details.aspx?FamilyID=B533619A-0008-4DD6-9ED1-47D482683C78&displaylang=en) or [self-extracting install](http://www.microsoft.com/downloads/details.aspx?FamilyID=cf76fcba-07af-47ac-8822-4ad346210670&DisplayLang=en)). Again, as with the integrated FxCop analysis, this will only be available with the Visual Studio Team Developer and Team Suite editions. I still think Microsoft is doing the development community a huge injustice with this decision, but I'm glad to see Visual Studio finally getting some more code analysis tools.

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/o_vscodemetrics.jpg) 

Right now, it only calculates five metrics:

1.  Maintainability Index (based on Halstead metrics)  Cyclomatic Complexity  Depth of Inheritance  Class Coupling  Lines of Code 

All of the metrics except Class Coupling are averaged at the type, namespace, and assembly level. Class Coupling displays the total number of distinct types referenced at the method and type level.

Several third-party add-ons for Visual Studio have had similar features for a while, but I like the way this is integrated with the editor environment. Hopefully, Microsoft will be adding additional metrics as well as a **well-documented and simple** extension interface so we can write our own metrics that plug in to the same framework. They will be incorporating some of [Rico Mariani's](http://blogs.msdn.com/ricom/) metrics in the future, but there is no indication of which ones and if they will make it in to the official release.

It's not clear at this point if the metrics will integrate with Team Build, although that would be a very nice feature. Providing that level of integration would allow build-to-build comparisons and historical trending analysis to be performed.

Unfortunately, there isn't a plan to make this available for Visual Studio 2005, which I think is a mistake. Orcas probably won't ship until close to the end of the year, and that is a long time to wait for this type of code analysis. There are open source tools available, such as [NDepend,](http://www.ndepend.com) but they don't integrate into Visual Studio.
