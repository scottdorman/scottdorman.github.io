---
layout: post
title: Windows PowerShell - Unix comes to Windows
date: 2006-06-18 16:18:00 -04:00
---

<P>Windows PowerShell (formerly known as “Monad”) is a Microsoft's answer to the power and flexibility of the Unix command shells. It should finally complete the Windows management picture by providing a solid command line shell to administer Windows systems. PowerShell is part of Vista, but fortunately for all of us, it is being released separately and is available for Windows XP as well.</P>
<P>PowerShell is a command line shell that is:</P>
<UL>
<LI>as interactive and composable as bash/ksh (or any other Unix shell)</LI>
<LI>as programmatic as Perl or Ruby</LI>
<LI>as production oriented as the AS400 CL or VMS DCL languages</LI>
<LI>allows access to data stores as easy as if they were a file system</LI>
<LI>provides “man-style“ help with a rich schema and searching capabilities</LI></UL>
<P><SPAN><SPAN>PowerShell seems to have incorporated many of the best features of the Unix shells, such as:</SPAN></SPAN></P>
<UL>
<LI>
<DIV v:shape="_x0000_s1026"><SPAN>series of profile files that can be run at startup (or logon)</SPAN></DIV></LI>
<LI>
<DIV v:shape="_x0000_s1026"><SPAN><SPAN><SPAN>command aliasing </SPAN></SPAN></SPAN></DIV></LI>
<LI><SPAN><SPAN>
<DIV v:shape="_x0000_s1026"><SPAN><SPAN>prompt customization</SPAN></SPAN></DIV></SPAN></SPAN></LI>
<LI><SPAN><SPAN>
<DIV v:shape="_x0000_s1026">
<DIV><SPAN>
<DIV v:shape="_x0000_s1026">
<DIV><SPAN><SPAN>tab completion</SPAN></SPAN></DIV></DIV></SPAN></DIV></DIV></SPAN></SPAN></LI>
<LI><SPAN><SPAN>
<DIV v:shape="_x0000_s1026">
<DIV><SPAN>
<DIV v:shape="_x0000_s1026">
<DIV></SPAN></SPAN></SPAN><SPAN><SPAN><SPAN><SPAN><SPAN><SPAN>many preferences controllable via variables</SPAN></SPAN></DIV></DIV></DIV></DIV></LI></SPAN>
<DIV></DIV></SPAN>
<DIV></DIV></SPAN></SPAN></UL>
<P><SPAN><SPAN>Scripting</SPAN></SPAN></P>
<UL>
<LI><SPAN><SPAN>Supports existing scripting models </SPAN></SPAN></LI>
<LI><SPAN><SPAN>U</SPAN><SPAN>NIX model of text processing including regular expressions </SPAN></SPAN></LI>
<LI><SPAN><SPAN></SPAN><SPAN>Visual Basic Script model of COM automation </SPAN></SPAN></LI>
<LI><SPAN><SPAN></SPAN><SPAN>Supports scripting .NET objects </SPAN></SPAN></LI>
<LI><SPAN><SPAN></SPAN><SPAN>Support loose, strong, and extensible typing models </SPAN></SPAN></LI>
<LI><SPAN><SPAN></SPAN><SPAN>Uniform syntax to access to a wide range of types </SPAN></SPAN></LI>
<UL>
<LI><SPAN><SPAN></SPAN><SPAN>WMI, XML, COM, ADSI, ADO </SPAN></LI></UL>
<LI>
<DIV v:shape="_x0000_s1026"><SPAN>Rich variable semantics (typed, read-only, constraints, descriptions) </SPAN></DIV></LI>
<LI>
<DIV v:shape="_x0000_s1026"><SPAN>Rich operators and control structures (Visual C#-like with access to cmds </SPAN><SPAN>and utilities) </SPAN></DIV></LI>
<LI>
<DIV v:shape="_x0000_s1026"><SPAN></SPAN><SPAN>Functions (positional, named, typed, constrained params) </SPAN></DIV></LI></UL>
<P v:shape="_x0000_s1026"><SPAN>Text Processing Model</SPAN></P>
<P v:shape="_x0000_s1026"></P>
<DIV v:shape="_x0000_s1026">
<UL>
<LI><SPAN>NET String class is the foundation </SPAN></LI>
<UL>
<LI><SPAN></SPAN><SPAN>Clone, CompareTo, Contains, CopyTo, EndsWith, Equals, IndexOf, </SPAN><SPAN>IndexOfAny, Insert,<SPAN>  </SPAN>LastIndexOf, LastIndexOfAny, Length, PadLeft, PadRight, </SPAN><SPAN>Remove, Replace, Split, StartsWith, Substring, ToCharArray, ToLower, </SPAN><SPAN>ToLowerInvariant, ToString, ToUpper, ToUpperInvariant, Trim, TrimEnd, </SPAN><SPAN>TrimStart </SPAN></LI></UL>
<LI><SPAN>Native support for useful datatypes </SPAN></LI>
<UL>
<LI><SPAN>REGEX, XML, Arrays, Associative arrays, </SPAN></LI></UL>
<LI><SPAN>Rich string operators </SPAN></LI>
<UL>
<LI><SPAN>+, *, -f, -replace, -match, -like, -eq, -ne, gt, -ge, -lt, -le </SPAN></LI>
<LI><SPAN>Implicit/explicit casting and coercion </SPAN></LI></UL>
<LI><SPAN>Here-strings </SPAN></LI>
<LI><SPAN>Rich control structures </SPAN></LI>
<LI><SPAN>Rich utilities </SPAN></LI>
<UL>
<LI><SPAN>Select-String, foreach, group, select, sort, where </SPAN></LI></UL></UL>
<DIV></DIV></DIV></SPAN>
<P></P>
<DIV v:shape="_x0000_s1026">
<DIV><SPAN><FONT face="Courier New">function top ($property=“Handles”, [int]$count=10) </FONT></SPAN></DIV>
<DIV><SPAN><FONT face="Courier New">{ <BR></FONT></SPAN><FONT face="Courier New"><SPAN><SPAN>   </SPAN>Get-Process | sort $property | select –first $count <BR></SPAN><SPAN>} </SPAN></FONT></DIV>
<DIV> </DIV>
<DIV>For those of you who have written Unix shell scripts before (and maybe a lot of people who haven't) the syntax should look familiar. This declares a function named “top” which takes two paramters (both with defaults) and returns a sorted list of the top $count processes sorted by $property.</DIV>
<DIV> </DIV>
<DIV> </DIV></DIV>
