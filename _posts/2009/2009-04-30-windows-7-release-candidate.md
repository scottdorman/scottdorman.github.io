---
layout: post
title: Windows 7 Release Candidate
date: '2009-04-30 09:07:17 -05:00'
---

Microsoft has reached a critical milestone in the Windows 7 development cycle with the limited release of the Windows 7 Release Candidate (RC) today for Microsoft TechNet and MSDN subscribers and general availability from the Microsoft Download Center on May 5th.

There has been a lot of excitement about Windows 7 and, so far, the excitement has been justified. The Windows 7 RC comes after extensive beta testing and feedback from the MVP community with a lot of enhancements and bug fixes since the last beta release. Some Windows 7 beta facts:

*   Over 2000 MVPs participated in the beta on Connect. 
*   MVPs contributed and filed over 700 bugs in the first week the beta was released. 
*   Engineering fixed over 2000 bugs during the first two weeks. 
*   The Windows 7 Forum was the premier destination support beta testers with over 25k posts in the first month 
*   Windows 7 Beta forums success continues to be moderated by 100+ MVPs. 
*   Windows 7 Beta forums answer rate soars to 88% on a volume of more than 40,000 posts. 
*   Highlights of positive feedback from beta testers:  Windows 7 beta speed / responsiveness, taskbar, and UX are top rated early features.   

**Reporting Bugs on Windows 7 RC**

The Windows 7 Feedback Tool is a pre-release only tool.  As a result, Microsoft has removed the launch UI for the Feedback Tool, however the tool itself is still in the RC build.  If you need to report a bug that falls into one of the categories mentioned below, you may run the following command to start the Feedback Tool: 

```
rundll32.exe FeedbackTool.dll,ShowWizard
```

If you would rather, you may create a desktop shortcut to the Feedback Tool command by right-clicking on your desktop, selecting New, Shortcut, then entering  "rundll32.exe FeedbackTool.dll,ShowWizard" (less the quotes) in the "Type the location of the item" field.  Then click Next, provide a shortcut name (for example, "Send Feedback"), then click Finish.  You may then launch the Feedback Tool from the desktop shortcut.

<div class="alert alert-info">**Note - Please be sure you have activated your copy of Windows 7 using your product key PRIOR to using the Windows Feedback Tool.**</div>

While testing indicates that the Release Candidate is a very solid build Microsoft does ask that you be on the lookout for any issues that might remain. <u>When filing bugs on Windows 7 RC only report the following types of issues:</u>

*   Issues that prevent installation or upgrade 
*   Any issues that involve corruption or data loss 
*   Security issues 
*   Regressions from Beta (Things worked in beta but do not work now) 
*   Any application or device issues that would prevent you from using Windows 7 as your primary OS. 
*   Reproducible crashes or hangs (issues that you cannot reproduce will be captured by CEIP Telemetry)   

**Additional Information**

> **Q:** How can I get access to the build?
>
> **A:**  TechNet and MSDN subscribers will have access to the build on those websites close to April 30th. All others can download the RC on the Microsoft Download Center on May 5th.
> 
> **Q:** How big is the Window 7 RC download?
>
> **A:** The x86 version of Windows 7 RC is approximately 2.47 gigs. The x64 version is approximately 3.2 gigs.
> 
> **Q:** Will the RC code be download-only, or can I have physical media mailed to me?
>
> **A:** The Windows 7 RC code will only be available for download.  
>
> **Q:** Will my product key from Beta work for the RC, or do I have to register to get a new one?
>
> **A:** No – you will need to register for a new PID in order to run RC. 
> 
> **Q:** Is there a cap to the total number of downloads for Windows 7 RC?
>
> **A:** There is no limit to the total number of downloads for Windows 7 RC.
>
> **Q:** Will Windows 7 RC be available in both 32-bit and 64-bit?
>
> **A:** Yes. 
> 
> **Q:** Is there a choice of SKUs for Windows 7 RC, or is it only available in Ultimate like the beta?
>
> **A:** There is one release candidate release, with all the capabilities of the Windows 7 Ultimate SKU.  
> 
> **Q:** When does this build expire?
>
> **A:** Windows 7 RC will expire on March 1, 2010 – at this time the system will reboot every two hours. The license of windows 7 RC will expire June 1, 2010.
> 
> **Q:** Where should I submit feedback on Windows 7 RC?
>
> **A:** The Beta testing has completed, and the release candidate is the time for customers and IT professionals to really start kicking the tires in terms of application compatibility, drivers and devices.  We will of course continue error monitoring, but application compatibility issues should be reported to the ISV. 
> 
> **Q:** What tools and resources are there available for IT pros to begin testing and deploying Windows 7?
>
> **A:** There are many tools available for IT Pros to begin their testing and deployments, including the Windows Automated Installation Kit, the Application Compatibility Toolkit and the Deployment Toolkit.  More information about these tools can be found at [www.microsoft.com/springboard](http://www.microsoft.com/springboard)

> ***Upgrade Experience***
> 
> **Q:** How does Microsoft recommend I install RC?
>
> **A:** To install the Windows 7 RC, users will be required to either upgrade from a Windows Vista image, or do a custom (clean) installation.  Windows 7 Beta users will need to do a custom (clean) installation.
> 
> **Q:** Why isn't there an easy way for me to upgrade from beta to RC?
>
> **A:** Upgrading from one pre-release build to another is not a scenario a real-world customer will experience.  We want our testers to experience real-world setup to provide us with real-world telemetry as we work on finalizing the product.
> 
> **Q:** Is there a smooth upgrade from Windows XP to Windows 7?
>
> **A:** As a result of the many changes we've made to the operating system, users who wish to upgrade from Windows XP to Windows 7 on the same computer will need to perform a custom (clean) installation.
> 
> **Q:** Does Microsoft provide any guidance on how to transfer files and settings from a previous operating system to Windows 7 when a clean installation is required?
>
> **A:** Tools, guidance and other resources are available on [windows.microsoft.com](http://www.microsoft.com/) to assist in the upgrade process.  Microsoft also provides a special utility on the release candidate CD to assist users with identifying, backing up and transferring files and settings to Windows 7.  For more information on the Windows Easy Transfer utility please visit [http://technet.microsoft.com/en-us/library/dd446674.aspx](http://technet.microsoft.com/en-us/library/dd446674.aspx).
