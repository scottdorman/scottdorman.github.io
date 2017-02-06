---
layout: post
title: Differences between release types
date: '2008-08-30 14:15:08 -05:00'
---

Phil has an excellent post that builds on Jeff Atwood's explanation which very clearly describes the differences between the various release types:

*   Beta 
*   CTP 
*   Daily Builds/Interim Releases 
*   Fully Supported Out-of-Band Releases 
*   RTM/RTW Releases 
*   Service Pack Releases   

Summarizing what both Phil and Jeff said:

> **Alpha**: The software is complete enough for *internal* testing. This is typically done by people other than the software engineers who wrote it, but still within the same organization or community that developed the software.
> 
> **Beta:** The software is complete enough for external testing -- that is, by groups outside the organization or community that developed the software. Beta software is usually feature complete, but may have known limitations or bugs. Betas are either closed (private) and limited to a specific set of users, or they can be open to the general public.
> 
> **CTP (Community Technology Preview):** It's generally an *incomplete* preview of a new technology in progress. These usually come out before beta and are a way to gather feedback from the community during the development of a product.
> 
> **Daily Builds/Interim Releases:** A daily build is really for those who like to play with fire, as they usually are not tested, and could represent work in progress that is not even working at all.
> 
> **Fully Supported Out-of-Band (OOB) Releases:** A release that is not part of the product (i.e. it's not included in an installation package), but is fully supported as if it were.
> 
> **RTM (Released to Manufacturing) / RTW (Released to Web) Releases**: The software is finished -- and by finished, we mean there are no show-stopping, little-children-killing bugs in it. *That we know of*. There are probably numerous lower-prority bugs [triaged into](http://www.codinghorror.com/blog/archives/000498.html) the next point release or service pack, as well.
> 
> **Service Pack Releases:** A Service Pack (or SP) is simply an RTM (or RTW) release of fixes and/or improvements to some software. It used to be that SPs rarely included new features, but it seems to be the norm now that they do. Service Packs tend to include all the hotfixes and patches released since the product originally was released, which is convenient for the end user in not having to install every fix individually.
