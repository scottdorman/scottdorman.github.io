---
layout: post
title: Standard and Custom Format Strings
date: 7/11/2008 2:57:33 PM
---

I was recently asked by a co-worker what the format string was for formatting a DateTime object in an ISO 8601 format. The way to do this is passing a format string to the ToString() method on the DateTime object. The question becomes, what is that format string? There are two ways to do this:
  <div style="border-right: gray 1px solid; padding-right: 4px; padding-left: 4px; font-size: 8pt; border-top: gray 1px solid; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">   

DateTime.Now.ToString(“yyyy<span style="color: #006080">'-'</span>MM<span style="color: #006080">'-'</span>dd<span style="color: #006080">'T'</span>HH<span style="color: #006080">':'</span>mm<span style="color: #006080">':'</span>ss<span style="color: #006080">'.'</span>fffffffK”)
DateTime.Now.ToString(“o”)

</div>



At this point, you might ask how you would know to use the “o”. This information is available through [MSDN](http://msdn.microsoft.com/en-us/library/26etazsy.aspx), but it isn’t always easy to find if you don’t already know where to look. Here is a quick “cheat sheet” of links to help you find the right information:

*   **[Composite Formatting](http://msdn.microsoft.com/en-us/library/txafckwd.aspx)**
*   **Numeric Format Strings** 
*   *   [Standard numeric format strings](http://msdn.microsoft.com/en-us/library/dwhawy9k.aspx) 
    *   [Custom numeric format strings](http://msdn.microsoft.com/en-us/library/0c899ak8.aspx) 

    **Date and Time Format Strings**
*   *   [Standard DateTime format strings](http://msdn.microsoft.com/en-us/library/az4se3k1.aspx) 
    *   [Custom DateTime format strings](http://msdn.microsoft.com/en-us/library/8kb3ddd4.aspx)

      [**Enumeration Format Strings**](http://msdn.microsoft.com/en-us/library/c3s1ez6e.aspx)
