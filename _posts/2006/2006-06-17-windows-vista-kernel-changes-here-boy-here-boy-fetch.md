---
layout: post
title: "Windows Vista: Kernel Changes - Here boy! Here boy! Fetch!"
date: '2006-06-17 16:16:00.00 -05:00:00'
tags: windows-vista
---

## SuperFetch&trade;

Everyone is probably familiar with Prefetch which was introduced in Windows XP. Prefetch really only handled single processes at process startup.
 
In Vista, SuperFetch&trade; prefetches across a set of applications and takes in to account the frequency of page usgae and the usage of the page in the context of other pages in memory. It adapts to memory usage patterns, including complex usage scenarios and uses a low-prioirty I/O request for pre-fetching and pre-population.
 
SuperFetch&trade; is implemented as both a kernel-mode and user-mode component. Page usage data is collected in the kernel and the SuperFetch&trade; service (sysmain.dll) implements the storage and prefecth algorithms. The SuperFetch&trade; service stores the scenarios in `\Windows\Prefetch\Ag*.db` files and calls the kernel to retrieve paging histories and pre-populate the page lists. Also new with SuperFetch&trade; is that private virtual memory is also prefetched, where Windows XP only did file and image data.
 
## ReadyBoost

ReadyBoost stores read-only pages on extnernal nonvolatile memory and can serve as a supplementary cache for SuperFetch&trade;. Data is cached proactively based on user activity and allows fast reads to satisfy page faults when the page is not in main memory. Reading from a ReadyBoost device can be up to 10x faster than random drive reads, but it can lower the lifetime of the device. Current estimates are that they will still last at least a few hundred years even using ReadyBoost technologoy, so we really don't have much to worry about. There can only be one ReadyBoost device per system.

Supported devices are:

* USB keys
* SD cards
* Compact Flash cards
* internal PCI express cards

Devices must meet the following minimun performacne requirements:
 
Transfer Rate:

* 2.5 MB/sec for random 4KB reads
* 1.75 MB/sec for random 512KB reads

Size:

* 256MB - 4GB (FAT32 limit)

## ReadyDrive and Hybrid Hard Drives

A Hybrid Hard Drive (HHD) includes a nonvaliticle cache which contains data that can be read and written when the disk is spun down and remains in the cache even when the disk is powered down. The cahce size can be anywhere from 50 MB to 2 TB, but is typically 256 MB.
 
A HHD cache can contain SuperFetch&trade; data, boot data, or part of the OS hibernation file. It can be used as a write cache when a system is on battery power and data can be "pinned" by an OEM to make it always available.
 
ReadyDrive requires support by the host operating system, but fortunatley Vista provides that support and can make use of HHDs to improve system responsiveness.
