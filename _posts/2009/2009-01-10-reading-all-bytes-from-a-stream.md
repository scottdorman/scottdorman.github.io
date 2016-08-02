---
layout: post
title: Reading all bytes from a Stream
date: 2009-01-10 15:24:47 -05:00
---

I was working on some [`Stream`](http://msdn2.microsoft.com/8f86tw9e.aspx) extensions today and added a method which will read all of the data from a stream in to a byte array. Some of the classes which derive from Stream provide a similar method ([`MemoryStream`](http://msdn2.microsoft.com/9a84386f.aspx), for example, provides a `GetBuffer()` method to do this). The drawback here is that the base `Stream` class doesn't provide an abstract `GetBuffer()` method; instead it's up to each individual derived class to implement such a method. This is perfectly reasonable as a stream may not have an underlying buffer for storage like MemoryStream does.

Taking that into consideration, you read streams the same way. The call to `Stream.Read()` takes an array of bytes as a buffer to fill during the read operation. It would be nice to be able to get the entire contents of the stream as a byte array.

Looking around I found an excellent [blog post](http://www.yoda.arachsys.com/csharp/readbinary.html) by Jon Skeet that provides a few implementations on how to do this. The thing I didn't like about Jon's implementation is that it uses `Array.Copy` in order to resize the array (when there is more data available than the buffer can hold) and to return the properly sized array at the end. (It also has two exit points, which I don't ordinarily like, but that's a minor issue.)

The concern with using `Array.Copy` is that it accesses the elements by index and must be somewhat generic in order to support all of the .NET languages. Since streams tend to be rather large, this introduces unnecessary overhead. 

At this point, you might be asking "Why unnecessary overhead? How else do you copy arrays?" This question brings us to [`System.Buffer`](http://msdn2.microsoft.com/teyhh36d.aspx), which has been available in .NET since .NET 1.1 although you've probably never heard of it until now. A `Buffer` is designed to manipulate arrays of primitive types and treats each type as a series of bytes without any regard to behavior or limitations. How does this help us? Remember, `Stream.Read` returns an array of bytes and byte is a primitive type. So we can use `Buffer` to copy the array elements directly in memory rather than by index, which provides better performance than `Array.Copy`.

After modifying Jon's implementation to use `Buffer`, fixing an issue I noticed (the stream's position was never reset to 0 prior to reading) and getting rid of that pesky second exit point, my implementation is:

```csharp
/// <summary>
/// Reads the contents of the stream into a byte array.
/// data is returned as a byte array. An IOException is
/// thrown if any of the underlying IO calls fail.
/// </summary>
/// <param name="stream">The stream to read.</param>
/// <returns>A byte array containing the contents of the stream.</returns>
/// <exception cref="NotSupportedException">The stream does not support reading.</exception>
/// <exception cref="ObjectDisposedException">Methods were called after the stream was closed.</exception>
/// <exception cref="System.IO.IOException">An I/O error occurs.</exception>
public static byte[] ReadAllBytes(this Stream source)
{
    long originalPosition = source.Position;
    source.Position = 0;
 
    try
    {
        byte[] readBuffer = new byte[4096];
        int totalBytesRead = 0;
        int bytesRead;
        while ((bytesRead = source.Read(readBuffer, totalBytesRead, readBuffer.Length - totalBytesRead)) > 0)
        {
            totalBytesRead += bytesRead;
            if (totalBytesRead == readBuffer.Length)
            {
                int nextByte = source.ReadByte();
                if (nextByte != -1)
                {
                    byte[] temp = new byte[readBuffer.Length * 2];
                    Buffer.BlockCopy(readBuffer, 0, temp, 0, readBuffer.Length);
                    Buffer.SetByte(temp, totalBytesRead, (byte)nextByte);
                    readBuffer = temp;
                    totalBytesRead++;
                }
            }
        }
 
        byte[] buffer = readBuffer;
        if (readBuffer.Length != totalBytesRead)
        {
            buffer = new byte[totalBytesRead];
            Buffer.BlockCopy(readBuffer, 0, buffer, 0, totalBytesRead);
        }
        return buffer;
    }
    finally
    {
        source.Position = originalPosition;
    }
}
```

It will still generally use at least 2 arrays (if the original array is already the same size as the total number of bytes read, it will not resize it) and sometimes a 3rd array (created inside the while loop) when the stream is larger than the original array. However, by using the `Buffer.BlockCopy` and `Buffer.SetByte` rather than the `Array` methods it should offer better performance.
