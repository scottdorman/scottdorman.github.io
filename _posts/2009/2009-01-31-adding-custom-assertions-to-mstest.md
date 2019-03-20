---
layout: post
title: Adding custom assertions to MSTest
date: '2009-01-31 21:10:45 -05:00'
tags: .net unit-testing
---

In my last [post]({% post_url /2009/2009-01-31-migrating-from-nunit-to-mstest %}) I talked about migrating from NUnit to MSTest and mentioned that there were some Assert methods that NUnit provided which did not have corresponding methods in MSTest. For reference, those unavailable Asserts are:

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

Even though MSTest does not provide the same extensibility capabilities as NUnit, it is still possible to add these missing Assert methods by creating your own class library to reference in your unit test project.

In order to help ease any potential issues in migrating from NUnit to MSTest caused by the lack of these Assert methods, I have created a class library that includes all of them except the `FileAssert` methods and `StringAssert.IsMatch`. These methods should behave exactly like they do in NUnit. (In fact, the unit tests are the same ones used in NUnit, with only a few minor differences.)

The following table shows the changes you will need to make in order to use the new asserts. As you can see, the changes can be easily made using search and replace.

|**NUnit**|**MSTest Extension Library**|
|`Assert.IsNaN`|`ConditionAssert.IsNaN`|
|`Assert.IsEmpty`|`CustomAssert.IsEmpty`|
|`Assert.IsNotEmpty`|`CustomAssert.IsNotEmpty`|
|`Assert.Greater`|`ConditionAssert.Greater`|
|`Assert.GreaterOrEqual`|`ConditionAssert.GreaterOrEqual`|
|`Assert.Less`|`ConditionAssert.Less`|
|`Assert.LessOrEqual`|`ConditionAssert.LessOrEqual`|
|`Assert.IsAssignableFrom`|`TypeAssert.IsAssignableFrom`|
|`Assert.IsNotAssignableFrom`|`TypeAssert.IsNotAssignableFrom`|
|`CollectionAssert.IsEmpty`|`CustomAssert.IsEmpty`|
|`CollectionAssert.IsNotEmpty`|`CustomAssert.IsNotEmpty`|
|`StringAssert.AreEqualIgnoringCase`|`CustomAssert.IsNotEmpty`|

I also added the [ExceptionAssert]({% post_url /2009/2009-01-17-unit-testing-and-expected-exceptions %}) class from my post talking about the dangers of using the ExpectedException attribute.

You can [download](http://cid-93d618d639ec9651.skydrive.live.com/self.aspx/Public/Campari.Software.UnitTest.Framework.zip) the class from my [SkyDrive](http://skydrive.live.com/) public folder.
