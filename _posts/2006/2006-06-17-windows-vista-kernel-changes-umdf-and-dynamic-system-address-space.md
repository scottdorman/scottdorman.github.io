---
layout: post
title: Windows Vista: Kernel Changes - UMDF and Dynamic System Address Space
date: 2006-06-17 15:30:00 -04:00
---

<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">User-Mode Driver Framework (UMDF)<?xml:namespace prefix="o" ns="urn:schemas-microsoft-com:office:office"?><o:p></o:p></span></b></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>


> <p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Everyone has seen at least one Blue Screen of Death (BSOD) when it comes to buggy kernel-mode drivers causing a crash or allowing privilege escalation.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">UMDF is <?xml:namespace prefix="st1" ns="urn:schemas-microsoft-com:office:smarttags"?><st1:place w:st="on">Vista</st1:place>'s attempt to solve at least some of these problems and supports migration of some USB, Bluetooth, and IP drivers to user mode.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Why is this good? Bugs in the driver won't crash the operating system and user-mode drivers can be transparently “restarted“.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Devices that are currently supporting UMDF are:<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<ul style="MARGIN-TOP: 0in" type="disc">
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Digital cameras<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Portable media players<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Cell phones<o:p></o:p></span> 
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Personal digital assistants (PDAs)<o:p></o:p></span></li></li></li></li></ul>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">A UMDF driver runs in a dedicated host process created by the UMDF service under the Local Service account to prevent privilege escalation and cannot directly access hardware or kernel memory. The UMDF Reflector manages the interface to system kernel-mode drivers.<o:p></o:p></span></p>


<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Dynamic System Address Space</span></b></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>


> <p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">In 32-bit <st1:place w:st="on">Vista</st1:place> virtual memory is assigned as needed which permits larger paged, non-paged and session pools. This supports larger terminal servers, desktop heaps, etc., but components still cannot exceed 2 GB.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">In order to improve virtual address space usage the kernel page tables are allocated on demand instead of at boot and the kernel stack usage has been reduced which allows more users on a terminal server system. Desktop heap expansion can also be done without requiring a reboot.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">In 64-bit <st1:place w:st="on">Vista</st1:place>, address space regions are configured at their maximum for all memory sizes.<o:p></o:p></span></p>
