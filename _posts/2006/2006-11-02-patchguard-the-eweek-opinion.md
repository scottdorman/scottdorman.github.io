---
layout: post
title: PatchGuard, the eWEEK opinion
date: 2006-11-02 16:44:00 -05:00
---

eWEEK Security Center Editor [Larry Seltzer](http://www.eweek.com/author_bio/0,1908,a=2299,00.asp "eWEEK - Author Bio") just published an [article](http://www.eweek.com/article2/0,1895,2049960,00.asp "What PatchGuard Really Breaks") on eWEEK.com providing his opinion on the benefits, and limitations, of PatchGuard.

In the article, Larry reiterates some of the points I made in my [post](http://geekswithblogs.net/sdorman/archive/2006/10/30/95540.aspx "Kernel Patch Protection aka "PatchGuard"") on PatchGuard a few days ago, namely:

*   *Only 64-bit Windows versions are affected by PatchGuard.*
*   *64-bit Windows versions, especially desktop versions, have puny market share.*
*   *The problems are limited to what can generally be called HIPS (Host Intrusion Prevention Systems).*
*   *Conventional security protection is unaffected by PatchGuard.*
*   *There is no documented, supported way for vendors to implement key HIPS functions in the face of PatchGuard.* 

As Larry mentions, HIPS primarily focuses on behavior blocking. In order to do that, it needs the ability to monitor certain kernel information such as the creation and manipulation of processes, image loading, and the creation of movement of memory.

The important thing to realize here is that most of the current security products (with the exception of those that are only HIPS products or that include HIPS features, which won't work on 64-bit Windows) will work just fine as they shouldn't be using anything that triggers interference from PatchGuard.

Yes, the security vendors that rely on HIPS do run in to the proverbial "brick wall" with PatchGuard. However, by removing the restrictions put in place by PatchGuard we are creating an inherently less secure environment. As I mentioned in my earlier post, one of the primary goals of PatchGuard is to ensure the integrity and security of the kernel.

The reality of the story is that as Microsoft is working to make Windows more secure by restricting the amount of access to kernel, the security industry publicly says "great" but internally cringes as it directly impacts their business. The unfortunate truth of this is that while some vendors are working to create products that [circumvent PatchGuard](http://www.eweek.com/article2/0,1895,2037052,00.asp "Microsoft Decries Vista PatchGuard Hack") (essentially hacking their way in to the kernel) they are giving credibility to the hacker community and proving in no uncertain terms that PatchGuard is vulnerable.

The fact that PatchGuard is vulnerable should not come as a surprise. It is virtually impossible to write an operating system that is actually usable and not have some level of vulnerabilities. According to [CERT](http://www.cert.org/stats/ "CERT/CC Statistics"), for this year alone (Q1-Q3) there have been 5,340 vulnerabilities reported. Compare this to 345 reported 10 years ago.

All this is telling us is that as the complexity in operating systems and applications increases, so does the number of vulnerabilities. As the malware vendors have almost limitless amounts of time and resources to create malware, this trend will only increase (at least for the foreseeable future).

The longer we draw out debates over issues like PatchGuard, the longer it will take to create a more secure operating system. As a whole, the security industry has played catch-up to the malware industry. Rather than about the fact that legitimate security vendors are being "locked out" of hacking the kernel, we need to realize that while the legitimate vendors are being locked out, so also are the malware vendors. Rather than finding ways to circumvent PatchGuard, the industry needs to be finding ways to strengthen it.
