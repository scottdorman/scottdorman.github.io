---
layout: post
title: .NET Core project versioning
date: '2018-08-10 19:41:00 -05:00'
---

Visual Studio has always allowed you to specify a version number for your .NET projects using the `[assembly:AssemblyVersionAttribute("2.0.1")]` syntax, usually in an `AssemblyInfo.cs` file. You can even use some special syntax so the build or revision number can be automatically generated.

> You can specify all the values or you can accept the default build number, revision number, or both by using an asterisk (\*). For example, [assembly:AssemblyVersion("2.3.25.1")] indicates 2 as the major version, 3 as the minor version, 25 as the build number, and 1 as the revision number. A version number such as [assembly:AssemblyVersion("1.2.\*")] specifies 1 as the major version, 2 as the minor version, and accepts the default build and revision numbers. A version number such as [assembly:AssemblyVersion("1.2.15.\*")] specifies 1 as the major version, 2 as the minor version, 15 as the build number, and accepts the default revision number. The default build number increments daily. The default revision number is the number of seconds since midnight local time (without taking into account time zone adjustments for daylight saving time), divided by 2. *(See the [AssemblyVersionAttribute Class](https://docs.microsoft.com/en-us/dotnet/api/system.reflection.assemblyversionattribute?view=netframework-4.7.1) documentation.)*

There are numerous, and well documented, issues with this approach. There are also a lot of different solutions as well.

With the introduction of .NET Core and the improvements to MSBuild in order to support these projects, it has become a lot simpler to achieve a consistent version number across all of the projects in a solution.