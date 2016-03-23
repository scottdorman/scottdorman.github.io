---
layout: post
title: What Is a Build System?
date: 2007-12-27 15:58:40 -05:00
---

A few days ago, I talked about my [views]({% post_url 2007-12-24-msbuild-or-nant %}) on MSBuild and NAnt. In that post I mentioned the phrase "build system" several times. That, combined with catching up and re-reading some blog posts that I had flagged led me to Jeff Atwood's post "[The F5 Key Is Not a Build Process](http://www.codinghorror.com/blog/archives/000988.html "The F5 Key Is Not a Build Process")". While some of Jeff's post is a bit of [tongue-in-cheek](http://en.wikipedia.org/wiki/Tongue-in-cheek) humor, the points he makes are extremely valid.

In order to understand what a "build system" is, you must first understand how you build code. This applies not just to individual developers, but to the development team as a whole. Even if you are a team of one developer and you do everything, you still have a series of steps you go through in order to build the code.

How many of you build code by following these steps (or something very similar):

1.  Open Visual Studio and load the solution.
2.  Perform a "Get Latest" operation from source control.
3.  Press F5 (or CTRL+SHIFT+B) 

At this point, Jeff makes the comment 

> **If your "build process" is the F5 key, *you have a problem*.** If you think this sounds ridiculous-- *who would possibly use their IDE as a substitute for a proper build process?* -- then I humbly suggest that you haven't worked much in the mainstream corporate development world. The very idea of a build script outside the IDE is alien to most of these teams.

While I agree with the reasoning, I think it's applied at the wrong level. Even in large development teams, the individual developers will still follow this process in their day-to-day work.

The problem occurs when this is your **only** build process. What that means is that when you are ready to release code outside of the development group, whether its to the QA group, some other internal group, or even an outside customer, if you still follow those same 3 steps *you have a problem*.

Unfortunately, as Jeff points out, the idea of a build script that is outside of the IDE is not only alien to most development teams but it's downright unthinkable. Just as unfortunately, it also appears that nothing changes until a major incident occurs - you ship code to your most important customer that is a "[Frankenstein's monster](http://en.wikipedia.org/wiki/Frankenstein%27s_monster)" amalgam of code from various earlier and future releases that completely kills all productivity at that client for an extended period of time or your network is hit by a pervasive and devastating virus that formats all of the hard-drives of the infected computer.

While those incidents may be at the very extreme end of the spectrum they can happen. Even worse is that there are any number of less extreme but equally harmful things that can happen without warning. It's usually at this point that the company realizes that something needs to change, although they aren't always sure what it is.

Here is where the idea of a build system comes in to play. However, before you can understand the importance of a build system, you must first understand the importance of a build script. There are some subtle and some not-so-subtle differences between the two.

Your project may consist of one solution or multiple solutions, installers, documentation, samples, web sites, and any number of other "things" that make up a finished product. The build script defines how you build all of those pieces, what depends on what (the build order), where all of those other "things" come from, and what third-party components are required. At the end of the day, the build script should be a form of living documentation for the project.

The build script should become the "standard" way of building the project when you are ready to release it outside of the development team. It can also be used by the developers to ensure that they can build the entire project on their individual systems.

Now that you have an understanding of what a build script it, we can start to look at a build system. Since a build script defines how to build an individual project, it's understandable (and even required) that the build script for Project A is different than the build script for Project B. They are, after all, different projects. However, even though the build scripts are different there will probably be certain portions of those scripts that are identical (or almost identical).

For instance, if you use InstallShield to author your installer projects the steps you will go through to compile the installer for Project A will be identical to the steps needed for Project B. The only difference will be the name of the InstallShield project file.

A build system takes these identical (or nearly identical) pieces and abstracts them into a common script file. This script file is then included by your project build scripts. If you take a look at any Visual Studio 2005 or 2008 project file, you will see a line that looks like this:
 <div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">

<span style="color: #0000ff"><</span><span style="color: #800000">Import</span> <span style="color: #ff0000">Project</span><span style="color: #0000ff">="$(MSBuildToolsPath)\Microsoft.CSharp.targets"</span> <span style="color: #0000ff">/></span>
</div>


If you then look at that file, you will see a similar line:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">

<span style="color: #0000ff"><</span><span style="color: #800000">Import</span> <span style="color: #ff0000">Project</span><span style="color: #0000ff">="Microsoft.Common.targets"</span> <span style="color: #0000ff">/></span>
</div>


These imported projects define the standard (think "core") features of any MSBuild build script. If you take another look at the project file, you will notice that it really is nothing more than the definition of what files and references make up that project. There is no target named "Build", yet you can run the following command line:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">

msbuild ProjectA.csproj /target:Build
</div>


and MSBuild will compile your project.

Where is the target named "Build"? If you dig in to the two included projects, you will eventually find the "Build" target.

This is the idea behind a build system and it's critical to creating a repeatable, reproducible and consistent build process. This becomes important as the company grows in size and more developers are added to the team and as more products are added to the product line. If each project does the same things in different ways it becomes increasingly more difficult to move developers from one project to another or for someone to provide coverage during vacations or illnesses. When you have a repeatable, reproducible and standard build process the developers are free to worry about the project, not how to build it.

At this point, you should have realized that there are three key tenets to a build system:

*   **Repeatable **- To do, experience, or produce again. [*The American Heritage® Dictionary of the English Language, Fourth Edition*. Houghton Mifflin Company, 2004. 27 December 2007.<Dictionary.com [http://dictionary.reference.com/browse/repeatable](http://dictionary.reference.com/browse/repeatable)>.]   

*   **Reproducible** - To produce again or anew; re-create. [*The American Heritage® Dictionary of the English Language, Fourth Edition*. Houghton Mifflin Company, 2004. 27 December 2007. <Dictionary.com [http://dictionary.reference.com/browse/reproducible](http://dictionary.reference.com/browse/reproducible)>.]  

*   **Standard** - Something, such as a practice or a product, that is widely recognized or employed, especially because of its excellence. [*The American Heritage® Dictionary of the English Language, Fourth Edition*. Houghton Mifflin Company, 2004. 27 December 2007. <Dictionary.com [http://dictionary.reference.com/browse/standard](http://dictionary.reference.com/browse/standard)>.]


By being **repeatable**, you ensure that that the project is built exactly the same way every time it builds no matter who "runs" the build or where it runs. This helps solve the "[works on my machine](http://www.codinghorror.com/blog/archives/000818.html)" syndrome. By being **reproducible** allows you to take the build system and move/copy it to a different computer (or even a build server) or otherwise easily recreate (reproduce) the steps that are required to perform a build. Repeatable and reproducible really go hand-in-hand. By being **standard**, you ensure that all of your projects follow what the development team (and/or the industry) has defined as best practices.

All of these combine to form a system that allows you to easily and accurately build the product for release outside of the development team with a high degree of confidence that it was built properly. (This has absolutely no way of guaranteeing that the product will pass all of the QA tests or meet the client needs, but that's an entirely different issue.)

Ultimately the build scripts that make up your build system should become an integral part of the way projects are built for release. They also serve to become the starting point for creating build servers and automated builds. At that point, you open yourself up to a lot of new ways to enhance and further automated your internal processes.

So remember, the bottom line to doing any of this is to create a set of standard, repeatable and reproducible processes that automate one or more manual tasks.
