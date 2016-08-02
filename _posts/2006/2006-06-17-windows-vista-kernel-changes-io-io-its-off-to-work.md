---
layout: post
title: "Windows Vista: Kernel Changes - I/O, I/O, It's off to work I go..."
date: 2006-06-17 15:26:00 -05:00
---

## Port Improvement

I/O completion ports allow threads to wait efficiently for completion of multiple I/O requests. Before Vista, each completion caused a context switch to the issuing thread. Now, the I/O completion is deferred to when the thread pulls off the completion port, which avoids the context switch.

## Scalability Improvements

Vista adds a new extended version of the GetQueuedCompletionStatus API named `GetQueuedCompletionStatusEx` which can return multiple I/O results in a single call. This reduces the user to kernel mode transitions and adds a new API (`SetFileCompletionNotificationModes`) to optimize the use of completion ports. There is also a new `SetFileIoOverlappedRange.API` that allows an application to lock a range of virtual addresses in memory that will be used for I/O.

## Cancellation Support

We have all encountered the problem where you browse to an off-line network share in the File Save dialog and the system appears to hang waiting for the network timeout to occur. Vista is trying to make these apparent system hangs a thing of the past.
 
Vista now allows opens and other synchronous I/O requests to be canceled. All of the common control file open/save dialogs implement cancellation support.
 
Cancellation is implemented using the following APIs:

* `CancelSynchronousIo` - cancels a pending synchronous I/O issued by another thread
* `CancelIoEx` - permits canceling all or individual I/Os from any thread (CancelIo could only cancel I/Os issued by the calling thread)

## I/O Prioritization

We've all seen how background I/O (antivirus scans, disk defragmenting, etc.) interferes with foreground tasks. Vista introduces two types of I/O prioritization and is implemented by both the ATAPI and USB storage drivers. These new prioritization are:

### I/O priority

I/O priority is based on the priority of the issuing thread or the explicitly set I/O priority.
 
There are five levels: Critical, High, Normal, Low, Very Low
 
High and Low are not implemented and Critical is for use only by the memory manager.
 
The I/O priority is stored in the Flags field of the I/O Request Packet (IRP).
 
Processes and threads (like the Vista background tasks of file indexing and Windows Defender scans) can lower their I/O priority using the `SetPriorityClass` and `SetThreadPriority` APIs.
 
Drivers can use the `IoGetIoPriorityHint` and `IoSetIoPriorityHint` kernel functions.

### I/O bandwidth reservation

Streaming multimedia applications (such as Windows Media Player) can use this to request an I/O bandwidth guarantee. This is specified on individual files with the following APIs:

* `GetFileBandiwthReservation`
* `SetFileBandwithReservation`

The I/O system reports back to the application the optimal transfer size and the number of outstanding I/Os they should maintain.
