# WSUDOR Content Models

**Note:** WSUDOR Content Models are also referred to as "Content Types" in code and documentation; they are referring to the same thing described below.

WSUDOR content models are a bit of a hybrid between **intellectual items** and **fedora objects** ([read more about that distinction here](fedora_objects.md)).  WSUDOR Content Models are python files, python classes specifically, that Ouroboroes leverages to create objects, edit and manage them, and provide access through the API and front-end.

Similar to [Islandora's Solution Packs](https://wiki.duraspace.org/display/ISLANDORA711/Solution+Packs), [Hydra Content Models](https://wiki.duraspace.org/display/hydra/Hydra+objects%2C+content+models+(cModels)+and+disseminators), and the inspiration behind the [Portland Common Data Model (PCDM)](https://github.com/duraspace/pcdm/wiki), WSUDOR Content Models are "opinionated" models, imposed at the level of code to faciliate the programmatic creation, preservation, managment, and access of things in our repository.  They are critically important as they codify our preservation and access approaches and philosophies in human and machine readable formats.

WSUDOR Content Models are models, but we often refer to the actual instantiation of of a content model -- technically one or many fedora objects -- as a **WSUDOR Object** because they do drive the creation of actual fedora objectcs.  Object-Oriented Programming (OOP) is a very nice metaphor for the whole thing, and in fact, has many direct parallels.  

For example, the WSUDOR Content Model `WSUDOR_Image` -- a python class -- has the method `regenJP2`.  This method creates a new JPEG2000 datastream based on the original TIFF image file.  When we open up a single Fedora object that is of the type `WSUDOR_Image` -- let's say a civil war item -- it will have that `regenJP2` as a method to regenerate its own JPEG200 datastream.

Or, there is an even more general WSUDOR Content Model, `WSUDOR_Object`, that all objects in our repository share as a parent content model.  `WSUDOR_Object` has a `index` method which indexes the object in Solr.  Whether its a simple image object like the civil war letter, or a complex object like the book *Sketches and Scraps*, the primary object for an item will have the method `index` to index itself.  

## Disclaimer

It's very easy to use the words "fedora object", "object", "item", "WSUDOR object", etc., interchangeably.  They do have specific meanings in the context of this repository, but it's common to use them somewhat interchangeably.  

One goal of the WSUDOR Content Models is that you don't have to constantly remember be cognizant of the fact that an ebook is actually comprised of dozens, or hundreds, of discrete fedora objects.  It is sufficient to refer to refer to it as a single "object" or "item" when indexing, migrating, etc.  On the back-end, dozens or hundreds of objects are being updated, with 5-10 datastreams each, but the ebook *Sketches and Scraps*, is for all intents and purposes, "an object in the repository," and we refer to it as such.

## Instantiating a Content Model



## Content Type Specific Models

Each Content Type -- e.g. Image, Audio, Document, etc. -- has its own WSUDOR Content Model.  These Content Type specific Models have their own markdown file in this directory with information specific to it.

A good starting place is [`WSUDOR_Object`](WSUDOR_Object.md), the WSUDOR Content Model from which all others are derived from and extend.

WSUDOR Content Models:

 * [WSUDOR_Object - Generic, base object](WSUDOR_Object.md)
 * [WSUDOR_Image - Image objects](WSUDOR_Image.md)



