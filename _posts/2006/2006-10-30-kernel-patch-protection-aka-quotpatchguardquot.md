---
layout: post
title: Kernel Patch Protection aka &quot;PatchGuard&quot;
date: 2006-10-30 17:06:00 -05:00
---

If anyone has been following this technology closely, there have been a lot of complaints by some of the security vendors regarding PatchGuard. I first heard about this technology at TechEd 2006 in a lot of the Vista sessions.

The recent controversy caused me to do a little more research in to this technology and the issues surrounding it.

The official name for this technology is called Kernel Patch Protection (KPP) and it's purpose is to increase the security and stability of the Windows kernel. KPP was first supported in Windows Server 2003 SP1, Windows XP, and Windows XP Professional Edition. The important thing to understand about this support is that it is for *<font color="#ff0000">x64 architectures only</font>*. 

KPP is a direct outgrowth of both customer complaints regarding the security and stability of the Windows kernel and Microsoft's [Trustworthy Computing](http://www.wired.com/news/business/0,1367,49826,00.html "Wired News: Bill Gates: Trustworthy Computing") initiative, announced in early 2002. 

In order to understand the controversy surrounding KPP, it is important to understand what KPP actually is and what aspects of the Windows operating system it deals with.

### What is the Kernel?

The kernel is the "heart" of the operating system and is one of the first pieces of code to load when the operating system starts. Everything in Windows (and almost any operating system, for that matter) runs on a layer that sits on top of the kernel. This makes the kernel the primary factor in the performance, reliability and security of the entire operating system.

Since all other programs and many portions of the operating system itself depend on the kernel, any problems in the kernel can make those programs crash or behave in unexpected ways. The "Blue Screen of Death" (BSoD) in Windows is the result of an error in the kernel or a kernel mode driver that is so severe that the system can't recover.

### What is Kernel Patching?

According to Microsoft's [KPP FAQ](http://www.microsoft.com/whdc/driver/kernel/64bitpatch_FAQ.mspx "Kernel Patch Protection: Frequently Asked Questions"), kernel patching (also known as kernel "hooking") is

> the practice of using internal system calls and other unsupported mechanisms to modify or replace code or critical structures in the kernel of the Microsoft Windows operating system with unknown code or data. "Unknown code or data" is any code or data that is not provided by Microsoft as part of the Windows kernel.

What exactly, does that mean? The most common scenario is for programs to patch the kernel by changing a function pointer in the system service table (SST). The SST is an array of function pointers to in-memory system services. For example, if the function pointer to the NtCreateProcess method is changed, anytime the service dispatch invokes NtCreateProcess, it is actually running the third-party code instead of the kernel code. While the third-party code might be attempting to provide a valid extension to the kernel functionality, it could also be malicious.

Even though almost all of the Windows kernels have allowed kernel patching, it has always been an officially unsupported activity.

Kernel patching breaks the integrity of the Windows kernel and can introduce problems in three critical areas:

*   **Reliability**  
Since patching replaces kernel code with third-party code, this code can be untested. There is no way for the kernel to assess the quality of intent of this new code. Beyond that, kernel code is very complex, so bugs of any sort can have a significant impact on system stability.  

*   **Performance**  
The overall performance of the operating system is largely determined by the performance of the kernel. Poorly designed third-party code can cause significant performance issues and can make performance unpredictable.  

*   **Security**  
Since patching replaces known kernel code with potentially unknown third-party code, the intent of that third-party code is also unknown. This becomes a potential attack surface for malicious code. 

### Why Kernel Patch Protection?

As I mentioned earlier, the primary purpose of KPP is to protect the integrity of the kernel and improve the reliability, performance, and security of the Windows operating systems. This is becoming increasingly more important with the prevalence of malicious software that is implementing "root kits". A root kit is a specific type of malicious software (although it is usually included as a part of another, larger, piece of software) that uses a variety of techniques to gain access to a computer. Increasingly, root kits are becoming more sophisticated and are attacking the kernel itself. If the rootkit can gain access to the kernel, it can actually hide itself from the file system and even from any anti-malware tools. Root kits are typically used by malicious software, however, they have also been used by large legitimate businesses, including [Sony](http://www.wired.com/news/privacy/0,1848,69601,00.html "Wired News: Real Story of the Rogue Rootkit").

While KPP is a good first step at preventing such attacks, it is not a "magic bullet". It does eliminate one way to attack the system...patching kernel images to manipulate kernel functionality. KPP takes the approach that there is no reliable way for the operating system to distinguish between "known good" and "known bad" components, so it prevents anything from patching the kernel. The only official way to disable KPP is by attaching a kernel debugger to the system.

KPP monitors certain key resources used by the kernel to determine if they have been modified. If the operating system detects that one of these resources has been modified it generates a "bug check", which is essentially a BSoD, and shuts down the system. Currently the following actions trigger this behavior:

*   Modifying system service tables.
*   Modifying the interpret descriptor table (IDT).
*   Modifying the global descriptor table (GDT).
*   Using kernel stacks that are not allocated by the kernel.
*   Patching any part of the kernel. This is currently detected only on AMD64-based systems. 

### Why x64?

At this point, you may begin to wonder why Microsoft chose to implement this on x64 based systems only. Microsoft is again responding to customer complaints in this decision. Implementing KPP will almost certainly impact comparability of many legitimate software, primarily security software such as anti-virus and anti-malware tools, which were built using unsupported kernel patching techniques. This would cause a huge impact on the consumer and also on Microsoft's partners. Since x64-based machines still make up the smaller install base (although they are gaining ground rapidly) and the majority of x64-based software has been rewritten to take advantage of the newer architecture, the impact is considered to be substantially smaller. 

### So...why the controversy?

Since KPP prevents an application or driver from modifying the kernel, it will, effectively, prevent that application or driver from running. KPP in [Vista x64](http://www.microsoft.com/whdc/system/platform/64bit/kmsigning.mspx "Digital Signatures for Kernel Modules on x64-based Systems Running Windows Vista") requires any application drivers be digitally signed, although there are some non-intuitive ways to turn that off. (Turning off signed drivers does prevent certain other aspects of Windows from operating, such as being able to view DRM protected media.) However, all that really means is anyone with a legitimately created company and about $500 per year to spend can get the required digital signature from [VeriSign](http://www.verisign.com/products-services/security-services/code-signing/digital-ids-code-signing/features-benefits.html "Code Signing Digital IDs - Features & Benefits"). Unfortunately, even it is a reputable company, it still doesn't provide any guarantees as to the reliability, performance, and security of the kernel.

In order for software (or drivers) to work properly on an operating system that implements KPP, the software must use Microsoft-documented interfaces. If what you are trying to do doesn't have such an interface, then you cannot safely use that functionality. This is what has lead to the controversy. The security vendors are saying that the interfaces they require are not publicly documented by Microsoft (or not yet at any rate) but that Microsoft's own security offerings (Windows OneCare, Windows Defender, and Windows Firewall) are able to work properly and use undocumented interfaces. The security vendors want to "level the playing field".

There are many arguments on both sides of the issue, but it seems that many of them are not thought out completely. Symantec and McAfee have argued that the legitimate security vendors be granted exceptions to KPP using some sort of signing process. (See the [TechWeb article](http://www.techweb.com/showArticle.jhtml?articleID=193300261&cid=RSSfeed_TechWeb "Microsoft Stands Frim on PatchGuard - Technology News by TechWeb").) However, this is fraught with potential problems. As I mentioned earlier, there is currently no reliable way to verify that code is actually from a "known good" source. The closest we can come to that is by digital signing, however, a piece of malicious code can simply include enough pieces from a legitimate "known good" source and hook into the exception.

So lets say, for arguments sake, that Microsoft does relent and is able to come up with some sort of exception mechanism that minimizes (or even removes) the chance of abuse. What happens next? Windows Vista, in particular, already includes an array of new features to provide security vendors ways to work within the KPP guidelines. 

The [Windows Filtering Platform](http://www.microsoft.com/whdc/device/network/WFP.mspx "Windows Filtering Platform") (WFP) is one such example. WFP enables software to perform network related activities, such as packet inspection and other firewall type activities. In addition to WFP, Vista implements an entirely new TCP stack. This new stack has some fundamentally different behavior than the existing TCP stack on Windows. We also have network cards that implement hardware based stacks to perform what is called "chimney offload", which effectively bypasses large portions of the software based TCP stack. Hooking the network related kernel functions (as a lot of software based firewalls currently do), will miss all of the traffic on a chimney offload based network card. However, hooking in to WFP will catch that traffic.

Should Microsoft stop making technological innovations in the Windows kernel simply because there are a handful of partners and other ISVs that are complaining? The important thing to realize is that KPP is not new in Windows Vista. It has been around since Windows XP 64-bit edition was released. Why is it now that the security vendors are realizing that their products don't work properly on the x64-based operating systems? The main point Microsoft is trying to get across is that most of the functionality required doesn't have to be done in the kernel. Microsoft has been working for the last few years trying to assist their security partners in making their solutions compatible. If there is an interface that isn't documented, or functionality that a vendor believes can only be accomplished by patching the kernel, they can contact their Microsoft representative or email [msra@microsoft.com](mailto:msra@microsoft.com) for help finding a documented alternative. According to the [KPP FAQ](http://www.microsoft.com/whdc/driver/kernel/64bitpatch_FAQ.mspx "Kernel Patch Protection: Frequently Asked Questions"), "if no documented alternative exists...the functionality will not be supported on the relevant Windows operating system version(s) that include patch protection support."

I think the larger controversy is the fact that there are now documented ways to break KPP. This is where Microsoft and it's security partners and other security ISVs should be spending their time and energy. If we are going to have a reliable and secure kernel, we need to focus on locking down the kernel so that no one is able to breach it, including the hackers. This is an almost endless process, as the attackers generally have almost infinite amounts of time to bring their "products" to market and don't really have an quality issues to worry about. Even with the recent introduction by Intel and AMD of hardware based virtualation technology (which essentially creates a virtual mini-core processor that can run a specially created operating system), there is still a [long way to go](http://theinvisiblethings.blogspot.com/2006/06/introducing-blue-pill.html "Introducing Blue Pill").

### What's next?

While it is important to understand the goals of KPP and the potential avenues of attack against it, the most important thing for the security community to focus on is in making sure that the Windows kernel stays safe. The best way to do this is to keep shrinking the attack surface until it is almost non-existent. There will always be an attack surface, however, the smaller that surface becomes the easier it is to protect. Imagine guarding a vault. If there is only one way in and out, and that entrance is only 2-feet wide it is much more easily guarded than a vault that has 2 entrances, each of which are 30-feet wide.

However, as malware technology advances it is important for the security technology that tries to protect against it to advance as well. In fact, the security technology really needs to be ahead of the malware if it is to be successful. PatchGuard has already been [hacked](http://uninformed.org/index.cgi?v=3&a=3 "Bypassing PatchGuard on Windows x64"), some of the proposed Microsoft APIs for KPP [won't be available until sometime in 2008](http://www.techweb.com/showArticle.jhtml;jsessionid=CZB20KNRYZ1X0QSNDLRSKH0CJUNN2JVN?articleID=193401077 "McAfee, Microsoft Trade Insults Over Vista - Technology News by TechWeb"), and the security vendors do have legitimate reasons for needing to access certain portions of the kernel.

Host Intrusion Prevention Systems (HIPS), for instance, uses kernel access to prevent certain types of attacks, such has buffer overflow attacks or process injection attacks, by watching for system functions being called from memory locations where they shouldn't be called. The [Code Red Worm](http://www.ciac.org/ciac/bulletins/l-117.shtml "Code Red Worm") would not have been detected if only file-based protection systems were in use.

The bottom line is that the malware vendors are unpredictable and not bound by any legal, moral, or ethical constraints. They are also not bound by customer reviews, deadlines, and code quality. The security vendors and Microsoft need to work together to ensure that the attack surface for the kernel and Windows itself is small and stays small. They can do this by:

*   Establishing a more reliable way to authenticate security vendors and their products that will prevent "spoofing" by the malware vendors.
*   Minimizing the attack surface of the Windows Kernel.
*   Establishing documented APIs to interact with the kernel to perform security related functions, such as firewall activities.
*   Enforcing driver signatures...in other words, don't allow this mechanism to be turned off. At least don't allow it to be turned off for certain security critical drivers.
*   Enforcing security software digital signatures. If you want your security tool to run, it must be signed. Again, don't allow this mechanism to be turned off.
*   Establishing a more secure way for the security products to hook in to the kernel.
*   Restricting products to patching only specific areas of the kernel. Currently, it is possible to [patch almost any portion of the kernel](http://uninformed.org/index.cgi?v=4&a=4 "What Were They Thinking?").
*   Enforcing Windows certification testing for any security products.
