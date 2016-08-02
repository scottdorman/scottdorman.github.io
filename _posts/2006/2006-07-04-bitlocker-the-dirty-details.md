---
layout: post
title: BitLocker - The dirty details
date: 2006-07-04 09:21:00 -05:00
---

One of the new security features coming in Windows Vista and Longhorn is the new BitLocker™ Drive Encryption technology. BitLocker™ is designed to help prevent information loss, whether it is by theft or accidental. Information loss is costly to business on several levels, and the U.S. Department of Justice estimates that intellectual property theft cost enterprises $250 billion in 2004.

![](/img/posts/{% page.id %}/r_SEC32520060613_190427-2.jpg)

BitLocker™ Drive Encryption gives you improved data protection on your notebooks, desktops, and servers by providing a transparent user experience that requires little to no interaction on a protected system. BitLocker also prevents the use of another operating system or hacking tool to break file and system protections by preventing the offline viewing of user data and OS files through enhanced data protection and boot validation using TPM v1.2.

For those of you who may not know, TPM stands for Trusted Platform Module. So what's that? TPM is a piece of hardware that is part of the motherboard that:

*   Performs cryptographic functions 
    *   RSA, SHA-1, RNG 
    * Meets encryption export requirements
* Can create, store, and manage keys 
    *   Provides a unique Endorsement Key (EK) 
    * Provides a unique Storage Root Key (SRK)
* Performs digital signature operations 
* Holds platform measurements (hashes) 
* Anchors a chain of trust for keys and credentials 
* Protects itself against attacks

So now that you know what a TPM is, why should you use one? A TPM is a hardware implementation of a Root-of-Trust, which can be certified to be tamper resistant. When combined with software, it can protect root secrets better than software alone. A TPM can ensure that keys and secrets are only available for use when the environment is appropriate.

The important thing to know about BitLocker is that it will only encrypt the Windows partition. You also won't be able to dual-boot another operating system on the same partition, different partitions are fine. Any attempts to modify the protected Windows partition will render it unbootable.

![](/img/posts/{% page.id %}/r_SEC32520060613_190427-1.jpg)

To completely protect all of the data on the computer, you will need to use a combination of BitLocker on the Windows partition and Encrypted File System (EFS) on the other partitions. When properly configured, EFS is computationally infeasible to crack.

Even with all of the new security that is provided by BitLocker, it can't stop everything. Some of the areas that BitLocker is helpless to defend against are:

* Hardware debuggers
* Online attacks—BitLocker is concerned only with the system's startup process 
* Post logon attacks
* Sabotage by administrators
* Poor security maintenance
* BIOS reflashing
    * Protection against this can be enabled if you wish

## Additional Resources

* [Windows Vista BitLocker Client Platform Requirements](http://www.microsoft.com/whdc/system/platform/hwsecurity/BitLockerReq.mspx)
* [Trusted Computing Group (TCG) Website](http://www.trustedcomputinggroup.org/)
* [BitLocker™ Blog](http://blogs.msdn.com/si_team/default.aspx)
* [BitLocker™ Questions or Ideas](mailto:bdeinfo@microsoft.com)
