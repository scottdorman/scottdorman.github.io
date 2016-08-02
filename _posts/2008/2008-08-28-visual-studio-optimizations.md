---
layout: post
title: Visual Studio Optimizations
date: 2008-08-28 15:04:32 -05:00
---

There are always a lot of posts about various add-ins, code snippets, macros, and other utilities that are designed to make you, the developer, more productive within Visual Studio as an editing environment. However, there seem to very few posts that talk about how to actually improve the performance of Visual Studio itself.

Browsing through some of the questions on [Stack Overflow](http://www.stackoverflow.com), I came across a [thread](http://beta.stackoverflow.com/questions/8440/visual-studio-optimizations) asking this very question. There were a lot of non-answers, but one that definitively listed some settings that you can change which will help speed up Visual Studio. These changes are all available from the Options dialog (Tools –> Options):

## Environment 

*   General:          
    *   Disable "Animate environment tools"        
*   Documents:          
    *   Disable "Detect when file is changed outside the environment"        
*   Keyboard:          
    *   Remove the F1 key from the Help.F1Help command        
*   Help\Online:          
    *   Set "When loading Help content" to "Try local first, then online" or "Try local only, not online"        
*   Startup:          
    *   Change the "At startup" option to "Show empty environment"

## Projects and Solutions

* General:
    * Disable "Track Active Item in Solution Explorer"

## Text Editor

* General (for each language you want):
    * Disable "Navigation bar" (this is the toolbar that shows the objects and procedures drop down lists allowing you to choose a particular object in your code.
* Disable "Track changes"

## Windows Forms Designer

* General:
    * Set "AutotoolboxPopulate" to false.
    * Set "EnableRefactoringOnRename" to false.

There is also one change that isn't part of the Options dialog. If you have any code file that can be viewed in either a visual editor (like the Windows Forms editor) or a code editor, you can change the default editor by right clicking on the file and choosing the "Open With..." menu option. Select the program you want to use to open the file and click the "Set as Default" button. For example, doing this on a CSharp file (*.cs) and choosing the "CSharp Editor" as the default causes **all** code files (even classes that inherit from a visual element like Form) to open in the code editor not the designer. Don't choose the editors that are listed as "with Encoding" as this will ask you for the encoding each time you open the file.
 