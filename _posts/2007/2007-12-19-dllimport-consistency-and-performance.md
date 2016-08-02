---
layout: post
title: DLLImport Consistency and Performance
date: 2007-12-19 20:53:51 -05:00
---

[Daniel Moth](http://www.danielmoth.com/Blog/index.htm) has an interesting post that talks about performance and the [DllImport](http://msdn2.microsoft.com/library/system.runtime.interopservices.dllimportattribute.aspx) attribute. The underlying theme to his post is that you should define a convention for how the DLL name is specified in the attribute. This actually has a significant enough impact that it really should become one of the rules in your coding standards documents.

If we take an example, all of the following are valid and will work at runtime without any problems:

```csharp
[DllImport("kernel32.dll")]
static extern ...;

[DllImport("kernel32")]
static extern ...;

[DllImport("Kernel32.DLL")]
static extern ...;

[DllImport("KERNEL32")]
static extern ...;

[DllImport("KeRnEl32.DlL")]
static extern ...;
```

At first glance, this probably doesn't look like it should be a big issue. It does show a lack of consistency by the developer, but other than that these attributes still import functions from kernel32.dll.

Looking at the results in both Reflector and ILDASM, you start to see the problem this lack of consistency causes.

![](http://www.danielmoth.com/Blog/dirtyKernel32References.png)

If you're still thinking that this isn't a problem because the loader is smart enough to only load one kernel32 instance into your process, you're only partly correct. The loader will only load one instance, but there is still a performance penalty because each string is treated as a separate module. At this point, you should start to see the problem. The more variations you have the more modules get processed by the loader.

Daniel recommends using all lowercase for the library name and always including the ".dll" extension, a recommendation that I agree with completely.
