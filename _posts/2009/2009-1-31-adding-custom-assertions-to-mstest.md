---
layout: post
title: Adding custom assertions to MSTest
date: 1/31/2009 9:10:45 PM
---

In my last [post](http://geekswithblogs.net/sdorman/archive/2009/01/31/migrating-from-nunit-to-mstest.aspx) I talked about migrating from NUnit to MSTest and mentioned that there were some Assert methods that NUnit provided which did not have corresponding methods in MSTest. For reference, those unavailable Asserts are:

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

Even though MSTest does not provide the same extensibility capabilities as NUnit, it is still possible to add these missing Assert methods by creating your own class library to reference in your unit test project.

In order to help ease any potential issues in migrating from NUnit to MSTest caused by the lack of these Assert methods, I have created a class library that includes all of them except the FileAssert methods and StringAssert.IsMatch. These methods should behave exactly like they do in NUnit. (In fact, the unit tests are the same ones used in NUnit, with only a few minor differences.)

The following table shows the changes you will need to make in order to use the new asserts. As you can see, the changes can be easily made using search and replace.
  <table border="0" cellspacing="0" cellpadding="2" width="460"><tbody>     <tr>       <td valign="top" width="224">**NUnit**</td>        <td valign="top" width="46">****</td>        <td valign="top" width="188">**MSTest Extension Library**</td>     </tr>      <tr>       <td valign="top" width="224">Assert.IsNaN</td>        <td valign="top" width="46"> </td>        <td valign="top" width="188">ConditionAssert.IsNaN</td>     </tr>      <tr>       <td valign="top" width="224">Assert.IsEmpty</td>        <td valign="top" width="46"> </td>        <td valign="top" width="188">CustomAssert.IsEmpty</td>     </tr>      <tr>       <td valign="top" width="224">Assert.IsNotEmpty</td>        <td valign="top" width="46"> </td>        <td valign="top" width="188">CustomAssert.IsNotEmpty</td>     </tr>      <tr>       <td valign="top" width="224">Assert.Greater</td>        <td valign="top" width="46"> </td>        <td valign="top" width="188">ConditionAssert.Greater</td>     </tr>      <tr>       <td valign="top" width="224">Assert.GreaterOrEqual</td>        <td valign="top" width="46"> </td>        <td valign="top" width="188">ConditionAssert.GreaterOrEqual</td>     </tr>      <tr>       <td valign="top" width="224">Assert.Less</td>        <td valign="top" width="46"> </td>        <td valign="top" width="188">ConditionAssert.Less</td>     </tr>      <tr>       <td valign="top" width="224">Assert.LessOrEqual</td>        <td valign="top" width="46"> </td>        <td valign="top" width="188">ConditionAssert.LessOrEqual</td>     </tr>      <tr>       <td valign="top" width="224">Assert.IsAssignableFrom</td>        <td valign="top" width="46"> </td>        <td valign="top" width="188">TypeAssert.IsAssignableFrom</td>     </tr>      <tr>       <td valign="top" width="224">Assert.IsNotAssignableFrom</td>        <td valign="top" width="46"> </td>        <td valign="top" width="188">TypeAssert.IsNotAssignableFrom</td>     </tr>      <tr>       <td valign="top" width="224">CollectionAssert.IsEmpty</td>        <td valign="top" width="46"> </td>        <td valign="top" width="188">CustomAssert.IsEmpty</td>     </tr>      <tr>       <td valign="top" width="224">CollectionAssert.IsNotEmpty</td>        <td valign="top" width="46"> </td>        <td valign="top" width="188">CustomAssert.IsNotEmpty</td>     </tr>      <tr>       <td valign="top" width="224">StringAssert.AreEqualIgnoringCase</td>        <td valign="top" width="46"> </td>        <td valign="top" width="188">CustomAssert.IsNotEmpty</td>     </tr>   </tbody></table>  

I also added the [ExceptionAssert](http://geekswithblogs.net/sdorman/archive/2009/01/17/unit-testing-and-expected-exceptions.aspx) class from my post talking about the dangers of using the ExpectedException attribute.

You can [download](http://cid-93d618d639ec9651.skydrive.live.com/self.aspx/Public/Campari.Software.UnitTest.Framework.zip) the class from my [SkyDrive](http://skydrive.live.com/) public folder.
  <div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:9a58342b-8105-4724-bead-1f703b65db4d" class="wlWriterSmartContent">*Technorati Tags: [Unit Tests](http://technorati.com/tags/Unit+Tests), [MSTest](http://technorati.com/tags/MSTest), [NUnit](http://technorati.com/tags/NUnit)*</div><div class="wlWriterHeaderFooter" style="text-align:left; margin:0px; padding:4px 4px 4px 4px;">[![DotNetKicks Image](http://www.dotnetkicks.com/Services/Images/KickItImageGenerator.ashx?url=http://geekswithblogs.net/sdorman/archive/2009/01/31/adding-custom-assertions-to-mstest.aspx&bgcolor=0080C0&fgcolor=FFFFFF&border=000000&cbgcolor=D4E1ED&cfgcolor=000000)](http://www.dotnetkicks.com/kick/?url=http://geekswithblogs.net/sdorman/archive/2009/01/31/adding-custom-assertions-to-mstest.aspx)</div>
