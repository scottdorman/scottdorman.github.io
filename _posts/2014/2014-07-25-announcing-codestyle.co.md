---
layout: post
title: Announcing codestyle.co
date: 2014-07-25 12:30:00 -05:00
---

Code style and standards has been a passion of mine for a long time. I've helped a lot of different companies create and adopt code standards. One of the main problems with documenting code standards is that once the document is created, no one ever goes back and adjusts them as new languages and technologies are introduced, new guidelines are implicitly put into place, or existing guidelines are dropped. I refer to this as the "staleness problem." To help combat the staleness problem, a lot of companies opted to put their standards documents online, either publicly or behind corporate firewalls. Again, just as with paper documents, the staleness problem would still occur. To make matters worse, for those documents that were put online publicly, no mechanism was provided for the larger community to provide feedback. 

Another problem that I see, particularly for polyglot programmers, is that there isn't a centralized place to go to find standards for multiple programming languages. Sure, there are publicly available standards for a lot of languages, but they are all individual silos of information.

> To address these problems (and several others), I created [codestyle.co](http://codestyle.co/).

What's different about [codestyle.co](http://codestyle.co/) is that all of the standards are maintained in the [codestyle.co GitHub repository](https://github.com/scottdorman/codestyle.co) and the code examples are maintained as a [GitHub gist](https://gist.github.com/scottdorman/6b4564565a9a110fdb7f). This means anyone who wants to contribute only needs to follow these three simple steps:

1.  Fork the repository or gist (or both).
2.  Make their changes.
3.  Submit a pull request.  

Anytime a change is checked in to the repository, a continuous integration build is triggered which uploads the content to the website. This allows me to maintain the content separately from the website and also means that I don't have to republish the entire site just to make content changes.

Since all of the content is maintained in GitHub, the GitHub issue tracker is also available. If you see a bug in the website itself (which isn't open sourced), or if you want to contribute but aren't comfortable forking repositories and submitting pull requests, simply [open an issue](https://github.com/scottdorman/codestyle.co/issues/new).

I'm hoping that by making the standards documents available as open source, the community at large will help maintain them by fixing mistakes, keeping guidelines current, or even adding new languages. In fact, I'm counting on the community stepping up to help maintain the standards and make [codestyle.co](http://codestyle.co/) the best place on the web to find code standards for any language.

Right now, there are standards available for .NET, HTML, and CSS. A general purpose language-agnostic standard is also available. I'll be adding more languages and more guidelines over time, but I think what's there now is a good start.
