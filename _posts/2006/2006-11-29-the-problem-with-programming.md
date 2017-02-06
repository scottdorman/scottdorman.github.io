---
layout: post
title: The Problem with Programming
date: '2006-11-29 13:37:00 -05:00'
---

Yesterday, the Technology Review published an [interview](http://www.technologyreview.com/InfoTech/17831/page1/ ) with [Bjarne Stroustrup](http://parasol.tamu.edu/people/bs/). It is an interesting interview, but I think it leaves out some important aspects of the real problems.

> I think the real problem is that "we" (that is, we software developers) are in a permanent state of emergency, grasping at straws to get our work done. We perform many minor miracles through trial and error, excessive use of brute force, and lots and lots of testing, but--so often--it's not enough.

While this is certainly true, it doesn't address the more fundamental issues that cause us to work this way. In many cases, we end up working in a "state of emergency" because of unrealistic deadlines imposed by management, lack of thorough QA testing (or any QA testing in some cases), decisions to release the software "early", and unchecked scope creep.

> Software developers have become adept at the difficult art of building reasonably reliable systems out of unreliable parts. The snag is that often we do not know exactly how we did it: a system just "sort of evolved" into something minimally acceptable. Personally, I prefer to know when a system will work, and why it will.

I agree...I want to know when a system will work and why it will work as well. Again, it goes to my earlier point of addressing why we have become "adept at...building reasonably reliable systems out of unreliable parts." I think it is, in some ways, a testament to the ingenuity and capability of a group of really talented developers to be able to create something that works at all under these conditions.

As the interviewer asks, "How can we fix the mess we are in?", I have to wonder about Bjarne's answer.

> In theory, the answer is simple: educate our software developers better, use more-appropriate design methods, and design for flexibility and for the long haul. Reward correct, solid, and safe systems. Punish sloppiness.

I think this is grossly understating things. I think that a competent, experienced, professional developer already wants to do these things. I don't know many people that actually enjoy spending their time creating something that they know someone else has already done (and possibly done better) when they could be focusing their efforts on parts of the project that are actually important. The best example that comes to mind is logging. How many times have we created routines (or even whole libraries) to do application run-time logging? There are lots of well-tested frameworks available (some commercial, some open-source) that do this, so why should we do it again?

This eventually leads to questions of code reuse, shared libraries, etc. The reality of shared libraries is that they are not difficult to develop. They are difficult to **manage**. A good rule for a shared library is that if the same operation is repeated 3 or more times in a project or multiple projects, it is a good candidate for a shared library. That's the easy part. The hard part is deciding who will have access to make code changes to the library, who will be responsible for reviewing the code, who is responsible for enforcing that the library is used by the projects and approving the inevitable exceptions.

I have been in a lot of places that think sharing code follows the principles of reusability. In a very general sense, it does. Sharing code does allow you to reuse code someone else has written, but this is almost always done at a source code level. You include the relevant file (or files) in to your own project and compile them along with the rest of your code. 

So far, so good, right? Wrong!

The problem here is that you now have multiple copies of the same code scattered throughout your projects. If there is ever a bug discovered, you now have *n* number of places to make the exact same fix, assuming that the project hasn't made customizations/enhancements to the original code that aren't compatible with the change. Obviously, this issue is limited based on the scope. If you only have 2 projects this isn't as big a problem as if you had 20 projects. However, it can become an issue for your customers when you issue updates/upgrades/patches that require the entire product to be reinstalled to fix a simple bug.

There needs to be accountability of the developers writing the code, but there also needs to be accountability of the managers allowing such code to be written. Without the "buy in" from management that there is a "right" and a "wrong" way to develop applications, nothing is going to change. As Bjarne points out, 

> ...the degree of effective formal education of the average software developer has declined. However, the solution is not to dumb down the programming languages but to use a variety of programming languages and educate more experts.

I think this problem is not limited to software developers. Technology is pervasive in our everyday lives and our professional lives. As a result, things that were "hard" 20 years ago are now easy. What we have lost are the skills to solve those "hard" problems. 

A perfect example is the space program. During the Apollo 13 mission, an oxygen tank exploded which put the crew in jeopardy and almost cost them their lives. The crew, working with engineers at Mission Control in Houston, were able to jury rig makeshift carbon dioxide scrubbers and determine the exact amount of power needed to safely splash-down. I'm not saying that the engineers at Mission Control couldn't solve this problem today...the difference is that this happened in 1970, when slide-rules were still the instrument "du jour" of the engineering community and computers were reserved for "major efforts" like sending a rocket in to space. If we had to solve this same problem today without the use of calculators and other personal computing devices, would we be able to solve it as efficiently and as quickly?

At this point, the interview turns in to an exercise in trying to bait Bjarne in to admitting that he made a mistake in designing the C++ language. I think C++ has had some fundamental impacts on the way modern programming languages and programs are designed. 

> The purpose of a programming language is to help build good systems, where "good" can be defined in many ways. My brief definition is, correct, maintainable, and adequately fast. Aesthetics matter, but first and foremost a language must be useful; it must allow real-world programmers to express real-world ideas succinctly and affordably.

This is an important point. As Bjarne points out, a "good" system is:

*   correct
*   maintainable
*   adequately fast 

The issue of "adequately fast" has largely gone away with the advances in hardware, but it still needs to be a concern. I have seen many programs that "crawl" along because they are doing large amounts of string concatenation inside a tight loop, something that can be resolved with a little bit of thought as to the design and implementation.

The issue of "correct" is also an important one, but is a bit more subjective. Correct should be defined in terms of the business problem being solved. If the customer wants a mouse trap, but you build him a perfect rabbit cage, the solution is not correct.

Maintainability is another problem entirely. Part of this goes back to the earlier comments about code reuse. It is also directly related to unrealistic deadlines and scope creep. The amount and type of QA is also a factor. The best QA is a group that is not only familiar with the business requirements so they can do application testing, but is also familiar with the code so they can do code analysis and participate in code reviews. 

So, all of this being said, does Bjarne have any regrets over what C++ has become?

> No regrets! Well, of course I dream of what I might have done differently and better, but seriously, who am I to second-guess, say, 1984 vintage Bjarne? He may have been less experienced than I, but he was no less smart, probably smarter, and he had a better understanding of the word of 1984 than I have. C++ has been used to build many systems that enhance our lives, and it has been a significant positive influence on later languages and systems. That's something to be proud of.
