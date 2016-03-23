---
layout: post
title: Windows 7 Federated Search
date: 2009-05-14 19:01:28 -04:00
---

Windows and the Windows Explorer have had search capabilities for a long time and they have gradually improved over the years. The one thing that was always lacking was an ability to search different contexts (or remote sources). There were some improvements with the Windows Desktop search, but I think the federated search capability in Windows 7 really gets it right.

Federated search in Windows 7 introduces support to search different remote data stores using OpenSearch technologies and allows you to search those sources from within Windows Explorer. Below is an example of searching a SharePoint 2007 from within Windows Explorer.

![image](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/Windows7FederatedSearch_10B84/image_14.png "image")The more interesting aspect of federated search is that, because it uses OpenSearch, there are already a lot of search sites that support search federation. Even better, Microsoft supports creating new federated search providers through the use of federated search connectors, which are simple XML files that describe the search provider.

You can [download](http://www.microsoft.com/downloads/details.aspx?FamilyID=C709A596-A9E9-49E7-BCD4-319664929317&displaylang=en) a document that describes how to build a basic web service that leverages the Windows 7 federated search and the search connector file format from Microsoft.

Here is a sample search connector that works with Microsoft Live Search:
  <div style="border-bottom: silver 1px solid; text-align: left; border-left: silver 1px solid; padding-bottom: 4px; line-height: 12pt; background-color: #f4f4f4; margin: 20px 0px 10px; padding-left: 4px; width: 97.5%; padding-right: 4px; font-family: 'Courier New', courier, monospace; direction: ltr; max-height: 200px; font-size: 8pt; overflow: auto; border-top: silver 1px solid; cursor: text; border-right: silver 1px solid; padding-top: 4px" id="codeSnippetWrapper">   <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; padding-left: 0px; width: 100%; padding-right: 0px; font-family: 'Courier New', courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px" id="codeSnippet">     

<span style="color: #606060" id="lnum1">   1:</span> <span style="color: #0000ff"><?</span><span style="color: #800000">xml</span> <span style="color: #ff0000">version</span><span style="color: #0000ff">="1.0"</span> <span style="color: #ff0000">encoding</span><span style="color: #0000ff">="UTF-8"</span>?<span style="color: #0000ff">></span>

<span style="color: #606060" id="lnum2">   2:</span> <span style="color: #0000ff"><</span><span style="color: #800000">OpenSearchDescription</span> <span style="color: #ff0000">xmlns</span><span style="color: #0000ff">="http://a9.com/-/spec/opensearch/1.1/"</span> <span style="color: #ff0000">xmlns:ms-ose</span><span style="color: #0000ff">="http://schemas.microsoft.com/opensearchext/2009/"</span><span style="color: #0000ff">></span>

<span style="color: #606060" id="lnum3">   3:</span>     <span style="color: #0000ff"><</span><span style="color: #800000">ShortName</span><span style="color: #0000ff">></span>Live Search<span style="color: #0000ff"></</span><span style="color: #800000">ShortName</span><span style="color: #0000ff">></span> 

<span style="color: #606060" id="lnum4">   4:</span>     <span style="color: #0000ff"><</span><span style="color: #800000">Description</span><span style="color: #0000ff">></span>Live Search<span style="color: #0000ff"></</span><span style="color: #800000">Description</span><span style="color: #0000ff">></span>

<span style="color: #606060" id="lnum5">   5:</span>     <span style="color: #0000ff"><</span><span style="color: #800000">Url</span> <span style="color: #ff0000">type</span><span style="color: #0000ff">="application/rss+xml"</span> <span style="color: #ff0000">template</span><span style="color: #0000ff">="http://search.live.com/results.aspx?q={searchTerms}&amp;count=50&amp;format=rss"</span><span style="color: #0000ff">/></span>

<span style="color: #606060" id="lnum6">   6:</span> <span style="color: #0000ff"></</span><span style="color: #800000">OpenSearchDescription</span><span style="color: #0000ff">></span>

</div>
</div>



Save this XML to a file named “Live Search.osdx” (you should use the .osdx extension since it is already registered in Windows as an “open search description” file) and then double-click the file. You will be prompted to add the search connector:

![image](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/Windows7FederatedSearch_10B84/image_13.png "image") 

Once you add the search connector, it will create a Search Connector file in the “Searches” folder (%userprofile%/Searches) and places a short cut to that file in the “Links” folder (%userprofile%/Links) that shows up in the Windows Explorer favorites section.

![image](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/Windows7FederatedSearch_10B84/image_12.png "image") 

By selecting “Live Search” and typing a search term in the search box, the query is sent to Live Search through the OpenSearch provider. Here is an example of searching for the term “federated search” in Live Search:

![image](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/Windows7FederatedSearch_10B84/image_11.png "image") 

Since the search results are integrated in Windows Explorer, you can take advantage of any built in file previewers and see both the search summary and a preview of each result:

[![image](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/Windows7FederatedSearch_10B84/image_thumb_5.png "image")](http://gwb.blob.core.windows.net/sdorman/WindowsLiveWriter/Windows7FederatedSearch_10B84/image_16.png) 

Overall, I think the new federated search capabilities in Windows 7 will become an extremely useful and popular way for people to search, especially as businesses take advantage of the technology and start exposing internal file servers and intranet portals as OpenSearch providers.
