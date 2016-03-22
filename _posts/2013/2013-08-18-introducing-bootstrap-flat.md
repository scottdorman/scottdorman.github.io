---
layout: post
title: Introducing Bootstrap Flat
date: 2013-08-18 22:23:15 -04:00
---

### What is Bootstrap Flat?

To put it simply, Bootstrap Flat is a custom theme on top of Bootstrap that provides a flat look to the user interface elements. That means there are no gradients, shadows, or rounded corners.

### Why?

Twitter Bootstrap is probably one of the most widely used CSS frameworks available today. It’s been very well received by the web development community and even Microsoft is embracing the framework by [including it in ASP.NET](http://www.asp.net/vnext/overview/latest/release-notes) (both for Web Forms and MVC 5). [Bootstrap](http://getbootstrap.com/) 3 is a significant change from [version 2](http://getbootstrap.com/2.3.2/). Not only has the CSS been redone to be mobile first, Bootstrap 3 adopted a simpler CSS model (which makes it much easier to customize) and also a flat design. This is probably most noticeable in the button styling, as seen in this image. (The top row of buttons are styled using Bootstrap 2 while the bottom row is Bootstrap 3.)

![image](https://gwb.blob.core.windows.net/sdorman/Windows-Live-Writer/Introducing-Bootstrap-Flat_12B65/image_11.png "image")

While the flat design is (in my opinion) a great change as it keeps Bootstrap in touch with the trend popularized by Windows Phone and Windows 8 for a flatter UI that helps keep the focus on the content being presented, I don’t think Bootstrap 3 goes far enough. There are still the rounded corners and slight shadows (on some components) that mean it doesn't completely embrace the "modern" design elements.

### How is Bootstrap Flat different?

Although there are already several other "flat" or "modern" skins for Bootstrap, very few of them are built for Bootstrap 3. They are also completely custom Bootstrap implementations. By this, I mean that in most cases these themes include their own, modified, version of `bootstrap.css` making it difficult (or impossible) to upgrade to newer versions of Bootstrap. 

> *To me, this completely misses the concept of a theme. I should be able to upgrade Bootstrap versions without having to worry about any customizations getting overwritten. These “themes” don’t allow me to do that. They also add additional functionality (which in some cases is useful) but also change the default colors, spacing, sizes, etc. from the original Bootstrap. The end result is that while these themes claim to be built on top of Bootstrap they are really built **from** Bootstrap.*

Bootstrap Flat aims to change that. It's built on top of Bootstrap 3 and uses Bootstrap's recommended method of providing "light" customizations. In other words, these customizations are pure CSS. 

To keep things as simple as possible, all of the CSS which achieves the flat look is contained in the `bootstrap-flat.css` stylesheet. Because this is done in a separate stylesheet, you can easily upgrade to newer versions of Bootstrap without fear of the flattening styles being overwritten. The following image shows what the buttons would look like after you include `bootstrap-flat.css`. (Again, the top row of buttons are styled using Bootstrap 2, the middle row is Bootstrap 3 and the bottom row is Bootstrap 3 after Bootstrap Flat has been included.)

![image](https://gwb.blob.core.windows.net/sdorman/Windows-Live-Writer/Introducing-Bootstrap-Flat_12B65/image_12.png "image")

This is pure Bootstrap 3 with square corners, no gradients, and no drop shadows. *(Unlike some of the other “themes”, there are also no color or functional changes.)*

In order to flatten your Bootstrap, you simply need to include the one additional `bootstrap-flat.css` stylesheet. ***There are no style changes needed!***

### Is there more?

In addition to the flattening, a `bootstrap-flat-extras.css` stylesheet is also available. This stylesheet adds additional (new) modern user interface elements and additional styles for some of the existing Bootstrap elements. For example, there is an additional button style (`btn-striped`) which takes the button color and applies it only to the left border and a new `callout` style (which is a variation of the alert styles.)

![image](https://gwb.blob.core.windows.net/sdorman/Windows-Live-Writer/Introducing-Bootstrap-Flat_12B65/image_18.png "image")

### [](http://scottdorman.github.io/cadru/#i-found-an-issue)I found an issue or want to request a feature.

Great, please [log a bug](https://github.com/scottdorman/bootstrap-flat/issues/new) so that it can be tracked.

### How do I get Bootstrap Flat?

I’ve tried to make it easy to get Bootstrap Flat for your own use. It’s available in source code form on [GitHub](https://github.com/scottdorman/bootstrap-flat) and also through [NuGet](https://www.nuget.org/packages/Twitter.Bootstrap.Flat).

### Who started Bootstrap Flat?

Bootstrap Flat is an open source project available to everyone to use and change. The project was initially started by [Scott Dorman](http://about.me/scottdorman) but has received inspiration and contributions from many others. Scott remains the project coordinator but encourages contributions in an open manner. Feel free to [fork the repository](https://github.com/scottdorman/bootstrap-flat/fork) and submit your own pull requests for changes. 

Scott is a [Microsoft C# MVP](https://mvp.support.microsoft.com/profile/Scott.Dorman), [author](http://www.amazon.com/gp/redirect.html?ie=UTF8&location=http%3A%2F%2Fwww.amazon.com%2Fgp%2Fentity%2FScott-Dorman%2FB003MF5X5C%3Fie%3DUTF8%26ref_%3Dntt_athr_dp_pel_pop_1&tag=scotdorm-20&linkCode=ur2&camp=1789&creative=390957), [speaker](http://speakerrate.com/scottdorman), [blogger](scottdorman.github.io), [developer](http://scottdorman.azurewebsites.net/), and the creator of [WP Requests](http://wprequests.uservoice.com/) and [WinStore Requests](http://winstorerequests.uservoice.com/) and has been working with .NET and C# since it was released. He’s been involved with computers in one way or another for as long as he can remember, but started professionally in 1993. Although his primary focus right now is commercial software applications, he prefers building infrastructure components, reusable shared libraries and helping companies define, develop and automate process and code standards and guidelines.
