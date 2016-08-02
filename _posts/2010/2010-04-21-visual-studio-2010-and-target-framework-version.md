---
layout: post
title: Visual Studio 2010 and Target Framework Version
date: 2010-04-21 22:03:56 -05:00
---

Almost two years ago, I [wrote]({% post_url /2008/2008-07-18-visual-studio-2008-and-targetframeworkversion %}) about a Visual Studio macro that allows you to change the Target Framework version of all projects in a solution. If you don't know, the Target Framework version is what tells the compiler which version of the .NET Framework to compile against (more information is available here![](http://i.ixnp.com/images/v6.27/t.gif)) and can be set to one of the following values:

*   .NET Framework 2.0 
*   .NET Framework 3.0 
*   .NET Framework 3.5
*   .NET Framework 3.5 Client Profile
*   .NET Framework 4.0
*   .NET Framework 4.0 Client Profile  

This can be easily accomplished by editing the project properties:

![](/img/posts/{{ page.id }}/image_3.png) 

The problem with this approach is that if you need to change a lot of projects at one time it becomes rather unwieldy. One possible solution is to edit the project files by hand in a text editor and change the `<TargetFrameworkVersion />` and `<TargetFrameworkProfile />` properties to the correct values.

For example, for the .NET Framework 4.0 Client Profile, these values would be:

```
<TargetFrameworkVersion>v4.0</TargetFrameworkVersion>
<TargetFrameworkProfile>Client</TargetFrameworkProfile>
```

Again, this is not only time consuming but can also be error-prone.

The better solution is to automate this through the use of a Visual Studio macro. Since I had already created a macro to do this for Visual Studio 2008, I updated that macro to work with Visual Studio 2010 and .NET 4.0. It prompts you for the target framework version you want to set for all of the projects and then loops through each project in the solution and makes the change. If you select one of the Framework versions that support a Client Profile, it will ask if you want to use the Client Profile or the Full Profile. It is smart enough to skip project types that don't support this property and projects that are already at the correct version. This version also incorporates the [changes]({% post_url /2008/2008-07-18-visual-studio-2008-and-targetframeworkversion %}) suggested by George (in the comments). 

The macro is [available](http://cid-93d618d639ec9651.skydrive.live.com/self.aspx/Public/Visual%20Studio%202008%20Macros/ProjectUtilities.vb) on my SkyDrive account. Download it to your <UserProfile>\Documents\Visual Studio 2010\Projects\VSMacros80\MyMacros folder, open the Visual Studio Macro IDE (Alt-F11) and add it as an existing item to the "MyMacros" project.

I make no guarantees or warranties on this macro. I have tested it on several solutions and projects and everything seems to work and not cause any problems, but, as always, use with caution. Since it is a macro, you have the full source code available to investigate and see what it's actually doing. If you find any bugs or make any useful changes, please let me know and I'll update the macro.
