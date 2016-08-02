---
layout: post
title: Migrating from NUnit to MSTest
date: 2009-01-31 12:39:15 -05:00
---

I have been writing a lot of unit tests over the past month using the Microsoft Test (MSTest) unit testing framework that is now part of Visual Studio 2008 Professional Edition (and higher SKUs). Currently I have about 223 unit tests covering 39 classes (about 18K lines of code, 325 methods and 176 properties) with a code coverage percent of 97%.

The classes that I'm testing previously had NUnit tests (although not as many as I currently have) and used NCover and NCover Explorer for my code coverage analysis. I had looked at MSTest when it first came out and decided against using it because it was only available in the Visual Studio Team System SKUs, which meant it wasn't generally available to the development community at large, and required Visual Studio to be installed in order to use it.

Since then, Microsoft has addressed both of those issues and I decided it was time to give MSTest another look. In doing so, I decided to see if it would be possible to leverage the existing NUnit tests rather than starting completely from scratch. One word of caution...if you use the newer constraint model in NUnit, your unit tests will not easily migrate to MSTest and you are probably better off starting fresh using MSTest.

It turned out to be a relatively painless process that can be broken down to the following steps:

1.  Replace the reference to the `Nunit.Framework` assembly with a reference to the `Microsoft.VisualStudio.QualityTools.UnitTestFramework` assembly.
2.  Replace the `using Nunit.Framework` line with `using Microsoft.VisualStudio.TestTools.UnitTesting`
3.  For each file containing unit tests, replace the following attributes (you can use global search and replace for this): 
|**NUnit Attribute**|**MSTest Attribute**|
|TestFixture|TestClass|
|Test|TestMethod|
|SetUp|TestInitialize|
|TearDown|TestCleanup|
|TestFixtureSetup|ClassInitialize|
|TestFixtureTearDown|ClassCleanup|      

4. Replace the following method calls:       
|**NUnit Method Code**|**MSTest Method Call**|
|Assert.Ignore|Assert.Inconclusive|

At this point, the easy stuff is done, but Visual Studio will not recognize your project as an MSTest unit test project. (This only applies if you don't create a new Unit Test project in Visual Studio to hold your converted tests.) If that's the case, you need to edit the project file using a text editor and add the following tag to the first <PropertyGroup> in the XML:

```xml
<ProjectTypeGuids>{3AC096D0-A1C2-E12C-1390-A8335801FDAB};{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}</ProjectTypeGuids> 
```

(These Guids are for a C# project. For a VB project, replace the second Guid with {F184B08F-C81C-45F6-A57F-5ABD9991F28F}.)

Depending on the complexity of your original NUnit tests, you may be done at this point. However, if you relied on NUnit TestFixtureSetup or TestFixtureTearDown methods you will need to make a few other changes.

In NUnit, these attributes would be applied to a non-static void method that takes no parameters. For MSTest, the methods must be static and the ClassInitialize method must take a [TestContext](http://msdn.microsoft.com/en-us/library/microsoft.visualstudio.testtools.unittesting.testcontext.aspx) parameter. This also means that you should add a public TestContext property as well. What you end up with is code that looks like this:


```csharp
private TestContext testContextInstance;

/// <summary>
///Gets or sets the test context which provides
///information about and functionality for the current test run.
///</summary>
public TestContext TestContext
{
    get
    {
        return testContextInstance;
    }

    set
    {
        testContextInstance = value;
    }
}

[ClassInitialize()]
void ClassInit(TestContext context)
{
    MessageBox.Show("ClassInit " + context.TestName);
}

[ClassCleanup()]
void ClassCleanup()
{
    MessageBox.Show("ClassCleanup");
}
```

If you had code in your NUnit `TestFixtureSetup` or `TestFixtureTearDown` methods that manipulated non-static data you will need to rework your tests or move that code to a constructor/finalizer combination to achieve the same results.

Unfortunately, the `Assert` (and related classes) used by MSTest are not as complete as the ones offered by NUnit so you may also end up changing some of your tests. The following Asserts are not available in MSTest:

* `Assert.IsNaN`
* `Assert.IsEmpty`
* `Assert.IsNotEmpty`
* `Assert.Greater`
* `Assert.GreaterOrEqual`
* `Assert.Less`
* `Assert.LessOrEqual`
* `Assert.IsAssignableFrom`
* `Assert.IsNotAssignableFrom`
* `CollectionAssert.IsEmpty`
* `CollectionAssert.IsNotEmpty`
* `StringAssert.AreEqualIgnoringCase`
* `StringAssert.IsMatch`
* `FileAssert.AreEqual`
* `FileAssert.AreNotEqual`

You may be tempted to replace `StringAssert.IsMatch` with `StringAssert.Matches` from MSTest but they really aren't equivalent methods. `StringAssert.Matches` matches the actual result against a regular expression pattern.

The other thing to watch out for is any place you use the `ExpectedException` attribute. The syntax is identical between NUnit and MSTest, however the meaning is not. In NUnit, the message parameter is used to verify the message of the exception (by comparing the Message property of the exception with this text). MSTest uses this text as the message to display if the exception is not thrown. There are [better ways]({% post_url /2009/2009-01-17-unit-testing-and-expected-exceptions %}) to test for exceptions that don't use the ExpectedException attribute at all.

All in all, I've been very happy with the relative ease of migrating my NUnit tests to MSTest and using the MSTest framework in general. Yes, there are things that the older unit testing frameworks provide that MSTest does not, but I believe that is just a matter of age. In time, MSTest will offer the same functionality. The nice thing about MSTest is that it is built in to Visual Studio and the code coverage and unit testing capabilities are integrated with the IDE without requiring additional tools, add-ins, macros, or other hoops in order to run your tests and evaluate the results. Everything you need to write effective unit tests, analyze the results and ensure good code coverage is already available to you.
