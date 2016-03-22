---
layout: post
title: Daylight Savings Time for Developers
date: 2/27/2007 11:08:00 PM
---

I know several other people who received an email from Microsoft late last week titled "Important Daylight Savings Time Update for Developers". As far as I know, none of us are exaclty sure why we recieved these emails but we all figured that at some point we signed up for something .NET and developer related with Microsoft.

Just in case you didn't "get the memo", here are the relevant parts:

> Developers who use the .NET Framework may find their applications affected if the application uses the time zone information for historical purposes or if they have derived custom classes from [System.TimeZone](http://response.microsoft.com/P/v3/r.asp?r=T1_Url0&e=102271%3B173375%3B30117911%3B2%3B02&a=1007) to provide custom time zone information. The standard System.TimeZone class provides a managed wrapper for the underlying Windows Operating System time zone functions.
> 
> In addition, developers who use Visual C++ may find their applications affected if they use the CRT time functions, or the TZ environment variable. Microsoft is currently working on a fix for this issue and will post information about its availability on the [Visual Studio Support](http://response.microsoft.com/P/v3/r.asp?r=T1_Url1&e=102271%3B173375%3B30117911%3B2%3B02&a=1007) page.
> 
> Most applications that use these affected classes will not need to be modified as this update will ensure that the correct data is provided seamlessly to the application. However, applications that use these classes or the underlying [Windows API](http://response.microsoft.com/P/v3/r.asp?r=T1_Url2&e=102271%3B173375%3B30117911%3B2%3B02&a=1007) to perform historical time look-ups will need to be modified.
> 
> In most cases, developers who have extended the .NET Framework’s time zone support by creating custom time zone classes derived from System.TimeZone, or by direct access to the Win32 API, will not have to update their applications as long as the available updates to the operating system are applied. However, solutions that rely on private time zone data, or that retrieve system time zone information by accessing the registry directly, may need to be updated. Applications that deal with historical time zone data may also need to be updated.

More information is available at the following links:

[http://msdn2.microsoft.com/en-us/vstudio/bb264729.aspx](http://msdn2.microsoft.com/en-us/vstudio/bb264729.aspx)

[Preparing for daylight saving time changes in 2007](http://response.microsoft.com/P/v3/r.asp?r=T1_Url4&e=102271%3B173375%3B30117911%3B2%3B02&a=1007)

[KB928388: 2007 time zone update for Microsoft Windows operating systems](http://response.microsoft.com/P/v3/r.asp?r=T1_Url5&e=102271%3B173375%3B30117911%3B2%3B02&a=1007).
