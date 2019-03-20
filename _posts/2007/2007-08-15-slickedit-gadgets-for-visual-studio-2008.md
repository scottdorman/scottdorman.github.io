---
layout: post
title: SlickEdit Gadgets for Visual Studio 2008
date: '2007-08-15 21:43:17 -05:00'
---

While I was getting the [Code Project Add-in for Visual Studio]({% post_url /2007/2007-08-15-the-code-project-browser-add-in-for-visual-studio %}) working on Visual Studio 2008 Beta 2, I decided to see if I could get the [SlickEdit Gadgets for Visual Studio 2005](http://www.slickedit.com/content/view/441) working as well. It turns out, with a little bit of registry tweaking, they work under Visual Studio 2008 Beta 2 without any problems (so far).

This is by no means a supported configuration from SlickEdit and requires modifying the registry, so you should do so only after making the necessary backups and any other precautions you feel are necessary.

In order to get these working, you will need to have the Gadgets already installed or have Visual Studio 2005 installed. The MSI package for the Gadgets requires Visual Studio 2005 and will not continue the installation if it isn't found. Once you have the gadgets installed, you need to modify your registry. There are a lot of registry keys that need to be duplicated, so I have created a .reg file that you can download and run. 

You can [download](http://cid-93d618d639ec9651.skydrive.live.com/self.aspx/Public/SlickEditGadgetsVS2008.reg) the file from my Windows Live SkyDrive public folder.
