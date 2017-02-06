---
layout: post
title: "Windows Vista: Kernel Changes - Resource Quotas and Symlinks"
date: '2006-06-17 15:13:00 -05:00'
---

## Resource Quotas

Prior to Vista, quotas were system-wide. Vista supports per-user hard resource quotas that cover:

* CPU usage
* working set minimum
* page file usage
* nonpaged pool
* paged pool

Process and thread creation have new extended attributes contained in the STARTUPINFOEX structure and new API functions:

* ProcThreadAttributeList.

Unfortunately, none of this information is documented yet, but keep an eye out. It promises to make quotas a lot more useful for the system administrators.

## Symbolic File Links

NTFS has supported only symbolic directory links (junctions). There are tools that let you create symbolic file links but they are difficult to manage and keep track of through the operating system.
 
Vista now gives NTFS direct support for symbolic file links. For those of you who are Unix (or Linux) geeks you know these better as "soft links" (`ln -s`). Symbolic links are built using the NTFS reparse points just like junctions.
 
In order to create symbolic links you must have the "Create Symbolic Links" privilege which is, by default, only assigned to Administrators.
 
Assuming you have the right privileges, creating symbolic links can be done programmaticly using the `CreateSymbolicLink` API or the mklink.exe command line utility. The command line utility can also be used to create hard links.
