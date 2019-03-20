---
layout: post
title: "CLR 4.0: Garbage Collection Changes"
date: '2008-11-07 14:37:50 -05:00'
tags: .net
---

The .NET garbage collector is one of the areas of the .NET Framework that is extremely important and probably one of the least understood. There are a lot of articles written about it and there have been very few changes since .NET 1.0 was first released. (There have been changes with almost each release, but they have been relatively minor.)

With .NET 4.0, however, there are some fairly substantial changes to the GC that will have some interesting performance implications (in a good way).

For a quick review, the GC in .NET is a generational garbage collector with 3 generations. Generation 0 and 1 collections are very fast since the segment (called the ephemeral segment) is small while Generation 2 collections can be relatively slow.

The GC in .NET also has two modes of operation: Server and Workstation. In Server GC, the algorithm maximizes the overall throughput but all managed code must be paused while it runs. In CLR 4, you can now subscribe to an event to be notified before a Generation 2 or Large Object Heap collection.

```csharp
public static void Main(string[] args)
{
  try
  {
    // Register for a set of notifications.
    // Parameters require tuning. First is 
    // for Gen2, second, Large Object Heap 
    GC.RegisterForFullGCNotification(10, 10);

    // Start a thread using WaitForFullGCProc
    Thread thWaitForFullGC = new Thread(new ThreadStart(WaitForFullGCProc));
    thWaitForFullGC.Start();
  }

  catch (InvalidOperationException invalidOp)
  {
    Console.WriteLine("GC Notifications are not supported while concurrent GC is enabled.\n" + invalidOp.Message);
  }
}

public static void WaitForFullGCProc()
{
    while (true)
    {
    // Wait for a notification
    GCNotificationStatus s = GC.WaitForFullGCApproach();

    if (s == GCNotificationStatus.Succeeded)
    {
      // This call will direct new traffic
      // away from machine; wait for old
      // traffic to finish; then call
      // GC.Collect()
      OnFullGCApproachNotify();
    }
    
    // Wait for a notification of completion
    s = GC.WaitForFullGCComplete();
    if (s == GCNotificationStatus.Succeeded)
    {
      OnFullGCCompleteEndNotify();
    }
}
```
The changes in the server GC will probably only affect a small number of applications. However, the changes to the workstation GC (which is the default mode) will affect almost all .NET applications.

In all .NET Framework versions from 3.5SP1 and earlier, workstation GC used a concurrent collection method. This means that the GC can do most, but not all, of a Generation 2 collection without pausing managed code. It can't, however, do a Generation 0 and Generation 1 collection at the same time as a Generation 2 collection. 

CLR 4.0 changes that to support background collection, which **can** do a Generation 0 and Generation 1 collection at the same time as a Generation 2 collection. This means that now only unusual circumstances should lead to long latency times.

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image-2.png) 

These charts are from some performance testing done by Microsoft and presented during PDC which shows how the new background collection algorithm should greatly reduce the latency times.
