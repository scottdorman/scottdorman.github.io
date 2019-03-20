---
layout: post
title: "CLR 4.0: Native-Managed Interoperability Improvements"
date: '2008-11-10 11:20:16 -05:00'
tags: .net
---

Exposing a native application to a managed application hasn't always been the easiest experience. The good news is that there are some significant improvements in the interoperability story between native and managed code.

In the current versions of the .NET Framework, the process starts with running the tlbimp tool to create an interop assembly. The problem here is that tlbimp doesn't always get everything right so you have to fix the assembly by running ildasm and then hand modify the IL or write some JScript to do it and then run ilasm to regenerate the assembly and designate it as a primary interop assembly (PIA).

This process becomes somewhat simpler now with the availability of a managed version of tlbimp on [CodePlex](http://www.codeplex.com/clrinterop). The other big improvement, and this is a pretty major change in the interop story, are the changes in the deployment experience. This falls under the name of "NoPIA", which means exactly that: no Primary Interop Assembly.

At design time when you add a reference to a PIA you now have a flag you can set which tells the compiler to embed only the methods that are used and pulls in the referenced types to local definitions. By using the new TypeIdentityAttribute, the CLR can maintain type equivalence by respecting the type GUID. (There is a whole lot more to the NoPIA work than this, which really deserves its own post.)

The other significant change is around writing p/invoke wrappers. This has become simpler with the managed debugging assistants (MDA) which look at the stack pointer before and after a p/invoke call. If you've ever seen an error message similar to this:

> A call to PInvoke function ....::SendMessage' has unbalanced the stack. This is likely because the managed PInvoke signature does not match the unmanaged target signature. Check that the calling convention and parameters of the PInvoke signature match the target unmanaged signature.

You've encountered one of these debug assistants. 

In .NET, defining a DLL entry point is disconnected from the actual code that gets called, which pulls parameters off the stack one at a time by changing the stack pointer by the size of the parameter being removed. P/invoke code does the opposite and puts things on the stack by increasing the stack pointer by the size of the parameter being added. If those two processes are not identical, the stack pointer will not be the same when the p/invoke call returns and means that p/invoke definition did not define the function parameters correctly. The p/invoke MDA is meant to catch these errors.

CLR 4.0 will provide a new wrapper tool, the P/Invoke Interop Assistant, available on [CodePlex](http://www.codeplex.com/clrinterop). This tool was first described by the [VB team](http://blogs.msdn.com/vbteam/archive/2008/03/14/making-pinvoke-easy.aspx) and then later made available on CodePlex. The really nice thing about this tool is that it not only generates the p/invoke wrapper code for you (simply copy and paste the resulting .NET code in to your application), it does so by reading the information in the windows.h header file and also the [SAL annotations](http://msdn.microsoft.com/en-us/library/ms235402.aspx). 

I think being able to read the SAL annotations are where the real power of this tool comes in. 

> If you examine the library header files, you will notice some unusual annotations such as `_In_z` and `_Out_z_cap_(_Size)`. These are examples of Microsoft's standard source code annotation language (SAL), which provides a set of annotations to describe how a function uses its parameters—the assumptions it makes about them, and the guarantees it makes upon finishing. The header file `<sal.h>` defines the annotations.
> 
> Annotations may be placed before either a function parameter's type or its return type, and describe the function's behavior regarding the parameter or return value. There are two classes of annotations: buffer annotations and advanced annotations. Buffer annotations describe how functions use their pointer parameters, and advanced annotations either describe complex/unusual buffer behavior, or provide additional information about a parameter that is not otherwise expressible. [[MSDN](http://msdn.microsoft.com/en-us/library/ms235402.aspx)]

Since this information is present in the header files and pretty clearly describe some of the behavior and data type semantics about the function, it makes a lot of sense to use this same information to create a proper p/invoke signature. The interop assistant does all of this for you and should make calling native Windows code easier and safer.
