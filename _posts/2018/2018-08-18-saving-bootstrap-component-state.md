---
layout: post
title: Saving Bootstrap component state
date: '2018-08-18 13:22:00 -05:00'
---

Bootstrap is a great front-end UI framework for web development and has a lot of great components. One of those components is the [collapse component](https://getbootstrap.com/docs/4.1/components/collapse/). This allows you to easily toggle the visibility of content on your site. It also allows you to make really great [accordion](https://getbootstrap.com/docs/4.1/components/collapse/#accordion-example) style content.

One of the issues with the accordion is that when you navigate to another page and then come back, you're back to the default open panel of the accordion. Sometimes that isn't an issue, but there are times when you want to remember the current state of the accordion and return the user to the same open panel they were on before the page navigation.

A similar issue exists with the [tab control (v3.x)](https://getbootstrap.com/docs/3.3/javascript/#tabs) or the [nav component (v4.x)](https://getbootstrap.com/docs/4.1/components/navs/).

You can easily solve these problems with a small amount of Javascript.

<script src="https://gist.github.com/scottdorman/dbe9cb3494e21dd880cf155a89b24622#file-bootstraphelpers-js"></script>

This uses the [HTML5 web storage feature](https://www.tutorialrepublic.com/html-tutorial/html5-web-storage.php), specifically the `localstorage`, but you can change this to use whatever storage mechanism you want.

Using these functions is just as simple:

<script src="https://gist.github.com/scottdorman/dbe9cb3494e21dd880cf155a89b24622#file-example-html"></script>