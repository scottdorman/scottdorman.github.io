---
layout: post
title: "Windows Vista: Kernel Changes - UMDF and Dynamic System Address Space"
date: 2006-06-17 15:30:00 -04:00
---

##User-Mode Driver Framework (UMDF)

> Everyone has seen at least one Blue Screen of Death (BSOD) when it comes to buggy kernel-mode drivers causing a crash or allowing privilege escalation.
 
UMDF is Vista's attempt to solve at least some of these problems and supports migration of some USB, Bluetooth, and IP drivers to user mode.
 
Why is this good? Bugs in the driver won't crash the operating system and user-mode drivers can be transparently “restarted“.
 
Devices that are currently supporting UMDF are:

 * Digital cameras 
 * Portable media players 
 * Cell phones 
 * Personal digital assistants (PDAs)	

A UMDF driver runs in a dedicated host process created by the UMDF service under the Local Service account to prevent privilege escalation and cannot directly access hardware or kernel memory. The UMDF Reflector manages the interface to system kernel-mode drivers.

##Dynamic System Address Space

> In 32-bit Vista virtual memory is assigned as needed which permits larger paged, non-paged and session pools. This supports larger terminal servers, desktop heaps, etc., but components still cannot exceed 2 GB.
 
In order to improve virtual address space usage the kernel page tables are allocated on demand instead of at boot and the kernel stack usage has been reduced which allows more users on a terminal server system. Desktop heap expansion can also be done without requiring a reboot.
 
In 64-bit Vista, address space regions are configured at their maximum for all memory sizes.
