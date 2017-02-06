---
layout: post
title: NameValueCollection and .NET Configuration Files
date: '2008-03-16 20:00:02 -05:00'
---

I spent most of yesterday trying to figure out how to make use of a [`NameValueCollection`](http://msdn2.microsoft.com/689y5thy.aspx) in a .NET configuration file. After wasting almost the entire night fighting with this problem, I thought I would let everyone know that it is possible, and easier than you might think. (By the way, this was a clear case of working too long on the problem. After a good nights sleep, I solved this in under 5 minutes.)

At this point you might wonder why this was so difficult. The largest and most significant problem is the fact that NameValueCollection isn't serializable ([KB 814187](http://support.microsoft.com/kb/814187)). The reason for this is that NameValueCollection doesn't implement [`ICollection`](http://msdn2.microsoft.com/b1ht6113.aspx) but extends [`NameObjectCollectionBase`](http://msdn2.microsoft.com/ts6a60s4.aspx) instead. The recommended solution is to use a [`SoapFormatter`](http://msdn2.microsoft.com/5ktza7xf.aspx) to serialize and deserialize the collection. While using the SoapFormatter does work, it seemed like a very complex solution for a seemingly simple problem.

Not wanting to over-engineer my solution, I started searching the web for alternatives. I found several newsgroup postings that all said to use the SoapFormatter since that was the recommended solution and the only way to go. Not having drunk too much blue kool-aid, I kept searching. That search turned up an article by [Keyvan Nayyeri](http://nayyeri.net/blog/Serialize-NameValueCollection/) that shows how to created a serializable NameValueCollection. This approach was intriguing and certainly seemed to be a more useful solution than using the SoapFormatter, but again it seemed like a lot of work.

Keep in mind, all I wanted to be able to do in the configuration file was to create a section that looked like this:
 
```xml
<copyFiles>
  <add name="C:\Windows" value="*.dll"/>
  <add name="C:\Temp"/>
</copyFiles>
```

Continuing the search, I thought I found my answer. I stumbled across an [article](http://dotnet.org.za/ncode/archive/2007/01/19/net-how-to-use-custom-name-value-config-sections.aspx) (".NET How To Create and Use Custom Name-Value Config Sections") that shows how to do this in 4 simple steps. Reading through the article, I realized that it is written using the the .NET 1.0 and 1.1 [`ConfigurationSettings`](http://msdn2.microsoft.com/kw224t90.aspx), which is provided for backwards compatibility only. Since the application I'm working on is .NET 3.5 and taking advantage of many of the new language features, I wanted to ensure that I wasn't using any deprecated classes.

This is where I started running into additional problems. It seems that Microsoft provides a [`NameValueSectionHandler`](http://msdn2.microsoft.com/5fwwx482.aspx), which the article makes us of. The problem is that NameValueSectionHandler is architected following the .NET 1.0/1.1 model and implements the [`System.Configuration.IConfigurationSectionHandler`](http://msdn2.microsoft.com/6950ee5e.aspx) interface. This is great if you want to use the deprecated ConfigurationSettings class; if you want to use the recommended [`System.Configuration.ConfigurationManager`](http://msdn2.microsoft.com/ms134260.asp) or [`System.Web.Configuration.WebConfigurationManager`](http://msdn2.microsoft.com/ms151430.aspx) classes you are out of luck. They will only work with a class that derives from [`ConfigurationSection`](http://msdn2.microsoft.com/x0kca287.aspx).

So, after all this I thought I was out of luck and would need to write my own configuration section handler. (Remember, this was about 1:00 AM.) After sleeping on it, I realized that there was a much simpler way. Along with the `NameValueSectionHandler`, Microsoft also implemented [`NameValueConfigurationCollection`](http://msdn2.microsoft.com/ms134603.aspx) and [`NameValueConfigurationElement`](http://msdn2.microsoft.com/ms134619.aspx), which derive from the appropriate configuration classes to be used by the ConfigurationManager. After seeing that, I realized that all I needed to do was implement a NameValueSection which derives from ConfigurationSection.

This is where the solution becomes easy. In it's simplest most form, the NameValueSection looks like this:

```csharp
public class NameValueSection : ConfigurationSection
{
    [ConfigurationProperty("", IsDefaultCollection = true)]
    public NameValueConfigurationCollection Settings
    {
        get
        {
            return (NameValueConfigurationCollection)base[""];
        }
    }
}
```

As you can see, this is pretty simple. In order to use it, you declare the section in your app.config file:

```xml
<sectionGroup name="customSettings">
   <section name="copyFiles" type="NameValueSection, CustomConfiguration"/>
</sectionGroup>
<copyFiles>
   <add name="C:\Windows" value="*.dll"/>
   <add name="C:\Temp"/>
</copyFiles>
```

To access this configuration section in code, you simply need to do this:

```csharp
NameValueSection nameValueSection = ConfigurationManager.GetSection("copyFiles") as NameValueSection;
if (nameValueSection != null)
{
    NameValueConfigurationCollection settings = nameValueSection.Settings;
    foreach (string key in settings.AllKeys)
    {
         Console.WriteLine(settings[key].Name + ": " + settings[key].Value);
    }
}
```

This is about as simple as it gets. Even though you aren't actually using the real `NameValueCollection` you are using the `NameValueConfigurationCollection`, which has almost identical behavior. This is the solution that I finally ended up implementing and it works great. As you can see, with a minimal amount of effort you are now able to use a `NameValueCollection` in your configuration files.
