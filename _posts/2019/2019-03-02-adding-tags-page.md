---
layout: post
title: Adding a tags page
date: '2019-03-02 21:35:00 -05:00'
---

I've wanted to add a [tags]({% link tags.html %}) page to the blog. However, all of the solutions I'd found required running a plugin or doing a lot of manual work that resulted in an off-line generated site being checked in to GitHub.

Since this blog runs under GitHub Pages a pugin-based solution wasn't an option. The manual options required more work than I was willing to do and would also mean giving up the ability to publish a new blog post, or update an existing one, by just checking in a commit.

The other day, however, I stumbled upon a [solution](http://codinfox.github.io/dev/2015/03/06/use-tags-and-categories-in-your-jekyll-based-github-pages/) that doesn't use plugins and doesn't require generating the site off-line. 

Since some, but not all, of my posts already had tags, I simply created a tags.html page which looked very similar to this:

{% raw %}
```html
---
layout: page
title: Tags
---

<div class="archives">
    <ul class="nav nav-pills">
        {% for tag in site.tags %}
        <li role="presentation"><a href="#{{ tag[0] | slugify }}" class="post-tag">{{ tag[0] }}</a></li>
        {% endfor %}
    </ul>
    <hr />
    {% for tag in site.tags %}
    <fieldset>
        <legend id="{{ tag[0] | slugify }}">{{ tag[0] }}</legend>
        <ul>
            {% for post in tag[1] %}
            <li>
                <span class="title"><a href="{{ post.url }}">{{post.title}}</a></span>
            </li>
            {% endfor %}
        </ul>
    </fieldset>
    {% endfor %}
</div>
```
{% endraw %}

This page reads the tags from all of my posts, creates a tag list at the top of the page and then a fieldset for each tag which lists the relevant posts.

I did do some additional work to style the page so it fit in with the rest of the blog and to make the tags list that appears in the post and in the index lists (for the home and archive pages) linkable. This was done in my tags.html include file, which looks like

{% raw %}
```html
{% if page.tags.size > 0 or post.tags.size > 0 %}
<ul class="list-inline">
    <li>
        <span class="mdl2 mdl2-tag"></span>
        {% for tag in page.tags %}
        <a href="{% link tags.html %}#{{ tag | slugify }}">{{ tag }}</a>
        {% endfor %}
        {% for tag in post.tags %}
        <a href="{% link tags.html %}#{{ tag | slugify }}">{{ tag }}</a>
        {% endfor %}
    </li>
</ul>
{% endif %}
```
{% endraw %}

This solution works equally well for categories. In fact, the only thing you have to change your categories.html page is to use `site.categories` instead of `site.tags`. If you then want to list all of the categories, simply use `page.categories` or `post.categories`.