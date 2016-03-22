---
layout: post
title: Windows Vista: Kernel Changes - I/O, I/O, It's off to work I go...
date: 6/17/2006 3:26:00 PM
---

<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none">
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"></span></p>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><span><strong>I/O <?xml:namespace prefix="st1" ns="urn:schemas-microsoft-com:office:smarttags"?><st1:placename w:st="on">Completion</st1:placename> <st1:placetype w:st="on">Port Improvement</st1:placetype></strong></span></span></p>


> <p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">I/O completion ports allow threads to wait efficiently for completion of multiple I/O requests. Before <st1:place w:st="on">Vista</st1:place>, each completion caused a context switch to the issuing thread. Now, the I/O completion is deferred to when the thread pulls off the completion port, which avoids the context switch.</span></p>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><?xml:namespace prefix="o" ns="urn:schemas-microsoft-com:office:office"?><o:p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><st1:place w:st="on"><st1:placename w:st="on"><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">I/O</span></b></st1:placename><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"> </span></b></st1:place><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Scalability Improvements</span></b></o:p></span></p>


> <p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><st1:place w:st="on"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Vista</span></st1:place><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"> adds a new extended version of the GetQueuedCompletionStatus API named GetQueuedCompletionStatusEx which can return multiple I/O results in a single call. This reduces the user to kernel mode transitions and adds a new API (SetFileCompletionNotificationModes) to optimize the use of completion ports. There is also a new </span><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">SetFileIoOverlappedRange.API that allows an application to lock a range of virtual addresses in memory that will be used for I/O.</span></p>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><st1:place w:st="on"><st1:placename w:st="on"><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">I/O</span></b></st1:placename><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"> </span></b></st1:place><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Cancellation Support</span></b></o:p></span><p>


> <p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><st1:place w:st="on"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">We have all encountered the problem where you browse to an off-line network share in the File Save dialog and the system appears to hang waiting for the network timeout to occur. Vista is trying to make these apparent system hangs a thing of the past.</span></st1:place></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><st1:place w:st="on"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"></span></st1:place> </p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><st1:place w:st="on"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Vista</span></st1:place><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"> now allows opens and other synchronous I/O requests to be canceled. All of the common control file open/save dialogs implement cancellation support.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Cancellation is implemented using the following APIs:<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>
<ul>
<li>
<div class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">CancelSynchronousIo - cancels a pending synchronous I/O issued by another thread<o:p></o:p></span></div>
<li>
<div class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">CancelIoEx - permits canceling all or individual I/Os from any thread (CancelIo could only cancel I/Os issued by the calling thread)</span></div></li></li></ul>

<span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><st1:place w:st="on"><st1:placename w:st="on"><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">I/O</span></b></st1:placename><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"> </span></b></st1:place><b style="mso-bidi-font-weight: normal"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Prioritization</span></b></span></p>


> <p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">We've all seen how background I/O (antivirus scans, disk defragmenting, etc.) interferes with foreground tasks. <st1:place w:st="on">Vista</st1:place> introduces two types of I/O prioritization and is implemented by both the ATAPI and USB storage drivers. These new prioritization are:<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><strong>I/O priority</strong> </span></p>
<blockquote dir="ltr" style="MARGIN-RIGHT: 0px">
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">I/O priority is based on the priority of the issuing thread or the explicitly set I/O priority.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">There are five levels: Critical, High, Normal, Low, Very Low<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">High and Low are not implemented and Critical is for use only by the memory manager.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">The I/O priority is stored in the Flags field of the I/O Request Packet (IRP).<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Processes and threads (like the <st1:place w:st="on">Vista</st1:place> background tasks of file indexing and Windows Defender scans) can lower their I/O priority using the SetPriorityClass and SetThreadPriority APIs.<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p> </o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Drivers can use the IoGetIoPriorityHint and IoSetIoPriorityHint kernel functions.</span></p></blockquote>
<p class="MsoNormal" dir="ltr" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"></span><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><strong>I/O bandwidth reservation</strong></span></p>
<blockquote dir="ltr" style="MARGIN-RIGHT: 0px">
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">Streaming multimedia applications (such as Windows Media Player) can use this to request an I/O bandwidth guarantee. This is specified on individual files with the following APIs:<o:p></o:p></span></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial"><o:p></o:p></span></p>
<ul>
<li>
<div class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">GetFileBandiwthReservation<o:p></o:p></span></div></li>
<li>
<div class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">SetFileBandwithReservation</span></div></li></ul>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt; mso-layout-grid-align: none"><span style="FONT-SIZE: 10pt; FONT-FAMILY: Arial">The I/O system reports back to the application the optimal transfer size and the number of outstanding I/Os they should maintain.</span></p></blockquote>
