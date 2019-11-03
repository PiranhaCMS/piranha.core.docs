# Media Storage

When uploading media assets to the media library they are stored in the current **media storage**. To enable this feature you have to register a storage service first. Besides storing the uploaded media asset the media storage is also responsible for storing all **resized** and **cropped** versions of images that you create.

When you create a new application from one the [Project Templates](../basics/project-templates) the project will be setup with the **File Storage** service from scratch.

## How To Register Media Storage

To register a storage service you need to register a service that implements `Piranha.IStorage` in your `Startup.cs`. Piranha provides two standard packages available for media storage that you can choose between, you can read more about them in their respective section.

## Other Types of Storage

You can easily implement your own storage services by implemented the interfaces `Piranha.IStorage` and `Piranha.IStorageSession`. You can read more about this [here](../extensions/media-storage).

