---
layout: post
title: "Windows Vista: Kernel Changes - Shadows of Reliability, Performance and Scalability"
date: 2006-06-18 13:59:00 -05:00
---

## Performance and Scalability


> Vista makes fewer and larger disk reads for page faults and system cache read-ahead and has removed the 64KB limit. Fewer, faster, and larger disk writes for the system page file and mapped file I/O reduce the page file fragmentation and allow a larger cluster size.

The CPU usage has also been improved by providing improvements in the concurrency management within the kernel. 


## Windows Error Reporting (WER)


> Vista is a more robust and resilient operating system that provides a read-only system cached view of the registry which protects it from being overwritten by drivers and helps reduce data loss in page crashes.

Prior to Vista, unhandled exceptions were handled in the context of the thread incurring the exception. This relied on the thread stack being valid and could result in the "silent death" of applications when the stack was corrupted.

In Vista, unhandled exceptions are sent to the Windows Error Reporting service, which launches Werfault.exe. This replaces Dwwin.exe (Doctor Watson), and permits WER to be invoked for threads that are too corrupted to invoke their unhandled exception handling.


## Volume Shadow Copy


> Windows Vista now uses Volume Shadow Copy for System Restore and Previous Versions. This creates a point-in-time copy-on-write snapshot of live volumes and solves the problem of open files not being backed up.

The Previous Versions tab was introduced as Windows Server 2003 "Shadow Copies for Shared Folders" feature.

Volume shadow copy now uses the kernel transaction manager for consistent cross-volume snapshots. Snapshots are taken once per day and when system restore points are taken.


## Other Reliability Features


> The kernel now supports the concept of a "flight data recorder" with the introduction of the circular kernel context logger.

There are new system events for virtual memory exhaustion, which can be used to help capture and report user-mode memory leaks.

The Restart Manager enables most applications and services to be shutdown and restarted to unblock access to DLLs needing to be replaced. This feature may finally allow seamless replacement of in-use DLLs, reducing the number of times a reboot is necessary at the end of an install.

For the developers, there are new debugger APIs that allow for "wait chain traversal" to help find and report deadlocks.
