---
layout: post
title: Subtext 1.9.5 Released
date: 2007-05-12 10:48:47 -05:00
---

![](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/Subtext1.9.5Released_97FC/subtextsubmarinelogo68.png)Subtext 1.9.5 has been [released](http://haacked.com/archive/2007/05/11/subtext-1.9.5-release.aspx) to the public. This is primarily a bug-fix release but does include some new features. Oddly enough, this is the first release to go out the door without a [codename](http://codeclimber.net.nz/archive/2007/02/07/Codename-your-releases.aspx).

Installing on a [clean](http://www.subtextproject.com/Home/About/Docs/Installation/tabid/111/Default.aspx) machine or [upgrading](http://www.subtextproject.com/Home/About/Docs/Upgrading/tabid/147/Default.aspx) an earlier 1.9 release are both relatively easy. If there are any ideas to make upgrading easier, we'd love to hear them.

This is scheduled to be the last release in the 1.9 branch, unless there are high priority bugs found that need to be fixed. What this means is that the development effort will be refocused on the 2.0 release, which hopefully won't take quite as long as 1.9.5 did.

 The main focus for the 2.0 release is a new plugin model that promises to be a major improvement over the current one and a custom MembershipProvider using the .NET 2.0 membership APIs. Of course, we are always looking at refactoring and code cleanup to help improve the stability and maintainability of the code base as well.

The new features included in this release are:

*  **Content Tagging and Tag Cloud -** for more details, refer to [this post](http://haacked.com/archive/2007/05/11/tagging-in-subtext.aspx).      
*  **Identicon Support** - Uses the [Identicon Handler project](http://haacked.com/archive/2007/03/19/identicon-handler-for-.net-on-codeplex.aspx) on CodePlex. 
*  **MyBrand Feedburner Support** - Updated our FeedBurner implementation to support custom feedburner URLs 
*  **Upgrade to [LightBox 2.0](http://www.huddletogether.com/projects/lightbox2/)** - If you referenced the default lightbox skin in your custom skin, please reference [this post](http://codeclimber.net.nz/archive/2007/05/11/Breaking-change-in-Subtext-1.9.5-update-your-custom-skins.aspx) by Simone to understand how to update the skin. 
*  **Author CSS Class** - The CSS class of "author" is added to comments left by the owner of a blog (must be logged in when leaving comment for this to work). This allows custom skin authors to highlight comments by authors. 
*  **Credits Page** - In the Admin section, we give credit where credit is due, displaying a list of the open source products we make use of in building Subtext. 
*  **Implemented ASP.NET AJAX** - We replaced MagicAjax panel with ASP.NET Ajax libraries. Keep in mind that this requires a bit of new Web.config configuration sections. So be careful when merging your Web.config changes.

A partial list of bug fixes is here:

*   [Metaweblog API getRecentPosts method does not send categories](http://sourceforge.net/tracker/index.php?func=detail&aid=1683847&group_id=137896&atid=739979) 
*   [Host Admin edits wrong blog host when not on page 1](http://sourceforge.net/tracker/index.php?func=detail&aid=1658118&group_id=137896&atid=739979) 
*   [Recent Posts control wrong URL](http://sourceforge.net/tracker/index.php?func=detail&aid=1679366&group_id=137896&atid=739979) 
*   [FeedBurner doesn't allow the / character, though it should](http://sourceforge.net/tracker/index.php?func=detail&aid=1685842&group_id=137896&atid=739979) 
*   [Comments allow unclosed tags](http://sourceforge.net/tracker/index.php?func=detail&aid=1677521&group_id=137896&atid=739979) 
*   [Fixed up CSS issues for several Skins](http://sourceforge.net/tracker/index.php?func=detail&aid=1545724&group_id=137896&atid=739979) 
*   [MultiBlog Caching Issue - Posts from one show in another](http://sourceforge.net/tracker/index.php?func=detail&aid=1452536&group_id=137896&atid=739979) - This bug bears special mention as it was a real pain to track down the root cause. 
*   Fixed issues with case sensitive databases 
*   ...and others...


Now I just need to wait for GeeksWithBlogs to upgrade...
