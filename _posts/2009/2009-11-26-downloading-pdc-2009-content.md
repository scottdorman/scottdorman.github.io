---
layout: post
title: Downloading PDC 2009 Content
date: 2009-11-26 20:37:06 -05:00
---

I wasn’t able to go to PDC09 this year, but Channel 9 has made most of the content from the sessions and keynotes available. If you want to download all of the content easily, you need to follow these simple steps:

1.  Download a recent build of of [cURL (~250K)](http://curl.haxx.se/download.html) and extract it to a folder.
2.  Download [PDC09Downloader](http://ecn.channel9.msdn.com/o9/pdc/PDC09DownloaderCSR.zip) and extract the .bat file to the same folder you extracted cURL.
3.  Run PDC09Downloader from a command prompt. This batch file takes a single parameter, which indicates the file type you want to download. The possible values are:
    

    *   WMVHIGH
    *   WMV
    *   MP4
    *   PPTX
    
4.  Download [PDC09Renamer](http://ecn.channel9.msdn.com/o9/pdc/PDC09RenamerCSR.zip) and extract the .bat file to the same folder as the downloaded content files.
5.  Run PDC09Renamer from a command prompt to rename the files to the full session title. This batch file accepts the following parameter values:
    

    *   WMV
    *   MP4
    *   PPTX
