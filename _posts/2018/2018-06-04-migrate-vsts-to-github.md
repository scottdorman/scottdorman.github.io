---
layout: post
title: Migrate VS Online to GitHub
date: '2018-06-12 14:15:00 -05:00'
tags: github
---

If you have a TFS-based code repo, especially one hosted on Visual Studio Team Services (VSTS), you might want to migrate your repos to GitHub. Unfortunatley, there isn't a direct way to migrate the code and all of your check in history, but there is a way as long as you don't mind dropping in to PowerShell for a bit.

1. Open PowerShell, running with elevated permissions.
1. Install the [chocolatey](https://chocolatey.org/install) package manager by executing the following command
`Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`
1. Install [git-tfs](https://chocolatey.org/packages/gittfs) by executing `choco install gittfs`.
1. Export your code from TFS into a local GitHub repo. Be prepared to wait a long while if the repo you're exporting has a lot of check ins. If your TFS project name has spaces in it, you need to make sure you put it in qoutations. You can export your repo by executing the following
`git-tfs clone <tfs server> <project> <git repo>`
1. Perform some cleanup operations by executing `git gc` and `git-tfs cleanup`

Before you commit the changes, you might want to add a .gitignore file. You may also want to perform a folder comparison between the two folders to make sure no files were accidentally missed.

At this point, you're ready to import the repository into GitHub. You can do this with `git remote add origin <repo path>` and then `git push origin master` or use the GitHub desktop client.
