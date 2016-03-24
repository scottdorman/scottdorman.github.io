---
layout: post
title: Live Search Box Updates
date: 2007-10-21 14:37:38 -05:00
---

Earlier today, I talked about [Live Search]({% post_url /2007/2007-10-21-Live-Search %}) and [how to add a Live Search Box to your website]({% post_url /2007/2007-10-21-Adding-a-Live-Search-Box-to-your-website %}). 

In those posts, I talked about the [3-step wizard](http://search.live.com/siteowner/searchboxstep1.aspx "-step wizard") that allows you to easily add the Advanced Search Box to your site and the fact that it doesn't allow you to specify multiple search macros.

If you look at the search results from my blog now, you will see that there are now 5 new tabs in the search results. (Before I only had 2, "My blog" and "Web".) These tabs show search results from the entire [GeeksWithBlogs](http://geekswithblogs.net/) site, [MSDN](http://msdn2.microsoft.com/), [MSDN Blogs](http://blogs.msdn.com/), [MSDN Forums](http://forums.microsoft.com/), the [Microsoft Support](http://support.microsoft.com/) site, and the entire web.

![image](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/LiveSearchBoxUpdates_C404/image_3.png)

You still can't add the additional macros using the wizard, but if you don't mind customizing the Javascript that it generates, you can add them by hand. It's best if you know Javascript, at least a little bit, but I don't think it's a requirement. No matter what, you should make a backup copy of either the original script or the entire page just in case something goes wrong.

In the Javascript, you will see a section that looks like this:
 <div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 900px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 443px; background-color: #f4f4f4"> <div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">

<span style="color: #606060">   1:</span> <span style="color: #0000ff">var</span> WLSearchBoxConfiguration=

<span style="color: #606060">   2:</span>       {

<span style="color: #606060">   3:</span>          <span style="color: #006080">"global"</span>:{

<span style="color: #606060">   4:</span>             <span style="color: #006080">"serverDNS"</span>:<span style="color: #006080">"search.live.com"</span>,

<span style="color: #606060">   5:</span>             <span style="color: #006080">"market"</span>:<span style="color: #006080">"en-US"</span>

<span style="color: #606060">   6:</span>          },

<span style="color: #606060">   7:</span>          <span style="color: #006080">"appearance"</span>:{

<span style="color: #606060">   8:</span>             <span style="color: #006080">"autoHideTopControl"</span>:<span style="color: #0000ff">false</span>,

<span style="color: #606060">   9:</span>             <span style="color: #006080">"width"</span>:800,

<span style="color: #606060">  10:</span>             <span style="color: #006080">"height"</span>:550,

<span style="color: #606060">  11:</span>             <span style="color: #006080">"theme"</span>:<span style="color: #006080">"Blue"</span>

<span style="color: #606060">  12:</span>          },

<span style="color: #606060">  13:</span>          <span style="color: #006080">"scopes"</span>:[

<span style="color: #606060">  14:</span>             {

<span style="color: #606060">  15:</span>                <span style="color: #006080">"type"</span>:<span style="color: #006080">"web"</span>,

<span style="color: #606060">  16:</span>                <span style="color: #006080">"caption"</span>:<span style="color: #006080">"&#x4d;&#x79;&#x20;&#x62;&#x6c;&#x6f;&#x67;"</span>,

<span style="color: #606060">  17:</span>                <span style="color: #006080">"searchParam"</span>:<span style="color: #006080">"site:geekswithblogs.net\/sdorman"</span>

<span style="color: #606060">  18:</span>             }

<span style="color: #606060">  19:</span>             ,

<span style="color: #606060">  20:</span>             {

<span style="color: #606060">  21:</span>                <span style="color: #006080">"type"</span>:<span style="color: #006080">"web"</span>,

<span style="color: #606060">  22:</span>                <span style="color: #006080">"caption"</span>:<span style="color: #006080">"&#x57;&#x65;&#x62;"</span>,

<span style="color: #606060">  23:</span>                <span style="color: #006080">"searchParam"</span>:<span style="color: #006080">""</span>

<span style="color: #606060">  24:</span>             }

<span style="color: #606060">  25:</span>          ]

<span style="color: #606060">  26:</span>       }
</div></div>


The part that we need to modify is the "scopes" declaration. This section effectively declares an array of search scopes, including the type, caption, and search parameters. You can add as many scope definitions as you want to this section, but make sure you only have one definition for searching the entire web (this is the definition that has an empty searchParam specification). If you decide to add multiple search macros,  you can find a bunch of predefined macros on the [Windows Live Gallery](http://gallery.live.com/default.aspx?pl=4&bt=13) or you can make your own. Be sure to separate the definitions with a comma (,) to prevent Javascript errors. 

As you can see, the caption is specified by using the [Hex](http://en.wikipedia.org/wiki/Hexadecimal) values for the letters. It will work using normal English letters, but I don't think it will be translated properly. If you want to easily find the Hex values, you can use this [String to ASCII/Hex/Binary](http://www.easycalculation.com/ascii-hex.php) online converter. Once you get the Hex string, you will need to make the hex values proper HTML entities by adding the "&#x" in front of the hex value and the ";" after it. The other thing to watch out for is that this creates an entity of &#x1; for a space instead of the correct &#x20; entity.

For example, to add an additional search macro that searches MSDN, you need to add the following bit of code:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">
<div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">

<span style="color: #606060">   1:</span> {

<span style="color: #606060">   2:</span>    <span style="color: #006080">"type"</span>:<span style="color: #006080">"web"</span>,

<span style="color: #606060">   3:</span>    <span style="color: #006080">"caption"</span>:<span style="color: #006080">"&#x4D;&#x53;&#x44;&#x4E;"</span>,

<span style="color: #606060">   4:</span>    <span style="color: #006080">"searchParam"</span>:<span style="color: #006080">"macro:livelabs.msdn"</span>

<span style="color: #606060">   5:</span> }
</div></div>


The same thing will work for adding additional sites, all you need to do is change the searchParam specification. For example, to search the entire Microsoft site, you would add the following:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">
<div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">

<span style="color: #606060">   1:</span> {

<span style="color: #606060">   2:</span>    <span style="color: #006080">"type"</span>:<span style="color: #006080">"web"</span>,

<span style="color: #606060">   3:</span>    <span style="color: #006080">"caption"</span>:<span style="color: #006080">"&#x4D;&#x69;&#x63;&#x72;&#x6F;&#x73;&#x6F;&#x66;&#x74;"</span>,

<span style="color: #606060">   4:</span>    <span style="color: #006080">"searchParam"</span>:<span style="color: #006080">"site:microsoft.com"</span>

<span style="color: #606060">   5:</span> }
</div></div>


You can create more advanced searchParam specifications, but I highly recommend [creating a macro](http://search.live.com/macros?mkt=en-us) if you are going to do that.
