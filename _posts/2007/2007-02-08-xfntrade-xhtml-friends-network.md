---
layout: post
title: XFN&trade; (XHTML Friends Network)
date: 2007-02-08 23:01:00 -05:00
---

I was recently introduced to the concept of [XFN](http://gmpg.org/xfn/) through a blog post I was reading from [Phil Haack](http://haacked.com/) regarding his meeting with Rob Conery, one of the [Subsonic](http://www.codeplex.com/Wiki/View.aspx?ProjectName=actionpack) developers.

After reading about XFN, I think it is an extremely interest concept on the entire social networking phenomenon. Take![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/o_sshot-1.png)n  from the XFN website:

> <abbr>XFN</abbr> puts a human face on linking. As more people have come online and begun to form social networks, services such as [Technorati](http://www.technorati.com/) and [Feedster](http://www.feedster.com/) have arisen in an attempt to show how the various nodes are connected. Such services are useful for discovering the mechanical connections between nodes, but they do not uncover the *human* relationships between the people responsible for the nodes.
> 
> XFN outlines the relationships between individuals by defining a small set of values that describe personal relationships. In HTML and XHTML documents, these are given as values for the `rel` attribute on a hyperlink. XFN allows authors to indicate which of the weblogs they read belong to friends, whom they've physically met, and other personal relationships. Using XFN values, which can be listed in any order, people can humanize their blogrolls and links pages, both of which have become a common feature of weblogs.

As I am a a fan of [Windows Live Writer,]({% post_url /2006/2006-08-24-windows-live-writer %}) I decided to write a plugin that allows me to insert XFN aware links. After spending way too much time on it for one night, I have it finished. Here is a  screenshot of the insert dialog.  

As you can see, it is patterned after the normal Windows Live Writer Insert Hyperlink dialog, but adds a section for the different XFN Relationships that are possible.  

This implementation follows the [XFN 1.1 Creator](http://gmpg.org/xfn/creator) rules. You can get the [full details](http://gmpg.org/xfn/background) of what the different categories mean at the XFN website, however there are tooltips available that provide a brief description.  

I have submitted the plugin to [Windows Live Gallery](http://gallery.live.com/) late last night (actually very early this morning) and am waiting for approval. As soon as it is approved, it will be available in the [Writer](http://gallery.live.com/default.aspx?l=8) subsection and should be called the "XFN plugin for Windows Live Writer". This is the first time I've submitted something to Windows Live Gallery, so I don't know how long the process takes to get an entry approved.
