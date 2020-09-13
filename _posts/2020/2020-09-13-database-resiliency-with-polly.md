---
layout: post
title: Database Resiliency with Polly
date: '2020-09-13 02:45:00 -05:00'
tags: .net .net-core polly fault-tolerance resiliency database cadru
---

Handling errors is important to make your application more reliable. We all understand the importance of [Defensive programming](http://en.wikipedia.org/wiki/Defensive_programming) (I [talked]({% post_url /2008/2008-07-04-what-is-defensive-programming %} 'What is "Defensive Programming"?')  about it way back in 2008), including standard programming constructions like [`try-catch`](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/try-catch), `null` checking, using things like [Code Contracts](https://docs.microsoft.com/en-us/dotnet/framework/debug-trace-profile/code-contracts)), error [logging and tracing](https://docs.microsoft.com/en-us/dotnet/core/diagnostics/logging-tracing), and a variety of other techniques. 

With all of that, one thing that frequently gets forgotten about is connection resiliency and fault tolerance. This applies to any action that needs a network connection to complete, such as calling REST APIs, or an external dependency, such as a database connection. Network latency, connectivity issues (short term or not), or resource throttling are just a few of the unexpected errors that can occur. While these errors are outside of our control, they're usually transient in nature and correct themselves automatically and, most of the time, quickly. 

> Resiliency is the ability to recover from failures and continue to function. It isn't about avoiding failures but accepting the fact that failures will happen and responding to them in a way that avoids downtime or data loss. The goal of resiliency is to return the application to a fully functioning state after a failure. <small>[Implement resilient applications](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/implement-resilient-applications/)</small>

Although we can write custom code to handle these transient errors, that's a time consuming and non-trivial task to do it correctly. It's much better to use a dedicated library for such concerns. The first library (at least that I'm aware of and used) was the [Transient Fault Handling Application Block ("TOPAZ")](https://github.com/microsoftarchive/transient-fault-handling-application-block) from the Microsoft Patterns &amp; Practices group. While that project was archived years ago, some of the ideas it introduced have made their way into parts of .NET Framework itself and other Microsoft cloud computing technologies. The current approach in .NET Core is to use [Polly](https://github.com/App-vNext/Polly), a .NET resilience and transient fault handling library. If you want to implement resilient HTTP requests using `IHttpClientFactory`, the [recommended approach](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/implement-resilient-applications/implement-http-call-retries-exponential-backoff-polly) is to use Polly policies.

While that's great for HTTP based resources, what about database connections? There are many additional challenges when it comes to making resilient database queries, such as determining which errors are transient and determining the appropriate *strategy* for retying. The important part here is the word *strategy*. Retrying database access is more than catching an error and retrying the query a few times before giving up and reporting an error. It can depend on the database server, the error that occurred, and even what your application is trying to do.

Although the retry strategy described in [Troubleshooting connectivity issues and other errors with Azure SQL Database and Azure SQL Managed Instance](https://docs.microsoft.com/en-us/azure/azure-sql/database/troubleshoot-common-errors-issues) is specific to Azure SQL, it applies equally well to on-premise SQL Server instance (and probably any other database back-end as well). Specifically, the strategy described is:

> It is strongly recommended that your client program has retry logic so that it could reestablish a connection after giving the transient fault time to correct itself. We recommend that you delay for 5 seconds before your first retry. Retrying after a delay shorter than 5 seconds risks overwhelming the cloud service. For each subsequent retry, the delay should grow exponentially, up to a maximum of 60 seconds.

As you can see, that's a non-trivial strategy to implement and requires specific retry policies in place. In searching for reasonable strategies using Polly, I came across [How To Build Resilient Applications with Polly](https://stackify.com/resilient-applications-polly/) and [Reliable Database Connections and Commands with Polly](https://sergeyakopov.com/reliable-database-connections-and-commands-with-polly/). While these are good resources, they each took a slightly different approach.

I used the Stackify implementation, along with some of the [comments](https://github.com/vany0114/resilience-strategy-with-polly/issues/1#issuecomment-483856082) from @reisenberger, to implement Cadru.Polly, available on [GitHub](https://github.com/scottdorman/cadru/tree/master/src/Cadru.Polly) and as a [NuGet](https://www.nuget.org/packages/Cadru.Polly/) package.

### Sql Strategies
One of the main benefits here is that it wraps the entire retry strategy, as described above, in a simple to use (at least I hope it's simple to use) `SqlStrategy`. A `SqlStrategy` instance holds a single synchronous and asynchronous policy, built as a [`PolicyWrap`](https://github.com/App-vNext/Polly/wiki/PolicyWrap). This allows a single policy to encapsulate the entire strategy of policies in a consistent manner. It also means that a `SqlStrategy` is database-agnostic. The specific strategies employed don't matter to the strategy, and executing an action using a strategy is almost as simple as using a regular Polly Policy:

```csharp
var sqlStrategy = SqlServerStrategyBuilder.Default.Build();
sqlStrategy.SyncPolicy.Execute(() => DoSomething());
```
This code creates a default strategy for accessing a SQL Server database which handles a variety of error codes using a combination of a [Timeout](https://github.com/App-vNext/Polly/wiki/Timeout) policy, a [Retry](https://github.com/App-vNext/Polly/wiki/Retry), and a series of [Circuit Breaker](https://github.com/App-vNext/Polly/wiki/Circuit-Breaker) policies, all wrapped together in the correct order.

If you need to customize the strategy's policies further, you can do so before calling `Build`. You can start with the default policies and add [Fallback](https://github.com/App-vNext/Polly/wiki/Fallback) policies by calling one of the `WithFallback` overloads or a [Timeout](https://github.com/App-vNext/Polly/wiki/Timeout) per retry policy by calling the `WithTimeoutPerRetry` method. Building the strategy validates the policies first, so it won't let you include any of the default policies a second time. If you want to customize the policies completely, you can call either `SqlServerStrategyBuilder.Empty` or clear the `Policies` list on the default strategy builder. Finally, suppose you need access to the underlying Polly `PolicyBuilder`. In that case, you can call either `GetDefaultPolicyBuilder`, which will return a `PolicyBuilder` that handles the exceptions in the default exception handling strategy, or `GetPolicyBuilder`, which will return a `PolicyBuilder` that handles all of the exceptions in the collection of exception handling strategies.

### Exception Handling Strategies
Since databases have a *lot* of errors they can raise (SQL Server has over 10,000 error messages it can raise!), I adapted a concept introduced in the Transient Fault Handling Application Block but updated it for use with Polly. To allow for flexibility in deciding what errors are considered transient, the strategy builder takes a collection of [`IExceptionHandlingStrategy`](https://github.com/scottdorman/cadru/blob/master/src/Cadru.Polly/IExceptionHandlingStrategy.cs) instances. These are simple classes that implement a `bool ShouldHandle(Exception)` delegate. If the exception passed in is one that the strategy should handle, the method returns `true`; otherwise, it returns `false`. You can take a look at [SqlServerExceptionHandlingStrategy.cs](https://github.com/scottdorman/cadru/blob/master/src/Cadru.Polly/Data/SqlServer/SqlServerExceptionHandlingStrategy.cs) for some examples.

There are a lot of benefits to this approach:
1. it allows the exceptions handled by the policy to more easily change over time without having to rewrite the entire strategy,
2. it should allow more flexibility in designing strategies for other database engines, and
3. it allows your application to customize the exceptions for your own needs without changing the core library.

Since `SqlStrategy` takes a collection of strategies, the first strategy in that collection acts as the default strategy. This is the one used when you call `GetDefaultPolicyBuilder`. You can change which strategy is the default simply by passing them in a different order.

Out of the gate, there are four different exception handling strategies for SQL Server, each handling a different set of error numbers:

| Exception Handling Strategy | Errors Handled |
|-|-|
| SqlServerTransientExceptionHandlingStrategy | 40501, 49920, 49919, 49918, 41839, 41325, 41305, 41302, 41301, 40613, 40197, 10936, 10929, 10928, 10060, 10054, 10053, 4221, 4060, 12015, 233, 121, 64, 20 |
| SqlServerTransientTransactionExceptionHandlingStrategy | 40549, 40550 |
| SqlServerTimeoutExceptionHandlingStrategy | -2 |
| NetworkConnectivityExceptionHandlingStrategy | 11001 |


If you use the standard .NET Core dependency injection mechanism, you can use the [`UseExceptionHandlingStrategies`](https://github.com/scottdorman/cadru/blob/f6c6f93141759acb7043376adfc9e58c7f494833/src/Cadru.Polly/Data/SqlServer/ServiceCollectionExtensions.cs#L41) to register these with the DI container easily.

### Configuration Options
With so many different policies in use, configuring the various values can be done through the [`SqlStrategyOptions`](https://github.com/scottdorman/cadru/blob/master/src/Cadru.Polly/Data/SqlStrategyOptions.cs) class. If you're using the .NET Core configuration system, you can use this class as a strongly typed configuration object and read values in from your `appsettings.json` file. An example section might look like

```json
  "RetryStrategy": {
    "RetryCount": 3,
    "ExceptionsAllowedBeforeBreaking": 2,
    "DurationOfBreak": "00:00:25"
  }
  ```
This defines that the action will only be retried three times, that two consecutive exceptions of the same type will trip the circuit breaker, and that once tripped, the circuit will remain open for 25 seconds.

There are also some helpful configuration [extensions](https://github.com/scottdorman/cadru/blob/master/src/Cadru.Polly/Data/SqlStrategyOptionsExtensions.cs) defined which encapsulate the logic of retrieving the configuration value or it's default. 

### Other Polly Goodness
To add or retrieve things from the Polly [Context ](https://github.com/App-vNext/Polly/wiki/Keys-And-Context-Data), you might be interested in the extensions defined in [ContextExtensions](https://github.com/scottdorman/cadru/blob/master/src/Cadru.Polly/ContextExtensions.cs). This includes the ability to add or retrieve an `ILogger` instance using the `WithLogger`, `GetLogger`, or `TryGetLogger` methods. You can also easily get a strongly typed object from the context with the `TryGetValue<T>` method or even add a collection of items to the context all at once using one of the `WithContextData` overloads.

If you need to bundle together a context and a policy, you can use an [`ExecutionEnvironment` or an `AsyncExecutionEnvironment`](https://github.com/scottdorman/cadru/blob/master/src/Cadru.Polly/ExecutionEnvironment.cs).

Adding a [`PolicyRegistry`](https://github.com/App-vNext/Polly/wiki/PolicyRegistry) to the standard .NET Core DI mechanism can be done with the [`AddPolicyRegistry`](https://github.com/scottdorman/cadru/blob/f6c6f93141759acb7043376adfc9e58c7f494833/src/Cadru.Polly/ServiceCollectionExtensions.cs#L47) extension. There is also a factory class, [`SqlServerStrategyFactory`](https://github.com/scottdorman/cadru/blob/master/src/Cadru.Polly/Data/SqlServer/SqlServerStrategyFactory.cs), which can be added to the DI container  to easily create a strategy:

```csharp
services.AddSingleton(serviceProvider => SqlServerStrategyFactory.Instance.Create(serviceProvider));
```

This takes both an `IServiceProvider` and an `IEnumerable<IExceptionHandlingStrategy>` as parameters, but if you add the exception handling strategies to your DI container, the strategies will be automatically provided.

There's also a [logging policy](https://github.com/scottdorman/cadru/tree/master/src/Cadru.Polly/Logging) available, which allows you to log exceptions or handled results easily and then rethrow the exception. This is, for the most part, a direct port of what's available in [Polly.Contrib.LoggingPolicy](https://github.com/Polly-Contrib/Polly.Contrib.LoggingPolicy).
