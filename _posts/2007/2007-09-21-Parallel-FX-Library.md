---
layout: post
title: Parallel FX Library
date: 2007-09-21 20:16:43 -04:00
---

In the latest online edition of MSDN magazine, there are two articles describing some upcoming additions to the .NET Framework that will add support for parallel processing. These additions are part of what is called the Parallel FX Library, which is currently in development. A CTP should be released sometime by the end of this year.

The two areas of the Parallel FX Library are the Task Parallel Library (TPL) and Parallel LINQ.

The Task Parallel Library provides optimized managed code for multi-core processors using a new thread pool that supports cancellation, waiting, pool isolation, which uses techniques from [The Cilk Project](http://supertech.csail.mit.edu/cilk/) from MIT and a [Dynamic-Sized Nonblocking Work Stealing Deque](http://research.sun.com/techrep/2005/abstract-144.html "http://research.sun.com/techrep/2005/abstract-144.html") from Sun Microsystems for superior scalability.

Parallel LINQ provides an implementation of [LINQ-to-Objects](http://msdn2.microsoft.com/en-us/library/bb394939.aspx) and [LINQ-to-XML](http://msdn2.microsoft.com/library/bb308960.aspx) which allow LINQ queries to utilize all of the CPUs or cores to get the job done by making use of data parallelism internally. Parallel LINQ supports the full set of LINQ operators and provides several ways to consume the output in parallel.

It will be interesting to see what the CTP brings and how quickly these new concepts will be picked up.
