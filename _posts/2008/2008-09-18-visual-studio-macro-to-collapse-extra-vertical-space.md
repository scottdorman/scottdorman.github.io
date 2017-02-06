---
layout: post
title: Visual Studio Macro to Collapse Extra Vertical Space
date: '2008-09-18 12:06:49 -05:00'
---

A few days ago in one of the CodeProject disucssion forums someone was looking for a way to easily remove the extra vertical whitespace in a file. This is really handy if you copy and paste code from the web or otherwise have a file that has multiple consecutive blank lines that you want to consolidate to a single blank line.

A solution was presented that used a Visual Studio macro, but that macro used pattern matching with find and replace, so it didn't feel very stable. Taking the opportunity to dig into Visual Studio macros again, I created a more full-featured version of this macro.

This macro uses the selection object of the active document and iterates over each line. Once it finds a blank line, it then advances over the following lines, deleting them until it finds a non-blank line again. At the end, it runs the format document command.

The macro is [available](http://cid-93d618d639ec9651.skydrive.live.com/self.aspx/Public/Visual%20Studio%202008%20Macros/FormattingUtilities.vb) on my SkyDrive account. Download it to your `<UserProfile>\Documents\Visual Studio 2008\Projects\VSMacros80\MyMacros` folder, open the Visual Studio Macro IDE (Alt-F11) and add it as an existing item to the "MyMacros" project.

I make no guarantees or warranties on this macro. I have tested it on several solutions and projects and everything seems to work and not cause any problems, but, as always, use with caution. Since it is a macro, you have the full source code available to investigate and see what it's actually doing. If you find any bugs or make any useful changes, please let me know and I'll update the macro.
