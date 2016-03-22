---
layout: post
title: BitLocker™ - The dirty details
date: 7/4/2006 9:21:00 AM
---

One of the new security features coming in Windows Vista and Longhorn is the new <span>BitLocker™ Drive Encryption technology. <span>BitLocker™ is designed to help prevent information loss, whether it is by theft or accidental. Information loss is costly to business on several levels, and t<span><span>he U.S. Department of Justice estimates that intellectual property theft cost enterprises $250 billion in 2004.</span></span></span></span>

<span><span><span><span>![](http://gwb.blob.core.windows.net/sdorman/5006/r_SEC32520060613_190427-2.jpg)</span></span></span></span>

<span><span><span>BitLocker™ Drive Encryption gives you improved data protection on your notebooks, desktops, and servers by providing a transparent user experience that requires little to no interaction on a protected system. BitLocker also prevents the use of another operating system or hacking tool to break file and system protections by preventing the offline viewing of user data and OS files through enhanced data protection and boot validation using TPM v1.2.</span></span></span>

<span><span><span><span><span><span>For those of you who may not know, TPM stands for Trusted Platform Module. So what's that? TPM is a piece of hardware that is part of the motherboard that:</span></span></span></span></span></span>

*   <span><span><span><span><span><span>Performs cryptographic functions</span></span></span></span></span></span> 


    *   <span><span><span><span><span><span>RSA, SHA-1, RNG</span></span></span></span></span></span> 
<span><span><span><span><span><span>Meets encryption export requirements</span></span></span></span></span></span>
<span><span><span><span><span><span>Can create, store, and manage keys</span></span></span></span></span></span> 


    *   <span><span><span><span><span><span>Provides a unique Endorsement Key (EK)</span></span></span></span></span></span> 
<span><span><span><span><span><span>Provides a unique Storage Root Key (SRK)</span></span></span></span></span></span>
<span><span><span><span><span><span>Performs digital signature operations</span></span></span></span></span></span> 
<span><span><span><span><span><span>Holds platform measurements (hashes)</span></span></span></span></span></span> 
<span><span><span><span><span><span>Anchors a chain of trust for keys and credentials</span></span></span></span></span></span> 
<span><span><span><span><span><span>Protects itself against attacks</span></span></span></span></span></span>


<span><span><span><span><span><span>So now that you know what a TPM is, why should you use one? A TPM is a hardware implementation of a Root-of-Trust, which can be certified to be tamper resistant. When combined with software, it can protect root secrets better than software alone. A TPM can ensure that keys and secrets are only available for use when the environment is appropriate.</span></span></span></span></span></span>

<span><span><span><span><span><span>The important thing to know about BitLocker is that it will only encrypt the Windows partition. You also won't be able to dual-boot another operating system on the same partition, different partitions are fine. Any attempts to modify the protected Windows partition will render it unbootable.</span></span></span></span></span></span>

<span><span><span><span><span><span>![](http://gwb.blob.core.windows.net/sdorman/5006/r_SEC32520060613_190427-1.jpg)</span></span></span></span></span></span>

<span><span><span><span><span><span>To completely protect all of the data on the computer, you will need to use a combination of BitLocker on the Windows partition and Encrypted File System (EFS) on the other partitions. When properly configured, EFS is computationally infeasible to crack.</span></span></span></span></span></span>

<span><span><span><span><span><span>Even with all of the new security that is provided by BitLocker, it can't stop everything. Some of the areas that BitLocker is helpless to defend against are:</span></span></span></span></span></span>

*   <span><span><span><span><span><span><span>Hardware debuggers </span></span></span></span></span></span></span>
<span><span><span><span><span><span><span></span><span>Online attacks—BitLocker is concerned only with the </span><span>system’s startup process </span>

    <div v:shape="_x0000_s1026"><span>Post logon attacks </span></div>

    <div v:shape="_x0000_s1026"><span>Sabotage by administrators </span></div>

    <div v:shape="_x0000_s1026"><span>Poor security maintenance </span></div>

    <div v:shape="_x0000_s1026"><span>BIOS reflashing </span></div>


    *   <div v:shape="_x0000_s1026"><span></span><span>Protection against this can be enabled if you wish</span></div>
*   </span></span></span></span></span></span>


<span><strong>Additional Resources</strong></span>

*   <div v:shape="_x0000_s1026"><span><span>[Windows Vista BitLocker Client Platform Requirements](http://www.microsoft.com/whdc/system/platform/hwsecurity/BitLockerReq.mspx)</span></span></div>

    <div v:shape="_x0000_s1026"><span><span><span>[Trusted Computing Group (TCG) Website](http://www.trustedcomputinggroup.org/)</span></span></span></div>

    <div v:shape="_x0000_s1026"><span><span>
<div v:shape="_x0000_s1026"><span><span>[BitLocker™ Blog](http://blogs.msdn.com/si_team/default.aspx)</span></span></div></span></span></div>

    <div v:shape="_x0000_s1026"><span><span>
<div v:shape="_x0000_s1026"><span><span></span></span></div></span></span><span><span><span><span><span>[BitLocker™ Questions or Ideas](mailto:bdeinfo@microsoft.com)</span></span></span></span></span></div>
