---
layout: post
title: Windows Vista: Kernel Changes - Kernel Transactions
date: 6/18/2006 1:38:00 PM
---

<p><strong>Kernel Transaction Manager (KTM)</strong></p>


> <p>Before Vista, applications had to do a lot of hard work to recover from errors during the modification of files and registry keys. Windows Vista implements a generalized transaction manager called the Kernel Transaction Manager (KTM) which provides “all or nothing” transaction semantics. This means that changes are committed only when the associated transaction is completed and commits.</p>
<p>The KTM is extensible through third-party resource managers and coordinates between the transaction clients (the applications) and the resource managers.</p>
<p>The registry and NTFS have been enhanced to provide transaction semantics across all operations and is used by the Windows Update service and the System Protection services.</p>
<p>Vista also picks up the Common Log File System (Clfs.sys) introduced in Windows Server 2003 R2, which provides efficient transaction logging facilities.</p>


<p dir="ltr"><strong>Transaction APIs</strong></p>


> <p dir="ltr">Transactions can span modification across one or many registry keys, files, and volumes. By using the Distributed Transaction Coordinator (DTC) transactions can coordinate changes across files, registry, databases, and MSMQ.</p>
<p dir="ltr">Transactions are relatively easy to use in Vista with the introduction of the new transaction command, which allows scripts to participate in the transaction process.</p>
<p dir="ltr">The Windows API also has a new set of API functions:</p>
<ul dir="ltr">
<li>
<div>CreateTransaction</div>
<li>
<div>SetCurrentTransaction</div>
<li>
<div>CommitTransaction</div>
<li>
<div>RollbackTransaction</div></li></li></li></li></ul>
<p>The kernel has IoCreateFile, which now has an ExtraCreateParameters which specified the transaction handle.</p>
