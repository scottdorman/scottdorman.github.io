---
layout: post
title: Source Analysis
date: 2008-05-25 10:13:41 -05:00
---

As many of you know, I'm a big proponent of [code styles and standards](http://geekswithblogs.net/sdorman/category/6657.aspx). As part of that, I'm always on the lookout for new tools that help enforce (or at least report) those standards. 

Some of you may have heard about a tool called StyleCop. In fact, there are references to StyleCop in some of the MSDN articles and other blogs. Since it was an internal tool, we could only imagine what features it provided and hope to find a copy of it somewhere. Well, imagine no longer. Earlier this week, Microsoft released StyleCop as [Source Analysis for C#](http://blogs.msdn.com/sourceanalysis/archive/2008/05/23/announcing-the-release-of-microsoft-source-analysis.aspx). 

I think the tool is still a little rough around the edges and doesn't have a lot of supporting documentation around the rules it checks, but it's a good first start. It installs into Visual Studio and allows you to run analysis on a solution, project, or file.

Source Analysis is different from static analysis (FxCop) since it analyzes the source code directly not a compiled binary. As a result, source analysis focuses on more design (or style) issues such as layout, readability and documentation. There are some interesting future directions, including the ability to fix many of the violations automatically.

There are a few things that I think Microsoft needs to address now that we have both FxCop and StyleCop available. First is the issue of names. The "FxCop" and "StyleCop" names are fine, however the names "Source Analysis" (StyleCop) and "Code Analysis" (FxCop) are way too similar and are going to lead to a lot of confusion. The better choice is to call everything source analysis (or code analysis, pick one and stick with it) as the overall technology/process concept and then create individual tools (and names) underneath that.

Second, the rules documentation for StyleCop really should be following the same pattern as FxCop. Again, these are very similar tools and really should provide a consistent experience. Along those lines, I'd really love to see the integrated static "Code" analysis ripped back out of Visual Studio and put directly into a stand-alone version of FxCop (that can integrate with both Visual Studio and MSBuild). This is how StyleCop works and I think it's a great model since it keeps these tools free for all developers and helps reinforce the idea that this type of analysis is important to the community as a whole, not just the small portion that can afford the more expensive Team Suite editions of Visual Studio.

Continuing the Visual Studio integration idea, the StyleCop settings really should be integrated with the project properties in the same way as the static code analysis. (This also means that if/when the code analysis becomes separate again (see the previous paragraph) that we don't loose that level of integration.)

I like the fact that StyleCop can integrate with MSBuild, but it would also be nice if I could get this integration directly through Visual Studio so I can make it part of my every day builds if I want. (Again, this is similar to the integrated static code analysis).

All of that aside, I think this is a good first start that should become part of your every day builds, particularly if you have any type of automated build environment. Be sure to download it from [Code Gallery](https://code.msdn.microsoft.com/Release/ProjectReleases.aspx?ProjectName=sourceanalysis).
