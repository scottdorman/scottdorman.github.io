---
layout: post
title: Visual Studio, .NET Framework, and language versions
date: '2010-04-23 16:03:49 -05:00'
tags: visual-studio .net
---

Every so often a question comes up about how Visual Studio, the .NET Framework, and a .NET programming language relate to each other. Mostly, these questions have to do with versions. The reality is that these are actually three different "products" that are versioned independently of each other but are related.

Looking at how Visual Studio, the .NET Framework version, and the CLR versions relate to each other results in the following:

| **Visual Studio** | **CLR** | **.NET Framework** |
| ----------------- | ------- | ------------------ |
| Visual Studio .NET (Ranier) | 1.0.3705 | 1.0 |
| Visual Studio 2003 (Everett) | 1.1.4322 | 1.1 |
| Visual Studio 2005 (Whidbey) | 2.0.50727 |2.0 |
| Visual Studio 2005 with .NET 3.0 Extensions | 2.0.50727 | 2.0, 3.0 |
| Visual Studio 2008 (Orcas) | 2.0.50727 | 2.0 SP1, 3.0 SP1, 3.5 |
| Visual Studio 2008 SP1 | 2.0.50727 | 2.0 SP2, 3.0 SP2, 3.5 SP1 |
| Visual Studio 2010 (Hawaii) | 4.0.30319 | 4.0 |

The actual Visual Studio version numbers are:

| **Product Name** | **Version** | **Ship Date** |
| ----------------- | ------- | ------------------ |
| Visual Studio .NET | 7.0.???? | 02/2002 |
| Visual Studio .NET 2002 SP1 | 7.0.???? |   |
| Visual Studio 2003 | 7.1.???? | 04/2003 |
| Visual Studio 2003 SP1 | 7.1.6030 | 09/13/2006 |
| Visual Studio 2005 | 8.0.5072 |   |
| Visual Studio 2005 SP1 |   | 12/14/2006 |
| Visual Studio 2008 | 9.0.21022.8 | 11/19/2007 |
| Visual Studio 2008 SP1 | 9.0.30729.1 |   | 
| Visual Studio 2010 | 10.0.30319.1 | 04/12/2010 |

(For those entries that are missing information, it simply means that I didn't already know it and/or couldn't easily find it online.)

So far, everything seems fairly reasonable and isn't terribly difficult to keep coordinated. However, when you start trying to find language versions and how those relate to .NET Framework, CLR, or Visual Studio releases it becomes more difficult.

The breakdown for the programming languages that are part of Visual Studio are:

| **Framework** | **CLR**  | **C#** | **VB** | **F#** |
| ------------- | -------- | ------ | ------ | ------ |
| 1.0 | 1.0.3705 | 1.0 | 7.0 | |
| 1.1 | 1.1.4322 | 1.1 | 7.1 | |
| 2.0 | 2.0.50727 | 2.0 | 8.0 | |
| 3.0 | 2.0.50727 | 2.0 | 8.0 | |
| 3.5 | 2.0.50727 | 3.0 | 9.0 | |
| 4.0 | 4.0.30319 | 4.0 | 10.0 | 2.0 |
  