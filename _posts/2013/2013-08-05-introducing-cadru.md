---
layout: post
title: Introducing Cadru
date: '2013-08-05 09:57:36 -05:00'
tags: cadru open-source
---

# What is Cadru?

[Cadru](http://scottdorman.github.io/cadru) is (hopefully) a helpful utility framework containing new APIs and extensions to the core .NET Framework to help complete your developer toolbox. Cadru is designed to be portable first, which means that the majority of the library is available as a Portable Class Library (PCL) targeting the following frameworks:

*   .NET Framework 4 and higher 
*   Silverlight 4 and higher 
*   Windows Phone 7 and higher 
*   .NET for Windows Store apps   

This set of target frameworks was chosen to provide Cadru with the broadest reach possible. Any platform specific functionality is exposed as more narrowly focused portable class libraries or as a non portable library if that's the only option.

The docs for Cadru are always evolving to be better. The [wiki docs](https://github.com/scottdorman/cadru/wiki) (coming soon) are the permanent place where the docs will continue to get better on specific use cases of the library. There are also a lot of unit tests that show how to use the APIs and can be a good starting place as the docs continue to evolve. (My goal is to as be as close to 100% code coverage as possible. Obviously, that will always be a work in progress.)

Cadru is provided as open source licensed under the [Microsoft Public License](http://opensource.org/licenses/Ms-PL.html), use it as you wish (but please provide some credit somewhere in your app.)

# Why another library?

Although Cadru was just released (2013-07-19) as an open source framework, some of the APIs it contains have 10 years of real world use behind them. These are things that I kept having to rewrite in the apps I was building. Rather than continuing to rewrite them, I decided to encapsulate them in a library and make it broadly available. Although Cadru grew from app development, I have rewritten everything with a focus on being part of an API. That means everything is (hopefully) well documented, cleanly written, and easy to use.

# I found an issue

Great, please [log a bug](https://github.com/scottdorman/cadru/issues/new) so that it can be tracked.

# How do I get Cadru?

I've tried to make it easy to get Cadru for your own use. Right now, it's available in source code form on [GitHub](https://github.com/scottdorman/cadru) but I'm working on making it available in binary form through NuGet and the Visual Studio Gallery.\

# Who started Cadru?

Cadru is an open source project available to everyone to use and change. The project was initially started by [Scott Dorman](http://about.me/scottdorman) but has received inspiration and contributions from many others. In some cases, APIs were inspired by existing APIs from other open source libraries. Scott remains the project coordinator but encourages contributions in an open manner. Feel free to [fork the repository](https://github.com/scottdorman/cadru/fork) and submit your own pull requests for changes. 

Scott is a [Microsoft C# MVP](https://mvp.microsoft.com/en-us/PublicProfile/4014220), [author](http://amzn.to/28ILhnG), [speaker](http://speakerrate.com/scottdorman), [blogger](scottdorman.github.io), [developer](http://scottdorman.azurewebsites.net/), and the creator of [WP Requests](http://wprequests.uservoice.com/) and [WinStore Requests](http://winstorerequests.uservoice.com/) and has been working with .NET and C# since it was released. He's been involved with computers in one way or another for as long as he can remember, but started professionally in 1993. Although his primary focus right now is commercial software applications, he prefers building infrastructure components, reusable shared libraries and helping companies define, develop and automate process and code standards and guidelines.
