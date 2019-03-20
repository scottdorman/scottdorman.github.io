---
layout: post
title: URL File Downloader for .NET Updates
date: '2007-08-16 19:35:58 -05:00'
---

It's been a while since I wrote the first version of my [FileDownloader](http://www.codeproject.com/cs/library/filedownloader.asp) article and class. Since that time, there have been a lot of positive comments about the article and a handful of feature requests. I finally made the time to update the classes and the article and resubmit it to The Code Project. This update has the following new methods and properties:


* **BlockSize** Gets or sets the download block size in Kilobytes (KB).
* **DownloadHtml** Gets or sets a value indicating if HTML pages should be allowed to be downloaded.
* **IndefiniteTimeout** Gets a value that represents an indefinite timeout for a synchronous download operation.
* **IsBusy** Gets a value indicating whether the FileDownloader is running an asynchronous operation.
* **Overwrite** Gets or sets a value indicating if the existing file should be overwritten.
* **PreAuthenticate** Indicates whether to pre-authenticate the request.
* **Timeout** Gets or sets a value indicating the timeout for asynchronous download operations.
* **DownloadAsync** Begin downloading the file at the specified URL, and save it to the current folder.
* **DownloadAsyncCancel** Cancel the current download operation.
* **GetLastModifiedDate** Retrieves the last modified date of the file at the specified URL.

There is another update pending (it has been submitted, but just needs to go through the editing queue) that adds the following property:

* **UserAgent** Gets or sets the value of the *User-agent* HTTP header.
