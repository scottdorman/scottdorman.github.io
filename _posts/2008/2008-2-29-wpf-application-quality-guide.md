---
layout: post
title: WPF Application Quality Guide
date: 2/29/2008 8:39:05 PM
---

Since WPF was released it has seen a fairly rapid adoption but not much in the way of guidance. The WPF team at Microsoft is hoping to change that with the release of the [WPF Application Quality Guide](http://windowsclient.net/wpf/white-papers/wpf-app-quality-guide.aspx). The guide is going to be released in stages and will be updated based on feedback provided by the community. While the first release is still missing a lot, it does provide some good tips on setting up your application for automated testing. 

They also provide a good list of tools for performance profiling: 
<li>[Using Performance Profiling Tools for WPF](http://msdn2.microsoft.com/en-us/library/aa969767.aspx#using_performance_profiling_tools).  </li><li>[Event Trace](http://msdn2.microsoft.com/en-us/library/aa969767.aspx#event_trace). Use this tool for analyzing events and generating event log files.  </li><li>[Perforator](http://msdn2.microsoft.com/en-us/library/aa969767.aspx#perforator). Use this tool for analyzing rendering behavior.  </li><li>[ETW Trace Viewer](http://msdn2.microsoft.com/en-us/library/aa969767.aspx#etw_trace_viewer). Use this tool to record, display, and browse Event Tracing for Windows (ETW) log files in a WPF user-interface format.  </li><li>[Visual Profiler](http://msdn2.microsoft.com/en-us/library/aa969767.aspx#visual_profiler). Use this tool for profiling the use of WPF services, such as layout and event handling, by elements in the visual tree.  </li><li>[Working Set Analyzer](http://msdn2.microsoft.com/en-us/library/aa969767.aspx#working_set_viewer). Use this tool for analyzing the working set characteristics of your application. </li>
