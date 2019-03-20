---
layout: post
title: Unit Testing and Expected Exceptions
date: '2009-01-17 13:20:39 -05:00'
tags: .net unit-testing
---

When writing unit tests that cover methods that can throw known exceptions, you generally want to make sure that your tests actually test the conditions that can cause the exception and that you do, in fact, throw the correct exception.

Most unit test frameworks, including MSTest and NUnit, use an ExpectedExceptionAttribute to decorate the test method. There are actually several problems with using ExpectedExceptions that make it more difficult to write good unit tests.

The first problem is the fact that once a test method with an ExpectedException attribute throws an exception the execution of that method stops. Why is that a problem? It's a problem because now you must write a separate test for each exception you might throw. This in and of itself isn't a problem but it does become very cumbersome and results in a lot of extra code.

The second problem is that the syntax is the same (or similar) but the behavior is different between different unit testing frameworks. For example, NUnit and MSTest both allow a message parameter on their ExpectedException attributes. However, in NUnit this is the expected message the exception contains while MSTest uses this as the message that will be reported if an exception is thrown that isn't the correct type.

Finally, it doesn't specify which line of code might actually throw the exception. It simply says that something in the unit test should throw an exception. Since the actual exception handling is done outside of the test, you don't have the ability to inspect the details of the exception.

There are some unit testing frameworks, like [xUnit.net](http://www.codeplex.com/xunit) that recognized these problems and took steps to address them. In xUnit.net, there are Assert.Throws, Assert.DoesNotThrow, and Record.Exception constructions. The Assert.Throws ensures that the code throws that exact exception while Assert.DoesNotThrow ensures the code does not throw any exceptions. Record.Exception simply records any exception that is thrown.

I wanted a way that worked like the xUnit.net Assert.Throws method and found a solution by [Chris Marino](http://srtsolutions.com/blogs/chrismarinos/archive/2008/06/06/testing-for-exceptions-in-unit-test-frameworks.aspx). This solution only works on .NET 2.0 or later as it uses the [System.Action](http://msdn2.microsoft.com/bb534741.aspx) delegate. He does talk about an interesting [JIT related bug](http://srtsolutions.com/blogs/chrismarinos/archive/2008/11/03/somebody-call-the-orkin-man.aspx) in his original implementation. I have found a work around for the JIT bug he mentions and have been successfully converting my unit tests to make use of this new style of expected exception testing.

I have taken his solution, worked around the JIT bug and also added a related method that allows you to verify the message of the exception as well:

```csharp
 /// <summary>
 /// Contains assertion types that are not provided with the standard MSTest assertions.
 /// </summary>
 internal static class ExceptionAssert
 {
     /// <summary>
     /// Checks to make sure that the input delegate throws a exception of type TException.
     /// </summary>
     /// <typeparam name="TException">The type of exception expected.</typeparam>
     /// <param name="blockToExecute">The block of code to execute to generate the exception.</param>
     public static void Throws<TException>(Action blockToExecute) where TException : System.Exception
     {
         try
         {
             blockToExecute();
         }
         catch (Exception ex)
         {
             Assert.IsTrue(ex.GetType() == typeof(TException), "Expected exception of type " + typeof(TException) +
              " but type of " + ex.GetType() + " was thrown instead.");
            return;
        }

        Assert.Fail("Expected exception of type " + typeof(TException) + " but no exception was thrown.");
    }
 
    /// <summary>
    /// Checks to make sure that the input delegate throws a exception of type TException.
    /// </summary>
    /// <typeparam name="TException">The type of exception expected.</typeparam>
    /// <param name="blockToExecute">The block of code to execute to generate the exception.</param>
    public static void Throws<TException>(string expectedMessage, Action blockToExecute) where TException : System.Exception
    {
        try
        {
            blockToExecute();
        }
        catch (Exception ex)
        {
            Assert.IsTrue(ex.GetType() == typeof(TException), "Expected exception of type " + typeof(TException) +
             " but type of " + ex.GetType() + " was thrown instead.");
            Assert.AreEqual(expectedMessage, ex.Message, "Expected exception with a message of '" + expectedMessage +
             "' but exception with message of '" + ex.Message + "' was thrown instead.");
            return;
        }

        Assert.Fail("Expected exception of type " + typeof(TException) + " but no exception was thrown.");
     }
}
```

This implementation should work with any unit testing framework.
