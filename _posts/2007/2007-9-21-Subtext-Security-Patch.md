---
layout: post
title: Subtext Security Patch
date: 9/21/2007 11:24:47 PM
---

[Phil](http://haacked.com) recently [blogged](http://haacked.com/archive/2007/09/20/urgent-subtext-security-patch.aspx) about a newly discovered security vulnerability in the [Subtext](http://www.subtextproject.com/) blogging engine due to a flaw in the way the [FCKEditor](http://www.fckeditor.net/) control was integrated. As far as we know, no one was seriously affected and both a fix and a workaround were found very quickly by the core development team. 

If you are running Subtext 1.9.x, a patched version of the *Subtext.Providers.BlogEntryEditor.FCKeditor.dll* is available as a zip file. After you [download the patch (*Subtext1.9.5-PATCH.zip 7.72KB*)](http://downloads.sourceforge.net/subtext/Subtext1.9.5-PATCH.zip?use_mirror=easynews) , unzip the assembly and copy it into your bin directory. 

If you’re running a customized version and the above patch causes problems, you can workaround this issue by backing up and then temporarily removing the following directory in your installation. 

> `Providers\BlogEntryEditor\FCKeditor\editor\filemanager`

The Subtext development team takes security very seriously and this vulnerability has caused us to review our security guidelines to reduce these risks in the future. Phil is planning on a follow up post describing the vulnerability in more detail as well as our revised security plans. He is also planning a post outlining general guidelines for reporting and handling security issues in an open source project based on guidance provided by the Karl Fogel book, *[Producing Open Source Software](http://haacked.com/archive/2006/01/16/RunningAnOpenSourceProject.aspx)*. 

The code has been fixed in the Subversion and a patched release has been uploaded to [SourceForge](http://sourceforge.net/projects/subtext/) (Subtext-1.9.5b).
