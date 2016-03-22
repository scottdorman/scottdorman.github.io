---
layout: post
title: Windows Vista: Kernel Changes - Pre-Boot and Startup
date: 2006-06-17 16:42:00 -04:00
---

<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Boot Configuration Database (BCD)</span></b></p>


> <p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"></span></b><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><?xml:namespace prefix="st1" ns="urn:schemas-microsoft-com:office:smarttags"?><st1:place w:st="on">Vista</st1:place> unifies the boot mechanism to be platform independent. The information stored in the boot.ini file is now replaced by the BCD, which abstracts the firmware and is unified across different OS installations. The BCD also uses Unicode strings to support internationalization. To help ensure the security of the boot environment, the BCD is </span><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">stored in the registry in a binary format and is protected by registry key security.</span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"></span> </p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">In order to edit the BCD data, Microsoft provides a WMI interface that is completely scriptable. A command line editor called BCDEdit is also provided. BCDEdit uses the WMI interfaces, so anything that can be done through the command line utility should also be possible in custom scripts.</span></p>


<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><strong>Pre-Boot Executables</strong></span></p>


> <p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">The pre-boot executable environment has also undergone changes in Vista. The NTLDR boot loader has been split in to two sections:</span></p>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"></span> </p>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><strong><em>Windows Boot Manager</em></strong></span></p>
<blockquote dir="ltr" style="MARGIN-RIGHT: 0px">
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">The Windows boot manager is launched by the Master Boot Record (MBR) code and replaces the first half of NTLDR (the part that read boot.ini) and now reads the data stored in the BCD. This is handled by the files in the \Bootmgr partition on the system drive and can launch other Windows pre-boot executables.</span></p>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"></span> </p>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Some of these other pre-boot executables include a new resume loader that helps improve startup time when returning from a sleep state. (This used to be implemented by NTLDR and is now implemented in \Systemreoot\System32\Winresume.exe.) Another pre-boot executable is a windows memory diagnostic tool called \Boot\Memtest.exe.</span></p></blockquote>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><strong><em>Operating System Loader</em></strong></span></p>
<blockquote dir="ltr" style="MARGIN-RIGHT: 0px">
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">The OS loader replaces the second half of NTLDR which was responsible for loading the OS image, boot drivers, and System registry hives. There is a single OS loader per installation located in the \Systemroot\System32\Winloader.exe program executable.</span></p></blockquote>


<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><strong>Startup Process Changes</strong></span></p>


> <p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Prior to Vista, session creation was done serially by the Session Manager (SMSS) which would result in a bottleneck for Terminal Services. The SMSS created the Winlogon and Csrss processes for each session. Winlogon (which is the interactive logon manager) would then create the Local Security Authority(Lsass.exe) and Services (services.exe) processes.</span></p>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"></span> </p>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">In Vista, this behavior follows a similar model to the Windows Installer service. The Initial SMSS creates an instance of itself to initialize each session. This permits parallel session creation of anywhere between 4 and the number of processors.</span></p>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"></span> </p>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">The initial SMSS process runs in Session 0 and runs Wininit.exe. Wininit starts what Winlogon used to start, namely lsass.exe and services.exe. It also starts a new process, the Local Session Manager (lsm.exe).</span></p>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"></span> </p>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Once each subsequent session is started, that sessions SMSS create the session specific instances of winlogon and csrss.</span></p>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"></span> </p>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">This process will allow more concurrent users to log on to a terminal services server at the same time with much less stress on the operating system and provide faster logon times for the users.</span></p>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"></span> </p>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Since the initial SMSS process runs in Session 0, the Console user now runs in Session 1 and cannot connect to Session 0. This eliminates name collisions and prevents poorly written services from displaying windows to the user. Prior to Vista, the console user ran in Session 0, which allowed the opportunity for “shatter“ attacks.</span></p>


<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><strong>Address Space Load Randomization (ASLR)</strong></span></p>


> <p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Prior to Vista, executables and DLLs loaded at fixed locations and buffer overflow attacks commonly relied on known system function addresses to cause specific code to execute.</span></p>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"></span> </p>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">The Vista loader bases modules at one of 256 random locations in the address space. Operating system images now include relocation information and this relocation is performed once per image and is shared across processes. </span><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">The user stack locations are also randomized.</span></p>
