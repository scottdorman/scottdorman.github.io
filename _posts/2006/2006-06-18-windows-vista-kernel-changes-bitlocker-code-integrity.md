---
layout: post
title: "Windows Vista: Kernel Changes - BitLocker, Code Integrity"
date: 2006-06-18 14:18:00 -04:00
---

<p><strong>BitLocker<sup>TM</sup> Drive Encryption</strong></p>


> <p>BitLocker allows the entire OS volume to be encrypted as well as any other volumes. In order to do this, a 1.5 GB unencrypted system volume is required.</p>
<p>BitLocker requires Trusted Platform Module (TPM) v1.2 or a USB device and USB-capable BIOS and is implemented as a file filter driver that sits just above the volume manager drivers.</p>
<p>There are several supported modes for storing the decryption key:</p>
<ul>
<li>TPM locked with signature of boot files 
<li>TPM locked with user-specified PIN 
<li>external USB flash device</li></li></li></ul>


<p dir="ltr"><strong>Code Integrity Verification</strong></p>


> <p dir="ltr">The operating system loader and the kernel now perform code signature checks. On 64-bit x64 platforms, all kernel mode code must be signed and the identity of all kernel mode binaries is verified. The system also audits events for integrity check failures.</p>
<p dir="ltr">On 32-bit platforms, the administrator is prompted to install unsigned code. Load-time checks are done on all kernel mode binaries, but if unsigned code is allowed to load you won't be able to play protected high-definition multimedia content.</p>
