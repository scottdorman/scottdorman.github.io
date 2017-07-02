---
layout: post
title: Integrating ASP.NET Core Configuration in MVC 4
date: '2016-03-19 14:15:08 -05:00'
categories: codeproject
tags: .net-core asp.net-core configuration
---

[ASP.NET Core 1.0](http://docs.asp.net/en/latest/conceptual-overview/aspnet.html) (what had been called ASP.NET 5) is a complete redesign of ASP.NET that is open-source and cross-platform. Since this is a redesign of the framework, it comes with a lot of architectural changes that make it more modular. One of those changes is that environment-based configuration is now built-in. The biggest benefit of this new configuration system is that it's not based on `System.Configuration` or `web.config`. Instead, it pulls from an ordered set of configuration providers that support a variety of file formats (such as XML and JSON) as well as environment variables. If one of the built-in configuration providers doesn't meet your needs, you can write your own.

What's nice about this model is that it's not integrated in to ASP.NET Core 1.0 as an intrinsic feature but rather implemented as NuGet packages. The most common ones are

*   [Microsoft.Extensions.Configuration](https://www.nuget.org/packages/Microsoft.Extensions.Configuration) 
*   [Microsoft.Extensions.Configuration.CommandLine](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.CommandLine) 
*   [Microsoft.Extensions.Configuration.EnvironmentVariables](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.EnvironmentVariables) 
*   [Microsoft.Extensions.Configuration.FileExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.FileExtensions) 
*   [Microsoft.Extensions.Configuration.Ini](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Ini) 
*   [Microsoft.Extensions.Configuration.Json](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Json) 
*   [Microsoft.Extensions.Configuration.UserSecrets](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.UserSecrets) 
*   [Microsoft.Extensions.Configuration.Xml](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Xml)   

Because the configuration support has been implemented as NuGet packages, they can be included in other projects, not just ASP.NET Core. Even more importantly, these packages support .NET Framework 4.5.1. (It would be nice for these packages to support even earlier versions of the Framework, but that's another post.)

There is already a lot of information about [using configuration](http://docs.asp.net/en/latest/fundamentals/configuration.html) in ASP.NET Core 1.0, including [details on how to work with environments](http://docs.asp.net/en/latest/fundamentals/environments.html), so I'm not going to cover that here. Instead, I'm going to talk about how to use these packages in an ASP.NET 4 MVC project.

Although it's possible to use the configuration system independently from dependency injection, if you couple them together you get built-in support to use POCOs for your settings classes and to pass them as constructor injected parameters. The implementation in this post assumes you're using the built-in dependency injection support and you can refer to my post about [how to integrate it in to an ASP.NET 4 MVC project]({% post_url /2016/2016-03-17-integrating-asp.net-core-dependency-injection-in-mvc-4 %}) for details about the `DefaultDependencyResolver` class that's used a bit later. If you're using another DI framework, you'll want to configure the container and resolver as necessary for that framework. For the purposes of this blog post, I'm going to work with a JSON configuration file, so add a reference to the `Microsoft.Extensions.Configuration.Json` NuGet package. This will add all of the other supporting packages needed.

If you don't already have a `Startup.cs` file, add one so it looks like the following. (If you do already have the file, you can simply modify it to include the `ConfigureServices` method if it's not already there or update it and the two lines in the `Configuration` method.)

```csharp
using System.Web.Mvc;
using Microsoft.Owin;
using Owin;

[assembly: OwinStartupAttribute(typeof(WebApplication1.Startup))]
namespace WebApplication1
{
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            var services = new ServiceCollection();
            ConfigureServices(services);
        }

        public void ConfigureServices(IServiceCollection services)
        {
           services.AddOptions();
           services.AddConfiguration();
           var resolver = new DefaultDependencyResolver(services.BuildServiceProvider());
           DependencyResolver.SetResolver(resolver);
        }
    }
}
```

The [`AddOptions`](http://docs.asp.net/en/latest/fundamentals/configuration.html#using-options-and-configuration-objects) method adds the support for injecting the options classes using the `IOptions<TOptions>` service. The `AddConfiguration` method tells the configuration system where to get its configuration data and can be added by including the following extensions class. (If you already have one, just add the `AddConfiguration` method and namespace reference.)

```csharp
public static class ServiceProviderExtensions
{
        public static IServiceCollection AddConfiguration(this IServiceCollection services)
        {
            var builder = new ConfigurationBuilder()
               .AddJsonFile(@"App_Data\config.json");

            var configuration = builder.Build();
            services.Configure<ApplicationOptions>(configuration.GetSection(ApplicationOptions.Key));
            return services;
        }
}
```

You'll want to make sure to include a reference to the `Microsoft.Extensions.Configuration` namespace in order to get access to the `ConfigurationBuilder` class and the `AddJsonFile` extension method.

In this example, I've put the my configuration file in the `App_Data` folder and named it `config.json`. You're free to put files anywhere that makes sense and name them whatever you want. If you keep all of your configuration files in the same folder, you can call the `SetBasePath` extension method and give it that common folder; that way you don't have to keep specifying the path for each of the `AddJsonFile` calls.

The settings class is called `ApplicationOptions` and would have public properties corresponding to the JSON structure. Although this isn't necessary, it seems like the convention adopted by the .NET team is to end the options classes with the word Options. I think this is a good convention as well, and recommend following it. Since the calls to `GetSection` expect a string key, I also add a public string constant called `Key` to my POCO classes that I can use instead of string literals all over the place. This allows me to easily change the value later on if needed.

Now, whenever you need access to your options, you can just pass it in on the constructor.

```csharp
public class HomeController : Controller
{
    public HomeController(IOptions<ApplicationOptions> options)
    {
        Options = options.Value;
    }

    ApplicationOptions Options { get; }

    public IActionResult Index()
    {
        return View(Options);
    }
}
```
