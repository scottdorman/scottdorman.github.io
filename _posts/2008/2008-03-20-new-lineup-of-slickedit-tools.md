---
layout: post
title: New Lineup of SlickEdit Tools
date: '2008-03-20 16:18:18 -05:00'
---

I have talked about the SlickEdit Tools and Gadgets in the past ([here]({% post_url /2007/2007-02-18-slickedit-gadgets %}) and [here]({% post_url /2007/2007-08-15-SlickEdit-Gadgets-for-Visual-Studio-2008 %})) and have always been impressed with both of them. Previously, the SlickEdit Tools were only available for Visual Studio 2005. Now that Visual Studio 2008 is here, SlickEdit has released an update that works with both VS2005 and VS2008.

The catch here is that this is much more than a simple update. The major difference is that the tools have been organized into two products: the [Editing Toolbox](http://www.slickedit.com/index.php?option=com_content&task=view&id=486&Itemid=57) ([datasheet](http://www.slickedit.com/images/stories/products/SlickEditTools/editingtoolbox3172008.pdf)), which contains all of the same tools available in version 1.0, and the [Versioning Toolbox](http://www.slickedit.com/index.php?option=com_content&task=view&id=488&Itemid=57) ([datasheet](http://www.slickedit.com/images/stories/products/SlickEditTools/versioningtoolbox3172008.pdf)).

The Editing Toolbox provides a very useful collection of utilities that add convenience to your daily programming tasks by:

*   **Aliases and Acronyms** Use directory aliases to save keystrokes and mouse usage when opening files. Use acronym expansion to save keystrokes when typing class, namespace, or function names in your code. 
*   **Auto Code Doc Viewer** Extract header comments into MSDN-like documentation, fully linked HTML help that can be browsed in Visual Studio as a tool window and exported for sharing with others. 
*   **Code Annotations**  Insert comments and notes about code without actually modifying the source file.
*   **Comment Wrapping** Enable automatic wrapping of any type of multi-line comment as you type. You can also reflow existing comments in the current file.
*   **Icon Extractor** Simplify the task of finding quality icons and applying them to your applications. 
*   **Quick Profiling** Fine-tune your profiling to get information about a specific section of code. This feature allows you to time many cases that are not possible with standard profilers, such as timing complex loops, recursive functions, and the time between an object's creation and disposal.
*   **Regex Evaluator** Interactively create and test regular expressions, which are used to express text patterns for searching. 
*   **Code Navigation** Use keyboard shortcuts to jump from a symbol to its definition and to list all references for the current symbol. 
*   **Word Completion** Use commands to search for and insert additional text from a matching string.  

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image_5.png) The Code Annotations feature is new in version 2.0 and is a great feature for collaboration and code reviews. It allows you to store annotations marked as "Bug", "Comment", and "Task". These annotations don't actually change the source file, they are stored in an external file. Annotations can be scoped as personal, project, or workspace.

The really nice thing about the Code Annotations window is that, unlike the Visual Studio Task List, the annotations are still displayed even when the source file is closed.

You can see all of the information about the annotation at a glance, including the full code element that is associated with that annotation.

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image_4.png) 

The Versioning Toolbox allows you to view your source control activity and help you understand when and where changes are being made and by whom. Easily understand and navigate your source code by using these powerful features: 

*   **Backup History** View, compare, and restore versions of files without having to use source control. 
*   **CVS/SVN Source Control** Use CVS and Subversion source control commands directly in the Solution Explorer. 
*   **DIFFzilla&reg;** Provides editable dynamic differencing and merging for files, directories, and source trees. 
*   **Find Version** Find the versions of one or more files that match specific criteria, such as which files were checked in by a certain user over a certain amount of time. 
*   **Line Version Info** View details about the check-in that last affected any specific line in a source file. 
*   **Version Graphs** View graphs depicting different historical aspects and trends of selected source-controlled files. 
*   **Version History** View the history of each version of a source file, including check-in comments, date, author, branches, and labels. 
*   **Visualizations** Uses color schemes to visualize the version for each line of code in the editor window. Allows you to answer the questions: ‘Who wrote this?' and ‘How old is this?' Different color schemes allow you to focus on specific users, dates, or labels. 

I think the most promising features here are the Visualization and the fact that all of these utilities work with CVS, SVN, TFS, or VSS in exactly the same way. There is only support right now for TFS if you have TFS 2005 installed, but the developers at SlickEdit are working very hard on getting TFS 2008 support worked out, which will allow you to work with either TFS 2005 or 2008. This update should be available soon.

The best part of the new SlickEdit Tools is the price. Each Toolbox is available for $49. If you aren't sure if the tools are for you, [download the free trial](http://www.slickedit.com/content/view/408/244/). Once you install them, I think you'll find that they will quickly become part of your every day development experience.
