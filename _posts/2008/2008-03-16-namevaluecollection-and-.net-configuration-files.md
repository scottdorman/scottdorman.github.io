---
layout: post
title: NameValueCollection and .NET Configuration Files
date: 2008-03-16 20:00:02 -04:00
---

I spent most of yesterday trying to figure out how to make use of a [NameValueCollection](http://msdn2.microsoft.com/689y5thy.aspx "NameValueCollection Class") in a .NET configuration file. After wasting almost the entire night fighting with this problem, I thought I would let everyone know that it is possible, and easier than you might think. (By the way, this was a clear case of working too long on the problem. After a good nights sleep, I solved this in under 5 minutes.)

At this point you might wonder why this was so difficult. The largest and most significant problem is the fact that NameValueCollection isn't serializable ([KB 814187](http://support.microsoft.com/kb/814187)). The reason for this is that NameValueCollection doesn't implement [ICollection](http://msdn2.microsoft.com/b1ht6113.aspx "ICollection Interface") but extends [NameObjectCollectionBase](http://msdn2.microsoft.com/ts6a60s4.aspx "NameObjectCollectionBase Class") instead. The recommended solution is to use a [SoapFormatter](http://msdn2.microsoft.com/5ktza7xf.aspx "SoapFormatter Class") to serialize and deserialize the collection. While using the SoapFormatter does work, it seemed like a very complex solution for a seemingly simple problem.

Not wanting to over-engineer my solution, I started searching the web for alternatives. I found several newsgroup postings that all said to use the SoapFormatter since that was the recommended solution and the only way to go. Not having drunk too much blue kool-aid, I kept searching. That search turned up an article by [Keyvan Nayyeri](http://nayyeri.net/blog/Serialize-NameValueCollection/ "Serialize NameValueCollection") that shows how to created a serializable NameValueCollection. This approach was intriguing and certainly seemed to be a more useful solution than using the SoapFormatter, but again it seemed like a lot of work.

Keep in mind, all I wanted to be able to do in the configuration file was to create a section that looked like this:
  <div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">   <div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">     

<span style="color: #606060">   1:</span> <span style="color: #0000ff"><</span><span style="color: #800000">copyFiles</span><span style="color: #0000ff">></span>

<span style="color: #606060">   2:</span>   <span style="color: #0000ff"><</span><span style="color: #800000">add</span> <span style="color: #ff0000">name</span><span style="color: #0000ff">="C:\Windows"</span> <span style="color: #ff0000">value</span><span style="color: #0000ff">="*.dll"</span><span style="color: #0000ff">/></span>

<span style="color: #606060">   3:</span>   <span style="color: #0000ff"><</span><span style="color: #800000">add</span> <span style="color: #ff0000">name</span><span style="color: #0000ff">="C:\Temp"</span><span style="color: #0000ff">/></span>

<span style="color: #606060">   4:</span> <span style="color: #0000ff"></</span><span style="color: #800000">copyFiles</span><span style="color: #0000ff">></span>

  </div>
</div>



Continuing the search, I thought I found my answer. I stumbled across an [article](http://dotnet.org.za/ncode/archive/2007/01/19/net-how-to-use-custom-name-value-config-sections.aspx) (".NET How To Create and Use Custom Name-Value Config Sections") that shows how to do this in 4 simple steps. Reading through the article, I realized that it is written using the the .NET 1.0 and 1.1 [ConfigurationSettings](http://msdn2.microsoft.com/kw224t90.aspx "ConfigurationSettings Class"), which is provided for backwards compatibility only. Since the application I'm working on is .NET 3.5 and taking advantage of many of the new language features, I wanted to ensure that I wasn't using any deprecated classes.

This is where I started running into additional problems. It seems that Microsoft provides a [NameValueSectionHandler](http://msdn2.microsoft.com/5fwwx482.aspx "NameValueSectionHandler Class"), which the article makes us of. The problem is that NameValueSectionHandler is architected following the .NET 1.0/1.1 model and implements the [System.Configuration.IConfigurationSectionHandler](http://msdn2.microsoft.com/6950ee5e.aspx "IConfigurationSectionHandler Interface") interface. This is great if you want to use the deprecated ConfigurationSettings class; if you want to use the recommended [System.Configuration.ConfigurationManager](http://msdn2.microsoft.com/ms134260.aspx "ConfigurationManager Class") or [System.Web.Configuration.WebConfigurationManager](http://msdn2.microsoft.com/ms151430.aspx "WebConfigurationManager Class") classes you are out of luck. They will only work with a class that derives from [ConfigurationSection](http://msdn2.microsoft.com/x0kca287.aspx "ConfigurationSection Class").

So, after all this I thought I was out of luck and would need to write my own configuration section handler. (Remember, this was about 1:00 AM.) After sleeping on it, I realized that there was a much simpler way. Along with the NameValueSectionHandler, Microsoft also implemented [NameValueConfigurationCollection](http://msdn2.microsoft.com/ms134603.aspx "NameValueConfigurationCollection Class") and [NameValueConfigurationElement](http://msdn2.microsoft.com/ms134619.aspx "NameValueConfigurationElement Class"), which derive from the appropriate configuration classes to be used by the ConfigurationManager. After seeing that, I realized that all I needed to do was implement a NameValueSection which derives from ConfigurationSection.

This is where the solution becomes easy. In it's simplest most form, the NameValueSection looks like this:


<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">
  <div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">
    

<span style="color: #606060">   1:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">class</span> NameValueSection : ConfigurationSection

<span style="color: #606060">   2:</span> {

<span style="color: #606060">   3:</span>     [ConfigurationProperty(<span style="color: #006080">""</span>, IsDefaultCollection = <span style="color: #0000ff">true</span>)]

<span style="color: #606060">   4:</span>     <span style="color: #0000ff">public</span> NameValueConfigurationCollection Settings

<span style="color: #606060">   5:</span>     {

<span style="color: #606060">   6:</span>         get

<span style="color: #606060">   7:</span>         {

<span style="color: #606060">   8:</span>             <span style="color: #0000ff">return</span> (NameValueConfigurationCollection)<span style="color: #0000ff">base</span>[<span style="color: #006080">""</span>];

<span style="color: #606060">   9:</span>         }

<span style="color: #606060">  10:</span>     }

<span style="color: #606060">  11:</span> }

  </div>
</div>



As you can see, this is pretty simple. In order to use it, you declare the section in your app.config file:


<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">
  <div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">
    

<span style="color: #606060">   1:</span> <span style="color: #0000ff"><</span><span style="color: #800000">sectionGroup</span> <span style="color: #ff0000">name</span><span style="color: #0000ff">="customSettings"</span><span style="color: #0000ff">></span>

<span style="color: #606060">   2:</span>    <span style="color: #0000ff"><</span><span style="color: #800000">section</span> <span style="color: #ff0000">name</span><span style="color: #0000ff">="copyFiles"</span> <span style="color: #ff0000">type</span><span style="color: #0000ff">="NameValueSection, CustomConfiguration"</span><span style="color: #0000ff">/></span>

<span style="color: #606060">   3:</span> <span style="color: #0000ff"></</span><span style="color: #800000">sectionGroup</span><span style="color: #0000ff">></span>

<span style="color: #606060">   4:</span> <span style="color: #0000ff"><</span><span style="color: #800000">copyFiles</span><span style="color: #0000ff">></span>

<span style="color: #606060">   5:</span>    <span style="color: #0000ff"><</span><span style="color: #800000">add</span> <span style="color: #ff0000">name</span><span style="color: #0000ff">="C:\Windows"</span> <span style="color: #ff0000">value</span><span style="color: #0000ff">="*.dll"</span><span style="color: #0000ff">/></span>

<span style="color: #606060">   6:</span>    <span style="color: #0000ff"><</span><span style="color: #800000">add</span> <span style="color: #ff0000">name</span><span style="color: #0000ff">="C:\Temp"</span><span style="color: #0000ff">/></span>

<span style="color: #606060">   7:</span> <span style="color: #0000ff"></</span><span style="color: #800000">copyFiles</span><span style="color: #0000ff">></span>

  </div>
</div>



To access this configuration section in code, you simply need to do this:


<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">
  <div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">
    

<span style="color: #606060">   1:</span> NameValueSection nameValueSection = ConfigurationManager.GetSection(<span style="color: #006080">"copyFiles"</span>) <span style="color: #0000ff">as</span> NameValueSection;

<span style="color: #606060">   2:</span> <span style="color: #0000ff">if</span> (nameValueSection != <span style="color: #0000ff">null</span>)

<span style="color: #606060">   3:</span> {

<span style="color: #606060">   4:</span>     NameValueConfigurationCollection settings = nameValueSection.Settings;

<span style="color: #606060">   5:</span>     <span style="color: #0000ff">foreach</span> (<span style="color: #0000ff">string</span> key <span style="color: #0000ff">in</span> settings.AllKeys)

<span style="color: #606060">   6:</span>     {

<span style="color: #606060">   7:</span>         Console.WriteLine(settings[key].Name + <span style="color: #006080">": "</span> + settings[key].Value);

<span style="color: #606060">   8:</span>     }

<span style="color: #606060">   9:</span> }

  </div>
</div>



This is about as simple as it gets. Even though you aren't actually using the real NameValueCollection you are using the NameValueConfigurationCollection, which has almost identical behavior. This is the solution that I finally ended up implementing and it works great. As you can see, with a minimal amount of effort you are now able to use a NameValueCollection in your configuration files.


<div class="wlWriterSmartContent" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:d6ec8741-e7ef-49b9-bbc5-e7512ab951ea" style="padding-right: 0px; display: inline; padding-left: 0px; padding-bottom: 0px; margin: 0px; padding-top: 0px">*Technorati Tags: [.NET](http://technorati.com/tags/.NET), [C#](http://technorati.com/tags/C#), [NameValueCollection](http://technorati.com/tags/NameValueCollection), [ConfigurationManager](http://technorati.com/tags/ConfigurationManager)*</div>
