---
layout: post
title: Windows Vista: Kernel Changes - Has any body seen Gina and what's a UAC?
date: 2006-06-17 17:15:00 -04:00
---

<p><strong>Interactive Logon Architecture</strong></p>


> <p>Vista changes the logon architecture and replaces GINAs with Credential Providers. Credential providers are easier to write than GINAs and plug in to the logonui.exe. The biggest advantage of Credential Providers (besides being easier to write) are that multiple concurrent providers are supported and can be user selected or event driven.</p>
<p>Credential providers are used to capture elevation credentials and run as first-class citizens of the logon process. Credential providers also do not have the ability to fully replace the logon user interface; rather they can specify what elements are displayed on the interface.</p>
<p>Vista will ship with a password credential provider (which provides the same functionality as the normal Windows logon GINA today) and a smart-card credential provider.</p>


<p dir="ltr"><strong>User Account Control (UAC)</strong></p>


> <p dir="ltr">User account control has the majestic goal of preventing malware or other malicious process from “owning” a system. In a nutshell, UAC means that almost nothing the user starts will blindly run as an administrator, even if that user is in the Administrators group.</p>
<p dir="ltr">Before everyone starts jumping up and down saying how much they hate the credentials dialogs that pop up everywhere, this can be turned off using the Local Security Policy Editor (secpol.msc), although Microsoft does not recommend doing so.</p>
<p dir="ltr">The problem UAC is trying to control is that the majority of users run as administrators and some applications will only run as an administrator. The solution is that even Administrators run as normal accounts and administrative actions require interactive consent or administrator credentials. Applications that are badly-behaved non-administrative applications get private virtualized views of portions of the registry and file system.</p>
<p dir="ltr">At logon, the LSASS creates both an Administrator and Limited User Account (LUA) version of the Administrator token and links both of them to the logon session. The userinit process (which is the first process created by winlogon) is created with the LUA token.</p>
<p dir="ltr">When an application requests account elevation, it uses the consent.exe application which presents the dialog on a secure desktop (in Session 0) and is a child of the AppInfo service. Consent.exe actually makes a static bitmap copy of the requesting session's desktop and displays that in the background of the secure desktop to provide the “seamless” feel of the request. Because the request runs in Session 0, the requesting application cannot interact with the dialog or influence it in any way.</p>
<p dir="ltr">An application can  be <span>marked for elevation in four ways: </span></p>
<div v:shape="_x0000_s1026">
<ul>
<li><span>In its manifest file </span>
<li><span>In the system’s application compatibility database </span>
<li><span>Heuristic installer detection </span>
<li><span>User explicitly asks for elevation </span></li></li></li></li></ul></div>
<p><span>UAC virtualization is implemented in the kernel and provides virtualization for potions of the file system and the registry. The registry has the virtualization support built-in while the file system support is provided by luafv.sys file system filter driver.</span></p>
<p><span>UAC virtualization redirects the following file system locations:</span></p>
<ul>
<li><span>\Program Files</span> 
<li><span>\Windows</span> 
<li><span>\Windows\System32</span></li></li></li></ul>
<p><span>The exceptions are write protected executables and dynamic link libraries and files that have executable extensions.</span></p>
<p><span>The HKLM\Software registry location is also redirected, except for many of the keys under the Microsoft key.</span></p>
<p><span>The redirects write to a per-user area of the file system or the registry and any reads look in the per-user area first. The per-user areas are:</span></p>
<ul>
<li><span><span>\Users\<username>\AppData\Local\Virtual Store</username></span><span><font size="3"> </font> 
<li>
<div v:shape="_x0000_s1026"><span>HKCU\Software\Classes\VirtualStore</span></div></li></span></span></li></ul>


<p dir="ltr" v:shape="_x0000_s1026"><span><strong>Integrity Levels</strong></span></p>


> <p dir="ltr" v:shape="_x0000_s1026"><span>Integrity Level (IL) SIDs are now required in the process token. Processes, threads, and tokens always have an IL ACE. Files and registry keys without an IL ACE have an implicit level of medium. Objects created by medium or higher processes are marked as having a medium IL and objects created by low IL processes are marked as low.</span></p>
<p dir="ltr" v:shape="_x0000_s1026"><span>The different ILs are:</span></p>
<ul dir="ltr">
<li>
<div v:shape="_x0000_s1026"><span>Low - Protected-mode IE</span></div></li>
<li>
<div v:shape="_x0000_s1026"><span>Medium - LUA processes</span></div></li>
<li>
<div v:shape="_x0000_s1026"><span>High - Elevated processes</span></div></li>
<li>
<div v:shape="_x0000_s1026"><span>System - System processes</span></div></li></ul>
<p v:shape="_x0000_s1026"><span>ILs are checked before DACLs are checked. A thread can only open an object for write access if its IL is equal to or higher than that of the object; however, it can open any object for read access if it is a non-process object. If it is a process, the thread IL must be equal or higher than the process IL.</span></p>
<p v:shape="_x0000_s1026"><span>The Windows subsystem also honors ILs and only query messages can be sent to the windows of elevated processes from LUA processes which helps prevent “shatter” attacks.</span></p>
