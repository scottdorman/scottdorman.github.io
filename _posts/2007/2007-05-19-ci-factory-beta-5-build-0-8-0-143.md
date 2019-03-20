---
layout: post
title: CI Factory Beta 5 (Build 0.8.0.143)
date: '2007-05-19 14:02:51 -05:00'
---

[Beta 5](http://code.google.com/p/ci-factory/downloads/detail?name=CI-Factory-Beta-0.8.0.143.zip&can=2&q=) (build 0.8.0.143) for CI Factory is now available. For a full description of what's in this release, check out the [release notes](http://docs.google.com/Doc?id=dd6cv3jm_09r2s2h). 

The big news for this release is that Vault package is ready for use and that NCover support has been updated to support NCover 1.5.8. NCover support also provides the ability to set the process for which you want coverage collected. This is important for MSTest users to utilize app.config for the test assemblies and means you don't need to use the /noisolation switch anymore. 

The following bugs have been fixed: 

*   A race condition in the CC.NET TFS source control block has been fixed.
*   TFS source control block paths case insensitive .
*   Added check to TFS source control block to handle duplicate notifications.
*   Fixed CC.NET config file watcher for TFS source control block.
*   Added support to the VSTSSourceControl Package to get only the triggering ChangeSet.
*   The Alerts Package now supports the DotNetUnitTest Package (MbUnit/NUnit).
*   Set all CI Factory assemblies action on error to no prompt.
*   "Ask" task will always be on top and centered.
*   Update to NCover 1.5.8.
*   First cut at Vault Package.
*   Added CC.NET documentation to the Documentation Folder.
*   Fixed some issues with the SourceModification CreateModificationList.
*   Added logic to better handle projects without assemblies NAnt functions for vsprojects. 

I am slowly working on creating some new CC.NET dashboard skins for CI Factory that will allow you to easily customize the color scheme and logo used. Hopefully, these will be complete sometime by the end of June.
