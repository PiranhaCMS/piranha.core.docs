# Caching

> For production scenarios we recommend a cache level of **at least** `Basic` to acheive maximum performance. This cache level will hold all meta-data in cache and avoid unneccesary roundtrips to the database.

All of the core services have built in support for caching. If enabled, all models are stored in cache after model transformation and invalidated from cache when the model is updated or deleted. The models are stored both as their CLR type **and** as a lighter info object (`PageInfo`, `PostInfo`) that can be used for listings. Please note that dynamic models are **not** cached and is therefor not suited for usage in high performance scenarios.

## How To Enable Cache

To enable the repository cache, simply register a cache service that implements `Piranha.ICache` in your `Startup.cs`. The following cache enables the standard memory cache:

using Piranha;

~~~ csharp
public void ConfigureServices(IServiceCollection services)
{
    ...

    services.AddPiranhaMemoryCache();

    ...
}
~~~

This will cause the cache to be injected to all services when they are created. Most cache services **should** be registered as `Singletons` as it is desirable that all instances reference the same cache object.

## Setting The Cache Level

By default Piranha caches **everything** when a Cache Service is registered, but you can configure the cache level by setting the property `Piranha.App.CacheLevel`. You can choose between the following levels:

##### CacheLevel.None

~~~ csharp
Piranha.App.CacheLevel = Piranha.Cache.CacheLevel.None;
~~~

Nothing is cached even if a cache service is registered.

##### CacheLevel.Minimal

~~~ csharp
Piranha.App.CacheLevel = Piranha.Cache.CacheLevel.Minimal;
~~~

The following data is kept in cache:

* Sites
* Params

##### CacheLevel.Basic

~~~ csharp
Piranha.App.CacheLevel = Piranha.Cache.CacheLevel.Basic;
~~~

The following data is kept in cache:

* Sites
* Params
* PageTypes
* PostTypes

##### CacheLevel.Full

~~~ csharp
Piranha.App.CacheLevel = Piranha.Cache.CacheLevel.Full;
~~~

Everything is kept in cache, including all Blocks and Fields for Content Types. This is the default cache level.
