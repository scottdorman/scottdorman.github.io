---
layout: post
title: Document Map Margin in Visual Studio
date: 2008-08-30 10:51:12 -05:00
---

Earlier this month [Charlie Calvert](http://blogs.msdn.com/charlie/default.aspx) introduced a potential new feature called [Document Map Margins](http://code.msdn.microsoft.com/vslangfutures/Wiki/View.aspx?title=Document%20Map%20Margin&referringTitle=Home) (DMM). The idea behind DMM is to make it easier for you to find and track important features in your code by visualizing the entire file. Overall I like the idea of DMM as it can really provide you with good contextual information, particularly for really large files.

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/DocumentMap_3_3.png) 

While DMM isn't here now, a very similar tool is. I came across this tool mentioned by [ScottHa](http://www.hanselman.com/blog/) in this [post](http://www.hanselman.com/blog/IntroducingRockScroll.aspx). What RockScroll does is to extend the Visual Studio scroll bar to show a thumbnail view of your code. 

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/RockScroll_5_2.png) 

One thing worth noting is that if you have collapsed code sections, RockScroll gets a bit confused and doesn't accurately reflect your position in the code. It also only works with source code files, not aspx files.
