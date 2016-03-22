---
layout: post
title: URL File Downloader for .NET Updates
date: 8/16/2007 7:35:58 PM
---

It's been a while since I wrote the first version of my [FileDownloader](http://www.codeproject.com/cs/library/filedownloader.asp) article and class. Since that time, there have been a lot of positive comments about the article and a handful of feature requests. I finally made the time to update the classes and the article and resubmit it to The Code Project. This update has the following new methods and properties:
 <dl> <dl> <dt>BlockSize  </dt><dd>Gets or sets the download block size in Kilobytes (KB).  </dd><dd>   </dd><dt>DownloadHtml  </dt><dd>Gets or sets a value indicating if HTML pages should be allowed to be downloaded.  </dd><dd>   </dd><dt>IndefiniteTimeout  </dt><dd>Gets a value that represents an indefinite timeout for a synchronous download operation.  </dd><dd>   </dd><dt>IsBusy  </dt><dd>Gets a value indicating whether the FileDownloader is running an asynchronous operation.  </dd><dd>   </dd><dt>Overwrite  </dt><dd>Gets or sets a value indicating if the existing file should be overwritten.  </dd><dd>   </dd><dt>PreAuthenticate  </dt><dd>Indicates whether to pre-authenticate the request.  </dd><dd>   </dd><dt>Timeout  </dt><dd>Gets or sets a value indicating the timeout for asynchronous download operations.  </dd><dd>   </dd><dt>DownloadAsync  </dt><dd>Begin downloading the file at the specified URL, and save it to the current folder.  </dd><dd>   </dd><dt>DownloadAsyncCancel  </dt><dd>Cancel the current download operation.  </dd><dd>   </dd><dt>GetLastModifiedDate  </dt><dd>Retrieves the last modified date of the file at the specified URL. </dd></dl></dl> 

There is another update pending (it has been submitted, but just needs to go through the editing queue) that adds the following property:
 <dl> <dl> <dt>UserAgent  </dt><dd>Gets or sets the value of the **User-agent** HTTP header. </dd></dl></dl>
