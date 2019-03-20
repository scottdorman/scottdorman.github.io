---
layout: post
title: "CLR 4.0: Corrupted State Exceptions"
date: '2010-05-03 10:58:14 -05:00'
tags: .net
---

Corrupted state exceptions are designed to help you have fewer bugs in your code by making it harder to make common mistakes around exception handling.

A very common pattern is code like this:

```csharp
public void FileSave(String name)
{
    try 
    {
        FileStream fs = new FileStream(name, FileMode.Create);
    } 
    catch (Exception e)
    {
        MessageBox.Show(<span style="color: #006080">"File Open Error");
        throw new Exception(IOException);
    }
}
```

The standard recommendation is not to catch `System.Exception` but rather catch the more specific exceptions (in this case, `IOException`).

While this is a somewhat contrived example, what would happen if `Exception` were really an `AccessViolationException` or some other exception indicating that the process state has been corrupted? What you really want to do is get out fast before persistent data is corrupted or more work is lost.

To help solve this problem and minimize the chance that you will catch exceptions like this, CLR 4.0 introduces Corrupted State Exceptions, which cannot be caught by normal catch statements.

There are still places where you do want to catch these types of exceptions, particularly in your application's "main" function or when you are loading add-ins.  There are also rare circumstances when you know code that throws an exception isn't dangerous, such as when calling native code.

In order to support these scenarios, a new HandleProcessCorruptedStateExceptions attribute has been added. This attribute is added to the function that catches these exceptions. There is also a process wide compatibility switch named legacyCorruptedStateExceptionsPolicy which when set to true will cause the code to operate under the older exception handling behavior.
