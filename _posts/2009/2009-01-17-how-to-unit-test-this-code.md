---
layout: post
title: How to unit test this code?
date: 2009-01-17 22:35:24 -05:00
---

This question is for all of the TDD and unit test folks, so I’m hoping someone comes up with an answer.

I’ve been writing unit tests and analyzing code coverage for one of my libraries for about a week now and I’m starting to see the end, at least for this particular library. However, I’ve run in to a problem trying to ensure as close to 100% code coverage as possible. This exists in several methods in a few different classes, but I’ll take the simplest one for illustration purposes.

I have cod that looks like this:
  <div style="border-bottom: silver 1px solid; border-left: silver 1px solid; padding-bottom: 4px; line-height: 12pt; background-color: #f4f4f4; margin: 20px 0px 10px; padding-left: 4px; width: 97.5%; padding-right: 4px; font-family: 'Courier New', courier, monospace; height: 520px; max-height: 3500px; font-size: 8pt; overflow: auto; border-top: silver 1px solid; cursor: text; border-right: silver 1px solid; padding-top: 4px" id="codeSnippetWrapper">   <div style="border-bottom-style: none; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; padding-left: 0px; width: 100%; padding-right: 0px; font-family: 'Courier New', courier, monospace; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px" id="codeSnippet">     

<span style="color: #606060" id="lnum1">   1:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> ProcessorArchitecture GetProcessorArchitecture()

<span style="color: #606060" id="lnum2">   2:</span> {

<span style="color: #606060" id="lnum3">   3:</span>     SYSTEM_INFO sysInfo = <span style="color: #0000ff">new</span> SYSTEM_INFO();

<span style="color: #606060" id="lnum4">   4:</span>  

<span style="color: #606060" id="lnum5">   5:</span>     <span style="color: #0000ff">if</span> (Environment.OSVersion.Version.Major > 5 || (Environment.OSVersion.Version.Major == 5 && Environment.OSVersion.Version.Minor >= 1))

<span style="color: #606060" id="lnum6">   6:</span>     {

<span style="color: #606060" id="lnum7">   7:</span>         SafeNativeMethods.GetNativeSystemInfo(<span style="color: #0000ff">out</span> sysInfo);

<span style="color: #606060" id="lnum8">   8:</span>     }

<span style="color: #606060" id="lnum9">   9:</span>     <span style="color: #0000ff">else</span>

<span style="color: #606060" id="lnum10">  10:</span>     {

<span style="color: #606060" id="lnum11">  11:</span>         SafeNativeMethods.GetSystemInfo(<span style="color: #0000ff">out</span> sysInfo);

<span style="color: #606060" id="lnum12">  12:</span>     }

<span style="color: #606060" id="lnum13">  13:</span>  

<span style="color: #606060" id="lnum14">  14:</span>     ProcessorArchitecture architecture = ProcessorArchitecture.Unknown;

<span style="color: #606060" id="lnum15">  15:</span>     <span style="color: #0000ff">switch</span> (sysInfo.uProcessorInfo.processorArchitecture.wProcessorArchitecture)

<span style="color: #606060" id="lnum16">  16:</span>     {

<span style="color: #606060" id="lnum17">  17:</span>         <span style="color: #0000ff">case</span> Constants.PROCESSOR_ARCHITECTURE_AMD64:

<span style="color: #606060" id="lnum18">  18:</span>             architecture = ProcessorArchitecture.X64;

<span style="color: #606060" id="lnum19">  19:</span>             <span style="color: #0000ff">break</span>;

<span style="color: #606060" id="lnum20">  20:</span>  

<span style="color: #606060" id="lnum21">  21:</span>         <span style="color: #0000ff">case</span> Constants.PROCESSOR_ARCHITECTURE_IA64:

<span style="color: #606060" id="lnum22">  22:</span>             architecture = ProcessorArchitecture.Itanium;

<span style="color: #606060" id="lnum23">  23:</span>             <span style="color: #0000ff">break</span>;

<span style="color: #606060" id="lnum24">  24:</span>  

<span style="color: #606060" id="lnum25">  25:</span>         <span style="color: #0000ff">case</span> Constants.PROCESSOR_ARCHITECTURE_INTEL:

<span style="color: #606060" id="lnum26">  26:</span>             architecture = ProcessorArchitecture.X86;

<span style="color: #606060" id="lnum27">  27:</span>             <span style="color: #0000ff">break</span>;

<span style="color: #606060" id="lnum28">  28:</span>     }

<span style="color: #606060" id="lnum29">  29:</span>  

<span style="color: #606060" id="lnum30">  30:</span>     <span style="color: #0000ff">return</span> architecture;

<span style="color: #606060" id="lnum31">  31:</span> }

</div>
</div>



My unit test for this particular method is relatively simple as well:


<div style="border-bottom: silver 1px solid; border-left: silver 1px solid; padding-bottom: 4px; line-height: 12pt; background-color: #f4f4f4; margin: 20px 0px 10px; padding-left: 4px; width: 97.5%; padding-right: 4px; font-family: 'Courier New', courier, monospace; height: 150px; max-height: 200px; font-size: 8pt; overflow: auto; border-top: silver 1px solid; cursor: text; border-right: silver 1px solid; padding-top: 4px" id="codeSnippetWrapper">
  <div style="border-bottom-style: none; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; padding-left: 0px; width: 100%; padding-right: 0px; font-family: 'Courier New', courier, monospace; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px" id="codeSnippet">
    

<span style="color: #606060" id="lnum1">   1:</span> [TestMethod]

<span style="color: #606060" id="lnum2">   2:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">void</span> GetProcessorArchitecture()

<span style="color: #606060" id="lnum3">   3:</span> {

<span style="color: #606060" id="lnum4">   4:</span>     ProcessorArchitecture expected = ProcessorArchitecture.X86;

<span style="color: #606060" id="lnum5">   5:</span>     ProcessorArchitecture actual = ExtendedEnvironment.GetProcessorArchitecture();

<span style="color: #606060" id="lnum6">   6:</span>     Assert.IsTrue(actual == expected);

<span style="color: #606060" id="lnum7">   7:</span> }

</div>
</div>



The problem here is that not all of this method is able to covered. Specifically, the else clause and the first two cases in the switch. Short of physically changing hardware or operating systems, how do I actually unit test those conditions? I don’t think creating a mock object will help in this case, as the object I would need to mock is the System.Environment object and then somehow be able to alter the processor architecture field of the SYSTEM_INFO struct that is returned from GetSystemInfo().

I realize this is a somewhat trivial example, but I think it does clearly demonstrate the impossibility of achieving 100% code coverage through unit tests.
<div class="wlWriterHeaderFooter" style="text-align:left; margin:0px; padding:4px 4px 4px 4px;">[![DotNetKicks Image](http://www.dotnetkicks.com/Services/Images/KickItImageGenerator.ashx?url=http://geekswithblogs.net/sdorman/archive/2009/01/17/how-to-unit-test-this-code.aspx&bgcolor=0080C0&fgcolor=FFFFFF&border=000000&cbgcolor=D4E1ED&cfgcolor=000000)]({% post_url 2009/2009-01-17-how-to-unit-test-this-code %})</div>
