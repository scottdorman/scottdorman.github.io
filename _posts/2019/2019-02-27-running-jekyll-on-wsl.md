---
layout: post
title: Running Jekyll on WSL
date: '2019-02-27 16:20:00 -05:00'
---

Almost 3 years ago I decided to [move my blog]({% post_url /2016/2016-03-23-moving-to-github-pages %}) to a GitHub repository. A few days ago, I needed to make some minor enhancements to it and also set up another blog. When I first set up my blog, it wasn't an entirely straightforward or easy process to get Jekyll running locally to debug issues. 

Since that time Microsoft has released, and improved, the [Windows Subsystem for Linux (WSL)](https://docs.microsoft.com/en-us/windows/wsl/about), which lets developers run a GNU/Linux environment -- including most command-line tools, utilities, and applications -- directly on Windows, unmodified, without the overhead of a virtual machine.

Why is this interesting news? As a Windows user, I now have direct access to a full Linux environment that allows me to run native Linux binaries and, more importantly, to follow the standard install/set-up guides for getting tools such as Ruby and Jekyll running.

## Installing the Windows Subsystem for Linux
I started with a fresh install of WSL. In order to do that, I first had to enable this optional Windows Feature. You can do this by running the following command in an elevated PowerShell script: 

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

## Installing the Ubuntu distro
After a reboot, I installed [Ubuntu](https://www.microsoft.com/store/p/ubuntu/9nblggh4msv6) from the Windows Store. You can also [download it using an elevated PowerShell script](https://docs.microsoft.com/en-us/windows/wsl/install-manual) if you want. Either way, installing the distro can take a little while. At the end of the install, you'll be asked to create a default Linux username and password. This doesn't have to be the same username/password as your Windows username/password, but make sure you remember the password.

Next, we need to update and upgrade the distro's packages by running the following commands in our bash shell:

```bash
sudo apt update
sudo apt upgrade
```

These commands can take a while to complete as well.

## Running Jekyll locally
Now we're finally ready to start following the GitHub [instructions](https://help.github.com/en/articles/setting-up-your-github-pages-site-locally-with-jekyll) on getting Jekyll installed locally. I'm going to skip certain sections of the GitHub tutorial as I already had a local repository setup.

### Prerequisites

The first step is to install the [prerequisites](https://help.github.com/en/articles/setting-up-your-github-pages-site-locally-with-jekyll#requirements), which include Ruby and Bundler.

Since this is a clean distro, we're going to need to install Ruby first. You can install Ruby using `apt` (which as of this blog post installs version 2.5.1) or you can use another package manager, such as [`rvm`](http://rvm.io/). 

To install using `apt`, run the following command:

```bash
sudo apt install ruby
```

To install using `rvm`, 

```bash
sudo apt install gnupg2
gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB

curl -sSL https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
rvm install ruby
```

I choose to install `rvm` both to get the latest version of Ruby (2.6.0 as of this blog post) but also to allow me to have multiple versions of Ruby installed. (Again, installing using `rvm` can take some time.)

Now that we have Ruby installed, it's time to install Bundler. 

> Unfortunately, this is where we have to take one additional step specific to running Linux on Windows, and it's because Windows 10 prioritizes IPv6 over IPv4 and `api.rubygems.org` has issues with its IPv6 setup. To fix this, you need to lower the priority of the IPv6 addresses so that `gem` will try the IPv4 addresses first.
>
> First, you need to lookup the IPv6 addresses using `dig AAAA api.rubygems.org +short`. Once you have them (as of this blog post it was `2a04:4e42::70`), you need to edit `/etc/gai.conf` using `sudo vi /etc/gai.conf` to add the following lines:
>
>```bash
># Debian defaults.
>precedence  ::1/128         50
>precedence  ::/0            40
>precedence  2002::/16       30
>precedence  ::/96           20
>precedence  ::ffff:0:0/96   10
>
># Low precedence for api.rubygems.org IPv6 addresses.
>precedence  2a04:4e42::70/32  5
>```


```bash
gem install bundler
```

### Install Jekyll and it's dependencies

Change directories into your repository. If you don't already have a repository, you can [create one](https://help.github.com/en/articles/setting-up-your-github-pages-site-locally-with-jekyll#step-1-create-a-local-repository-for-your-jekyll-site) using the steps in the GitHub article.

If you don't already have a `Gemfile` (capitalization is important here!), create one using your favorite editor. Add the following lines to your `Gemfile`:

```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

Now you're ready to install Jekyll and other [dependencies](https://pages.github.com/versions/) from the GitHub Pages gem.

```bash
bundle install
```

Again, this can take a while.

Finally, you're ready to run Jekyll and build your site. 

> This assumes you already have Jekyll site files in your repository, from a gh-pages branch, for example. If you don't, you can [follow these steps](https://help.github.com/en/articles/setting-up-your-github-pages-site-locally-with-jekyll#step-3-optional-generate-jekyll-site-files).

Navigate into the root directory of your local Jekyll site repository and run:

```bash
bundle exec jekyll serve
```

This will build your site and run it under a local web server built in to Jekyll so you can browse the site.

## Wrapping up
As you can see, other than having to deal with the IPv6 issues, we followed the tutorials and installation guides as they were written for "real" Linux because we are, in fact, running a real version of Linux.

The days of Windows development machines needing to run Linux in a virtual machine environment or jumping through lots of hoops, running modified binaries, and having to follow special setup instructions are gone. Now we can get on with the task at hand, using whatever tools best fit our need.

> Every so often, I've run into an error about an `operation not permitted apply2files` error when trying to build locally. Closing my `bash` shell and reopening it seems to fix the issue.

> If you want to edit files using vi, you may want to change the default console colors from gray text on a black background to black text on a gray background. I found that the default colors when editing files were very hard to read. A good [vi cheat sheet](https://ryanstutorials.net/linuxtutorial/cheatsheetvi.php) may also be helpful.
