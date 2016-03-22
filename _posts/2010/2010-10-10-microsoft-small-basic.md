---
layout: post
title: Microsoft Small Basic
date: 2010-10-10 14:54:39 -04:00
---

If you have children and want them to learn programming at an early age (recommended age is between 10 and 16), you should check out [Microsoft Small Basic](http://msdn.microsoft.com/en-us/beginner/ff384126.aspx), which combines a simple language and a rich set of libraries together with a friendly development environment.

![Small Basic Screen Shot](http://i.msdn.microsoft.com/ff384126.smallbasicscreenshot(en-us).jpg)

The Small Basic language draws its inspiration for an early version of BASIC but it is actually based on the .NET Framework. Like the early variants of BASIC it is based on, Small Basic is imperative and doesn't use or expose beginners to concepts like scopes, types, object orientation, etc.

Even though it is based on the .NET Framework, it really is small and consists of just 14 keywords. In fact, there really isn’t a type system. You can create string and numeric constants and assign them to variables. Operations performed on these variables will be interpreted according to the content. All variables are global and are always initialized, so they can be used before they're assigned.

You can even make use of events by creating a sub-routine and assigning it to an event. This will wire the it up to an the event.

Small Basic also contains libraries which provide static "Objects" that group operations, properties and events. New libraries can be created using other .Net Languages and added to the Small Basic runtime.

Since Small Basic is, well, small, it shouldn’t be considered the language of choice for solving every conceivable problem. It focuses on a beginner persona, and as such doesn’t contain features that don’t cater to that persona. The compiler and the environment do allow 3rd party Small Basic libraries to be plugged in, extending the possibilities of what you can do from within Small Basic. When you are ready to “graduate” to a more complete programming language and environment, you can easily export your Small Basic program to Visual Basic.

Although there are other beginner focused programming languages, like [Scratch](http://scratch.mit.edu/) and [Alice](http://www.alice.org/) they are different than Small Basic. Both Scratch and Alice are great tools that help beginners learn the concepts of programming by enabling people to write "codeless" programs. Small Basic takes a different approach by introducing code as a first class concept.

Possibly the best part of Small Basic (at least in my opinion) is the support for Turtle Graphics, which is something I first learned as a child. I’m definitely looking forward to what becomes of Small Basic and using it teach my son programming when he gets older.
