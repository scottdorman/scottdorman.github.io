---
layout: post
title: Introducing Cadru 2.0
date: '2015-11-10 20:07:52 -05:00'
---

Just over two years ago, Cadru was released as an open source framework. Since then, there have been numerous changes, improvements, and updates. This latest update includes a lot of new features and, unfortunately, one breaking change.

## First up, the breaking change.

In an earlier release, [ToRelativeTimeString](https://github.com/scottdorman/cadru/commit/6102e4fdeeddcb6a28cfb10c2c38498ed97bc632) and [ToRelativeDateString](https://github.com/scottdorman/cadru/commit/45286b8f617f7fbf1a46838595f1fb0460e22882) methods were added that included a formatting options enum named RelativeDateFormattingOptions. The problem is that this was a plural name for a non-flags enum and it really didn't portray the meaning of the enum very well. This has been renamed to just RelativeDateFormatting.

## Now, for the new features.

A new extension method on IEnumerable has been added called Partition. This takes an IEnumerable and breaks it up into smaller collections of equal size. If there aren't enough elements to fully populate the final partition, it's the size of the number of elements.

```csharp
int[] numbers = { 0, 30, 20, 15, 90, 85, 40, 75 }; 
var partitions = numbers.Partition(3).ToArray(); 

// partitions[0] = { 0, 30, 20 }
// partitions[1] = { 15, 90, 85 }
// partitions[2] = { 40, 75 }
```

Next is a simple [ReverseComparisonComparer](https://github.com/scottdorman/cadru/commit/6d3f6ebdd7bf94f8da4c505e2a2d126a103eadf7). This takes a given Comparison<T> instance and reverses the Compare operation.

The code contracts classes, [Requires and Assumes](https://github.com/scottdorman/cadru/commit/5116b74f3e6388f26c8d0f115c7c794e2fc72712), also gained a method to test if a parameter is of a given type and one to test if it's an enum.

The Cadru.UnitTest.Framework library also picked up a change by adding a [WithInnerException](https://github.com/scottdorman/cadru/commit/c4cd4d9ea04ec71c7c42e7bc108322a81496dbec) method on ExceptionAssert. This allows you to assert that the inner exception of a thrown exception is a specific exception type.

Enumerated types also [gained some new methods](https://github.com/scottdorman/cadru/commit/187f1970f528894d59be54105239870ecafbe83b). Cadru always had extension methods on enums, one of which was GetDescription, which would return the value of an EnumDescription attribute applied to an enum member. When the strongly typed Enum<T> class was introduced, it was purely a strongly typed pass-through for the methods exposed by the standard Enum class. With this latest release, Enum<T> gains GetDescription and GetDescriptions. In addition, to keep things consistent, the GetDescription extension method has been updated to behave in the same way as Enum<T>.GetDescription, specifically, if an EnumDescription attribute does not exist, it returns null. To keep this from being a breaking change, this behavior was introduced as a new overload.

Finally, and probably the biggest addition to this release, is support for Ranges, through the Range<T> class. This allows easy creation of a range of values. Since it's a generic class, you can create a range over pretty much any data type. Ranges are similar to a mathematical interval and allow you to include or exclude either endpoint (using standard interval notation), provide intersection and union operations, and be enumerable using a default enumeration function or a custom function. (I will describe ranges in much more detail in a separate blog post.)

```csharp
var range = new Range<char>('a', 'e', RangeEndpointOption.Closed);
range.SetDefaultEnumerator();
var expanded = range.ToList();

// expanded = {'b', 'c', 'd' }
```

## Unit tests and code coverage

Ever since Cadru was first created (long before it became an open source framework), it always had good unit tests and code coverage. I'm very happy that tradition has continued. Even with all of the new changes (about 26 files spread over 15 different commits), I'm still at 89.49% code coverage for the entire library (all 4 projects) and 98.41% code coverage for Cadru.Core where almost all of these changes took place (according to the analysis tools built in to Visual Studio).

Be sure to check out the newest release on [NuGet](https://www.nuget.org/packages?q=Tags%3A%22cadru%22).

## Bugs and feature requests

Do you have a bug or a feature request? Please use the [issue tracker](https://github.com/scottdorman/cadru/issues) and search for existing and closed issues. If your problem or request isn't addressed yet, go ahead and [open a new issue](https://github.com/scottdorman/cadru/issues/new). 

## Contributing

You can also get involved and [fork the repository](https://github.com/scottdorman/cadru/fork) to submit your own pull requests. (More detailed contributor guidelines will be available soon.)
