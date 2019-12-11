# Databases

The core library of Piranha is totally **database agnostic**. This means that it could very well use `JSON` files or a `NoSql` database to store it's data. However, we only provide core packages for using `Entity Framework Core` as data access so in the following pages we will focus on this scenario.

## Using Entity Framework Core

All data access in Piranha is implemented using `Linq Queries` over `Entity Framework Core`. In that sense Piranha should be compatible with all databases that have a provider for Entity Framework Core available. We try to keep the schema of Piranha as simple as possible only using:

* Primary Key Constraints
* Foreign Key Constraints
* Unique Indexes

This way we try to stay clear of things that we know are implemented differently in different providers, for example `auto-increment` columns. Some packages rely on external components (like `ASP.NET Identity`) that does not have this approach, and for these we provide multiple packages managaging database migrations.

To use the standard repositories for `Entity Framework Core` you must include the following package in your application:

~~~ csharp
PM> install-package Piranha.Data.EF
~~~

## Official Support

We only test and support `SQLite`, `SQLServer` and `SQLAzure`. The packages we have available for other database providers (for example `MySql` and `Postgres`) are **community initiatives**. If you encounter any issues with other database providers than the ones specified above, support for these should be handled by the people providing these packages in their respective GitHub repositories.

## Setting Up Database Provider

You can read more about how to configure your application for the different databases in their respective sections.