---
layout: post
title: Virtual Earth v6
date: 10/21/2007 11:36:21 AM
---

A few days ago, Microsoft released a pretty major [upgrade](http://blogs.msdn.com/virtualearth/archive/2007/10/17/virtual-earth-version-6-now-available.aspx) to [Live Search Maps](http://maps.live.com/) with the release of the Virtual Earth 6 API. There are some pretty cool enhancements, and, with the exception of two bugs found by [Joe Healy](http://www.devfish.net/FullBlogItemView.aspx?BlogId=452), is as simple as change the "v=5" parameter in your link to "v=6".

I'm not going to list all of the upgrades, since there are a lot of them. If you want to see the full list, check out the [VE developer blog](http://blogs.msdn.com/virtualearth/archive/2007/10/17/virtual-earth-version-6-now-available.aspx) or the [online SDK](http://msdn2.microsoft.com/en-us/library/bb429619.aspx). I will list some of the features that are my current favorites (taken from the [VE developer blog](http://blogs.msdn.com/virtualearth/archive/2007/10/17/virtual-earth-version-6-now-available.aspx)):

> **Multipoint routing
> **The new GetDirections API can take multiple points for a route instead of just the start and end points, allowing for more complex trip planning.  In addition, it is also possible to import routes from Excel through the GeoRSS API.
> 
> **Traffic Tile Overlay
> **The V6 map Control now supports fetching of Traffic tiles, for client token authenticated users, containing rendered traffic flow data.  While the Virtual Earth Platform does not automatically offer incident information, users can query MapPoint Web Service to get this information.
> 
> **Bird’s eye pushpin accuracy
> **Bird’s Eye pushpin placement accuracy has been enhanced for V6.  In this release, when users convert pixels to latlong in Bird’s Eye, Virtual Earth will make server side calls for accurate calculations taking into account camera metadata.  The result will be that when users add a pushpin in a road or aerial view, and switch to bird’s eye, the pushpin will still display in the correct location.

One thing that wasn't mentioned is a great improvement to the driving directions which allows you not only to see that traffic conditions along your planned route, but also change your route based on those traffic conditions. 

This release also incorporates the [PhotoSynth](http://labs.live.com/photosynth) technology for the 3D view and party maps (also known as 1-Click Directions). The PhotoSynth integration is just plain cool, and allows you to view a location using orthogonal imagery. Party maps allow you to create a single page that shows driving directions from the major 4 compass points (as available) to your destination and also lets you get directions from a specific location. They aren't yet integrated with [Windows Live Events](http://geekswithblogs.net/sdorman/archive/2007/10/12/Windows-Live-Events.aspx "Windows Live Events") (Live Search Maps is integrated, but the party maps technology isn't), but it should only be a matter of time before they are integrated, which will make both Party Maps and [Windows Live Events](http://geekswithblogs.net/sdorman/archive/2007/10/12/Windows-Live-Events.aspx "Windows Live Events") more useful.
