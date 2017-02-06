---
layout: post
title: Windows PowerShell - Unix comes to Windows
date: '2006-06-18 16:18:00 -05:00'
---

Windows PowerShell (formerly known as "Monad") is a Microsoft's answer to the power and flexibility of the Unix command shells. It should finally complete the Windows management picture by providing a solid command line shell to administer Windows systems. PowerShell is part of Vista, but fortunately for all of us, it is being released separately and is available for Windows XP as well.

PowerShell is a command line shell that is:

* as interactive and composable as bash/ksh (or any other Unix shell)
* as programmatic as Perl or Ruby
* as production oriented as the AS400 CL or VMS DCL languages
* allows access to data stores as easy as if they were a file system
* provides "man-style" help with a rich schema and searching capabilities

PowerShell seems to have incorporated many of the best features of the Unix shells, such as:

* series of profile files that can be run at startup (or logon)
* command aliasing
* prompt customization
* tab completion
* many preferences controllable via variables


### Scripting

* Supports existing scripting models 
* UNIX model of text processing including regular expressions
* Visual Basic Script model of COM automation
* Supports scripting .NET objects
* Support loose, strong, and extensible typing models
* Uniform syntax to access to a wide range of types
    * WMI, XML, COM, ADSI, ADO
* Rich variable semantics (typed, read-only, constraints, descriptions) 
* Rich operators and control structures (Visual C#-like with access to cmds and utilities) 
* Functions (positional, named, typed, constrained params) </UL>

### Text Processing Model

* NET String class is the foundation 
    * Clone, CompareTo, Contains, CopyTo, EndsWith, Equals, IndexOf, IndexOfAny, Insert, LastIndexOf, LastIndexOfAny, Length, PadLeft, PadRight, Remove, Replace, Split, StartsWith, Substring, ToCharArray, ToLower, ToLowerInvariant, ToString, ToUpper, ToUpperInvariant, Trim, TrimEnd, TrimStart
* Native support for useful datatypes
    * REGEX, XML, Arrays, Associative arrays
* Rich string operators
    * +, \*, -f, -replace, -match, -like, -eq, -ne, gt, -ge, -lt, -le 
    * Implicit/explicit casting and coercion
* Here-strings
* Rich control structures
* Rich utilities
    * Select-String, foreach, group, select, sort, where

```    
function top ($property="Handles", [int]$count=10)
{
    Get-Process | sort $property | select –first $count
}
```

For those of you who have written Unix shell scripts before (and maybe a lot of people who haven't) the syntax should look familiar. This declares a function named "top" which takes two paramters (both with defaults) and returns a sorted list of the top `$count` processes sorted by `$property`.
