---
layout: post
title: Windows Live Spaces URL Confusion
date: 2007-10-16 00:47:54 -05:00
---

A few days ago I talked about [Windows Live SkyDrive Updates]({% post_url /2007/2007-10-12-Windows-Live-SkyDrive-Updates %}) and the new [Windows Live Events]({% post_url /2007/2007-10-12-Windows-Live-Events %}), both of which are part of Windows Live Spaces. Since then, I've been browsing around the Windows Live site and checking out how things are working and noticed a few really annoying inconsistencies with the URLs being used for all of the different services.

When you sign in to your Windows Live account, you are presented with the following secondary toolbar:

 ![image](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/WindowsLiveSpacesURLConfusion_14239/image_3.png) 

If you look at the URLs used for each of these links, you will see the problem I'm talking about. This toolbar provides links for both administration pages and public pages. The administration links all start with [http://name.home.services.live.com](http://name.home.services.live.com) and are the following toolbar items:

*   <div align="left">Spaces home ([http://sjdorman.home.services.spaces.live.com/](http://sjdorman.home.services.spaces.live.com/ "Spaces home"))</div>
*   <div align="left">Events ([http://sjdorman.home.services.spaces.live.com/events/](http://sjdorman.home.services.spaces.live.com/events/ "Events"))</div> 

The public pages all have links that start with [http://name.spaces.live.com](http://name.spaces.live.com) and are the following toolbar items:

*   <div align="left">Your space (([http://sjdorman.spaces.live.com/](http://sjdorman.spaces.live.com/))</div>
*   <div align="left">Friends ([http://sjdorman.spaces.live.com/friends/](http://sjdorman.spaces.live.com/friends/ "Friends"))</div>
*   <div align="left">Photos ([http://sjdorman.spaces.live.com/photos/](http://sjdorman.spaces.live.com/photos/ "Friends"))</div> 

So far things make sense, right? The links are logically grouped and are fairly consistent. I'm not crazy about the "home.services" portion that gets inserted in between the name and the "spaces.live.com" part of the URL for the administrative pages, but I can live with it. 

Did you notice that the SkyDrive toolbar item isn't listed under either group? It's not listed because it doesn't follow either pattern. Unless you have a direct link to a SkyDrive public folder or file, you must be logged in to the Windows Live site in order to use the service. The link for the toolbar item is simply [http://skydrive.live.com/](http://skydrive.live.com/ "SkyDrive"), which if you are logged in actually maps to a very hard to remember link that actually looks like a user SID. In my case, the link maps to [https://cid-93d618d639ec9651.skydrive.live.com/home.aspx](https://cid-93d618d639ec9651.skydrive.live.com/home.aspx "https://cid-93d618d639ec9651.skydrive.live.com/home.aspx"). 

Here is where the inconsistency starts to happen. Since SkyDrive is part of the Windows Live family of services and it requires a Windows Live identity in order to share files, why force people (both me and anyone I share files with) to use some cryptic link instead of [https://sjdorman.skydrive.live.com](https://sjdorman.skydrive.live.com)?

For that matter, the new Windows Live Events suffers from a similar problem. When you create an event, it is assigned a unique id. This makes perfect sense as it is the easiest way to identify events and keep them separate from each other. However, the URL for each event looks like [http://cid-00092add5fbc75a9.events.live.com/](http://cid-00092add5fbc75a9.events.live.com/ "http://cid-00092add5fbc75a9.events.live.com/"). Again, why force people to use another cryptic link instead of [http://sjdorman.events.live.com/cid-00092add5fbc75a9](http://sjdorman.events.live.com/cid-00092add5fbc75a9)? Ok...I know that the link I just suggested still has some cryptic ID in it, but it's better than what we currently have. Of course, the best URL would be something like [http://sjdorman.events.live.com/2007/10/15/SomeEvent](http://sjdorman.events.live.com/2007/10/15/SomeEvent).

So far Microsoft has been doing a good job keeping the Windows Live offerings consistent in the way the look and are providing a very useful set of services. However, that consistency needs to go beyond just the look and feel of the web sites and services and extend to the underlying URLs and even the programming interfaces.
