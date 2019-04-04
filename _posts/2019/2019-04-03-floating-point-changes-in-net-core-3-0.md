---
layout: post
title: Floating Point Changes in .NET Core 3.0
date: '2019-04-03 20:36:00 -05:00'
---

.NET Core 3.0 contains changes improve the parsing and formatting for floating point values. These were changes that started in .NET Core 2.1 and are now almost done, with .NET Core 3.0 being updated to be [IEEE compliant](https://en.wikipedia.org/wiki/IEEE_754-2008_revision). One of the biggest repercussions of this change is that the default behavior of `ToString` for floating point types ([`System.Single`](https://docs.microsoft.com/en-us/dotnet/api/system.single?view=netcore-3.0)(`float`) and [`System.Double`](https://docs.microsoft.com/en-us/dotnet/api/system.double?view=netcore-3.0)(`double`)) is to produce a roundtrippable string.

This is different than earlier releases of .NET and .NET Core and was [necessary](https://github.com/dotnet/corefx/issues/36579#issuecomment-479661545) to fix a variety of issues where all of the various combinations of x86 vs x64 vs ARM vs ARM64 and Windows vs Linux vs OSX could have been returning different results for `ToString` or `Parse`.

To summarize the changes:

- `ToString()`, `ToString("G")`, and `ToString("R")` will now return the shortest roundtrippable string.
- For the `G` format specifier that takes a precision (e.g. `G3`), the precision specifier is now always respected.
- For the `C`, `E`, `F`, `N`, and `P` format specifiers the changes are similar. The difference is that these format specifiers treat the precision as the number of digits after the decimal point, in contrast to `G` which treats it as the number of significant digits.
- For custom format strings, they have the same behavior as before and will only print up to 15 significant digits, regardless of how many are requested. 

This is potentially a big breaking change for existing code, so if you use floating point types and rely on the output of `ToString` or perform string parsing, you should update your code to handle these changes, if possible. If it's not possible, you may have to update your code to implement a workaround.

There were already parsing differences across various operating systems (i.e. Linux, Windows, macOS, etc) and architectures (i.e. x86, x64, ARM, ARM64, etc), so it's not possible to fallback to the old behavior.

To get equivalent behavior for formatting differences:

- For `ToString()` and `ToString("G")` you can use `G15` as the format specifier.
- For `ToString("R")` there is no fallback.
- For the `G` format-specifier that takes a precision, you can force precisions greater than 15 (exclusive) to be exactly 17. For example, if your code is doing `ToString("G20")` you can instead change this to `ToString("G17")`.
- For the remaining format-specifiers that take a precision (`C`, `E`, `F`, `N`, and `P`) there is no fallback.

For more details about these changes, see Tanner Gooding's [post](https://devblogs.microsoft.com/dotnet/floating-point-parsing-and-formatting-improvements-in-net-core-3-0/) or the GitHub [issue](https://github.com/dotnet/corefx/issues/36579).
