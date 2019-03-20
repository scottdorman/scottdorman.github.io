---
layout: post
title: Search Driven Development
date: '2007-05-20 15:05:35 -05:00'
---

A few months ago, [Phil Haack](http://haacked.com) wrote about a phenomena being referred to as [Search Driven Development](http://haacked.com/archive/2007/03/16/increase-productivity-with-search-driven-development.aspx) (SDD). If you don't know what Search Driven Development is, there is a great [article](http://www.linuxworld.com/news/2007/012907-search.html) on LinuxWorld by Ken Krugler and John D. Mitchell. According to them article

> About 25% of a developer's time is spend [sic] searching for information. It's well spent, though -- finding reusable code can get a project done on time and with high quality results.

I don't know about you, but (like Phil) I find that [Google](http://google.com/) and [Google Groups](http://groups.google.com/) are major productivity enhancers. I also find that [The Code Project](http://www.codeproject.com/) and developer blogs are also productivity enhancers. I have a feeling that the majority of developers would agree.

With the amount of new technologies being released lately (especially from Microsoft: .NET 3.0 (WPF, WCF, WF, CardSpaces), Silverlight, .NET 3.5 "Orcas", and Vista just to name a few) it is hard, if not impossible, to keep up. Trying to learn everything up front is not realistically feasible anymore, so it's time to find an alternative.

Many developers live and die by the IntelliSense feature found in Visual Studio. Asked to write some code at a whiteboard, many don't know how to start or what functions are available on the String class. We start coding and rely on the IntelliSense to let us know what functions are available, to catch our syntax errors, and help us refactor our code. But what happens when we start coding and run into a problems? We turn to Google or Code Project, or your own favorite site, and start searching for an answer or similar work that we can use to glean ideas from.

That's great, but what happens when your writing a function and you get that "nagging feeling" that someone, somewhere must have solved this very same problem before. (Or even better, you don't get that nagging feeling and end up completely [reinventing the wheel](http://en.wikipedia.org/wiki/Reinvent_the_wheel).) Again, you turn to Google or Code Project and start searching. At this point, maybe you even start looking at one of the code indexing sites like [Koders.com](http://www.koders.com/) or [Krugle.com](http://krugle.com/). 

Visual Studio 2005 already provides a lot of developer productivity enhancements such as Line Revision Marks, Code Snippets, improved IntelliSense, source browsing, and the Resolve context menu. However, wouldn't it be great if the search power of a code indexing site was integrated as well? This would allow you to write the name of the function and easily see if there are matches (or related functions) available to help prevent you from reinventing the wheel.

![Search Box](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image%7B0%7D%5B18%5D.png)

It turns out that [Koders.com](http://www.koders.com/) have done just that. They provide two free IDE plugins available, one for Eclipse and one for Visual Studio.NET, on their website in the [downloads section](http://www.koders.com/info.aspx?c=tools). 

The Koders.com IDE plugin enables you to perform searches directly within Visual Studio. The search panel is displayed as a toolbar component, you can search directly from the code editor by right clicking on a term, and the plugin is localized for additional languages. The plugin also provides a technology called SmartSearch&trade; and is a good application of context based searching. There is some room for improvement, but I think as the Search Driven Development phenomena really starts to pick up momentum they will improve. SmartSearch&trade; finds and recommends existing source code in real-time and runs transparently in the background as you work.

![Screenshot of Koders SmartSearch&trade; in action.](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image%7B0%7D%5B13%5D.png)

Here is an example of the SmartSearch&trade; technology in action. (A short animation is also available on the downloads page. If you missed it the first time around click the "View Again" button. A longer demonstration, with audio is also [available](http://www.koders.com/demo/plugins/PluginSmartSearch2.htm).)

Just after typing the method name, the SmartSearch&trade; results display and tells you that there are 1673 methods indexed by Koders.com that have the name "GetHttpResponse". By clicking the link, you can see the search results and simply copy and past the appropriate implementation into your code.

It will be interesting to watch the development of Search Driven Development and these plugins. I have a feeling that they will become a very integral part of our everyday development experience.
