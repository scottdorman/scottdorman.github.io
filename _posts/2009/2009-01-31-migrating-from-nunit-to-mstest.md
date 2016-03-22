---
layout: post
title: Migrating from NUnit to MSTest
date: 2009-01-31 12:39:15 -05:00
---

I have been writing a lot of unit tests over the past month using the Microsoft Test (MSTest) unit testing framework that is now part of Visual Studio 2008 Professional Edition (and higher SKUs). Currently I have about 223 unit tests covering 39 classes (about 18K lines of code, 325 methods and 176 properties) with a code coverage percent of 97%.

The classes that I’m testing previously had NUnit tests (although not as many as I currently have) and used NCover and NCover Explorer for my code coverage analysis. I had looked at MSTest when it first came out and decided against using it because it was only available in the Visual Studio Team System SKUs, which meant it wasn’t generally available to the development community at large, and required Visual Studio to be installed in order to use it.

Since then, Microsoft has addressed both of those issues and I decided it was time to give MSTest another look. In doing so, I decided to see if it would be possible to leverage the existing NUnit tests rather than starting completely from scratch. One word of caution…if you use the newer constraint model in NUnit, your unit tests will not easily migrate to MSTest and you are probably better off starting fresh using MSTest.

It turned out to be a relatively painless process that can be broken down to the following steps:

1.  Replace the reference to the Nunit.Framework assembly with a reference to the Microsoft.VisualStudio.QualityTools.UnitTestFramework assembly.
2.  Replace the “using Nunit.Framework” line with “using Microsoft.VisualStudio.TestTools.UnitTesting”
3.  For each file containing unit tests, replace the following attributes (you can use global search and replace for this):       

4.  <table border="0" cellspacing="0" cellpadding="2" width="400"><tbody>       <tr>         <td valign="top" width="200">**NUnit Attribute**</td>          <td valign="top" width="200">**MSTest Attribute**</td>       </tr>        <tr>         <td valign="top" width="200">TestFixture</td>          <td valign="top" width="200">TestClass</td>       </tr>        <tr>         <td valign="top" width="200">Test</td>          <td valign="top" width="200">TestMethod</td>       </tr>        <tr>         <td valign="top" width="200">SetUp</td>          <td valign="top" width="200">TestInitialize</td>       </tr>        <tr>         <td valign="top" width="200">TearDown</td>          <td valign="top" width="200">TestCleanup</td>       </tr>        <tr>         <td valign="top" width="200">TestFixtureSetup</td>          <td valign="top" width="200">ClassInitialize</td>       </tr>        <tr>         <td valign="top" width="200">TestFixtureTearDown</td>          <td valign="top" width="200">ClassCleanup</td>       </tr>        <tr>         <td valign="top" width="200"> </td>          <td valign="top" width="200"> </td>       </tr>     </tbody></table>    Replace the following method calls:       

5.  <table border="0" cellspacing="0" cellpadding="2" width="400"><tbody>       <tr>         <td valign="top" width="200">**NUnit Method Code**</td>          <td valign="top" width="200">**MSTest Method Call**</td>       </tr>        <tr>         <td valign="top" width="200">Assert.Ignore</td>          <td valign="top" width="200">Assert.Inconclusive</td>       </tr>     </tbody></table>   

At this point, the easy stuff is done, but Visual Studio will not recognize your project as an MSTest unit test project. (This only applies if you don’t create a new Unit Test project in Visual Studio to hold your converted tests.) If that’s the case, you need to edit the project file using a text editor and add the following tag to the first <PropertyGroup> in the XML:
  <div style="border-bottom: silver 1px solid; border-left: silver 1px solid; padding-bottom: 4px; line-height: 12pt; background-color: #f4f4f4; margin: 20px 0px 10px; padding-left: 4px; width: 97.5%; padding-right: 4px; font-family: 'Courier New', courier, monospace; max-height: 200px; font-size: 8pt; overflow: auto; border-top: silver 1px solid; cursor: text; border-right: silver 1px solid; padding-top: 4px" id="codeSnippetWrapper">   <div style="border-bottom-style: none; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; padding-left: 0px; width: 100%; padding-right: 0px; font-family: 'Courier New', courier, monospace; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px" id="codeSnippet">     

<span style="color: #606060" id="lnum1">   1:</span> <span style="color: #0000ff"><</span><span style="color: #800000">ProjectTypeGuids</span><span style="color: #0000ff">></span>{3AC096D0-A1C2-E12C-1390-A8335801FDAB};{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}<span style="color: #0000ff"></</span><span style="color: #800000">ProjectTypeGuids</span><span style="color: #0000ff">></span>

</div>
</div>



(These Guids are for a C# project. For a VB project, replace the second Guid with {F184B08F-C81C-45F6-A57F-5ABD9991F28F}.)

Depending on the complexity of your original NUnit tests, you may be done at this point. However, if you relied on NUnit TestFixtureSetup or TestFixtureTearDown methods you will need to make a few other changes.

In NUnit, these attributes would be applied to a non-static void method that takes no parameters. For MSTest, the methods must be static and the ClassInitialize method must take a [TestContext](http://msdn.microsoft.com/en-us/library/microsoft.visualstudio.testtools.unittesting.testcontext.aspx) parameter. This also means that you should add a public TestContext property as well. What you end up with is code that looks like this:


<div style="border-bottom: silver 1px solid; border-left: silver 1px solid; padding-bottom: 4px; line-height: 12pt; background-color: #f4f4f4; margin: 20px 0px 10px; padding-left: 4px; width: 97.5%; padding-right: 4px; font-family: 'Courier New', courier, monospace; height: 239px; max-height: 200px; font-size: 8pt; overflow: auto; border-top: silver 1px solid; cursor: text; border-right: silver 1px solid; padding-top: 4px" id="codeSnippetWrapper">
  <div style="border-bottom-style: none; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; padding-left: 0px; width: 100%; padding-right: 0px; font-family: 'Courier New', courier, monospace; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px" id="codeSnippet">
    

<span style="color: #606060" id="lnum1">   1:</span> <span style="color: #0000ff">private</span> TestContext testContextInstance;

<span style="color: #606060" id="lnum2">   2:</span>  

<span style="color: #606060" id="lnum3">   3:</span> <span style="color: #008000">/// <summary></span>

<span style="color: #606060" id="lnum4">   4:</span> <span style="color: #008000">///Gets or sets the test context which provides</span>

<span style="color: #606060" id="lnum5">   5:</span> <span style="color: #008000">///information about and functionality for the current test run.</span>

<span style="color: #606060" id="lnum6">   6:</span> <span style="color: #008000">///</summary></span>

<span style="color: #606060" id="lnum7">   7:</span> <span style="color: #0000ff">public</span> TestContext TestContext

<span style="color: #606060" id="lnum8">   8:</span> {

<span style="color: #606060" id="lnum9">   9:</span>     get

<span style="color: #606060" id="lnum10">  10:</span>     {

<span style="color: #606060" id="lnum11">  11:</span>         <span style="color: #0000ff">return</span> testContextInstance;

<span style="color: #606060" id="lnum12">  12:</span>     }

<span style="color: #606060" id="lnum13">  13:</span>     set

<span style="color: #606060" id="lnum14">  14:</span>     {

<span style="color: #606060" id="lnum15">  15:</span>         testContextInstance = <span style="color: #0000ff">value</span>;

<span style="color: #606060" id="lnum16">  16:</span>     }

<span style="color: #606060" id="lnum17">  17:</span> }

<span style="color: #606060" id="lnum18">  18:</span>  

<span style="color: #606060" id="lnum19">  19:</span> [ClassInitialize()]

<span style="color: #606060" id="lnum20">  20:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">void</span> ClassInit(TestContext context)

<span style="color: #606060" id="lnum21">  21:</span> {

<span style="color: #606060" id="lnum22">  22:</span>     MessageBox.Show(<span style="color: #006080">"ClassInit "</span> + context.TestName);

<span style="color: #606060" id="lnum23">  23:</span> }

<span style="color: #606060" id="lnum24">  24:</span>  

<span style="color: #606060" id="lnum25">  25:</span> [ClassCleanup()]

<span style="color: #606060" id="lnum26">  26:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">void</span> ClassCleanup()

<span style="color: #606060" id="lnum27">  27:</span> {

<span style="color: #606060" id="lnum28">  28:</span>     MessageBox.Show(<span style="color: #006080">"ClassCleanup"</span>);

<span style="color: #606060" id="lnum29">  29:</span> }

</div>
</div>



If you had code in your NUnit TestFixtureSetup or TestFixtureTearDown methods that manipulated non-static data you will need to rework your tests or move that code to a constructor/finalizer combination to achieve the same results.

Unfortunately, the Assert (and related classes) used by MSTest are not as complete as the ones offered by NUnit so you may also end up changing some of your tests. The following Asserts are not available in MSTest:

*   Assert.IsNaN
*   Assert.IsEmpty
*   Assert.IsNotEmpty
*   Assert.Greater
*   Assert.GreaterOrEqual
*   Assert.Less
*   Assert.LessOrEqual
*   Assert.IsAssignableFrom
*   Assert.IsNotAssignableFrom
*   CollectionAssert.IsEmpty
*   CollectionAssert.IsNotEmpty
*   StringAssert.AreEqualIgnoringCase
*   StringAssert.IsMatch
*   FileAssert.AreEqual
*   FileAssert.AreNotEqual



You may be tempted to replace StringAssert.IsMatch with StringAssert.Matches from MSTest but they really aren’t equivalent methods. StringAssert.Matches matches the actual result against a regular expression pattern.

The other thing to watch out for is any place you use the ExpectedException attribute. The syntax is identical between NUnit and MSTest, however the meaning is not. In NUnit, the message parameter is used to verify the message of the exception (by comparing the Message property of the exception with this text). MSTest uses this text as the message to display if the exception is not thrown. There are [better ways]({% post_url 2009/2009-01-17-unit-testing-and-expected-exceptions %}) to test for exceptions that don’t use the ExpectedException attribute at all.

All in all, I’ve been very happy with the relative ease of migrating my NUnit tests to MSTest and using the MSTest framework in general. Yes, there are things that the older unit testing frameworks provide that MSTest does not, but I believe that is just a matter of age. In time, MSTest will offer the same functionality. The nice thing about MSTest is that it is built in to Visual Studio and the code coverage and unit testing capabilities are integrated with the IDE without requiring additional tools, add-ins, macros, or other hoops in order to run your tests and evaluate the results. Everything you need to write effective unit tests, analyze the results and ensure good code coverage is already available to you.


<div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:8e530e48-a136-4398-b4d6-7da6416e2cd3" class="wlWriterSmartContent">*Technorati Tags: [MSTest](http://technorati.com/tags/MSTest), [Unit Tests](http://technorati.com/tags/Unit+Tests), [NUnit](http://technorati.com/tags/NUnit)*</div><div class="wlWriterHeaderFooter" style="text-align:left; margin:0px; padding:4px 4px 4px 4px;">[![DotNetKicks Image](http://www.dotnetkicks.com/Services/Images/KickItImageGenerator.ashx?url=http://geekswithblogs.net/sdorman/archive/2009/01/31/migrating-from-nunit-to-mstest.aspx&bgcolor=0080C0&fgcolor=FFFFFF&border=000000&cbgcolor=D4E1ED&cfgcolor=000000)]({% post_url 2009/2009-01-31-migrating-from-nunit-to-mstest %})</div>
