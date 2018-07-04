---
layout: post
title: Comments using GitHub
date: '2018-07-03 19:41:00 -05:00'
---

When I moved my blog to GitHub, [way back in 2016]({% post_url /2016/2016-03-23-moving-to-github-pages %}), I also moved the commenting system to Disqus. At the time, it seemed like the best option for me.

As of earlier today however, I have dropped support for Disqus in favor of using GitHub issues as the underlying data store. This is the route [Microsoft is currently taking in Microsoft Docs](https://docs.microsoft.com/en-us/teamblog/a-new-feedback-system-is-coming-to-docs) and there is an open source implementation that served as the proof of concept for Microsoft's approach at https://utteranc.es/. With the new system, you can now create GitHub issues directly from a content page, which enables you to interact in a much richer way. 

The first time you sign in, you'll be asked to authorize utterances. ![Authorize](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/2018-07-03 19_44_25-Authorize utterances.png) This is a one-time authorization and it's what allows you to enter comments directly from the blog post.

Apart from some `config.yml` changes and replacing the Disqus code with the code generated from utterances, it was relatively easy to implement by following the few simple steps on the utterances homepage. 

Right now, unfortunately, there isn't a way to automatically migrate Disqus comments to GitHub issues. (At least, none that I know of. If you happen to know a way to do this, please let me know.)

Just like in Disqus, you have to be logged in to leave a comment, except this time you just log in to your GitHub account.
