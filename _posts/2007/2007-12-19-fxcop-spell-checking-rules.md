---
layout: post
title: FxCop Spell Checking Rules
date: 2007-12-19 20:22:09 -05:00
---

I just came across this [post](http://paraesthesia.com/archive/2007/12/19/fxcop-1.35-spell-checking-uses-office-2003.aspx) by [Travis Illig](http://paraesthesia.com/Default.aspx), one of the [Subtext](http://subtextproject.com/) developers, that brings up an interesting issue with FxCop 1.35. Apparently, FxCop 1.35 uses the Office 2003 spell checker for the spelling rules. If you don't have Office 2003 (and it must be Office 2003) installed, the spell check rules will fail. Travis isn't the [first person](http://blogs.parivedasolutions.com/borrell/archive/2007/07/02/520.aspx) to document this problem.

This problem is known and will be fixed in newer versions of FxCop. Visual Studio 2008 [code analysis tools](http://blogs.msdn.com/fxcop/archive/2007/09/20/new-for-visual-studio-2008-code-analysis-policy-improvements.aspx) have [spelling rules built in](http://blogs.msdn.com/fxcop/archive/2007/08/12/new-for-visual-studio-2008-spelling-rules.aspx) and support [custom dictionaries](http://blogs.msdn.com/fxcop/archive/2007/08/20/new-for-visual-studio-2008-custom-dictionaries.aspx), but that will only help if you have one of the more expensive Team System editions of Visual Studio. [FxCop 1.36](http://blogs.msdn.com/fxcop/archive/2007/10/10/fxcop-1-36-beta-released.aspx), which is available in beta, also ships with the [spell checker built in](http://forums.microsoft.com/MSDN/ShowPost.aspx?PostID=2445459&SiteID=1) so you don't need to have Office installed.
