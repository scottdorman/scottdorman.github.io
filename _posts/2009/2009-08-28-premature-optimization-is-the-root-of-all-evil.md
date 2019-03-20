---
layout: post
title: Premature optimization is the root of all evil
date: '2009-08-28 22:24:41 -05:00'
tags: coding-style code-standards
---

I've lost count how many times I've heard that quote. It's a great quote said by one of the leading minds in computer programming and formal mathematics, [Donald Knuth](http://en.wikipedia.org/wiki/Donald_Knuth). The problem with this quote is that, like so many other things, people have only remembered (or only quote) a small portion of the entire thing.

To read the full quote, you need to look at a paper published in December 1974 titled <u>Structured Programming with go to Statements</u> in Computing Surveys.

The full quote is this (in reference to a loop optimization technique that provides a 12% performance improvement):

> The conventional wisdom shared by many of today's software engineers calls for ignoring efficiency in the small; but I believe this is simply an overreaction to the abuses they see being practiced by pennywise-
> and-pound-foolish programmers, who can't debug or maintain their "optimized" programs. In established engineering disciplines a 12% improvement, easily obtained, is never considered marginal; and I believe the same viewpoint should prevail in software engineering. Of course I wouldn't bother making such optimizations on a oneshot job, but when it's a question of preparing quality programs, I don't want to restrict myself to tools that deny me such efficiencies.
> 
> There is no doubt that the grail of efficiency leads to abuse. Programmers waste enormous amounts of time thinking about, or worrying about, the speed of noncritical parts of their programs, and these attempts at efficiency actually have a strong negative impact when debugging and maintenance are considered. We should forget about small efficiencies, say about 97% of the time: premature optimization is the root of all evil.
> 
> Yet we should not pass up our opportunities in that critical 3%. A good programmer will not be lulled into complacency by such reasoning, he will be wise to look carefully at the critical code; but only after that code
> has been identified. It is often a mistake to make a priori judgments about what parts of a program are really critical, since the universal experience of programmers who have been using measurement tools has been
> that their intuitive guesses fail. <small>(Computing Surveys, Vol. 6, No. 4, December 1974, p. 268 [p. 8 of the [PDF](http://pplab.snu.ac.kr/courses/adv_pl05/papers/p261-knuth.pdf)])</small>

While the overall sentiment could be summed up simply as "premature optimization is the root of all evil", I think the point being made here is that **well-known optimizations** can and should be applied otherwise time spent on optimizing code should be focused on that small percent of critical code and should be performed with quantitative means.

What are well-known optimizations? That partly depends on your programming language and partly on your problem domain. Optimizations specific to a problem domain are very domain specific and not easily communicated outside of that domain. However, language specific well-known optimizations are a different story.

Take string concatenation inside a loop, particularly for languages like C# where strings are immutable objects. Why is that important? Since strings are immutable, they cannot be changed once created. When concatenating two strings you incur overhead from the creation of temporary strings. For example, consider the following code:
 
```csharp
string s = "this is " + "a test.";
```

While this is an arbitrary example, in order for this line to execute it would be necessary to create 3 strings. (Yes, I know the compiler (and if not the compiler, the JIT) would optimize this to remove the concatenation, but pretend for a moment that it didn't.) Now, imagine this line running inside a loop 10 times. That loop has just created approximately 30 temporary string objects to perform that concatenation. In such a situation, it should be intuitive that the use of a `StringBuilder` to perform the string concatenation is preferable as you no longer have the intermediate string object creation and result in one allocation to create the `StringBuilder` and one allocation to convert the `StringBuilder` to an actual string object. There is always the possibility that while iterating through the loop the `StringBuilder` may need to perform a few additional buffer reallocations, but that still results in less overhead than creating immutable string objects.

The point here is that while it is true that premature optimization is the root of all evil, optimization should be a measured undertaking and well-known optimizations applied early are not premature.
