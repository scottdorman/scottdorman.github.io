---
layout: post
title: Why NAnt Is Almost Better Than MSBuild
date: 2008-01-11 22:30:53 -05:00
---

Earlier this week, [Travis Illig](http://paraesthesia.com/Default.aspx) wrote about [Why NAnt Is Better Than MSBuild](http://paraesthesia.com/archive/2008/01/08/why-nant-is-better-than-msbuild.aspx). It seems he is taking the opposite position that I have been lately. He makes some interesting and valid points in this post that I wanted to address.

> **NAnt lets you run tasks before any targets run; MSBuild doesn't.** I commonly have some "setup" actions that need to happen before anything else in a build script happens. Stuff like registering NCover or starting up TypeMock. It's stuff that needs to happen once, before any other target runs. In NAnt, I can put all of that stuff at the top of the build script, outside any target, and it'll all get run. In MSBuild, every task has to be inside a target, so I have to make sure that every single target in my build script depends on my "setup" target.

Like Travis, I routinely have common actions that need to happen before anything else in the build script runs. In my NAnt scripts, this was done at the top of the build script, outside of any targets. However, as Travis points out, in MSBuild every task has to be inside a target which does mean that these tasks must be placed in some sort of "Initialization" target. The important thing here is that you don't actually need to make sure that all of the other targets have a dependency on the Initialization target. You can get around this by using the InitialTargets attribute of the [Project Element](http://msdn2.microsoft.com/en-us/library/bcxfsh87.aspx). The InitialTargets attribute specifies the target or targets to be run before the targets specified in the DefaultTargets attribute or on the command line. You can list multiple targets in a semi-colon (;) delimited list.

> **NAnt custom tasks can interact with build properties; MSBuild custom tasks can't. **Some of the custom task stuff I want to do is to make things easy for people by letting them set up properties in the environment and having things "just work." For example, a task to generate an AssemblyInfo.cs file with assembly version information already populated based on CruiseControl settings might look for the CCNetLabel property in the environment and set things up automatically based on that.

This is one area where NAnt tasks do provide more flexibility than MSBuild tasks. The only way to pass information into an MSBuild task is through explicit properties (attributes) on the task. Hopefully this is something that later versions of MSBuild will address, but for now there is no way to do this.

> **NAnt properties are manipulated in a consistent fashion; MSBuild properties are handled differently in different contexts.** In NAnt, I can create or change a property just by calling the <property> task. In MSBuild, it's different if I'm outside of a target (<PropertyGroup>) or inside a target (<CreateProperty>). This inconsistency makes for a difficult learning curve.

This is true for versions of MSBuild earlier than the v3.5 release. MSBuild 3.5 has added [new methods for manipulating items and properties](http://msdn2.microsoft.com/library/bb651786.aspx), which allow you to define an ItemGroup or a PropertyGroup inside a target in the same way you do outside of a target. The CreateItem and CreateProperty tasks are still available, but you no longer need to use them.

> **NAnt wildcards, when dealing with the filesystem, match both files and folders; MSBuild wildcards only match files.** This is a heck of a problem when you want to create a dynamic item list in MSBuild of folders you want to clean up. You can't just delete "**/bin" - you have to manually locate *every single one*.

I think this is more of a syntax problem. MSBuild uses the same wild-card syntax as NAnt, which means the following ItemGroup will match all files in the current directory and any subdirectory:
  <div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 98.24%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 84px; background-color: #f4f4f4">   <div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">     

<span style="color: #606060">   1:</span> <span style="color: #0000ff"><</span><span style="color: #800000">ItemGroup</span><span style="color: #0000ff">></span>

<span style="color: #606060">   2:</span>     <span style="color: #0000ff"><</span><span style="color: #800000">Files</span> <span style="color: #ff0000">Include</span><span style="color: #0000ff">="**\bin\**"</span><span style="color: #0000ff">/></span>

<span style="color: #606060">   3:</span> <span style="color: #0000ff"></</span><span style="color: #800000">ItemGroup</span><span style="color: #0000ff">></span>

  </div>
</div>



> **NAnt allows you to load an entire assembly's worth of tasks at once; MSBuild requires each task to be separately loaded.** In NAnt, I do <loadtasks> on an assembly and I've got all of the tasks in the assembly at my disposal. In MSBuild, I have to do a <UsingTask> for every single task I'm using.

This is entirely true. NAnt allows you to load an entire assembly's tasks all at once while MSBuild requires you to specify a UsingTask element for each task in the assembly you want to use. There really isn't a way around this, however you can create a "Tasks" file that lists the tasks. If your task assembly is named "BuildSystemCommonTasks.dll", you would create a file named "BuildSystemCommonTasks.Tasks", which would include all of the UsingTask elements for each task defined in the task assembly. You can then import this file using the Import element.

> **NAnt includes task assemblies in the executing AppDomain; MSBuild doesn't.** This is a problem if you have one custom task assembly that references another custom task assembly. Say you have custom task MyDerivedTask that is a derived/modified version of SomeBaseTask. They're in separate assemblies. Maybe SomeBaseTask is in a third-party assembly I don't want to (or can't) redistribute.

This is also an area that NAnt is considerably different from MSBuild in that it does take a much more isolationist approach to loading task assemblies. This is probably related in some ways to the restriction that MSBuild tasks don't have access to the underlying properties and project information. Again, hopefully this is an area that will be addressed in later versions of MSBuild.

I think NAnt feels more flexible than MSBuild because it doesn't impose some of the same restrictions as MSBuild on the structure of the file. The other benefit NAnt has going for it is that it is a much older technology and has had more time to mature. This is clearly evident when looking at the set of tasks available in NAnt as compared to MSBuild. NAnt also has a much more active development community since the entire project and NAntContrib project are both open source. There is an [MSBuildContrib](http://codeplex.com/MSBuildContrib) project that aims to fill in the gaps between NAnt and MSBuild. (If you want to help, let me know.) Give MSBuild another 7 years (about how old NAnt is now) and then compare them...I think you'll find that they are much more comparable to each other than they are now.
