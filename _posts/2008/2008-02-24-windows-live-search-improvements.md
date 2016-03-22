---
layout: post
title: Windows Live Search Improvements
date: 2008-02-24 19:46:00 -05:00
---

Last week, some improvements to Windows Live Search were [announced](http://blogs.msdn.com/webmaster/default.aspx) which will improve the efficiency of how Live Search crawls and indexes a web site. The main improvements are:

*   

**HTTP Compression**, which allows faster transmission time by compressing static files and application responses, reducing network load between the web server and the Live Search crawler.

*   

**Conditional Get**, as defined by RFC 2616 (Section 14.25). What this means is that generally a page will not be downloaded unless it has changed since the last crawl.

There are some other improvements as well, which also caused the user agent to change. The new user agent is "msnbot/1.1".

While these improvements are important and definitely needed, the frequency of searches needs to be improved dramatically. The last time I checked there was a pretty good lag time (days to weeks) between the time I posted a new blog entry and the time the Live Search crawlers picked it up. On the contrary, the Google crawlers would pick up that same entry in the matter of a few hours.

I think until the frequency of crawls is improved to match or pass that of Google, Live Search isn't going to be a strong competitor. People using search sites expect the content to not only be relevant to their search terms but to also contain up-to-date results. Right now Google does a much better job at this than Live Search, although the Live Search interface is much easier to use.
