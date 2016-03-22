---
layout: post
title: Windows Vista: Kernel Changes - Here boy! Here boy! Fetch!
date: 2006-06-17 16:16:00 -04:00
---

<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><?xml:namespace prefix="o" ns="urn:schemas-microsoft-com:office:office"?><o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">SuperFetch<sup>TM</sup><o:p></o:p></span></b></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>


> <p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Everyone is probably familiar with Prefetch which was introduced in Windows XP. Prefetch really only handled single processes at process startup.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">In <?xml:namespace prefix="st1" ns="urn:schemas-microsoft-com:office:smarttags"?><st1:place w:st="on">Vista</st1:place>, SuperFetch<sup>TM</sup> prefetches across a set of applications and takes in to account the frequency of page usgae and the usage of the page in the context of other pages in memory. It adapts to memory usage patterns, including complex usage scenarios and uses a low-prioirty I/O request for pre-fetching and pre-population.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">SuperFetch<sup>TM</sup> is implemented as both a kernel-mode and user-mode component. Page usage data is collected in the kernel and the SuperFetch<sup>TM</sup> service (sysmain.dll) implements the storage and prefecth algorithms. The <span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">SuperFetch<sup>TM</sup> service stores the sc</span>enarios in \Windows\Prefetch\Ag*.db files and calls the kernel to retrieve paging histories and pre-populate the page lists. Also new with <span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">SuperFetch<sup>TM</sup> is that p</span>rivate virtual memory is also prefetched, where Windows XP only did file and image data.</span></p>


<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">ReadyBoost<o:p></o:p></span></b></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>


> <p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">ReadyBoost stores read-only pages on extnernal nonvolatile memory and can serve as a supplementary cache for SuperFetch<sup>TM</sup>. Data is cached proactively based on user activity and allows fast reads to satisfy page faults when the page is not in main memory. Reading from a ReadyBoost device can be up to 10x faster than random drive reads, but it can lower the lifetime of the device. Current estimates are that they will still last at least a few hundred years even using ReadyBoost technologoy, so we really don't have much to worry about. There can only be one ReadyBoost device per system.</span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Supported devices are:<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<ul style="MARGIN-TOP: 0in" type="disc">
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">USB keys<o:p></o:p></span></li>
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">SD cards<o:p></o:p></span></li>
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Compact Flash cards<o:p></o:p></span></li>
<li class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none; mso-list: l0 level1 lfo1; tab-stops: list .5in"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">internal PCI express cards<o:p></o:p></span></li></ul>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Devices must meet the following minimun performacne requirements:<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Transfer Rate:</span></p>
<ul>
<li>
<div class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">2.5 MB/sec for random 4KB reads<o:p></o:p></span></div></li>
<li>
<div class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">1.75 MB/sec for random 512KB reads<o:p></o:p></span></div></li></ul>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Size:<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>
<ul>
<li>
<div class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">256MB - 4GB (FAT32 limit)</span></div></li></ul>


<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">ReadyDrive and Hybrid Hard Drives<o:p></o:p></span></b></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>


> <p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">A Hybrid Hard Drive (HHD) includes a nonvaliticle cache which contains data that can be read and written when the disk is spun down and remains in the cache even when the disk is powered down. The cahce size can be anywhere from 50 MB to 2 TB, but is typically 256 MB.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">A HHD cache can contain SuperFetch<sup>TM</sup> data, boot data, or part of the OS hibernation file. It can be used as a write cache when a system is on battery power and data can be “pinned” by an OEM to make it always available.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">ReadyDrive requires support by the host operating system, but fortunatley <st1:place w:st="on">Vista</st1:place> provides that support and can make use of HHDs to improve system responsiveness.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
