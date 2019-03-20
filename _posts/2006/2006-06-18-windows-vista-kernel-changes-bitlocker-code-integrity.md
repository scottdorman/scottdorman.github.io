---
layout: post
title: "Windows Vista: Kernel Changes - BitLocker, Code Integrity"
date: '2006-06-18 14:18:00.00 -05:00:00'
tags: windows-vista
---

## BitLocker&trade; Drive Encryption

> BitLocker allows the entire OS volume to be encrypted as well as any other volumes. In order to do this, a 1.5 GB unencrypted system volume is required.
BitLocker requires Trusted Platform Module (TPM) v1.2 or a USB device and USB-capable BIOS and is implemented as a file filter driver that sits just above the volume manager drivers.
There are several supported modes for storing the decryption key:
>
>- TPM locked with signature of boot files 
>- TPM locked with user-specified PIN 
>- external USB flash device

## Code Integrity Verification

> The operating system loader and the kernel now perform code signature checks. On 64-bit x64 platforms, all kernel mode code must be signed and the identity of all kernel mode binaries is verified. The system also audits events for integrity check failures.

On 32-bit platforms, the administrator is prompted to install unsigned code. Load-time checks are done on all kernel mode binaries, but if unsigned code is allowed to load you won't be able to play protected high-definition multimedia content.
