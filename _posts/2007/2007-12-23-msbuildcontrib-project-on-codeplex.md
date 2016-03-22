---
layout: post
title: MSBuildContrib project on CodePlex
date: 2007-12-23 12:14:11 -05:00
---

[MSBuildContrib](http://www.codeplex.com/MSBuildContrib) is the project for tasks and tools that aren't in MSBuild. This is similar to the [NAntContrib](http://nantcontrib.sourceforge.net/) project and will be incorporating as many of the [NAnt](http://nant.sourceforge.net/) and NAntContrib tasks as possible. There is still a long way to go, so if you are interested in helping out please let me know and I will add you to the project.

Here is the list of NAnt or NAntContrib tasks that are planned and the current status:


<table cellspacing="0" cellpadding="2" width="929" border="0">
    <tbody>
        <tr>
            <td valign="top" width="178">**<u>NAnt/NAntContrib Task</u>**</td>
            <td valign="top" width="156">**<u>MSBuildContrib Task</u>**</td>
            <td valign="top" width="87">**<u>Status</u>**</td>
            <td valign="top" width="506">**<u>Description</u>**</td>
        </tr>
        <tr>
            <td valign="top" width="177">codestats</td>
            <td valign="top" width="157">CodeStats</td>
            <td valign="top" width="90">Complete</td>
            <td valign="top" width="506">Generates statistics from source code.</td>
        </tr>
        <tr>
            <td valign="top" width="177">gac-install</td>
            <td valign="top" width="157">GacUtil</td>
            <td valign="top" width="93">Complete</td>
            <td valign="top" width="506">Installs assemblies into the Global Assembly Cache (GAC) by using the gacutil SDK tool.</td>
        </tr>
        <tr>
            <td valign="top" width="177">gac-uninstall</td>
            <td valign="top" width="157">GacUtil</td>
            <td valign="top" width="95">Complete</td>
            <td valign="top" width="506">Uninstalls assemblies into the Global Assembly Cache (GAC) by using the gacutil SDK tool.</td>
        </tr>
        <tr>
            <td valign="top" width="176">grep</td>
            <td valign="top" width="157">Grep</td>
            <td valign="top" width="97">Complete</td>
            <td valign="top" width="506">Searches files for a regular-expression and produces an XML report of the matches.</td>
        </tr>
        <tr>
            <td valign="top" width="176">attrib</td>
            <td valign="top" width="156">Attrib</td>
            <td valign="top" width="99">In Progress</td>
            <td valign="top" width="506">Changes the file attributes of a file or set of files and directories.</td>
        </tr>
        <tr>
            <td valign="top" width="176">checksum</td>
            <td valign="top" width="156">Checksum</td>
            <td valign="top" width="99">In Progress</td>
            <td valign="top" width="506">Calculates checksums for a set of files. Loosely based on Ant's Checksum task.</td>
        </tr>
        <tr>
            <td valign="top" width="176">concat</td>
            <td valign="top" width="156">Concat</td>
            <td valign="top" width="99">In Progress</td>
            <td valign="top" width="506">A task that concatenates a set of files. Loosely based on Ant's Concat task.</td>
        </tr>
        <tr>
            <td valign="top" width="176">mail</td>
            <td valign="top" width="156">Mail</td>
            <td valign="top" width="99">Planned</td>
            <td valign="top" width="506">Sends an SMTP message.</td>
        </tr>
        <tr>
            <td valign="top" width="176">move</td>
            <td valign="top" width="156">Move</td>
            <td valign="top" width="99">In Progress</td>
            <td valign="top" width="506">Moves a file or set of files to a new file or directory.</td>
        </tr>
        <tr>
            <td valign="top" width="176">servicecontroller</td>
            <td valign="top" width="156">ServiceController</td>
            <td valign="top" width="99">Planned</td>
            <td valign="top" width="506">Allows a Windows service to be controlled.</td>
        </tr>
        <tr>
            <td valign="top" width="176">sleep</td>
            <td valign="top" width="156">Sleep</td>
            <td valign="top" width="99">Planned</td>
            <td valign="top" width="506">A task for sleeping a specified period of time, useful when a build or deployment process requires an interval between tasks.</td>
        </tr>
    </tbody>
</table>
