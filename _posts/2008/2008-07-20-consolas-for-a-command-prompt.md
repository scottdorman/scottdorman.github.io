---
layout: post
title: Consolas for a Command Prompt
date: 2008-07-20 09:40:59 -05:00
---

This actually came out a while ago, but if you like the Consolas font that ships with Vista and Office 2007 you can change the Command Prompt (CMD.EXE) settings to allow you to use Consolas. If you don’t have Consolas installed, you can [download](http://www.microsoft.com/downloads/details.aspx?familyid=22e69ae4-7e40-4807-8a86-b3d36fab68d3&displaylang=en "free download") from the Microsoft Download Center.

In order to add Consolas to the list of fonts available for the Command Prompt, you need to run the following command (run this in an elevated command prompt in Vista):
  <div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 41px; background-color: #f4f4f4">   <div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">     

<span style="color: #606060"> </span>reg add <span style="color: #006080">"HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Console\TrueTypeFont"</span> /v 00 /d Consolas

  </div>
</div>



After that, log off and when you log back in, Consolas will be an option in the properties window. 

If you make this change, there are a few things to watch out for:

*   You may have to adjust the font size in order to actually see the font change.
*   The display quality of the font will depend on your graphics card, apparently some people have reported that the font looks fuzzy or has a “rainbow” appearance.
*   The font doesn’t support the line draw characters that Lucida Console and the raster fonts support, so commands like “Tree” will display box characters instead.
