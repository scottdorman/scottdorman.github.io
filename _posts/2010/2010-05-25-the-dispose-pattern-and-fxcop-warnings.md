---
layout: post
title: The Dispose Pattern (and FxCop warnings)
date: '2010-05-25 10:40:09 -05:00'
tags: .net c# coding-style code-standards
---

*[This is actually a response to [Bill's blog post](http://srtsolutions.com/public/item/254680), but since it isn't possible to leave this as a comment on his blog it's a post here.]*

There are many different ways to implement the Dispose pattern correctly. Some are (in my opinion) better than others. In Bill's blog post he presents a particular pattern, which is an excerpt from his book [Effective C#](http://amzn.to/28JyfJh). The issue centers around the fact that a reader took the code sample presented in the book and ran FxCop (Code Analysis) on it, which generated a warning: "Ensure that base.Dispose() is always called." The "lesson learned" that Bill presents is that "tools are there to help us, not control us."

While I completely agree with the belief that tools are there to help us, I think it's important to understand *why* FxCop is raising this particular warning. The code presented in Bill's book looks like:

```csharp
// Have its own disposed flag.
private bool disposed = false;  

protected override void Dispose(>bool isDisposing)  
{  
    // Don't dispose more than once.  
    if (disposed)  
        return;  
    
    if (isDisposing)  
    {  
        // TODO: free managed resources here.  
    }

    // TODO: free unmanaged resources here.  
    // Let the base class free its resources.  
    
    // Base class is responsible for calling  
    // GC.SuppressFinalize( )  
    base.Dispose(isDisposing);  
    
    // Set derived class disposed flag:  
    disposed = true;  
}
```

This code does follow all of the guidelines for implementing the Dispose pattern. In this case, it's presumably part of a larger example showing how to implement the pattern as part of a base class. The reason FxCop is warning you about this code is the first if statement in the Dispose method, which will cause the method to exit if disposed is true.

The problem here is that there is the possibility that if the disposed flag is true, the call to `base.Dispose()` will never be executed. As Bill points out, it is possible for some other code elsewhere in the class to set this flag. He states that this is an "unlikely occurrence." While that is probably true, it can be a potentially dangerous assumption to make and is one that can be easily corrected. By changing the code slightly you can remove this assumption and correct the FxCop violation. 

```csharp
private bool disposed = false;  

protected override void Dispose(bool disposing)  
{  
   if (!disposed)  
   {  
        if (disposing)  
        {  
            // Dispose managed resources.  
        }  

        // Dispose unmanaged resources.  
        disposed = true;  
    }  

    base.Dispose(disposing);  
}  

```

Using this implementation allows the call to `base.Dispose()` to always occur, which ensures that the the disposal chain is always properly followed.
