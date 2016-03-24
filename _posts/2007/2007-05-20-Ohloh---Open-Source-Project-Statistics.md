---
layout: post
title: Ohloh - Open Source Project Statistics
date: 2007-05-20 13:13:36 -05:00
---

![](http://www.ohloh.net/images/logo_med.png)While I'm on the topic of [code metrics]({% post_url /2007/2007-05-20-NDepend-2.2 %}), I thought I would mention another interesting set of statistics provided by the Ohloh web site. This is a site that we use on [Subtext](http://subtextproject.com/) to monitor the project and the statistics are integrated with our CruiseControl.NET [dashboard](http://build.subtextproject.com) as well.

Ohloh collects software metrics from a variety of sources including the project's source code and the software development infrastructure used by the project's development team. Ohloh was founded in 2004 as a way to provide more visibility into the software development process. The type of information you can learn about your project is invaluable in determining the activity and strength of the project and about the individual contributors. Currently Ohloh is limited to scanning open source project only, but the information it provides would certainly be useful to any software development company.

(All of the images and statistics are taken from the [Ohloh Subtext project](http://www.ohloh.net/projects/3167 "Subtext Analysis Report") page.)

## Contributors

The Contributors page shows the Top 10 active contributors, but shows it in a very visual manner that shows not only who they are but also the amount of activity and effort contributed. For each contributor, you can drill down and see the list of source code "commits" and also view a summary of the languages used, and a visual timeline showing all of that persons' activity.

![](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/OhlohOpenSourceProjectStatistics_B9EE/image%7B0%7D4.png) 

## Project File Licenses

Ohloh determines the licensing of a project strictly through a detailed analysis of the source code instead of simply trusting the license terms that the project owners claim. This can be a useful tool when determining the risks associated with using a project.

![](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/OhlohOpenSourceProjectStatistics_B9EE/image%7B0%7D11.png)  

## Codebase History

The codebase history shows the evolution of the source code of a project. It specifically shows the total size of a project's source code over time.

![](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/OhlohOpenSourceProjectStatistics_B9EE/image%7B0%7D16.png) 

## Project Languages

The languages table shows the project's current total physical source lines of code (pslocs), categorized by programming language.

![](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/OhlohOpenSourceProjectStatistics_B9EE/image%7B0%7D21.png)
