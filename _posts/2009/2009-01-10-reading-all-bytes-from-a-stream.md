---
layout: post
title: Reading all bytes from a Stream
date: 2009-01-10 15:24:47 -05:00
---

I was working on some [Stream](http://msdn2.microsoft.com/8f86tw9e.aspx "Stream Class") extensions today and added a method which will read all of the data from a stream in to a byte array. Some of the classes which derive from Stream provide a similar method ([MemoryStream](http://msdn2.microsoft.com/9a84386f.aspx "MemoryStream Class"), for example, provides a GetBuffer() method to do this). The drawback here is that the base Stream class doesn’t provide an abstract GetBuffer() method; instead it’s up to each individual derived class to implement such a method. This is perfectly reasonable as a stream may not have an underlying buffer for storage like MemoryStream does.

Taking that into consideration, you read streams the same way. The call to Stream.Read() takes an array of bytes as a buffer to fill during the read operation. It would be nice to be able to get the entire contents of the stream as a byte array.

Looking around I found an excellent [blog post](http://www.yoda.arachsys.com/csharp/readbinary.html) by Jon Skeet that provides a few implementations on how to do this. The thing I didn’t like about Jon’s implementation is that it uses Array.Copy in order to resize the array (when there is more data available than the buffer can hold) and to return the properly sized array at the end. (It also has two exit points, which I don’t ordinarily like, but that’s a minor issue.)

The concern with using Array.Copy is that it accesses the elements by index and must be somewhat generic in order to support all of the .NET languages. Since streams tend to be rather large, this introduces unnecessary overhead. 

At this point, you might be asking “Why unnecessary overhead? How else do you copy arrays?” This question brings us to [System.Buffer](http://msdn2.microsoft.com/teyhh36d.aspx "Buffer Class"), which has been available in .NET since .NET 1.1 although you’ve probably never heard of it until now. A Buffer is designed to manipulate arrays of primitive types and treats each type as a series of bytes without any regard to behavior or limitations. How does this help us? Remember, Stream.Read returns an array of bytes and byte is a primitive type. So we can use Buffer to copy the array elements directly in memory rather than by index, which provides better performance than Array.Copy.

After modifying Jon’s implementation to use Buffer, fixing an issue I noticed (the stream’s position was never reset to 0 prior to reading) and getting rid of that pesky second exit point, my implementation is:
  <div style="border-bottom: gray 1px solid; border-left: gray 1px solid; padding-bottom: 4px; line-height: 12pt; background-color: #f4f4f4; margin: 20px 0px 10px; padding-left: 4px; width: 97.5%; padding-right: 4px; font-family: consolas, 'Courier New', courier, monospace; max-height: 1200px; font-size: 8pt; overflow: auto; border-top: gray 1px solid; cursor: text; border-right: gray 1px solid; padding-top: 4px">   <div style="border-bottom-style: none; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; padding-left: 0px; width: 100%; padding-right: 0px; font-family: consolas, 'Courier New', courier, monospace; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">     

<span style="color: #606060">   1:</span> <span style="color: #008000">/// <summary></span>

<span style="color: #606060">   2:</span> <span style="color: #008000">/// Reads the contents of the stream into a byte array.</span>

<span style="color: #606060">   3:</span> <span style="color: #008000">/// data is returned as a byte array. An IOException is</span>

<span style="color: #606060">   4:</span> <span style="color: #008000">/// thrown if any of the underlying IO calls fail.</span>

<span style="color: #606060">   5:</span> <span style="color: #008000">/// </summary></span>

<span style="color: #606060">   6:</span> <span style="color: #008000">/// <param name="stream">The stream to read.</param></span>

<span style="color: #606060">   7:</span> <span style="color: #008000">/// <returns>A byte array containing the contents of the stream.</returns></span>

<span style="color: #606060">   8:</span> <span style="color: #008000">/// <exception cref="NotSupportedException">The stream does not support reading.</exception></span>

<span style="color: #606060">   9:</span> <span style="color: #008000">/// <exception cref="ObjectDisposedException">Methods were called after the stream was closed.</exception></span>

<span style="color: #606060">  10:</span> <span style="color: #008000">/// <exception cref="System.IO.IOException">An I/O error occurs.</exception></span>

<span style="color: #606060">  11:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">byte</span>[] ReadAllBytes(<span style="color: #0000ff">this</span> Stream source)

<span style="color: #606060">  12:</span> {

<span style="color: #606060">  13:</span>     <span style="color: #0000ff">long</span> originalPosition = source.Position;

<span style="color: #606060">  14:</span>     source.Position = 0;

<span style="color: #606060">  15:</span>  

<span style="color: #606060">  16:</span>     <span style="color: #0000ff">try</span>

<span style="color: #606060">  17:</span>     {

<span style="color: #606060">  18:</span>         <span style="color: #0000ff">byte</span>[] readBuffer = <span style="color: #0000ff">new</span> <span style="color: #0000ff">byte</span>[4096];

<span style="color: #606060">  19:</span>  

<span style="color: #606060">  20:</span>         <span style="color: #0000ff">int</span> totalBytesRead = 0;

<span style="color: #606060">  21:</span>         <span style="color: #0000ff">int</span> bytesRead;

<span style="color: #606060">  22:</span>  

<span style="color: #606060">  23:</span>         <span style="color: #0000ff">while</span> ((bytesRead = source.Read(readBuffer, totalBytesRead, readBuffer.Length - totalBytesRead)) > 0)

<span style="color: #606060">  24:</span>         {

<span style="color: #606060">  25:</span>             totalBytesRead += bytesRead;

<span style="color: #606060">  26:</span>  

<span style="color: #606060">  27:</span>             <span style="color: #0000ff">if</span> (totalBytesRead == readBuffer.Length)

<span style="color: #606060">  28:</span>             {

<span style="color: #606060">  29:</span>                 <span style="color: #0000ff">int</span> nextByte = source.ReadByte();

<span style="color: #606060">  30:</span>                 <span style="color: #0000ff">if</span> (nextByte != -1)

<span style="color: #606060">  31:</span>                 {

<span style="color: #606060">  32:</span>                     <span style="color: #0000ff">byte</span>[] temp = <span style="color: #0000ff">new</span> <span style="color: #0000ff">byte</span>[readBuffer.Length * 2];

<span style="color: #606060">  33:</span>                     Buffer.BlockCopy(readBuffer, 0, temp, 0, readBuffer.Length);

<span style="color: #606060">  34:</span>                     Buffer.SetByte(temp, totalBytesRead, (<span style="color: #0000ff">byte</span>)nextByte);

<span style="color: #606060">  35:</span>                     readBuffer = temp;

<span style="color: #606060">  36:</span>                     totalBytesRead++;

<span style="color: #606060">  37:</span>                 }

<span style="color: #606060">  38:</span>             }

<span style="color: #606060">  39:</span>         }

<span style="color: #606060">  40:</span>  

<span style="color: #606060">  41:</span>         <span style="color: #0000ff">byte</span>[] buffer = readBuffer;

<span style="color: #606060">  42:</span>         <span style="color: #0000ff">if</span> (readBuffer.Length != totalBytesRead)

<span style="color: #606060">  43:</span>         {

<span style="color: #606060">  44:</span>             buffer = <span style="color: #0000ff">new</span> <span style="color: #0000ff">byte</span>[totalBytesRead];

<span style="color: #606060">  45:</span>             Buffer.BlockCopy(readBuffer, 0, buffer, 0, totalBytesRead);

<span style="color: #606060">  46:</span>         }

<span style="color: #606060">  47:</span>         <span style="color: #0000ff">return</span> buffer;

<span style="color: #606060">  48:</span>     }

<span style="color: #606060">  49:</span>     <span style="color: #0000ff">finally</span>

<span style="color: #606060">  50:</span>     {

<span style="color: #606060">  51:</span>         source.Position = originalPosition;

<span style="color: #606060">  52:</span>     }

<span style="color: #606060">  53:</span> }

  </div>
</div>



It will still generally use at least 2 arrays (if the original array is already the same size as the total number of bytes read, it will not resize it) and sometimes a 3rd array (created inside the while loop) when the stream is larger than the original array. However, by using the Buffer.BlockCopy and Buffer.SetByte rather than the Array methods it should offer better performance.

<div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:9c0ac743-4ee7-42c3-91bc-8aa43718286f" class="wlWriterSmartContent">*Technorati Tags: [C#](http://technorati.com/tags/C%23), [.NET](http://technorati.com/tags/.NET), [Streams](http://technorati.com/tags/Streams), [Buffer](http://technorati.com/tags/Buffer)*</div><div class="wlWriterHeaderFooter" style="text-align:left; margin:0px; padding:4px 4px 4px 4px;">[![DotNetKicks Image](http://www.dotnetkicks.com/Services/Images/KickItImageGenerator.ashx?url=http://geekswithblogs.net/sdorman/archive/2009/01/10/reading-all-bytes-from-a-stream.aspx&bgcolor=0080C0&fgcolor=FFFFFF&border=000000&cbgcolor=D4E1ED&cfgcolor=000000)]({% post_url /2009/2009-01-10-reading-all-bytes-from-a-stream %})</div>
