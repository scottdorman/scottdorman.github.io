---
layout: post
title: How to unit test this code?
date: 2009-01-17 22:35:24 -05:00
---

This question is for all of the TDD and unit test folks, so I'm hoping someone comes up with an answer.

I've been writing unit tests and analyzing code coverage for one of my libraries for about a week now and I'm starting to see the end, at least for this particular library. However, I've run in to a problem trying to ensure as close to 100% code coverage as possible. This exists in several methods in a few different classes, but I'll take the simplest one for illustration purposes.

I have code that looks like this:

```csharp
 public static ProcessorArchitecture GetProcessorArchitecture()
 {
     SYSTEM_INFO sysInfo = new SYSTEM_INFO();

     if (Environment.OSVersion.Version.Major > 5 || (Environment.OSVersion.Version.Major == 5 && Environment.OSVersion.Version.Minor >= 1))
     {
         SafeNativeMethods.GetNativeSystemInfo(out sysInfo);
     }
     else
     {
         SafeNativeMethods.GetSystemInfo(out sysInfo);
     }

     ProcessorArchitecture architecture = ProcessorArchitecture.Unknown;
     switch (sysInfo.uProcessorInfo.processorArchitecture.wProcessorArchitecture)
     {
         case Constants.PROCESSOR_ARCHITECTURE_AMD64:
             architecture = ProcessorArchitecture.X64;
             break;

         case Constants.PROCESSOR_ARCHITECTURE_IA64:
             architecture = ProcessorArchitecture.Itanium;
             break;

         case Constants.PROCESSOR_ARCHITECTURE_INTEL:
             architecture = ProcessorArchitecture.X86;
             break;
     }

     return architecture;
 }

```

My unit test for this particular method is relatively simple as well:

```csharp
 [TestMethod]
 public void GetProcessorArchitecture()
 {
     ProcessorArchitecture expected = ProcessorArchitecture.X86;
     ProcessorArchitecture actual = ExtendedEnvironment.GetProcessorArchitecture();
     Assert.IsTrue(actual == expected);
 }
```

The problem here is that not all of this method is able to covered. Specifically, the else clause and the first two cases in the switch. Short of physically changing hardware or operating systems, how do I actually unit test those conditions? I don't think creating a mock object will help in this case, as the object I would need to mock is the `System.Environment` object and then somehow be able to alter the processor architecture field of the `SYSTEM_INFO` struct that is returned from `GetSystemInfo()`.

I realize this is a somewhat trivial example, but I think it does clearly demonstrate the impossibility of achieving 100% code coverage through unit tests.
