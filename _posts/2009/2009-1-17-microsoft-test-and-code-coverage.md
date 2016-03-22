---
layout: post
title: Microsoft Test and Code Coverage
date: 1/17/2009 12:30:21 PM
---

I have been writing a lot of unit tests lately using Microsoft Test. This included converting a bunch of old NUnit tests to the MS Test format, which was relatively painless. While examining the code coverage results (after all, what good are unit tests if you don’t know what portions of the code are being tested and not tested), I have noticed that the results sometimes lie.

For example, I have a class that contains some extension methods for manipulating enums. One of those methods takes an enum and coverts it to an IList of KeyValuePairs containing the enum value and a description.

[![image](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/MicrosoftTestandCodeCoverage_AD9C/image_thumb_1.png "image")](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/MicrosoftTestandCodeCoverage_AD9C/image_4.png) 

As you can see by the highlighted row in the code coverage results window, the ToList() method is only covered at 90.91% and there are 2 blocks that aren’t covered. At first glance, this looked reasonable so I reviewed the actual ToList() method with code coverage highlighting turned on.

[![image](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/MicrosoftTestandCodeCoverage_AD9C/image_thumb_2.png "image")](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/MicrosoftTestandCodeCoverage_AD9C/image_6.png) 

What’s wrong with this picture? I’m using the default code coverage highlighting colors, so the light blue coloring indicates 100% coverage. Knowing that, I’m seeing a method that is colored as being 100% covered yet the coverage results are showing it as a different number.

This stays consistent no matter how many times I re-run the tests and I have also seen it on other methods in other classes.
  <div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:7ab5e9d3-8b53-4cfa-8b93-9f8c8dc50e2f" class="wlWriterSmartContent">*Technorati Tags: [Unit Tests](http://technorati.com/tags/Unit+Tests), [Code Coverage](http://technorati.com/tags/Code+Coverage), [MSTest](http://technorati.com/tags/MSTest)*</div><div class="wlWriterHeaderFooter" style="text-align:left; margin:0px; padding:4px 4px 4px 4px;">[![DotNetKicks Image](http://www.dotnetkicks.com/Services/Images/KickItImageGenerator.ashx?url=http://geekswithblogs.net/sdorman/archive/2009/01/17/microsoft-test-and-code-coverage.aspx&bgcolor=0080C0&fgcolor=FFFFFF&border=000000&cbgcolor=D4E1ED&cfgcolor=000000)](http://www.dotnetkicks.com/kick/?url=http://geekswithblogs.net/sdorman/archive/2009/01/17/microsoft-test-and-code-coverage.aspx)</div>
