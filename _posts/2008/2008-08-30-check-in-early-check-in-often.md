---
layout: post
title: Check In Early, Check In Often
date: '2008-08-30 11:32:40 -05:00'
---

[Jeff Atwood](http://www.codinghorror.com/blog/archives/001165.html) talks about what he considers the "Golden Rule" of source control:

> Check in early, check in often.

For Jeff, it seems, going more than 1 day without checking in code is too long and will cause integration headaches down the road. I completely agree with this sentiment, and the idea of [not going dark](http://www.codinghorror.com/blog/archives/001134.html), up to a point. Where Jeff's arguments start to fail is long-running development tasks that have large (or fundamental) impact on an existing code-base, particularly one that is heavily used.

Ordinarily, you would think that these large changes should absolutely be in source control, to which I would say "Yes, as long as you have a private area to check them in." This "private" area could be a dedicated branch, a TFS shelfset, or even a completely new project or repository. The idea here is that while you still want the benefits of source control, you don't want to be checking in changes (breaking or not) to the main-line development trunk to prevent incomplete changes from finding their way into an internal release and to allow you the ability to fix bugs on the main-line trunk without trying to figure out exactly what is safe to check in and what isn't.

There are, obviously, drawbacks to this approach as well. You will almost certainly run in to merge conflicts down the road when you are ready to check in against the main development trunk. There may also be cases where a bug needs to be fixed in multiple locations. Sometimes, problems like this just can't be avoided.

I think making blanket statements such as "don't go dark" and having "empty stubs and basic API skeletons in place" are ideals but they should be tempered by the realities of your project, the scope of the changes being made and the maturity (age) of the code base.
