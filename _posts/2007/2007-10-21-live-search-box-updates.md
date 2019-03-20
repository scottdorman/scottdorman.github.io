---
layout: post
title: Live Search Box Updates
date: '2007-10-21 14:37:38 -05:00'
---

Earlier today, I talked about [Live Search]({% post_url /2007/2007-10-21-Live-Search %}) and [how to add a Live Search Box to your website]({% post_url /2007/2007-10-21-Adding-a-Live-Search-Box-to-your-website %}). 

In those posts, I talked about the [3-step wizard](http://search.live.com/siteowner/searchboxstep1.aspx) that allows you to easily add the Advanced Search Box to your site and the fact that it doesn't allow you to specify multiple search macros.

If you look at the search results from my blog now, you will see that there are now 5 new tabs in the search results. (Before I only had 2, "My blog" and "Web".) These tabs show search results from the entire [GeeksWithBlogs](http://geekswithblogs.net/) site, [MSDN](http://msdn2.microsoft.com/), [MSDN Blogs](http://blogs.msdn.com/), [MSDN Forums](http://forums.microsoft.com/), the [Microsoft Support](http://support.microsoft.com/) site, and the entire web.

![image](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/LiveSearchBoxUpdates_C404/image_3.png)

You still can't add the additional macros using the wizard, but if you don't mind customizing the Javascript that it generates, you can add them by hand. It's best if you know Javascript, at least a little bit, but I don't think it's a requirement. No matter what, you should make a backup copy of either the original script or the entire page just in case something goes wrong.

In the Javascript, you will see a section that looks like this:

```javascript
var WLSearchBoxConfiguration=
      {
         "global":{
            "serverDNS":"search.live.com",
            "market":"en-US"
         },
         "appearance":{
            "autoHideTopControl":false,
            "width":800,
            "height":550,
            "theme":"Blue"
         },
         "scopes":[
            {
               "type":"web",
               "caption":"&#x4d;&#x79;&#x20;&#x62;&#x6c;&#x6f;&#x67;",
               "searchParam":"site:geekswithblogs.net\/sdorman"
            }
            ,
            {
               "type":"web",
               "caption":"&#x57;&#x65;&#x62;",
               "searchParam":""
            }
         ]
      }
```

The part that we need to modify is the "scopes" declaration. This section effectively declares an array of search scopes, including the type, caption, and search parameters. You can add as many scope definitions as you want to this section, but make sure you only have one definition for searching the entire web (this is the definition that has an empty searchParam specification). If you decide to add multiple search macros,  you can find a bunch of predefined macros on the [Windows Live Gallery](http://gallery.live.com/default.aspx?pl=4&bt=13) or you can make your own. Be sure to separate the definitions with a comma (,) to prevent Javascript errors. 

As you can see, the caption is specified by using the [Hex](http://en.wikipedia.org/wiki/Hexadecimal) values for the letters. It will work using normal English letters, but I don't think it will be translated properly. If you want to easily find the Hex values, you can use this [String to ASCII/Hex/Binary](http://www.easycalculation.com/ascii-hex.php) online converter. Once you get the Hex string, you will need to make the hex values proper HTML entities by adding the "&#x" in front of the hex value and the ";" after it. The other thing to watch out for is that this creates an entity of &#x1; for a space instead of the correct &#x20; entity.

For example, to add an additional search macro that searches MSDN, you need to add the following bit of code:

```javascript
{
   "type":"web",
   "caption":"&#x4D;&#x53;&#x44;&#x4E;",
   "searchParam":"macro:livelabs.msdn"
}
```

The same thing will work for adding additional sites, all you need to do is change the searchParam specification. For example, to search the entire Microsoft site, you would add the following:

```javascript
{
    "type":"web",
    "caption":"&#x4D;&#x69;&#x63;&#x72;&#x6F;&#x73;&#x6F;&#x66;&#x74;",
    "searchParam":"site:microsoft.com"
}
```

You can create more advanced searchParam specifications, but I highly recommend [creating a macro](http://search.live.com/macros?mkt=en-us) if you are going to do that.
