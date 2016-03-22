---
layout: post
title: FxCop Rules
date: 1/18/2008 1:16:38 AM
---

Earlier this month, the Code Analysis Team [talked](http://blogs.msdn.com/fxcop/archive/2008/01/07/faq-which-rules-shipped-in-which-version.aspx) about which code analysis rules shipped in what version of Visual Studio and FxCop. There is a great [spreadsheet](http://blogs.msdn.com/fxcop/attachment/7018062.ashx) that shows all of the rules and in which versions they are available. Here is the list of rules that are different or removed in Visual Studio 2008 and FxCop 1.36:

**Removed due to removal of data flow engine:** 

*   CA1062 [ValidateArgumentsOfPublicMethods](http://msdn2.microsoft.com/en-us/library/ms182182.aspx)  
*   CA1303 [DoNotPassLiteralsAsLocalizedParameters](http://msdn2.microsoft.com/en-us/library/ms182187(VS.80).aspx)  
*   CA2100 [ReviewSqlQueriesForSecurityVulnerabilities](http://msdn2.microsoft.com/en-us/library/ms182310(VS.80).aspx) 
*   CA2202 [DoNotDisposeObjectsMultipleTimes](http://msdn2.microsoft.com/en-us/library/ms182334(vs.80).aspx)  
*   CA2204 [LiteralsShouldBeSpelledCorrectly](http://msdn2.microsoft.com/en-us/library/bb264488(vs.80).aspx)  
*   CA2215 [DisposeMethodsShouldCallBaseClassDispose](http://msdn2.microsoft.com/en-us/library/ms182330(VS.80).aspx)  
*   CA2241 [ProvideCorrectArgumentsToFormattingMethods](http://msdn2.microsoft.com/en-us/library/ms182361(vs.80).aspx)  
*   CA2000 [DisposeObjectsBeforeLosingScope](http://msdn2.microsoft.com/en-us/library/ms182289(vs.80).aspx) 

**Removed due to high noise or no longer applicable analysis:** 

*   CA1807 [AvoidUnnecessaryStringCreation](http://msdn2.microsoft.com/en-us/library/ms182266(VS.80).aspx)  
*   CA1817 [DoNotCallPropertiesThatCloneValuesInLoops](http://msdn2.microsoft.com/en-us/library/ms182270(VS.80).aspx)  
*   CA1818 [DoNotConcatenateStringsInsideLoops](http://msdn2.microsoft.com/en-us/library/ms182272(vs.80).aspx) 

**Analysis in this rule was moved to [IdentifiersShouldBeCasedCorrectly](http://msdn2.microsoft.com/en-us/library/ms182240(VS.80).aspx):** 

*   CA1705 [LongAcronymsShouldBePascalCased](http://msdn2.microsoft.com/en-us/library/ms182249(VS.80).aspx)  
*   CA1706 [ShortAcronymsShouldBeUppercase](http://msdn2.microsoft.com/en-us/library/ms182256(VS.80).aspx) 

**Analysis in this rule was moved to [IdentifiersShouldNotContainTypeNames](http://msdn2.microsoft.com/de-de/library/bb531486.aspx):** 

*   CA1718 [AvoidLanguageSpecificTypeNamesInParameters](http://msdn2.microsoft.com/en-us/library/ms182233(VS.80).aspx) 

**Analysis in this rule was moved to [OverrideLinkDemandsShouldBeIdenticalToBase](http://msdn2.microsoft.com/en-us/library/ms182305(VS.80).aspx):** 

*   CA2110 [SecureGetObjectDataOverrides](http://msdn2.microsoft.com/en-us/library/ms182315(VS.80).aspx) 

The part that I find most surprising and troubling are the rules that were removed because of the removal of the data flow engine. I understand the reasoning and look forward to seeing the new engine based on the [Phoenix](http://research.microsoft.com/phoenix/ "Phoenix") technology.

The other interesting thing is how similar the rules are between the integrated code analysis in Visual Studio and the stand-alone FxCop 1.36 release. It's good to see Microsoft continuing to keep these in sync, although it would be good if the code metrics related rules were also included in FxCop.
