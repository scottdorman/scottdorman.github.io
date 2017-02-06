---
layout: post
title: OpenGauntlet Project
date: '2007-12-19 21:12:13 -05:00'
---

One of the new features that will be available as part of the Visual Studio "Rosario" release is called "Gated Checkin". This is based on an internal tool that Microsoft uses called Gauntlet. Gauntlet was originally created in 1996 by the IE team, but is now used fairly widely in a few different variations. The idea behind gated checkin is that it helps prevent build breaks by verifying the changes before the checkin occurs and rejecting them if something fails. Continuous integration also provides features that help identify build breaks as soon as after the checkin as possible.  

OpenGauntlet is an open-source add-on for Microsoft's [Team Foundation Server](http://msdn2.microsoft.com/en-us/teamsystem/aa718934.aspx) which provides the gated checkin feature now. OpenGauntlet works because users are not allowed to check code directly into source control. Instead, they shelve their changes with a specific naming prefix when they are ready to check some changes in, and OpenGauntlet unshelves their changes into a temporary workspace, checks the changes compile and pass unit tests, and then checks the changes into source control under the requesting developer's username.

This avoids the problems associated with large development teams whereby a single developer will check in non-compiling code, which subsequently causes delays in the development life cycle as the team waits for the issues to be resolved. It can also be configured to disallow check ins if the proposed code changes break the unit tests. This can speed up the overall development portion of the project lifecycle, increase code quality, and reduce intra-team tensions and frustration due to poor code reviewing. The responsibility is shifted onto the individual developers to check and maintain the quality of their code without affecting the rest of the development team.

This is the first time I've heard about a system like this but it sounds like an interesting idea and is one that I hope to explore in more detail.
