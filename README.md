# Welcome to the Piranha Docs

This documentation is designed to be presented on the official [piranhacms.org](http://piranhacms.org) website. In order to do so we're using a small Module we've created called `Statica` that converts a hierarchical `markdown` structure into a partial sitemap which can be used in a Piranha site. You can find the source code for this module here:

[https://github.com/tidyui/statica](https://github.com/tidyui/statica)

For everything to work as smooth as possible you need to follow the syntax of this tool, which is fairly simple:

* All files or folders **must exactly** follow the syntax `xx. Title`, where `xx` is the sort order of the item.
* All files must be in markdown `.md`.
* Folder pages that should also have content must include a `Index.md`
* URL's to images or other content **must** be absolute URL's and not hosted in this repo.