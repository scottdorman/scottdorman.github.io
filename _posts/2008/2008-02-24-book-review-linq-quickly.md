---
layout: post
title: "Book Review: LINQ Quickly"
date: 2008-02-24 19:40:59 -05:00
---

[![LINQ Quickly](http://images.packtpub.com/images/100x123/1847192548.png "LINQ Quickly")](http://www.packtpub.com/#)

I was recently introduced to a UK based publisher called [Pact Publishing](http://www.packtpub.com). They are a UK based publisher and have a book focused on the new Language Integrated Query (LINQ) features available in .NET 3.5 called [LINQ Quickly: A practical guide to programming Language Integrated Query with C#](http://amzn.to/28KvxCq) by N Satheesh Kumar.

The book provides a good overview of LINQ and it's supporting language features, such as anonymous types, implicit typing, object initializers, extension methods, and expressions. It then builds on that introduction to cover the various LINQ implementations, such as LINQ to Objects, LINQ to XML, and LINQ to SQL. A very thorough look at the different Standard Query Operators closes the book.

Also provided are two simple examples that really help highlight the power and flexibility of LINQ. The first example shows how to create a web site that uses LINQ to populate a data grid and some form elements. The other example shows how to use LINQ against the Outlook object model to retrieve the details of an Outlook contact.

One thing that this book mentions very clearly that hasn't been talked about much is that LINQ to SQL is able to make use of not just embedded SQL but also stored procedures and walks the reader through the steps necessary in order to make effective use of LINQ and stored procedures.

As I mentioned, the last chapter provides a very thorough look at the Standard Query Operators and breaks them up into the different types:

Operators | Description
------------ | -------------
Aggregation | Used to compute a single value from a collection of values.
Projection | Used to transform elements.
Concatenation | Used to concatenate one sequence to another.
Element | Used to return a single element from a sequence of elements.
Conversion | Used to change the type of the input object.
Equality | Used to check for equality of two sequences.
Generation | Used for generating a new sequence of values.
Grouping | Used for grouping elements together that share a common attribute.
Join | Used to associate objects from one data source with objects in another data source based on a common attribute.
Partitioning | Used to divide an input sequence into two or more sections and then return the one section that is required.
Quantifiers | Used to perform the operation of checking whether some or all of the elements in a sequence satisfy a condition.
Restriction | Used to restrict the query result to contain elements that satisfy the specific condition.
Set | Used to get the result sets based on the presence or absence of equivalent elements in the same or another collection.
Ordering | Used for ordering elements in a sequence based on one or more attributes.

While the style of writing in the book was a little hard to follow, the technical content of the book appeared to be both accurate and thorough, taking the most in-depth look at LINQ to XML and then the Standard Query operators.
