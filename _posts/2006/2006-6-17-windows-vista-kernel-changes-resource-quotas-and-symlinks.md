---
layout: post
title: Windows Vista: Kernel Changes - Resource Quotas and Symlinks
date: 6/17/2006 3:13:00 PM
---

<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Resource Quotas<?xml:namespace prefix="o" ns="urn:schemas-microsoft-com:office:office"?><o:p></o:p></span></b></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>


> <p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Prior to <?xml:namespace prefix="st1" ns="urn:schemas-microsoft-com:office:smarttags"?><st1:place w:st="on">Vista</st1:place>, quotas were system-wide. <st1:place w:st="on">Vista</st1:place> supports per-user hard resource quotas that cover:<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>
<ul>
<li>
<div class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">CPU usage<o:p></o:p></span></div>
<li>
<div class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">working set minimum<o:p></o:p></span></div>
<li>
<div class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">page file usage<o:p></o:p></span></div>
<li>
<div class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">nonpaged pool<o:p></o:p></span></div>
<li>
<div class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">paged pool<o:p></o:p></span></div></li></li></li></li></li></ul>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Process and thread creation have new extended attributes contained in the STARTUPINFOEX structure and new API functions: *ProcThreadAttributeList.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>
<p><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial; mso-fareast-font-family: 'Times New Roman'; mso-ansi-language: EN-US; mso-fareast-language: EN-US; mso-bidi-language: AR-SA">Unfortunately, none of this information is documented yet, but keep an eye out. It promises to make quotas a lot more useful for the system administrators.</span></p>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial; mso-fareast-font-family: 'Times New Roman'; mso-ansi-language: EN-US; mso-fareast-language: EN-US; mso-bidi-language: AR-SA">
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Symbolic File Links<o:p></o:p></span></b></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>


> <p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">NTFS has supported only symbolic directory links (junctions). There are tools that let you create symbolic file links but they are difficult to manage and keep track of through the operating system.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><st1:place w:st="on"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Vista</span></st1:place><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"> now gives NTFS direct support for symbolic file links. For those of you who are Unix (or Linux) geeks you know these better as “soft links” (ln -s). Symbolic links are built using the NTFS reparse points just like junctions.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">In order to create symbolic links you must have the “Create Symbolic Links” privilege which is, by default, only assigned to Administrators.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Assuming you have the right privileges, creating symbolic links can be done programmaticly using the CreateSymbolicLink API or the mklink.exe command line utility. The command line utility can also be used to create hard links.</span>

</span><p>
