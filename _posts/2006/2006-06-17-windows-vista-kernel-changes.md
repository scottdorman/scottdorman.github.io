---
layout: post
title: Windows Vista: Kernel Changes
date: 2006-06-17 15:01:00 -04:00
---

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Windows Vista is coming and will be here sooner than some might think. By now you have probably seen the graphical changes coming in Vista with the new Aero and Aero Glass user interfaces (and the associated hardware needed to support them) and heard all about the new user account controls in Vista that are designed to make the operating system more secure. <?xml:namespace prefix="o" ns="urn:schemas-microsoft-com:office:office"?><o:p></o:p></span>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">But what about the “under-the-hood” changes in the <?xml:namespace prefix="st1" ns="urn:schemas-microsoft-com:office:smarttags"?><st1:place w:st="on">Vista</st1:place> kernel? Lots of exciting changes in Windows Vista kernel are being made in the areas of performance, scalability, reliability, and security. <o:p></o:p></span>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Early in the week, Mark Russinovich and David Solomon presented a talk on some of the new kernel features, including:<o:p></o:p></span>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span>

<ul style="MARGIN-TOP: 0in" type="disc"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">CPU Utilization Improvements<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Multimedia streaming improvements<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Resource Quotas<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">New Synchronization APIs<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Symbolic File Links<o:p></o:p></span><st1:place w:st="on"><st1:placename w:st="on"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial; mso-fareast-font-family: 'Times New Roman'; mso-ansi-language: EN-US; mso-fareast-language: EN-US; mso-bidi-language: AR-SA"> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in">I/O</li></span></st1:placename><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial; mso-fareast-font-family: 'Times New Roman'; mso-ansi-language: EN-US; mso-fareast-language: EN-US; mso-bidi-language: AR-SA"> <st1:placename w:st="on">Completion</st1:placename> <st1:placetype w:st="on">Port</st1:placetype></span></st1:place><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial; mso-fareast-font-family: 'Times New Roman'; mso-ansi-language: EN-US; mso-fareast-language: EN-US; mso-bidi-language: AR-SA">, Scalability, Cancellation, and Prioritization Improvements</span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial; mso-fareast-font-family: 'Times New Roman'; mso-ansi-language: EN-US; mso-fareast-language: EN-US; mso-bidi-language: AR-SA"></span>User Mode Driver Framework (UMDF)<o:p></o:p></li></li></li></li></li></li></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">SuperFetch<sup>TM</sup><o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">ReadyBoost<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">ReadyDrive<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Boot Configuration Database (BCD)<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Session 0 Isolation<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Interactive Logon Architecture<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Delayed Autostart services<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Clean Service Shutdown and Shutdown Ordering<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Reliable Sleep Transitions<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Kernel Transaction Manager<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Volume Shadow Copy<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Windows Error Reporting<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><st1:street w:st="on"><st1:address w:st="on"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">BitLocker<sup>TM</sup> Drive</span></st1:address></st1:street><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"> Encryption<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Code Integrity Verification<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Protected Processes<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Address Space Load Randomization (ASLR)<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Service Security Improvements<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">User Account Controls<o:p></o:p></span></li></li></li></li></li></li></li></li></li></li></li></li></li></li></li></li></li></li></ul>


<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Windows Server “Longhorn” will be a superset of the changes being made in <st1:place w:st="on">Vista</st1:place>. Many of the changes made in “Longhorn” will be merged back in to <st1:place w:st="on">Vista</st1:place> with Vista Service Pack 1. So right off the bat, we have the beginnings of the first service pack and the operating system hasn't even shipped.<o:p></o:p></span>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">For more information:<o:p></o:p></span>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Kernel Enhancements for Windows <st1:place w:st="on">Vista</st1:place> and Windows Server "Longhorn"<o:p></o:p></span>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">[http://www.microsoft.com/whdc/system/vista/kernel-en.mspx](http://www.microsoft.com/whdc/system/vista/kernel-en.mspx) <o:p></o:p></span>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">MSDN Vista developer resources<o:p></o:p></span>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">[http://msdn.microsoft.com/windowsvista/](http://msdn.microsoft.com/windowsvista/) <o:p></o:p></span>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Driver developer resources</span>

<ul>
<li>
<div class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Windows Hardware Developer Central<br></span><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">[http://www.microsoft.com/whdc/default.mspx](http://www.microsoft.com/whdc/default.mspx)</span><br></div>
<li>
<div class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">WinHEC 2006 presentations<br></span><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">[http://www.microsoft.com/whdc/winhec/](http://www.microsoft.com/whdc/winhec/)</span></div></li></li></ul>
