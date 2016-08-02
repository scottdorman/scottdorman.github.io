---
layout: post
title: Windows Mobile and U.S. Daylight Saving Time changes
date: 2007-02-15 21:18:00 -05:00
---

Hopefully everyone that lives in the United States (or deals with United States based companies) has heard that the U.S. Congress has changed the dates for Daylight Saving Time (DST) starting this year. The changes are the result of the [Energy Policy Act of 2005](http://en.wikipedia.org/wiki/Energy_Policy_Act_of_2005) and modifies the [Uniform Time Act](http://en.wikipedia.org/wiki/Uniform_Time_Act) of 1966 by changing the start and end dates of daylight saving time.

These changes mean that any electronic devices that were pre-programmed for adjusting to daylight saving time will be obsolete and incorrect. The intent of the change is so that the United States can reduce the energy costs. However, the effort of changing clocks on all of the embedded computer systems, enterprise servers, business and home computers, and anything else that keeps time will be enormous.

Just in case you are wondering, the clocks will move ahead one hour on the second Sunday of March  and fall back one hour on the first Sunday in November. This year, those dates are March 11, 2007 and November 4, 2007. (Previously they were the first Sunday of April (April 1, 2007) and the last  Sunday of October (October 28, 2007). Hey, at least it still happens on a Sunday.)

Those of you who have a normal cell phone shouldn't be affected as your phone synchronizes it's time with the servers at your cellular provider. Unfortunately, those of us who have "smart" phones, PDA, or anything running Windows Mobile aren't so lucky. Microsoft does have [instructions](http://www.microsoft.com/windowsmobile/daylightsaving/default.mspx) on how to update your Windows Mobile device, but they do make you bounce around a bit to download everything.

## For Windows Mobile users who connect to a PC

1. Install the [February 2007 cumulative time zone update for Microsoft Windows operating systems](http://support.microsoft.com/default.aspx/kb/931836). I have included the direct download links here:
    * [Windows Server 2003](http://www.microsoft.com/downloads/details.aspx?FamilyId=554A94FE-A478-47A7-B004-0277A292E90E) 
    * [Windows Server 2003 for Itanium-based Systems](http://www.microsoft.com/downloads/details.aspx?FamilyId=5D16F9EC-BE72-487B-84E8-E4368049A644) 
    * [Windows Server 2003 x64 Edition](http://www.microsoft.com/downloads/details.aspx?FamilyId=53D4F49B-AA6F-48A9-9244-6A1F7DCF2A94) 
    * [Windows XP](http://www.microsoft.com/downloads/details.aspx?FamilyId=66F1420C-DF2D-400B-A8A9-EF9061A9A3CA) 
    * [Windows XP x64 Edition](http://www.microsoft.com/downloads/details.aspx?FamilyId=6404F3E9-736D-449A-911E-F7CC99A375A4)
2. If you use Microsoft Outlook to synchronize your calendar, install the [Time Zone Data Update Tool for Microsoft Office Outlook](http://www.microsoft.com/downloads/info.aspx?na=90&p=&SrcDisplayLang=en&SrcCategoryId=&SrcFamilyId=e343a233-b9c8-4652-9dd8-ae0f1af62568&u=http%3a%2f%2fdownload.microsoft.com%2fdownload%2f6%2fe%2f9%2f6e9c86d7-9215-44d9-8b77-b91e95fac778%2ftzmove.exe). 
3. Connect your Windows Mobile device to your PC, make sure ActiveSync is running and connected, and install the [Daylight Saving Time 2007 Update Tool](http://download.microsoft.com/download/a/8/8/a8896b5f-69d7-4381-b12d-6fe27ff0d07a/Setup.msi) for Windows Mobile. 
4. Manually change the time zone on your device. The easiest way to do this is to change the current time zone to any time zone other than the one selected, close the settings screen, and then change it back to the current time zone.

There are instructions for Windows Mobile users who don't connect to their PC, but essentially you need to browse to [http://www.microsoft.com/windowsmobile/default.mspx](http://www.microsoft.com/windowsmobile/default.mspx) and download the "Daylight Saving Time 2007 Update for Windows Mobile".
