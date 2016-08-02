---
layout: post
title: "Windows Vista: Kernel Changes - Pre-Boot and Startup"
date: 2006-06-17 16:42:00 -05:00
---

**Boot Configuration Database (BCD)**

> ******Vista unifies the boot mechanism to be platform independent. The information stored in the boot.ini file is now replaced by the BCD, which abstracts the firmware and is unified across different OS installations. The BCD also uses Unicode strings to support internationalization. To help ensure the security of the boot environment, the BCD is stored in the registry in a binary format and is protected by registry key security.
 
In order to edit the BCD data, Microsoft provides a WMI interface that is completely scriptable. A command line editor called BCDEdit is also provided. BCDEdit uses the WMI interfaces, so anything that can be done through the command line utility should also be possible in custom scripts.

## Pre-Boot Executables

The pre-boot executable environment has also undergone changes in Vista. The NTLDR boot loader has been split in to two sections:

### Windows Boot Manager

The Windows boot manager is launched by the Master Boot Record (MBR) code and replaces the first half of NTLDR (the part that read boot.ini) and now reads the data stored in the BCD. This is handled by the files in the \Bootmgr partition on the system drive and can launch other Windows pre-boot executables.

Some of these other pre-boot executables include a new resume loader that helps improve startup time when returning from a sleep state. (This used to be implemented by NTLDR and is now implemented in \Systemreoot\System32\Winresume.exe.) Another pre-boot executable is a windows memory diagnostic tool called \Boot\Memtest.exe.

### Operating System Loader

The OS loader replaces the second half of NTLDR which was responsible for loading the OS image, boot drivers, and System registry hives. There is a single OS loader per installation located in the \Systemroot\System32\Winloader.exe program executable.

## Startup Process Changes

Prior to Vista, session creation was done serially by the Session Manager (SMSS) which would result in a bottleneck for Terminal Services. The SMSS created the Winlogon and Csrss processes for each session. Winlogon (which is the interactive logon manager) would then create the Local Security Authority(Lsass.exe) and Services (services.exe) processes.

In Vista, this behavior follows a similar model to the Windows Installer service. The Initial SMSS creates an instance of itself to initialize each session. This permits parallel session creation of anywhere between 4 and the number of processors.

The initial SMSS process runs in Session 0 and runs Wininit.exe. Wininit starts what Winlogon used to start, namely lsass.exe and services.exe. It also starts a new process, the Local Session Manager (lsm.exe).

Once each subsequent session is started, that sessions SMSS create the session specific instances of winlogon and csrss.

This process will allow more concurrent users to log on to a terminal services server at the same time with much less stress on the operating system and provide faster logon times for the users.

Since the initial SMSS process runs in Session 0, the Console user now runs in Session 1 and cannot connect to Session 0. This eliminates name collisions and prevents poorly written services from displaying windows to the user. Prior to Vista, the console user ran in Session 0, which allowed the opportunity for "shatter" attacks.

## Address Space Load Randomization (ASLR)

Prior to Vista, executables and DLLs loaded at fixed locations and buffer overflow attacks commonly relied on known system function addresses to cause specific code to execute.

The Vista loader bases modules at one of 256 random locations in the address space. Operating system images now include relocation information and this relocation is performed once per image and is shared across processes. The user stack locations are also randomized.
