---
layout: post
title: Visual Studio and Code Analysis
date: 2008-08-19 13:04:32 -05:00
---

Even with the newest releases of [StyleCop](http://code.msdn.microsoft.com/sourceanalysis), [FxCop](http://msdn.microsoft.com/en-us/library/bb429476(VS.80).aspx), and Visual Studio 2008, there is still a lot of room for improvement in the suite of technologies and products that make up what should probably be termed “Microsoft Source Analysis”.

I know that calling StyleCop that name caused a lot of confusion since it was being compared to the built-in source analysis features of Visual Studio (at least the Team Edition SKUs of Visual Studio). I think the real heart of the problem is that Visual Studio comes integrated “out of the box” with code analysis capabilities.

Here is what has happened:

First, Microsoft releases a tool called FxCop on GotDotNet. This tool is a “static analysis tool” that looks at a compiled assembly and analyzes it for various violations of “best practice” design guidelines (mostly those spelled out in the [Framework Design Guidelines](http://amzn.to/28JOJA1). Then, Visual Studio 2005 Team Edition is released, which includes a built-in utility to perform static analysis. This built-in package uses (at a guess) 90% of the standalone FxCop release (the rules assemblies can be shared, the settings/options are almost the same, the analysis engines are almost the same as well), but includes some extra rules that weren’t part of the FxCop release and drops others that were. 

At this point we have two tools that are designed to do the exact same thing which yield different results. One is tightly integrated in to Visual Studio and the other isn’t integrated at all. To remedy this situation, FxCop 1.36 Beta is released which brings FxCop closer in-line with the integrated analysis.

Then Microsoft releases a tool called StyleCop, which performs analysis on the actual source code looking for “best practice” violations partially based on the Framework Design Guidelines but also based on some internal code standards used by various teams at Microsoft.

Looking at the Wikipedia entry for [Static Code Analysis](http://en.wikipedia.org/wiki/Code_analysis):

> **Static code analysis** is the analysis of computer [software](http://en.wikipedia.org/wiki/Software) that is performed without actually executing programs built from that software…In most cases the analysis is performed on some version of the [source code](http://en.wikipedia.org/wiki/Source_code) and in the other cases some form of the [object code](http://en.wikipedia.org/wiki/Object_code)…The sophistication of the analysis performed by tools varies from those that only consider the behavior of individual statements and declarations, to those that include the complete source code of a program in their analysis.

So we now have three tools from Microsoft (two of which are almost the same) which all perform some aspect of code analysis. These tools are released by different teams within Microsoft and provide varying levels of integration with the Visual Studio development environment. 

I think this is where Microsoft is really failing to provide a consistent experience to the developer community and failing to recognize the real need of the community when it comes to code analysis.

I think tools like FxCop and StyleCop are absolutely critical to good development practices and producing more stable and maintainable code. So, if these tools are so critical how has Microsoft failed in this regard?

There are actually several small failures, any one taken by itself is not a big issue but taken together they form a complete picture:

1. Visual Studio Integration (FxCop): It’s great that there is a version/variant of FxCop integrated with Visual Studio (at least the more expensive Team Edition SKUs). At the same time, that’s also one of the problems.        
   
   As an MVP, I present a lot of talks to the community about code style and standards. I can’t talk about the integrated code analysis since at least half of my audience generally does not have one of the Team Edition SKUs. That means they don’t have the integrated analysis, so all of the “cool features” that provides (that Microsoft heavily advertised to the developer community as a big selling point for upgrading to VS2005) aren’t available to them.         

   What they do have available is the stand-alone FxCop tool. The problem here is that it doesn’t integrate with Visual Studio (unless you want to do extra work, and even then you don’t get a good integrated experience). The other problems are:         

   *   The stand-alone FxCop still generates slightly different results than the integrated analysis. 
   *   The settings are stored in a separate .fxcop file and aren’t integrated in any way with the actual Visual Studio project file. 
   *   Running an analysis is a completely separate (and generally manual) step.    

2. Visual Studio Integration (StyleCop): Again, like the integration for FxCop, this is both good and bad. StyleCop fixes some of the failings with the FxCop integration by providing a stand-alone tool that can also integrate with Visual Studio. While the settings are stored in an external file, you can modify them through Visual Studio. You can also run an analysis through Visual Studio, although you can’t make it an automatic part of the build. The failures here are:        

    *   The integration puts the code analysis menu options under the “Tools” menu. While this doesn’t sound like a big deal, if you have one of the Team Edition SKUs, you also get an “Analyze” menu (for the built-in FxCop analysis). Intuitively one would expect the source analysis (StyleCop) menus to be under the Analyze menu (see my earlier point about the definition of code analysis).
    *   The rules documentation is not integrated with the rest of the Visual Studio documentation.
    *   There is no actual stand-alone GUI, so you either run through Visual Studio or MSBuild.   

3.  Competing rules: Even though FxCop and StyleCop have completely different reasons for existing, there is some overlap in what they analyze. That means that you can get duplicate rule violations for the same thing if you run both tools, but it also means you can get conflicting rule violations.       

   In the cases where both tools analyze for the same rule, that rule should be consistent. This goes for the actual definition of the rule as well as the documentation. The fact that these tools use different documentation styles for the rules simply adds to a feeling of inconsistent branding across these tools and within Microsoft’s developer products.
   
4.  Different “SDKs” to create custom rules: (I’m guessing here since the StyleCop SDK hasn’t been released, but I’m reasonably sure this is the case.)  Just because these are different products, with different analysis engines and different rule sets doesn’t mean that I should learn two completely different SDKs to create a code analysis rule.  

So, what can Microsoft do to correct these issues? A lot, actually…and none of it should conflict with any of Microsoft’s internal goals for the products or teams.

1.  Make FxCop and StyleCop consume at least the System.AddIn namespace, or ideally the new Managed Extensibility Framework. This allows both products to:
   *   use a consistent and common way to handle the rules assemblies and will help provide an environment where there is a single way to create a custom rule for either product
   *   use a consistent and common GUI (ideally patterned after the current FxCop GUI).    Provide consistent rules across both products. There is absolutely a need for certain rules to exist in both products and that shouldn’t be changed; what should be changed is that those rules should not contradict each other.
3.  Allow FxCop to integrate with Visual Studio the same way StyleCop integrates, but expand that integration to:
    *   allow controlling the analysis settings through the project properties (still store them in an external file so the GUI can use the same settings; or allow the GUI to read the VS project files)
    *   allow controlling the actual analysis through project settings (like the integrated FxCop analysis)
    *   put all of the menu options under a single “Analyze” menu.    **Allow both FxCop and StyleCop to integrate with *all* Visual Studio SKUs, *including* the Express Editions.**
5.  Provide consistently formatted documentation for the rules. From a developer perspective, especially with point #3, the rules should look like they came from a single product.
6.  Move the current “Code metrics analysis” features from being integrated with Visual Studio to being part of FxCop (or as a stand-alone utility, provided it follows all of the same rules listed here).
7.  Remove the current “Code analysis” features from being integrated with Visual Studio in favor of a more integrated FxCop experience.
8.  Ensure that both FxCop and StyleCop provide the same level of MSBuild integration.
9.  Allow StyleCop to work with more than just C# code. Just like FxCop, it needs to be able to analyze any .NET language (or at least the mainstream ones initially).  

These changes would provide a consistent developer experience around any type of code analysis activity that can be run as a stand-alone GUI, integrated in to Visual Studio (all SKUs), or as part of MSBuild. It also further reinforces the idea that performing code analysis is a general best practice for all developers, not just certain segments of the developer community.