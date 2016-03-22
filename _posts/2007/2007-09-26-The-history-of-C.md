---
layout: post
title: The history of C#
date: 2007-09-26 12:13:39 -04:00
---

I just came across a very interesting post from [James Kovacs](http://www.jameskovacs.com/blog/CNETHistoryLesson.aspx ".NET History Lesson") that describes how C# and .NET evolved. I had [blogged]({% post_url /2006/2006-11-27-99231 %}) about this almost a year ago, but James' post adds some additional background.

Around 1997, Microsoft started a project that was internally known as [Project Lightning](http://en.wikipedia.org/wiki/List_of_Microsoft_codenames "http://en.wikipedia.org/wiki/List_of_Microsoft_codenames") (and also known as Project 42). The name "Project 42" was most likely because DevDiv (the Microsoft Developer Division) is in Building 42, which (as James points out) is probably an homage to [The Hitchhiker's Guide to the Galaxy](http://www.amazon.com/gp/redirect.html?ie=UTF8&location=http%3A%2F%2Fwww.amazon.com%2FUltimate-Hitchhikers-Guide-Complete-Novels%2Fdp%2F0517226952%3Fie%3DUTF8%26s%3Dbooks%26qid%3D1190822000%26sr%3D8-1&tag=scotdorm-20&linkCode=ur2&camp=1789&creative=9325) by Douglas Adams.

There were several names being considered, one of which was the COM Object Runtime (COR), which is where the name for the mscorlib.dll assembly came from. This is the assembly which contains all of the CLR's main types and is really the only one that must be loaded by every .NET app domain.

Speaking of assembly loading, the code name for the CLR Loader is Fusion, which provides the name for the Assembly Log Binding Log Viewer utility - fuslogvw.exe: **Fus**ion Assembly **Log** **V**ie**w**er.

The codename of C# was [Project Cool](http://www.jameskovacs.com/blog/ct.ashx?id=1f081e93-297b-492a-86b8-4bed6e42e977&url=http%3a%2f%2fwww.theregister.co.uk%2f2000%2f09%2f12%2fofficial_microsofts_csharp_is_cool%2f) and was supposedly a "clean-room" implementation of Java. It was later changed to C# based on a musical scale. Just as C++ added the "++" to "C" since it was considered to be "adding to" or "one greater than" C, the sharp (#) on a musical scale means one semi-tone above the note. So, in both cases the name implies one above or higher than the original.

This musical theme continues today, as there are two MS Research languages that follow this same scheme: [F#](http://research.microsoft.com/fsharp/fsharp.aspx) and [Polyphonic C#](http://research.microsoft.com/~nick/polyphony/?0sr=a) (which is now part of [Cω](http://research.microsoft.com/comega/)).
