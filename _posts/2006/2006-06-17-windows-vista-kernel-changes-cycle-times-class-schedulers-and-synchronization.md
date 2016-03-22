---
layout: post
title: Windows Vista: Kernel Changes - Cycle Times, Class Schedulers and Synchronization
date: 2006-06-17 15:08:00 -04:00
---

<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Cycle Time Counter<?xml:namespace prefix="o" ns="urn:schemas-microsoft-com:office:office"?><o:p></o:p></span></b></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Prior to <?xml:namespace prefix="st1" ns="urn:schemas-microsoft-com:office:smarttags"?><st1:place w:st="on">Vista</st1:place>, the kernel accounted for CPU time based on the interval clock timer which had a resolution of between 10-15ms. This timing interval was not always fair or accurate since threads where charged for interrupts that occurred while they were running and a thread might not get a turn to execute or could get up to three turns to execute.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><st1:place w:st="on"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Vista</span></st1:place><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"> changes this timing mechanism by reading the Time Stamp Counter (TSC) at each context switch. This allows the CPU to charge the thread with the actual CPU cycles consumed and does not charge the thread for interrupt time. This allows for a more accurate time accounting model and means that threads get at least one turn and can get at most one turn plus one tick.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">This new time accounting is handled by the following API functions:<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<ul style="MARGIN-TOP: 0in" type="disc">
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">QueryThreadCycleTime <o:p></o:p></span>
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">QueryProcessCycleTime <o:p></o:p></span>
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">QueryIdleProcessorCycleTime<o:p></o:p></span></li></li></li></ul>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Multimedia Class Scheduler<o:p></o:p></span></b></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">The multimedia class scheduler is a new service that boost the thread priorities of multimedia applications to support glitch-free audio and video streaming. This service runs in a Svchost process and is implemented in the Mmcss.dll used by Media Player 11.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">In order to make use of this service, threads must declare themselves as multimedia with the following API functions:<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<ul style="MARGIN-TOP: 0in" type="disc">
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l1 level1 lfo2; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">AvSetMmThreadCharacteristics</span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l1 level1 lfo2; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">AvSetMmThreadPriority</span></li></li></ul>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Multimedia threads are boosted into real-time for 80% of a task's clock rate (default is 1ms). If they consume all of that time, they are lowered so other threads can run. The percentage can be reconfigured through the following registry key:<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>


> <p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile</span></p>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">New Synchronization APIs<o:p></o:p></span></b></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>


> <p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><st1:place w:st="on"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Vista</span></st1:place><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"> also introduces some new kernel synchronization methods such as:<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<ul style="MARGIN-TOP: 0in" type="disc">
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Condition variables (*ConditionVariable*) <o:p></o:p></span>
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Reader/writer locks (*SRWLock*) <o:p></o:p></span>
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">One time initialization (Initonce*) <o:p></o:p></span>
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Extended version of Create object APIs to allow specification of desired access <o:p></o:p></span>
<ul style="MARGIN-TOP: 0in" type="circle">
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level2 lfo1; tab-stops: list 1.0in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Event, Mutex, Semaphore, Waitable Timer</span></li></ul></li></li></li></li></ul>


<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level2 lfo1; tab-stops: list 1.0in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><strong>Protected Processes</strong></span></p>


> <p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level2 lfo1; tab-stops: list 1.0in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Protected processes prevent unauthorized access to media content and can only be created through the new Protected Media Path APIs that are part of Media Foundation. This is used to enforce a secure path to the output devices and allows only signed images to be mapped into a secure process. Images must be signed by Microsoft and third-party codes must be signed with a Windows Media DRM certificate.</span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level2 lfo1; tab-stops: list 1.0in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"></span> </p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level2 lfo1; tab-stops: list 1.0in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Standard processes (even with debugging rights) have limited access to protected processes.</span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level2 lfo1; tab-stops: list 1.0in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"></span>

</span> <p>
