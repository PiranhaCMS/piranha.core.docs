# Getting Started

> The fastest way to get started is to use one of the Project Templates available. If you want to read more about this, please go to [Project Templates](getting-started/project-templates).


## Installing From NuGet

All libraries and components for Piranha is available on NuGet. You can read more about all of the available core packages [here](getting-started/nuget-packages).


## Installing From GitHub

If you want the latest source code and maybe be a part of the community and contribute to Piranha you should head over to `GitHub`. You can read more about this [here](getting-started/source-code).

## Project Setup

### Configure the services

When configuring the services you should register of the Piranha modules you want to use. As an example, let's look at the service configuration for a project that uses `SQLite` and `Piranha.AspNetCore.Identity.SQLite`.

**Setup For Version `7.0`**

    public void ConfigureServices(IServiceCollection services)
    {
        services.AddLocalization(options =>
            options.ResourcesPath = "Resources"
        );
        services.AddMvc()
            .AddPiranhaManagerOptions()
            .SetCompatibilityVersion(CompatibilityVersion.Version_2_2);

        services.AddPiranha();
        services.AddPiranhaApplication();
        services.AddPiranhaFileStorage();
        services.AddPiranhaImageSharp();
        services.AddPiranhaManager();

        services.AddPiranhaEF(options =>
            options.UseSqlite("Filename=./piranha.razorweb.db"));
        services.AddPiranhaIdentityWithSeed<IdentitySQLiteDb>(options =>
            options.UseSqlite("Filename=./piranha.razorweb.db"));
    }

**Setup For Version `6.0`**

    public void ConfigureServices(IServiceCollection services)
    {
        services.AddMvc(config =>
        {
            config.ModelBinderProviders.Insert(0,
                new Piranha.Manager.Binders.AbstractModelBinderProvider());
        });

        services.AddPiranha();
        services.AddPiranhaApplication();
        services.AddPiranhaFileStorage();
        services.AddPiranhaImageSharp();
        services.AddPiranhaManager();

        services.AddPiranhaEF(options =>
            options.UseSqlite("Filename=./piranha.db"));
        services.AddPiranhaIdentityWithSeed<IdentitySQLiteDb>(options =>
            options.UseSqlite("Filename=./piranha.db"));
    }

## Configure the application

Once the services has been configure you initialize the Piranha CMS application. Let's again look at how it's done in the example project. Please note that generic AspNetCore setup has been omitted.

    public void Configure(IApplicationBuilder app, IHostingEnvironment env, IApi api)
    {
        ...

        // Initialize Piranha
        App.Init(api);

        // Build page types
        var pageTypeBuilder = new Piranha.AttributeBuilder.PageTypeBuilder(api)
            .AddType(typeof(Models.StandardPage))
            .AddType(typeof(Models.TeaserPage));
        pageTypeBuilder.Build()
            .DeleteOrphans();

        // Register middleware
        app.UseStaticFiles();
        app.UseAuthentication();
        app.UsePiranha();
        app.UsePiranhaManager();
        app.UseMvc(routes =>
        {
            ...
        });

        ...
    }

The important part here is the **order** in which middleware is registered. The current `security` component should always be registered before the rest of the Piranha middleware, and the rest of the Piranha middleware should be registered **before** MVC. This is needed as the middleware re-writes the request and passes it on to the correct MVC route that should handle it.