# Getting Started

> The fastest way to get started is to use one of the Project Templates available. If you want to read more about this, please go to [Project Templates](getting-started/project-templates).


## Installing From NuGet

All libraries and components for Piranha is available on NuGet. You can read more about all of the available core packages [here](getting-started/nuget-packages).


## Installing From GitHub

If you want the latest source code and maybe be a part of the community and contribute to Piranha you should head over to `GitHub`. You can read more about this [here](getting-started/source-code).

## Project Setup

### Configure the services

When configuring the services you should register of the Piranha modules you want to use. As an example, let's look at the service configuration for a project that uses `SQLite` and `Piranha.AspNetCore.Identity.SQLite`.

#### Setup For Verison `7.0`

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

#### Setup For Version `6.0`

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

