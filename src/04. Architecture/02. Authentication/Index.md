# Authentication

Piranha doesn't really care **how** your users gets authenticated, whether it's the end users of your application or the administrators accessing the manager interface. Instead, Piranha uses a claims based security model to check what the current user has access to.

We provide two different packages for handling authentication, one for development and one for production scenarios.

To read more about how the implement custom authentication services for your application, please refer to [Authentication](../extensions/authentication) under the Extensions section.

## Adding Permissions

Besides the claims used by the default pages in the manager interface you can add custom claims for you application, both for custom manager pages **or** for securing pages in your application.

### Adding Application Claims

The application claims you add will be available when you edit and set up **Roles** in the manager if you're using the `Identity` package. These claims will also be available in the settings for your Pages & Posts and can be used for securing certain instances of your content. This should be added in your `Startup.cs`.

~~~ csharp
App.Permissions["Application"].Add(new Piranha.Security.PermissionItem
{
    Name = "WebUser",
    Title = "Web User"
});
~~~

The first name is the main category you want to group your permissions in and can be anything you like. In this example we've choosen the name "Application".

### Adding Manager Claims

Manager claims works in the same way as application claims, the only difference is that you set the property `IsInternal` to `true`. By doing this they are not shown when specifying permissions for your public pages & posts and should only be used when validating if the current manager should have access to something in the manager interface.

~~~ csharp
App.Permissions["Application"].Add(new Piranha.Security.PermissionItem
{
    Category = "My Manager Feature",
    Name = "EditStuff",
    Title = "Edit Stuff",
    IsInternal = true
});
App.Permissions["Application"].Add(new Piranha.Security.PermissionItem
{
    Category = "My Manager Feature",
    Name = "DeleteStuff",
    Title = "Delete Stuff",
    IsInternal = true
});
~~~

## Core Claims

The core Piranha application has two Claims that are used when trying to preview unpublished content.

* `PiranhaPagePreview`
* `PiranhaPostPreview`

## Manager Claims

The following claims define the different actions the logged in user can perform in the manager interface. To assign these claims to different users you setup `Roles` which have access to different `Claims`. A user can have several roles.

### Basic

* `PiranhaAdmin` If the user has access to the manager interface

### Aliases

* `PiranhaAliases` If the user can view the alias page
* `PiranhaAliasesDelete` If the user can delete existing aliases
* `PiranhaAliasesEdit` If the user can add and edit existing aliases

### Config

* `PiranhaConfig` If the user can view the config page
* `PiranhaConfigEdit` If the user can update config settings

### Media

* `PiranhaMedia` If the user can view the media page
* `PiranhaMediaAdd` If the user can upload new media
* `PiranhaMediaDelete` If the user can delete existing media
* `PiranhaMediaEdit` If the user can update existing media
* `PiranhaMediaAddFolder` If the user can add new folders in the media library
* `PiranhaMediaDeleteFolder` If the user can delete existing media folders

### Pages

* `PiranhaPages` If the user can view the page structure
* `PiranhaPagesAdd` If the user can add new pages
* `PiranhaPagesDelete` If the user can delete existing pages
* `PiranhaPagesEdit` If the user can view the page details
* `PiranhaPagesPublish` If the user can publish and unpublish pages
* `PiranhaPagesSave` If the user can update existing pages

### Posts

* `PiranhaPosts` If the user can view posts 
* `PiranhaPostsAdd` If the user can add new posts
* `PiranhaPostsDelete` If the user can delete existing posts
* `PiranhaPostsEdit` If the user can view the post details
* `PiranhaPostsPublish` If the user can publish and unpublished posts
* `PiranhaPostsSave` If the user can update existing posts

### Sites

* `PiranhaSites` If the user can view the site page
* `PiranhaSitesAdd` If the user can add new sites
* `PiranhaSitesDelete` If the user can delete existing sites
* `PiranhaSitesEdit` If the user can view site details
* `PiranhaSitesSave` If the user can update existing sites
