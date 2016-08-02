---
layout: post
title: Windows 7 Federated Search
date: 2009-05-14 19:01:28 -05:00
---

Windows and the Windows Explorer have had search capabilities for a long time and they have gradually improved over the years. The one thing that was always lacking was an ability to search different contexts (or remote sources). There were some improvements with the Windows Desktop search, but I think the federated search capability in Windows 7 really gets it right.

Federated search in Windows 7 introduces support to search different remote data stores using OpenSearch technologies and allows you to search those sources from within Windows Explorer. Below is an example of searching a SharePoint 2007 from within Windows Explorer.

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image_14.png)The more interesting aspect of federated search is that, because it uses OpenSearch, there are already a lot of search sites that support search federation. Even better, Microsoft supports creating new federated search providers through the use of federated search connectors, which are simple XML files that describe the search provider.

You can [download](http://www.microsoft.com/downloads/details.aspx?FamilyID=C709A596-A9E9-49E7-BCD4-319664929317&displaylang=en) a document that describes how to build a basic web service that leverages the Windows 7 federated search and the search connector file format from Microsoft.

Here is a sample search connector that works with Microsoft Live Search:

```xml
<?xml version="1.0" encoding="UTF-8"?>
  <OpenSearchDescription xmlns="http://a9.com/-/spec/opensearch/1.1/" xmlns:ms-ose="http://schemas.microsoft.com/opensearchext/2009/">
    <ShortName>Live Search</ShortName>
    <Description>Live Search</Description>
    <Url type="application/rss+xml" template="http://search.live.com/results.aspx?q={searchTerms}&count=50&format=rss"/>
  </OpenSearchDescription> 
```

Save this XML to a file named "Live Search.osdx" (you should use the .osdx extension since it is already registered in Windows as an "open search description" file) and then double-click the file. You will be prompted to add the search connector:

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image_13.png) 

Once you add the search connector, it will create a Search Connector file in the "Searches" folder (`%userprofile%/Searches`) and places a short cut to that file in the "Links" folder (`%userprofile%/Links`) that shows up in the Windows Explorer favorites section.

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image_12.png) 

By selecting "Live Search" and typing a search term in the search box, the query is sent to Live Search through the OpenSearch provider. Here is an example of searching for the term "federated search" in Live Search:

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image_11.png) 

Since the search results are integrated in Windows Explorer, you can take advantage of any built in file previewers and see both the search summary and a preview of each result:

![](/img/posts{{ page.path | remove: '_posts' | remove: '.md' }}/image_16.png) 

Overall, I think the new federated search capabilities in Windows 7 will become an extremely useful and popular way for people to search, especially as businesses take advantage of the technology and start exposing internal file servers and intranet portals as OpenSearch providers.
