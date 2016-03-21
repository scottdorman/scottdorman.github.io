---
layout: post
title: Integrating ASP.NET Core Dependency Injection in MVC 4
---

<a href="http://docs.asp.net/en/latest/conceptual-overview/aspnet.html" target="_blank">ASP.NET Core 1.0</a> (what had been called ASP.NET 5) is a complete redesign of ASP.NET that is open-source and cross-platform. Since this is a redesign of the framework, it comes with a lot of architectural changes that make it more modular. One of those changes is that dependency injection (DI) is now built-in. This built-in DI support is not intended to replace more full-featured DI frameworks (like <a href="http://docs.structuremap.net/" target="_blank">StructureMap</a>, <a href="http://autofac.org/" target="_blank">Autofac</a>, <a href="http://www.ninject.org/" target="_blank">Ninject</a>, <a href="https://github.com/unitycontainer/unity" target="_blank">Unity</a>, and others), but rather provides common DI abstractions and allows you to replace the built-in container with one provided by another DI framework.

The important (and, in my opinion, more interesting) part of this DI support is that it’s not integrated in to ASP.NET Core 1.0 as an intrinsic feature but rather implemented as two separate NuGet packages: <a href="https://www.nuget.org/packages/Microsoft.Extensions.DependencyInjection/" target="_blank">Microsoft.Extensions.DependencyInjection</a> and <a href="https://www.nuget.org/packages/Microsoft.Extensions.DependencyInjection.Abstractions/" target="_blank">Microsoft.Extensions.DependencyInjection.Abstractions</a>. Because the DI support has been implemented as NuGet packages, they can be included in other projects, not just ASP.NET Core. Even more importantly, these packages support .NET Framework 4.5.1. (It would be nice for these packages to support even earlier versions of the Framework, but that’s another post.)

There is already a lot of information about using DI in ASP.NET Core 1.0, including a <a href="http://docs.asp.net/en/latest/fundamentals/dependency-injection.html" target="_blank">good explanation</a> on the ASP.NET site, so I’m not going to cover that here. Instead, I’m going to talk about how to use these packages in an ASP.NET 4 MVC project.

The first question you might ask is: Why? There are already a lot of DI frameworks that support ASP.NET 4 and also provide support for ASP.NET Core. If you’re comfortable using one of those frameworks, there is really no reason to switch. However, if you’re not already using one (or only making very light use of one), you might want to consider switching to reduce the overhead of including the larger DI framework and also to get familiar with how the built-in DI framework works in ASP.NET Core.

If you look at your ASP.NET 4 MVC project (or create a new one), you may have a `Startup.cs` file. (This is automatically created if you choose the “Individual User Accounts” authentication option.) If you don’t have this file, you’ll want to add it but make sure to leave out the call to `ConfigureAuth` since that’s part of the ASP.NET Identity framework which you won’t have.

By default, this file looks like:

```c#
using Microsoft.Owin;
using Owin;

[assembly: OwinStartupAttribute(typeof(WebApplication1.Startup))]
namespace WebApplication1
{
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
}
```

The first thing you need to do is add a reference to the `Microsoft.Extensions.DependencyInjection` NuGet package to your web project. Then, add a new method named `ConfigureServices` to the `Startup` class:

```c#
public void ConfigureServices(IServiceCollection services)
{
}
```

Inside `ConfigureServices`, you will want to add any services you need. This is done pretty much the same way you would in ASP.NET Core and is similar to what you would do using any of the other DI containers.

The first problem you’ll run in to is that you don’t implicitly have an `IServiceCollection` instance so you’ll need to create one. Change the `Configuration` method so it looks like this:

```c#
public void Configuration(IAppBuilder app) 
{

   var services = new ServiceCollection();
   ConfigureAuth(app);
   ConfigureServices(services);
}
```

Now that we have some services registered in the `ServiceCollection` instance, we need to build the provider and set it as the current dependency resolver. There are a couple of steps needed here, including a custom implementation of `IDependencyResolver` such as

```c#
public class DefaultDependencyResolver : IDependencyResolver
{
    protected IServiceProvider serviceProvider;

    public DefaultDependencyResolver(IServiceProvider serviceProvider)
    {
        this.serviceProvider = serviceProvider;
    }

    public object GetService(Type serviceType)
    {
        return this.serviceProvider.GetService(serviceType);
    }

    public IEnumerable&lt;object&gt; GetServices(Type serviceType)
    {
        return this.serviceProvider.GetServices(serviceType);
    }
}
```

You’ll want to make sure to include a reference to the `Microsoft.Extensions.DependencyInjection` namespace in order to get access to the `GetServices` extension method.

Once you’ve added this class, you need to change the `Configuration` method one more time, so that it looks like

```c#
public void Configuration(IAppBuilder app) 
{

   var services = new ServiceCollection();
   ConfigureAuth(app);
   ConfigureServices(services);
   var resolver = new DefaultDependencyResolver(services.BuildServiceProvider());
   DependencyResolver.SetResolver(resolver);
}
```

If you change your controller to now take a constructor dependency and try to run the project at this point, you’ll get a runtime error about a missing method exception saying that your constructor doesn’t implement the default parameterless constructor. That’s because we need to register the controllers as a service with the DI container. To do that (and make it easier to add other things to the DI container), add the following extensions class:

```c#
public static class ServiceProviderExtensions
{
   public static IServiceCollection AddControllersAsServices(this IServiceCollection services, IEnumerable<type> controllerTypes)
   {
      foreach (var type in controllerTypes)
      {
         services.AddTransient(type);
      }

      return services;
   }
}
```

Then add the following line to the `ConfigureServices` method:

```c#
services.AddControllersAsServices(typeof(Startup).Assembly.GetExportedTypes()
   .Where(t => !t.IsAbstract && !t.IsGenericTypeDefinition)
   .Where(t => typeof(IController).IsAssignableFrom(t) 
      || t.Name.EndsWith("Controller", StringComparison.OrdinalIgnoreCase)));
```

This will find all of the public types that implement the `IController` interface or end with the word “Controller” in the class name that aren’t abstract or an open generic type and add cause them to be added to the services collection. Now, if you run the project again, everything should work.

One important thing to be aware of is that we haven’t completely switched over to using a DI framework. If you created your project using the “Individual User Accounts” authentication option, you’ll also have a Startup.Auth.cs file in the `App_Start` folder of your project. That’s where the `ConfigureAuth` method can be found. If you haven’t made any changes to that code, the `ConfigureAuth` method registers the `ApplicationDbContext`, `ApplicationUserManager`, and `ApplicationSignInManager` with the `IAppBuilder` instance. More specifically, it registers them as part of the `OwinContext` that is then later retrieved by calling `HttpContext.GetOwinContext().Get<ApplicationSignInManager>()` or `HttpContext.GetOwinContext().GetUserManager<ApplicationUserManager>()`, which aren’t resolved through the `DependencyResolver`. I’ll show how to move these to use our new service provider in an upcoming post. 
