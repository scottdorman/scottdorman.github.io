---
layout: post
title: Visual Studio 2010 Beta 2
date: 2009-10-19 13:09:29 -04:00
---

Visual Studio 2010 Beta 2 is now available for [MSDN subscribers](http://msdn.microsoft.com/en-us/vstudio/dd582936.aspx), and generally available on October 21. I haven’t had a chance yet to play around with it, but some of the CLR changes that are **very** exciting to hear about are:

*   The new [String.IsNullOrWhiteSpace](http://msdn.microsoft.com/en-us/library/system.string.isnullorwhitespace(VS.100).aspx) method indicates whether a string is null, empty, or consists only of white-space characters. 
*   New overloads have been added to the [String.Concat](http://msdn.microsoft.com/en-us/library/system.string.concat(VS.100).aspx) and [String.Join](http://msdn.microsoft.com/en-us/library/system.string.join(VS.100).aspx) methods that concatenate members of an [IEnumerable<T>](http://msdn.microsoft.com/en-us/library/9eekhta0(VS.100).aspx) collections.
*   The [String.Concat<T>](http://msdn.microsoft.com/en-us/library/dd991828(VS.100).aspx) method lets you concatenate each element in an enumerable collection without first converting the elements to strings.
*   The new [Enum.HasFlag](http://msdn.microsoft.com/en-us/library/system.enum.hasflag(VS.100).aspx) method determines whether one or more bit fields or flags are set in an enumeration value. 
*   The [Enum.TryParse<TEnum>](http://msdn.microsoft.com/en-us/library/dd991876(VS.100).aspx) method returns a Boolean value that indicates whether a string or integer value could be successfully parsed.
*   You can now easily copy one stream into another with the [CopyTo](http://msdn.microsoft.com/en-us/library/system.io.stream.copyto(VS.100).aspx) method in classes that inherit from the [System.IO.Stream](http://msdn.microsoft.com/en-us/library/system.io.stream(VS.100).aspx) class.
*   New [Path.Combine](http://msdn.microsoft.com/en-us/library/system.io.path.combine(VS.100).aspx) method overloads enable you to combine file paths.
*   You can now parse [System.Guid](http://msdn.microsoft.com/en-us/library/system.guid(VS.100).aspx) structures. 
*   The new [Microsoft.Win32.RegistryOptions](http://msdn.microsoft.com/en-us/library/microsoft.win32.registryoptions(VS.100).aspx) enumeration lets you specify a volatile registry key that does not persist after the computer restarts.
*   Registry keys no longer are restricted to a maximum length of 255 characters.  

I’m really looking forward to these improvements, particularly [Enum.HasFlags](http://msdn.microsoft.com/en-us/library/system.enum.hasflag(VS.100).aspx), [Enum.TryParse](http://msdn.microsoft.com/en-us/library/dd991876(VS.100).aspx), [String.IsNullOrWhiteSpace](http://msdn.microsoft.com/en-us/library/system.string.isnullorwhitespace(VS.100).aspx), [Guid.TryParse](http://msdn.microsoft.com/en-us/library/system.guid.tryparse(VS.100).aspx), and [Path.Combine(string[])](http://msdn.microsoft.com/en-us/library/dd991142(VS.100).aspx). Of course, since some of these weren’t in Beta 1 (at least as far as I saw), it means revising some of the chapters for my [book]({% post_url /2009/2009-06-26-sams-teach-yourself-c-2010-in-24-hours %}).
