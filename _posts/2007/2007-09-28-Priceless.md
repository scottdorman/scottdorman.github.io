---
layout: post
title: Priceless
date: 2007-09-28 15:15:13 -05:00
---

I was pulled in to a side conversation today about comments and it reminded me of something I blogged about on my personal blog (don't bother going to it as the last entry was February of this year and it isn't really maintained) about some comments I ran across in one of the projects I used to manage. After re-reading the post, I thought it was worthy of moving to this blog (which is probably where it should have been in the first place).

So, without further ado...here is the original post (with some minor formatting cleanup so it looks consistent with the rest of this blog):

* * *

In the process of cleaning up some of the source code for one of the projects I manage, I came across the following comments: 

 <div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 400px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 195px; background-color: #f4f4f4">

```
<span style="color: #008000">/*</span>
<span style="color: #008000">    MAB 08-05-2004: Who wrote this routine? When did they do it? Who should I</span>
<span style="color: #008000">    call if I have questions about it? It's worth it to have a good header here.</span>
<span style="color: #008000">    It should helps to set context, it should identify the author (hero or </span>
<span style="color: #008000">    culprit!), including contact information, so that anyone who has questions can</span>
<span style="color: #008000">    call or email. It's useful to have the date noted, and a brief statement of</span>
<span style="color: #008000">    intention. On the other hand, this isn't meant to be busy work; it's meant to</span>
<span style="color: #008000">    make maintenance easier--so don't go overboard.</span>
<span style="color: #008000"></span>
<span style="color: #008000">    One other good reason to put your name on it: take credit! This is your craft</span>
<span style="color: #008000">*/</span>
```
</div>


and then a little further down:


<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 600px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">

```
#include <span style="color: #006080">"xxxMsg.h"</span> <span style="color: #008000">// xxx messages</span>
<span style="color: #008000">/*</span>
<span style="color: #008000">    MAB 08-05-2004: With respect to the comment above, I gathered that</span>
<span style="color: #008000">    from the filename. I think I need either more or less here. For one</span>
<span style="color: #008000">    thing, xxxMsg.h is automatically generated from the .mc file. That might</span>
<span style="color: #008000">    be interesting information. Another thing is that xxxMsg.h should NOT be</span>
<span style="color: #008000">    added to source control, because it's auto-generated. Alternatively, don't</span>
<span style="color: #008000">    bother with a comment at all.</span>
<span style="color: #008000">*/</span>
```
</div>


and then yet again:


<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 400px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 89px; background-color: #f4f4f4">

```
<span style="color: #008000">/*</span>
<span style="color: #008000">    MAB 08-05-2004: Defining a keyword?? This seems problemmatic [sic],</span>
<span style="color: #008000">    in principle if not in practice. Is this a common idiom? </span>
<span style="color: #008000">*/</span>
```
</div>


So, what does this tell us? Well, for starters it sounds like MAB wasn't very happy about having to work on this particular file and was doing some serious ranting. I can rant about things as well, such as the benefit of good, pertinent code comments. I've maintained enough code (both someone else's code and my own) that I understand the value of good comments.

However, to paraphrase "[Mary Poppins](http://www.imdb.com/title/tt0058331/)"...

> I've always said that there is nothing like a good *comment*. And that was nothing like a good *comment*.
> - Bert and Uncle Albert "Mary Poppins"

Honestly, those comments weren't any better than not having them there in the first place. While the points made by MAB are, for the most part, valid there are much better ways to make them.

One good reason to not put your name on it: Your bad comments living on for posterity.

> No comments at all: 0 minutes
> Ranting about the lack of comments: 10 minutes
> Laughing at the rants years later: priceless
