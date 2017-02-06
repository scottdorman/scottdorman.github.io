---
layout: post
title: Historical Evolution of C# Code Style
date: '2008-07-20 13:32:06 -05:00'
---

Jason Allor, the developer behind the Microsoft [StyleCop](http://code.msdn.microsoft.com/sourceanalysis) tool has an excellent [blog post](http://blogs.msdn.com/sourceanalysis/archive/2008/05/25/a-difference-of-style.aspx) about the historical evolution of C# code style. The post came about largely in response to some criticisms about the code style enforced by StyleCop and how it doesn't match C/C++ style or that it differs in some areas with the [Framework Design Guidelines](http://amzn.to/28JOJA1). 

As Jason points out, most of the differences are historical and are there because the of two reasons:

1.  The original development team for the CLR consisted mainly of C++ developers.
2.  There were no other code standards available since C# was a brand new language, so the team writing the first version of the .NET Framework really only had C++ guidelines to follow.  

As more Microsoft development teams began writing C# code the C# style began to evolve. This is the hallmark of any coding style...it isn't set in stone, but is, instead, a living, breathing, thing. In order for a style to survive time and language changes it must be adapted as the need arises. 

This is exactly what has happened to the C# style. Is there a possibility that we end up with competing styles? Absolutely! Does anyone remember the K&R C style vs. BSD KNF? Both of these styles are very much alive in the C/C++ community today and there are no signs of either of these going away any time soon.

With tools like StyleCop and [FxCop](http://msdn.microsoft.com/en-us/library/bb429476(VS.80).aspx), hopefully we won't end up with multiple competing standards. As a community we should decide on a core set of guidelines and enforce them whenever possible.
