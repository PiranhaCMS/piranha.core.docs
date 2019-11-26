# Authentication

Piranha doesn't really care **how** your users gets authenticated, whether it's the end users of your application or the administrators accessing the manager interface. Instead, Piranha uses a claims based security model to check what the current user has access to.

We provide two different packages for handling authentication, one for development and one for production scenarios.

To read more about how the implement custom authentication services for your application, please refer to [Authentication](../extensions/authentication) under the Extensions section.

## Core Claims

The core Piranha application has two Claims that are used when trying to preview unpublished content.

* `PiranhaPagePreview`
* `PiranhaPostPreview`

## Manager Claims

THe following claims define the different actions the logged in user can perform in the manager interface. To assign these claims to different users you setup `Roles` which have access to different `Claims`. A user can have several roles.

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