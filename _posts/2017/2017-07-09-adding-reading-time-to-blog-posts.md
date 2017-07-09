---
layout: post
title: Adding reading time to blog posts
date: '2017-07-09 12:30:00 -05:00'
---

One of the nicer usability features many content-heavy sites have started implementing is showing the estimated reading time for an article (or blog post) and it was something that I wanted to add to my own blog. The issue for me is that I host my blog using GitHub Pages and allow the standard Jekyll commit-build-publish sequence that's built-in with GitHub Pages to actually publish my blog. That allows me to write a blog post anywhere, including using the GitHub web interface and add a new blog post. The downside is that GitHub pages only allows a whitelisted set of plugins. After some searching, I came across [this post](https://carlosbecker.com/posts/jekyll-reading-time-without-plugins/), which gave me a great starting point for what I wanted to do without needing to use a plugin.

The first thing I needed to do was add a new include file. I added a new file in the `_includes\post` folder named [`reading_time.html`](https://github.com/scottdorman/scottdorman.github.io/blob/master/_includes/post/reading_time.html).

This file should be fairly straight-forward. The first thing it does is get the number of words from the content passed in to the include (in `include.text`) and then uses that number to determine the approximate number of minutes it will take to read the post.

In the header area of my post, in [`meta.html`](https://github.com/scottdorman/scottdorman.github.io/blob/master/_includes/post/meta.html), I included this file and passes the post content to the include in the `text` parameter using the following 

```liquid
{% include post/reading_time.html text=content %}
```

To include the same reading time estimation in the index required a slightly different include, otherwise it would use the content of the actual index page rather than the content of the post. That include, which is in [`meta_index.html`](https://github.com/scottdorman/scottdorman.github.io/blob/master/_includes/post/meta_index.html), is 

```liquid
{% include post/reading_time.html text=post.content %}
```

Now, my blog posts show estimated reading time.
