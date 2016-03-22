---
layout: post
title: Cloud hosted CI for .NET projects
date: 6/2/2014 9:26:35 AM
---

Continuous integration (CI) is important. If you don’t have it set up…you should. There are a lot of different options available for hosting your own CI server, but they all require you to maintain your own infrastructure. If you’re a business, that generally isn’t a problem. However, if you have some open source projects hosted, for example on [GitHub](http://github.com), there haven’t really been any options. That has changed with the latest release of [AppVeyor](http://appveyor.com/), which bills itself as “Continuous integration for busy developers.” What’s different about AppVeyor is that it’s a hosted solution. 

Why is that important? By being a hosted solution, it means that I don’t have to maintain my own infrastructure for a build server. 

How does that help if you’re hosting an open source project? AppVeyor has a really competitive pricing plan. For an unlimited amount of public repositories, it’s free. That gives you a cloud hosted CI system for all of your GitHub projects for the cost of some time to set them up, which actually isn’t hard to do at all.

I have several open source projects (hosted at [https://github.com/scottdorman](https://github.com/scottdorman)), so I signed up using my GitHub credentials. AppVeyor fully supported my two-factor authentication with GitHub, so I never once had to enter my password for GitHub into AppVeyor. Once it was done, I authorized GitHub and it instantly found all of the repositories I have (both the ones I created and the ones I cloned from elsewhere). You can even add “build badges” to your markdown files in GitHub, so anyone who visits your project can see the status of the lasted build.

Out of the box, you can simply select a repository, add the build project, click New Build and wait for the build to complete. You now have a complete CI server running for your project. The best part of this, besides the fact that it “just worked” with almost zero configuration is that you can configure it through a web-based interface which is very streamlined, clean and easy to use or you can use a appveyor.yml file. This means that you can define your CI build process (including any scripts that might need to be run, etc.) in a standard file format (the [YAML](http://yaml.org/) format) and store it in your repository. The benefits to that are huge. The file becomes a versioned artifact in your source control system, so it can be branched, merged, and is completely transparent to anyone working on the project.

> By the way, AppVeyor isn’t limited to just GitHub. It currently supports GitHub, BitBucket, Visual Studio Online, and Kiln.

I did have a few issues getting one of my projects to build, but the same day I posted the problem to the support forum a fix was deployed, and I had a functioning CI build about 5 minutes after that. Since then, I’ve provided some additional feature requests and had a few other questions, all of which have seen responses within a 24-hour period. I have to say that it’s easily been one of the best customer support experiences I’ve seen in a long time.

AppVeyor is still young, so it doesn’t yet have full feature parity with some of the older (more established) CI systems available,  but it’s getting better all the time and I have no doubt that it will quickly catch up to those other CI systems and then pass them. The bottom line, if you’re looking for a good cloud-hosted CI system for your .NET-based projects, look at AppVeyor.
