---
layout: post
title: "Windows Vista: Kernel Changes - Can I get some service?"
date: 2006-06-18 13:17:00 -04:00
---

<p><strong>Delayed AutoStart Services</strong></p>


> <p>There are a lot of services that are set to autostart that aren't needed by the boot process. Unfortunately these services start at boot time and login time, which can severely impact login performance. Vista solves this by allowing services that can request a delayed autostart. These services are started by the Service Control Manager (SCM) after the automatic start services. Delayed autostart services also start with the initial thread set to THREAD_PRIORITY_LOWEST and have their I/O priority set to Very Low. After the service is running, the priority is increased to THREAD_PRIORITY_NORMAL.</p>
<p>This can only be used by services that are not critical to the system boot, such as BITS and Windows Update client.</p>


<p dir="ltr"><strong>Clean Service Shutdown</strong></p>


> <p dir="ltr">Until Vista, services had no way to extend the time allowed for shutdown. After a fixed timeout (the default is 20 seconds), the SCM is killed and the system is halted...while those services are still running. This is a significant problem for those services that needed to flush data to disk.</p>
<p dir="ltr">Enter Vista and the pre-shutdown notification. Services that request pre-shutdown notification (by setting the SERVICE_ACCEPT_PRESHUTDOWN state) can take as long as they want to shut down. SCM notifies pre-shutdown services first with a SERVICE_CONTROL_PRESHUTDOWN message and then waits for all pre-shutdown services to enter the SERVICE_STOPPED state. The default timeout is 3 minutes, but services can delay the shutdown indefinitely by setting SERVICE_STOP_PENDING. </p>
<p dir="ltr">After all of the pre-shutdown services are stopped, the system performs a Windows XP style shutdown for the other running services.</p>


<p dir="ltr"><strong>Service Shutdown Ordering</strong></p>


> <p dir="ltr">Vista now allows services to specify their shutdown order. This solves the issue of service dependencies not being implicitly understood or honored by SCM.</p>
<p dir="ltr">In order to specify the shutdown order, services must request pre-shutdown notification and must include their name in  <span>HKLM\System\CurrentControlSet\Control\<br></span><span><span></span>PreShutdownOrder.</span></p>


<p dir="ltr"><span><strong>Service Security Improvements</strong></span></p>


> <p dir="ltr"><span>Services now apply the principle of least-privilege to limit system exposure. Service specific SIDs permit a service's access to the system to be limited. Write-restricted service process further limit write access.</span></p>
<p dir="ltr"><span>Services can now specify which privileges they require (shutdown, audit, etc.) which limits the power of service processes. This is specified in a new MULTI_SZ registry value under the service key called RequiredPrivileges.</span></p>
<p dir="ltr"><span>On service startup, the SCM computes the union of all required privileges for the service (or services) inside the service process. Privileges not explicitly specified are removed. If no required privileges are specified, SCM assumes all privileges in the process token are needed.</span></p>
<p dir="ltr"><span></span> </p>
