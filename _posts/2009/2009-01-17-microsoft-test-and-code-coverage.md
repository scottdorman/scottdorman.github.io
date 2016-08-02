---
layout: post
title: Microsoft Test and Code Coverage
date: 2009-01-17 12:30:21 -05:00
---

I have been writing a lot of unit tests lately using Microsoft Test. This included converting a bunch of old NUnit tests to the MS Test format, which was relatively painless. While examining the code coverage results (after all, what good are unit tests if you don't know what portions of the code are being tested and not tested), I have noticed that the results sometimes lie.

For example, I have a class that contains some extension methods for manipulating enums. One of those methods takes an enum and coverts it to an IList of KeyValuePairs containing the enum value and a description.

![image](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image_4.png) 

As you can see by the highlighted row in the code coverage results window, the `ToList()` method is only covered at 90.91% and there are 2 blocks that aren't covered. At first glance, this looked reasonable so I reviewed the actual `ToList()` method with code coverage highlighting turned on.

![image](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image_6.png) 

What's wrong with this picture? I'm using the default code coverage highlighting colors, so the light blue coloring indicates 100% coverage. Knowing that, I'm seeing a method that is colored as being 100% covered yet the coverage results are showing it as a different number.

This stays consistent no matter how many times I re-run the tests and I have also seen it on other methods in other classes.
