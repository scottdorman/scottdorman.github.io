---
layout: post
title: StyleCop &ndash; Some Constructive Criticism
date: '2008-12-31 19:29:18 -05:00'
tags: coding-style code-standards
---

It's been a while since I last talked about [StyleCop](http://code.msdn.microsoft.com/sourceanalysis). I've been using it a lot recently on an internal project of mine and have come to really like the idea behind the tool. After using it extensively over the last few days, however, I think there are a few glaring omissions and features that need to be implemented before this tool can become truly useful.

The first issue that I ran in to was the sheer volume of violations reported. In an effort to try and trim down the violations to a workable number, I found the information in this [blog post](http://blogs.msdn.com/sourceanalysis/archive/2008/11/11/introducing-stylecop-on-legacy-projects.aspx) which talks about how to introduce StyleCop to legacy projects. This is a fairly simple 2 step process which involves enabling StyleCop MSBuild integration and then editing the .csproj file to exclude files from StyleCop by adding an *ExcludeFromStyleCop* property to each file.

I wrongly assumed that since I was running StyleCop from within Visual Studio that it would take care of enabling the MSBuild integration for each analysis run and the files marked with the *ExcludeFromStyleCop* property would be correctly excluded. As you can guess, this was a completely wrong assumption. Apparently, when running StyleCop through Visual Studio, it either doesn't use the MSBuild integration or it just flat out ignores the *ExcludeFromStyleCop* property.

Since I wasn't able to exclude files from StyleCop (short of running it on individual files directly from Visual Studio), I next opted to exclude classes of rules so that I could focus on specific issues. Most of my issues come from the documentation rules and there were a lot from internal classes. Fortunately, StyleCop has a setting for the Documentation rules that allows you to tell it to "Ignore privates", "Ignore internals", and "Include fields". I promptly unchecked the "Include fields" choice (the default is for this to be checked) and checked the two "Ignore" options (whose default is to be unchecked). Not only do these defaults seem backwards to me but they also appear to be ignored for certain rules. For instance, I still hit a lot of "SA1600: The class must have a documentation header." violations...even for internal classes. Yes, the help text for the "Ignore internals" option does clearly say that it does not apply to classes, structs, and interfaces...but why doesn't it?

The next problem I ran in to was the result of rules SA1632 and SA1630 which collectively state that the documentation text must be at least two words long (separated by white space) and at least 10 characters long. Normally this is extremely valid and important. However, in one case I have an enum which contains the ISO 3166 two-character country codes. The documentation text for each enum entry is the name of the country represented, which in most cases is a single word and is less than the 10 character minimum. Unfortunately, I have no way of excluding just that file and there is no corresponding SuppressMessage attribute that StyleCop recognizes so I could simply exclude that violation for each enum entry. The only choice is to disable both of those rules entirely so I can get the noise generated out of the way.

I'm still working through resolving the StyleCop issues and I'm sure it will take me several more days of resolving issues, enabling more rules, figuring out what can be safely ignored, and repeating. Don't get me wrong, I think StyleCop is a great tool and seems to be continually improving. I think Jason has done an incredible job so far, but if I could leave him with two key takeaways from this, it would be:

1.  Allow StyleCop to always respect the *ExcludeFromStyleCop* property. Even better, actually allow you to set it through the properties window on the file.
2.  Provide support for using the SupressMessage attribute. (Please don't create a new attribute for this either. The SuppressMessage attribute already includes everything you should need and is even in the correct namespace.)  

While I'm at it, the [FxCop](http://msdn.microsoft.com/en-us/library/bb429476(VS.80).aspx) team should follow suit and provide support for an *ExcludeFromFxCop* property in MSBuild and allow it to be set through the properties window on the file as well.
 
