---
layout: post
title: "CLR 4.0: In Process Side-by-Side CLR Hosting"
date: '2008-11-10 10:43:55 -05:00'
tags: .net
---

The CLR is the core set of APIs that make up the .NET Framework.

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image-2.png) 

Each release of the CLR has added functionality, with the most functionality being added in the .NET 3.0 and .NET 3.5 releases. These releases used a "layer cake model"

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image-6.png) 

This model works reasonably well for solving application compatibility issues but does restrict the kinds of functionality that can be added. The other problem with this approach is that the hosting process (any application that hosts an instance of the .NET Framework directly) could only load one version in to memory.

This limitation isn't an issue until you start looking at extensible applications using System.AddIn, the Managed Extensibility Framework (MEF) or some other extensibility framework. At this point, the limitation becomes more significant as your hosting application can only load extensions in to the same version of the Framework that it runs.

CLR 4.0 solves this problem by introducing a new In-Process Side by Side hosting model, which allows a host application to run both 2.0-based and 4.0-based CLRs in the same process. Let me repeat that: CLR 4.0 will allow process to host both 2.0 and 4.0-based CLRs in the same process.

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image-8.png) 

This allows a host process to load older components running against the 2.0 CLR and components running against the 4.0 CLR seamlessly. This level of control is exposed for both applications and COM through a config file which describes versions you run on and which you prefer. There are also a new set of hosting APIs for the host application (typically an unmanaged application) to use:

These new interfaces are:

* `ICLRMetaHost`
* `ICLRMetaHostPolicy`
* `ICLRRuntimeInfo`
* `ICLRRuntimeHost3`
* `ICLRStrongName` 

The older legacy static global hosting functions will be marked as deprecated.
