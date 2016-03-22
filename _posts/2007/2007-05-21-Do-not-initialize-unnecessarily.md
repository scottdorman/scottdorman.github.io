---
layout: post
title: Do not initialize unnecessarily
date: 2007-05-21 15:17:21 -04:00
---

If any one has ever run FxCop or Visual Studio Code Analysis (yes, I know they are basically the same thing, but there are some subtle differences) you have probably run into rule CA1805: Do not initialize unnecessarily.

As I was cleaning up some FxCop errors on some inherited code today, I hit a few of these. These errors are probably one of the easiest to correct, but for some uknown reason I decided to actually look at the [error help](ms-help://MS.VSCC.v80/MS.MSDN.v80/MS.VSENT.v80.en/dv_vsetsa03/html/b5279c9e-068c-484a-966d-d7126a810301.htm) this time around.

What I saw there surprised me. The help page has all of the standard FxCop sections:

*   Cause
*   Rule Description
*   How to Fix Violations
*   When to Exclude Warnings
*   Example 

It is the "When to Exclude Warnings" that surprised me. Keep in mind that this rule falls under the Microsoft.Performance category. Knowing that, it is relatively safe to assume that if you are actually paying attention to this rule that you have some level of concern for performance. (This should cover even those who simply accept the default behavior of checking against all rules.)

The reasons provided for excluding this violation are as follows:

1.  Exclude a warning from this rule if the constructor calls another constructor in the same or base class that initializes the field to a non-default value.
2.  It is also safe to exclude a warning from this rule, or disable the rule entirely, if performance and code maintenance are not priorities. 

To me, #2 seems to defeat the purpose of the rule. As I said, if you're looking at this violation, chances are you are interested in performance (at least on some level). That being said, why would you be looking at this rule if you weren't concerned with performance and maintenance.

Taking this to the next logical step...why aren't you concerned with performance and maintenance? These rules should be excluded only under very controlled circumstances and done with a good understanding of the implications.
