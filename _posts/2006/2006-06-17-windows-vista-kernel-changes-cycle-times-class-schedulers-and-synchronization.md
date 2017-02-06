---
layout: post
title: "Windows Vista: Kernel Changes - Cycle Times, Class Schedulers and Synchronization"
date: '2006-06-17 15:08:00 -05:00'
---

## Cycle Time Counter
 
Prior to Vista, the kernel accounted for CPU time based on the interval clock timer which had a resolution of between 10-15ms. This timing interval was not always fair or accurate since threads where charged for interrupts that occurred while they were running and a thread might not get a turn to execute or could get up to three turns to execute.
 
Vista changes this timing mechanism by reading the Time Stamp Counter (TSC) at each context switch. This allows the CPU to charge the thread with the actual CPU cycles consumed and does not charge the thread for interrupt time. This allows for a more accurate time accounting model and means that threads get at least one turn and can get at most one turn plus one tick.
 
This new time accounting is handled by the following API functions:
 
* QueryThreadCycleTime 
* QueryProcessCycleTime 
* QueryIdleProcessorCycleTime

## Multimedia Class Scheduler
 
The multimedia class scheduler is a new service that boost the thread priorities of multimedia applications to support glitch-free audio and video streaming. This service runs in a Svchost process and is implemented in the Mmcss.dll used by Media Player 11.
 
In order to make use of this service, threads must declare themselves as multimedia with the following API functions:
 
* AvSetMmThreadCharacteristics 
* AvSetMmThreadPriority

Multimedia threads are boosted into real-time for 80% of a task's clock rate (default is 1ms). If they consume all of that time, they are lowered so other threads can run. The percentage can be reconfigured through the following registry key:

```
HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile
```

## New Synchronization APIs

Vista also introduces some new kernel synchronization methods such as:

* Condition variables (*ConditionVariable*) 
* Reader/writer locks (*SRWLock*) 
* One time initialization (*Initonce*) 
* Extended version of Create object APIs to allow specification of desired access 
  * Mutex, Semaphore, Waitable Timer

## Protected Processes

Protected processes prevent unauthorized access to media content and can only be created through the new Protected Media Path APIs that are part of Media Foundation. This is used to enforce a secure path to the output devices and allows only signed images to be mapped into a secure process. Images must be signed by Microsoft and third-party codes must be signed with a Windows Media DRM certificate.

Standard processes (even with debugging rights) have limited access to protected processes.
