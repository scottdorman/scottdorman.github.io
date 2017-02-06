---
layout: post
title: Personalized Live Event web addresses
date: '2007-11-03 09:42:24 -05:00'
---

Not too long ago I talked about the [Windows Live Spaces URL Confusion]({% post_url 2007-10-16-Windows-Live-Spaces-URL-Confusion %}), and the really cryptic URLs being used for [SkyDrive](http://skydrive.live.com/) and [Live Events](http://events.live.com/). Today, I found something that makes Live Event addresses a little bit better. I'm not sure if this has always been available or if it's new, but either way it's a feature that is not obvious at all.

I'm talking about the "Personalize your web address" option that is available from the event settings page (if you've already created the event) or from the create event page. It's very difficult to see on the create event page, since it appears as just a single sentence at the very bottom of the page:

![image](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image_5.png)

It's a little bit easier to find once you've created the event if you go to the event settings page:

![image](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image_6.png) 

While this will allow you to create more friendly addresses for your events, it is still far from an optimal solution. It requires me, as the event creator, to take additional steps to create a friendly address.  It is a little better if you do this when you create the event, since there is a "Generate my web address for me" link. (This isn't available for an already created event.) However, when you click on it, the web address section collapses and you don't see the resulting address. This means you then have to click on the "Personalize the address" link to display the section and you still have to click the "Check availability" button to ensure that the web address is available. By the way, the generated address is simply the title of the event with any spaces and special characters removed.

Why should we be required to take all of these extra steps just to generate a friendly address? Windows Live is already using the convention of name.service_name.live.com, so why not update Windows Live Events to follow this same convention? Then the web address can always be generated with much fewer possibilities of a collision. As an example, if you create an event named "Scott's Test Event", the address could be sjdorman.events.live.com/ScottsTestEvent or even sjdorman.events.live.com/2007/11/01/ScottsTestEvent (which is my preferred choice).
