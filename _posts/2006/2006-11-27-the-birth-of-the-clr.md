---
layout: post
title: The Birth of the CLR
date: 2006-11-27 13:37:00 -05:00
---

I recently came across the blog of [Patrick Dussud](http://blogs.msdn.com/patrick_dussud/default.aspx "CLR, architectures, and stuff"), who is the lead architect of the CLR/UIFX group. His first (and currently only post) discusses his role in the birth of the .NET CLR. There is a link to a [mailing list archive](http://discuss.develop.com/archives/wa.exe?A2=ind0008&L=DOTNET&P=R9831&I=-3 "DOTNET Archives - August 2000 (#106)") that also gives some more background.

In a nutshell, the CLR was born out of the COM+ team, created by merging the MTS and COM teams, and some of the people from the JVM team. The COM+ team was working on the next generation of COM, then called COM 2.0 and the JVM guys were realizing that the JVM was not going to give them the support for other languages and the flexibility they were looking for. Combine this with disagreements on some fundamental technology issues, such as object management and garbage collection, and you end up with two teams: COM+ and CLR.

The CLR team was also eventually joined by people from other Microsoft teams, including some of the C++ teams, which helped with the evolution of the IL instruction set, which is based on the Microsoft p-Code instruction set introduced in MSVC 5.0.

Perhaps the most interesting aspect of this is that the initial architecture and prototype for the Garbage Collector was written first in Common Lisp. Unfortunately, Patrick doesn't give a reason for this.
