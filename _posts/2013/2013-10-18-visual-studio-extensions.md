---
layout: post
title: Visual Studio Extensions
date: 2013-10-18 14:22:52 -05:00
---

As a product, Visual Studio has been around for a long time. In fact, it’s been 18 years since the first Visual Studio product was launched. In that time, there have been some major changes but perhaps the most important (or at least influential) changes for the course of the product have been in the last few years. While we can argue over what was and wasn’t an important change or what has and hasn’t changed, I want to talk about what I think is the single most important change Microsoft has made to Visual Studio. Specifically, I’m referring to the Visual Studio Gallery (first introduced in Visual Studio 2010) and the ability for third-parties to *easily* write extensions which can add new functionality to Visual Studio or even change existing functionality.

I know Visual Studio had this ability before the Gallery existed, but it was expensive (both from a financial and development resource) perspective for a company or individual to write such an extension. The Visual Studio Gallery changed all of that. As of today, there are over 4000 items in the Gallery. Microsoft itself has over 100 items in the Gallery and more are added all of the time. 

Why is this such an important feature? Simply put, it allows third-parties (companies such as JetBrains, Telerik, Red Gate, Devart, and DevExpress, just to name a few) to provide enhanced developer productivity experiences directly within the product by providing new functionality or changing existing functionality. However, there is an even more important function that it serves. It also allows Microsoft to do the same. By providing extensions which add new functionality or change existing functionality, Microsoft is not only able to rapidly innovate on new features and changes but to also get those changes into the hands of developers world-wide for feedback. The end result is that these extensions become very robust and often end up becoming part of a later product release.

An excellent example of this is the new CodeLens feature of Visual Studio 2013. This is, perhaps, the single most important developer productivity enhancement released in the last decade and already has huge potential. As you can see, out of the box CodeLens supports showing you information about references, unit tests and TFS history.

![CodeLens indicators in the code editor](http://i.msdn.microsoft.com/dynimg/IC686558.png "CodeLens indicators in the code editor")  

Fortunately, CodeLens is also accessible to Visual Studio extensions, and Microsoft DevLabs has already written such an extension to show code “health.” This extension shows different code metrics to help make sure your code is maintainable.

![](http://i1.visualstudiogallery.msdn.s-msft.com/f85a7ab9-b4c2-436c-a6e5-0f06e0bac16d/image/file/112412/1/codelens.jpg)

At this point, you may have already asked yourself, “With over 4000 extensions, how do I find ones that are good?” That’s a really good question. Fortunately, the Visual Studio Gallery has a ratings system in place, which definitely helps but that’s still a lot of extensions to look through. To that end, here is my personal list of favorite extensions. This is something I started back when Visual Studio 2010 was first released, but so much has changed since then that I thought it would be good to provide an updated list for Visual Studio 2013.

These are extensions that I have installed and use on a regular basis as a developer that I find indispensible. This list is in no particular order.

*   [NuGet Package Manager for Visual Studio 2013](http://visualstudiogallery.msdn.microsoft.com/4ec1526c-4a8c-4a84-b702-b21a8f5293ca "NuGet Package Manager for Visual Studio 2013")
*   [Microsoft CodeLens Code Health Indicator](http://visualstudiogallery.msdn.microsoft.com/f85a7ab9-b4c2-436c-a6e5-0f06e0bac16d "Microsoft CodeLens Code Health Indicator")
*   [Visual Studio Spell Checker](http://visualstudiogallery.msdn.microsoft.com/a23de100-31a1-405c-b4b7-d6be40c3dfff "Visual Studio Spell Checker")
*   [Indent Guides](http://visualstudiogallery.msdn.microsoft.com/e792686d-542b-474a-8c55-630980e72c30 "Indent Guides")
*   [Web Essentials 2013](http://visualstudiogallery.msdn.microsoft.com/56633663-6799-41d7-9df7-0f2a504ca361 "Web Essentials 2013")
*   [VSCommands for Visual Studio 2013](http://visualstudiogallery.msdn.microsoft.com/c6d1c265-7007-405c-a68b-5606af238ece "VSCommands for Visual Studio 2013")
*   Productivity Power Tools (right now this is only for Visual Studio 2012, but it should be updated to support Visual Studio 2013.)  

Everyone has their own set of favorites, so mine is probably not going to match yours. If there is an extension that you really like, feel free to leave me a comment! 
