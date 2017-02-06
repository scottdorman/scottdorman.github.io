---
layout: post
title: SlickEdit Gadgets
date: '2007-02-18 18:04:00 -05:00'
---

Since I've been looking into writing a custom Visual Studio package, I came across a nice set of free "[gadgets](http://www.slickedit.com/content/view/441)" from SlickEdit. These can only be described as a set of very cool power toys for Visual Studio. These gadgets will only work with Visual Studio 2005, but should work with any of the Visual Studio 2005 editions except the Express Editions.

I think these gadgets are aimed at creating more business for the [Tools v1.1 for Microsoft Visual Studio 2005](http://www.slickedit.com/content/view/385/234/) product, which also has some very nice features and is currently priced at $99.00.

The SlickEdit Gadgets include 5 gadgets, but I think only a few are useful for the everyday programmer. 

*   Editor Gadgets  
    *   Line ruler - This places a shaded highlight across the current line and can optionally display tick marks to show the indentation levels. (The colors are customizable.)  Indentation guide - Draws a vertical dashed line in the editor indicating the indention level of the current line. (The colors are customizable.)  Auto-copy selection - Automatically copies the selected text to the clipboard and allows pasting by clicking the middle mouse button (or scroll wheel). This is very similar to XMouse and the copy/paste features found in most of the Unix code editors for years. 

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/o_sshot-3.png) 

*   File Explorer - Provides an easy way to open solutions, projects, or single files in Visual Studio. It also makes it easy to drag-and-drop files into an open Visual Studio project. 

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/o_file_x.jpg) 

*   The SLOC Report - This provides an easy way to count lines of code. The count is divided into code, comments, and whitespace and shown as a pie chart. Reports can be generated for solutions, projects, or individual files. 

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/o_sloc.jpg) 

The SlickEdit Tools for Visual Studio product also only integrates with Visual Studio 2005 except the Express Editions. You can download a 15 day trial version, but you do have to fill out a registration form to get your trial key. The following features (taken directly from SlickEdit's product page) are provided:

> **Comment Wrapping** Comment Wrapping enhances the code editor by formatting comments as you type. Wrapping works with any type of multi-line comment: line comments, block comments, and XMLdoc and Javadoc comments. Additionally, existing comments can be "reflowed" to reformat them.
> 
> **Backup History** Backup History creates local versions of files each time a file is saved, providing a convenient way to access previous versions of a file even if it has not been checked into source control. Backup History does not replace source control; it bridges the gap between check-ins, providing a greater safety net for your coding.
> 
> **Auto Code Doc Viewer** The Auto Code Doc Viewer automatically turns your comments into MSDN-like documentation. The tool creates fully linked HTML help that can be browsed in a Visual Studio tool window. All help pages provide a link to jump directly to the referenced source code, so it's easy to get from a help page to the actual source code.
> 
> **Aliases and Acronyms** SlickEdit Tools now provides directory aliases and has enhanced the Microsoft&reg; Intellisense&reg; feature with acronym expansion. Directory aliases are short identifiers for long directory names, which save a lot of typing and mouse use when opening files. Acronyms work similarly but represent class, namespace, and function names in your code.
> 
> **Regex Evaluator** Regex Evaluator provides the ability to interactively create, save, and re-use tests of regular expressions. Regular expressions may be run in the test window or may be applied directly against the active document.
> 
> **Icon Extractor** The Icon Extractor has the ability to search Windows executables and DLLs (both managed and unmanaged) for embedded icons and images. These icons and images are presented in a list and can be applied to WinForm designer components with simple drag-and-drop operations.
> 
> **DIFFzilla&reg;** DIFFzilla enables you to compare files or directories and view the differences. Documents in the Diff window can be easily edited in place, updating the comparison as you type. DIFFzilla offers customizable options related to file comparison, integration with Backup History, and Source Control integration for Source Safe 2005 and CVS.
> 
> **Quick Profiling** Quick Profiling provides an extremely precise way to profile your code without profiling the whole thing. It provides a way to time many cases that are extremely difficult to analyze with standard profilers. Additionally, the results of several runs may be graphed and compared to view the results of code changes and determine the effect of those changes.
> 
> **Word Completions** Word Completions enhances existing visual studio completions by completing words elsewhere in the current document, even in comments.
> 
> **Code Navigation** Code navigation provides rapid navigation from a symbol to a definition or from a symbol to a reference allowing you to navigate your code the way you think about it.
> 
> **Quick Launch** Quick Launch provides the capability to open the active document or Visual Studio solution in the SlickEdit application. This provides a quick convenient way to start the standalone SlickEdit editor from Visual Studio to work with the current file or solution. * Requires SlickEdit v10.0.2 or higher

While some of these features are available in competing products, like [CodeRush with Refactor! Pro](http://www.devexpress.com/Products/NET/IDETools/CodeRush/), the price is $99.00 (normally $149) compared to $249.00 for CodeRush. I've used the CodeRush tools before and find that they are powerful but rather complicated for what they do. I want editor enhancements to be natural and easy to use, not in-your-face and cumbersome.
