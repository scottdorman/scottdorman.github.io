---
layout: post
title: Code Contracts in .NET
date: 2009-03-02 18:44:15 -05:00
---

[![dd491992_codecontracts_project(en-us)](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/CodeContractsin.NET_10367/dd491992_codecontracts_project(en-us)_thumb.png "dd491992_codecontracts_project(en-us)")](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/CodeContractsin.NET_10367/dd491992_codecontracts_project(en-us)_2.png) 

I have [previously](http://geekswithblogs.net/sdorman/archive/2008/12/10/more-on-.net-4.0-code-contracts.aspx) talked about code contracts in .NET 4.0, and while .NET 4.0 isn’t out yet you can work with them now in Visual Studio 2008 through [MSDN DevLabs](http://msdn.microsoft.com/en-us/devlabs/dd491992.aspx).

In case you aren’t familiar with code contracts in .NET, this is a feature that was actually built by the .NET CLR team to provide a language-agnostic way to express code assumptions in the form of pre-conditions, post-conditions, and object invariants.

There are currently two tools provided:

*   **Runtime Checking**, which uses a binary rewriter to modify a program by injecting the contracts, which are checked as part of program execution.
*   **Static Checking **can decide if there are any contract violations without even running the program. It checks for implicit contracts, such as null dereferences and array bounds, as well as the explicit contracts.   

This is definitely something to take a look at and start getting familiar with in order to simplify your code and testing.
  <div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:3fb497fb-909c-4674-a27d-5ae1a6ce58c2" class="wlWriterEditableSmartContent">Technorati Tags: [Code Contracts](http://technorati.com/tags/Code+Contracts),[.NET](http://technorati.com/tags/.NET)</div>
