---
layout: post
title: Microsoft Terminal Settings
date: '2020-05-07 13:27:00 -05:00'
tags: microsoft-terminal
---

A year ago, in May 2019, Microsoft [introduced](https://devblogs.microsoft.com/commandline/introducing-windows-terminal/) the new Windows Terminal. If you haven't checked out Windows Terminal before, it's a multi-terminal application for users of command-line tools and shells like Command Prompt, PowerShell, and WSL. Yes, there are lots of other terminal applications out there which do the same thing, many with a lot more features, but Windows Terminal is still in a pre-release status.

One of the convenient features of Windows Terminal is that all of the settings are controlled by a `settings.json` file. This includes being able to define new color schemes and new terminal profiles.

I haven't used Windows Terminal very often since I first installed it, falling back to my old default workflow of launching the Visual Studio Developer Command Prompt from the Start Menu shortcut. However, in the past month I've been using it a lot more, and have come to really like it.

One thing that I found lacking was public support for being able to find working (meaning correct) terminal profiles. To help with that situation, I'm happy to introduce [microsoft-terminal-settings](https://github.com/scottdorman/microsoft-terminal-settings). The repository has a lot of color schemes and some profiles for both the command prompt and PowerShell terminals for the various Visual Studio 2019 editions.

It's still a bit nascent at the moment, consisting of just the GitHub repository, but I'll be working on adding a GitHub Pages branch over the next week, once I decide how I want things to look, which will make it easier to preview the themes and add some polish to things. In the meantime, check out the [repository](https://github.com/scottdorman/microsoft-terminal-settings), [open a new issue](https://github.com/scottdorman/microsoft-terminal-settings/issues/new) for your favorite color scheme or terminal profile or, better yet, [fork the repository](https://github.com/scottdorman/microsoft-terminal-settings/fork) to submit your own pull requests.
