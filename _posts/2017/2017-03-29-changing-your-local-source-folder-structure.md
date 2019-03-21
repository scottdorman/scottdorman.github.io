---
layout: post
title: Changing your local source folder structure
date: '2017-03-29 20:32:24 -05:00'
tags: visual-studio .net-core
---

Visual Studio is a great IDE for developing .NET-based web sites, especially if you're building .NET Core sites using Visual Studio 2017.

There is one scenario, though, that can completely destabilize your development environment: Moving (or changing) your source code directory structure.

While this probably isn't an everyday thing, it does happen from time to time. For me, this happened recently when I upgraded my boot drive to a larger SSD. In doing so, I restructured my source folder (which was on a secondary drive) from `D:\Scott\Source\Repos` (for GitHub repositories) to `D:\Scott\Source\github`. (I also made a similar change for my TFS Online folder structure.) This was done because lately I'm working in more top-level repositories (coming from multiple TFS instances or different GitHub organizations) and I wanted to put a better structure in place.

On the surface, this is a simple and painless change: Either simply move the folders around on disk or start fresh and reclone everything. 

For GitHub repositories, either option seems to work just fine. However, for TFS repositories, it's not as simple becasuse Visual Studio seems to "loose" the knowledge that the code is under source control due to workspace mappings. I found it much simpler to simply start completely over by remapping the workspace, getting latest, and then doing folder diffs to get them back in sync (which you only need to do if you have changes that haven't been checked in before you start moving things around.)

At this point, everything is moved to the new folder structure and compiles without issues so you may be tempted to think that everything is working correctly. However, as soon as you try to debug your website, you'll be hit with a rather unexpected and extremely unhelpful error: "Unable to start process C:\Program Files\dotnet\dotnet.exe. The web server requrest failed with status code 500, Internal Server Error."

{% include post/image.html image-file="error-message.png" alt="Error Message" %}

Although it's not entirely obvious, this problem occurs because IIS Express isn't able to find the path to the compiled website any longer. In order to fix this, you actually need to look at the `.vs\config\applicationhost.config` file (you may need to turn on showing hidden files in order to see the `.vs` folder). Open that file in a text editor and look for the `<sites>` element. It will look similar to

```xml
    <sites>
      <site name="WebSite1" id="1" serverAutoStart="true">
        <application path="/">
          <virtualDirectory path="/" physicalPath="%IIS_SITES_HOME%\WebSite1" />
        </application>
        <bindings>
          <binding protocol="http" bindingInformation=":8080:localhost" />
        </bindings>
      </site>
      <site name="TampaDev.Web" id="2">
        <application path="/" applicationPool="Clr4IntegratedAppPool">
          <virtualDirectory path="/" physicalPath="D:\Scott\Source\Repos\TampaDev\TampaDev\TampaDev.Web" />
        </application>
        <bindings>
          <binding protocol="http" bindingInformation="*:61400:localhost" />
        </bindings>
      </site>
    </sites>
```
As you can see, some of those `<site>` elements have a `physicalPath` attribute which still points to the old path structure. You just need to update the value of those attributes to point to the new path structure and you're all set. (In my case, I changed them to point to `D:\Scott\Source\github\` rather than `D:\Scott\Source\Repos`.) Now you'll be able to debug your projects again.
