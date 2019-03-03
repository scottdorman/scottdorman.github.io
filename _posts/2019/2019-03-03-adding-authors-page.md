---
layout: post
title: Adding authors page
date: '2019-03-03 10:35:00 -05:00'
---

Many blogs, especially business blogs, have multiple authors or have occasional guest authors. In those cases, it's always a good idea to include a small author bio on their blog post and even give your readers a way to find other posts written by that author.

Just like the possible solutions for [adding a tags page]({% post_url /2019/2019-03-02-adding-tags-page %}), almost all of the solutions involve running a plugin or doing a lot of manual work that resulted in an off-line generated site being checked in to GitHub.

If your blog runs under GitHub Pages a pugin-based solution isn't an option. The manual options require a lot of work to maintain and would also mean giving up the ability to publish a new blog post, or update an existing one, by just checking in a commit.

There is a way that doesn't use plugins and doesn't require generating the site off-line, based on the way I added a tags page.

The first step is to create an `authors.yml` file in a `_data` folder. 

> The `_data` folder is where you can store additional data for Jekyll to use when generating your site. These files must be YAML, JSON, or CSV files (using either the `.yml`, `.yaml`, `.json` or `.csv` extension), and they will be accessible via `site.data`.

This file contains all of your author information, such as their name, twitter, and bio. It can really contain any information about your authors that you want to capture and possibly display.

An example `authors.yml` file might look like this:

```yml
scott-dorman:
    name: Scott Dorman
    twitter: http://twitter.com/sdorman
    github: https://github.com/scottdorman
    bio: Scott is a Microsoft C# MVP, author, speaker, blogger, developer, and entrepreneur.
    image: http://www.gravatar.com/avatar/e74e26bfd345fdd80bedf436178c5829?s=80
john-smith:
    name: John Smith
    bio: John is a developer.
```

Next, you need to include the author in the front matter for each of their posts by adding an `author: <key>` line, so for my posts it would be `author: scott-dorman`.

> If you have a default author, you can add that default into your `_config.yml` file by adding
>```yml
>defaults:
>  -
>    scope:
>      path: ""
>      type: "posts"
>    values:
>      author: scott-dorman
>```
> That will prevent you from always needing to include the author.

Next, you'll need to create an include for the author bio information that will be included in the blog post. This file should go in your `_includes` folder. An example file might look like

{% raw %}
```html
<!-- Look the author details up from the site config. -->
{% assign author = site.data.authors[page.author] %}

{% if author.bio %}
<div class="well well-sm">
    <h1>About <a href="{% link authors.html %}#{{ page.author }}" target="_blank">{{ author.name }}</a>{{author.name}}</h1>
    {% if author.image %}
    <img src="{{author.image}}" class="img-circle pull-left m-a-1">
    {% endif %}
    <p>{{ author.bio }}</p>
    <ul class="list-inline social">
        {% if author.github %}
        <li><a href="{{author.github}}" title="GitHub"><i class="fa fa-github fa-1x"></i></a></li>
        {% endif %}
        {% if author.twitter %}
        <li><a href="{{author.twitter}}" title="Twitter"><i class="fa fa-twitter fa-1x"></i></a></li>
        {% endif %}
      </ul>
</div>
{% endif %}

```
{% endraw %}

Next, make sure to include this file into your layout used for blog posts by adding {% raw %}`{% include author_bio.html %}`{% endraw %} where you want your author bio information to appear.

Finally, create an `authors.html` page that looks like

{% raw %}
```html
---
layout: page
title: Authors
banner: true
---

<div class="archives">
    <ul class="nav nav-pills">
        {% for author in site.data.authors %}
        <li role="presentation"><a href="#{{ author[0] | slugify }}" class="post-tag">{{ author[1].name }}</a></li>
        {% endfor %}
    </ul>
    <hr />
    {% for author in site.data.authors %}
    <fieldset>
        <legend id="{{ author[0] | slugify }}">{{ author[1].name }}</legend>

        {% assign author_posts = site.posts | where: "author", author[0] %}
        <ul>
            {% for post in author_posts %}
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

This page reads the authors from the `site.data.authors` collection, creates a navigation list at the top of the page and then a fieldset for each author which lists their posts.

