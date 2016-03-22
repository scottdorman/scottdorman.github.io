---
layout: post
title: Unit Testing and Expected Exceptions
date: 2009-01-17 13:20:39 -05:00
---

When writing unit tests that cover methods that can throw known exceptions, you generally want to make sure that your tests actually test the conditions that can cause the exception and that you do, in fact, throw the correct exception.

Most unit test frameworks, including MSTest and NUnit, use an ExpectedExceptionAttribute to decorate the test method. There are actually several problems with using ExpectedExceptions that make it more difficult to write good unit tests.

The first problem is the fact that once a test method with an ExpectedException attribute throws an exception the execution of that method stops. Why is that a problem? It’s a problem because now you must write a separate test for each exception you might throw. This in and of itself isn’t a problem but it does become very cumbersome and results in a lot of extra code.

The second problem is that the syntax is the same (or similar) but the behavior is different between different unit testing frameworks. For example, NUnit and MSTest both allow a message parameter on their ExpectedException attributes. However, in NUnit this is the expected message the exception contains while MSTest uses this as the message that will be reported if an exception is thrown that isn’t the correct type.

Finally, it doesn’t specify which line of code might actually throw the exception. It simply says that something in the unit test should throw an exception. Since the actual exception handling is done outside of the test, you don’t have the ability to inspect the details of the exception.

There are some unit testing frameworks, like [xUnit.net](http://www.codeplex.com/xunit) that recognized these problems and took steps to address them. In xUnit.net, there are Assert.Throws, Assert.DoesNotThrow, and Record.Exception constructions. The Assert.Throws ensures that the code throws that exact exception while Assert.DoesNotThrow ensures the code does not throw any exceptions. Record.Exception simply records any exception that is thrown.

I wanted a way that worked like the xUnit.net Assert.Throws method and found a solution by [Chris Marino](http://srtsolutions.com/blogs/chrismarinos/archive/2008/06/06/testing-for-exceptions-in-unit-test-frameworks.aspx). This solution only works on .NET 2.0 or later as it uses the [System.Action](http://msdn2.microsoft.com/bb534741.aspx "Action Delegate") delegate. He does talk about an interesting [JIT related bug](http://srtsolutions.com/blogs/chrismarinos/archive/2008/11/03/somebody-call-the-orkin-man.aspx) in his original implementation. I have found a work around for the JIT bug he mentions and have been successfully converting my unit tests to make use of this new style of expected exception testing.

I have taken his solution, worked around the JIT bug and also added a related method that allows you to verify the message of the exception as well:
  <div style="border-bottom: gray 1px solid; border-left: gray 1px solid; padding-bottom: 4px; line-height: 12pt; background-color: #f4f4f4; margin: 20px 0px 10px; padding-left: 4px; width: 97.5%; padding-right: 4px; font-family: consolas, 'Courier New', courier, monospace; height: 757px; max-height: 800px; font-size: 8pt; overflow: auto; border-top: gray 1px solid; cursor: text; border-right: gray 1px solid; padding-top: 4px">   <div style="border-bottom-style: none; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; padding-left: 0px; width: 100%; padding-right: 0px; font-family: consolas, 'Courier New', courier, monospace; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px">     

<span style="color: #606060">   1:</span> <span style="color: #008000">/// <summary></span>

<span style="color: #606060">   2:</span> <span style="color: #008000">/// Contains assertion types that are not provided with the standard MSTest assertions.</span>

<span style="color: #606060">   3:</span> <span style="color: #008000">/// </summary></span>

<span style="color: #606060">   4:</span> <span style="color: #0000ff">internal</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">class</span> ExceptionAssert

<span style="color: #606060">   5:</span> {

<span style="color: #606060">   6:</span>     <span style="color: #008000">/// <summary></span>

<span style="color: #606060">   7:</span>     <span style="color: #008000">/// Checks to make sure that the input delegate throws a exception of type TException.</span>

<span style="color: #606060">   8:</span>     <span style="color: #008000">/// </summary></span>

<span style="color: #606060">   9:</span>     <span style="color: #008000">/// <typeparam name="TException">The type of exception expected.</typeparam></span>

<span style="color: #606060">  10:</span>     <span style="color: #008000">/// <param name="blockToExecute">The block of code to execute to generate the exception.</param></span>

<span style="color: #606060">  11:</span>     <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">void</span> Throws<TException>(Action blockToExecute) <span style="color: #0000ff">where</span> TException : System.Exception

<span style="color: #606060">  12:</span>     {

<span style="color: #606060">  13:</span>         <span style="color: #0000ff">try</span>

<span style="color: #606060">  14:</span>         {

<span style="color: #606060">  15:</span>             blockToExecute();

<span style="color: #606060">  16:</span>         }

<span style="color: #606060">  17:</span>         <span style="color: #0000ff">catch</span> (Exception ex)

<span style="color: #606060">  18:</span>         {

<span style="color: #606060">  19:</span>             Assert.IsTrue(ex.GetType() == <span style="color: #0000ff">typeof</span>(TException), <span style="color: #006080">"Expected exception of type "</span> + <span style="color: #0000ff">typeof</span>(TException) + <span style="color: #006080">" but type of "</span> + ex.GetType() + <span style="color: #006080">" was thrown instead."</span>);

<span style="color: #606060">  20:</span>             <span style="color: #0000ff">return</span>;

<span style="color: #606060">  21:</span>         }

<span style="color: #606060">  22:</span>  

<span style="color: #606060">  23:</span>         Assert.Fail(<span style="color: #006080">"Expected exception of type "</span> + <span style="color: #0000ff">typeof</span>(TException) + <span style="color: #006080">" but no exception was thrown."</span>);

<span style="color: #606060">  24:</span>     }

<span style="color: #606060">  25:</span>  

<span style="color: #606060">  26:</span>     <span style="color: #008000">/// <summary></span>

<span style="color: #606060">  27:</span>     <span style="color: #008000">/// Checks to make sure that the input delegate throws a exception of type TException.</span>

<span style="color: #606060">  28:</span>     <span style="color: #008000">/// </summary></span>

<span style="color: #606060">  29:</span>     <span style="color: #008000">/// <typeparam name="TException">The type of exception expected.</typeparam></span>

<span style="color: #606060">  30:</span>     <span style="color: #008000">/// <param name="blockToExecute">The block of code to execute to generate the exception.</param></span>

<span style="color: #606060">  31:</span>     <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">void</span> Throws<TException>(<span style="color: #0000ff">string</span> expectedMessage, Action blockToExecute) <span style="color: #0000ff">where</span> TException : System.Exception

<span style="color: #606060">  32:</span>     {

<span style="color: #606060">  33:</span>         <span style="color: #0000ff">try</span>

<span style="color: #606060">  34:</span>         {

<span style="color: #606060">  35:</span>             blockToExecute();

<span style="color: #606060">  36:</span>         }

<span style="color: #606060">  37:</span>         <span style="color: #0000ff">catch</span> (Exception ex)

<span style="color: #606060">  38:</span>         {

<span style="color: #606060">  39:</span>             Assert.IsTrue(ex.GetType() == <span style="color: #0000ff">typeof</span>(TException), <span style="color: #006080">"Expected exception of type "</span> + <span style="color: #0000ff">typeof</span>(TException) + <span style="color: #006080">" but type of "</span> + ex.GetType() + <span style="color: #006080">" was thrown instead."</span>);

<span style="color: #606060">  40:</span>             Assert.AreEqual(expectedMessage, ex.Message, <span style="color: #006080">"Expected exception with a message of '"</span> + expectedMessage + <span style="color: #006080">"' but exception with message of '"</span> + ex.Message + <span style="color: #006080">"' was thrown instead."</span>);

<span style="color: #606060">  41:</span>             <span style="color: #0000ff">return</span>;

<span style="color: #606060">  42:</span>         }

<span style="color: #606060">  43:</span>  

<span style="color: #606060">  44:</span>         Assert.Fail(<span style="color: #006080">"Expected exception of type "</span> + <span style="color: #0000ff">typeof</span>(TException) + <span style="color: #006080">" but no exception was thrown."</span>);

<span style="color: #606060">  45:</span>     }

<span style="color: #606060">  46:</span> }

  </div>
</div>



This implementation should work with any unit testing framework.


<div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:3de43a25-c278-4ce4-b89a-c79908563ee1" class="wlWriterSmartContent">*Technorati Tags: [MSTest](http://technorati.com/tags/MSTest), [Unit Tests](http://technorati.com/tags/Unit+Tests), [ExpectedException](http://technorati.com/tags/ExpectedException)*</div><div class="wlWriterHeaderFooter" style="text-align:left; margin:0px; padding:4px 4px 4px 4px;">[![DotNetKicks Image](http://www.dotnetkicks.com/Services/Images/KickItImageGenerator.ashx?url=http://geekswithblogs.net/sdorman/archive/2009/01/17/unit-testing-and-expected-exceptions.aspx&bgcolor=0080C0&fgcolor=FFFFFF&border=000000&cbgcolor=D4E1ED&cfgcolor=000000)]({% post_url 2009/2009-01-17-unit-testing-and-expected-exceptions %})</div>
