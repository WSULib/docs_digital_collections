# WSUDOR Content Models

WSUDOR content models are a bit of a hybrid between **intellectual items** and **fedora objects**.  WSUDOR Content Models are python files, classes specifically, that are used in Ouroboros to create objects, edit them, and provide access through the API and front-end.

Similar to Islandora Solution Packs, or Hydra Content Models, WSUDOR Content Models are "opinionated" models, imposed at the level of code to faciliate the programmatic creation, preservation, managment, and access of things in our repository.  They are critically important to the whole enterprise, as they codify our preservation and access approaches and philosophies.

WSUDOR Content Models are models, but we often refer to the actual instantiation of of a content model -- technically one or many fedora objects -- as a **WSUDOR Object**.  Object-Oriented Programming (OOP) is a very nice metaphor for the whole thing, and in fact, has many direct parallels.  

For example, the WSUDOR Content Model `WSUDOR_Image`, itself a python class, has the method `regenJP2`.  This method creates a new JPEG2000 datastream based on the original image TIFF file.  When we open up a real, single Fedora object as a `WSUDOR_Image` instance -- let's say a civil war fedora object -- it will have that `regenJP2` as a method to regenerate its own JPEG200 datastream.

Or, there is an even more general WSUDOR Content Model, `WSUDOR_Object`, that all objects in our repository share as a parent content model.  `WSUDOR_Object` has a `index` method which indexes the object in Solr.  Whether its a simple image object like the civil war letter, or a complex object like the book *Sketches and Scraps*, the primary object for an item will have the method `index` to index itself.  

## Disclaimer

It's very easy to use the words "fedora object", "object", "item", "WSUDOR object", etc., interchangeably.  They do have specific meanings in the context of this repository, but it's often okay to use them somewhat interchangeably.  

One goal of the WSUDOR Content Models is that you don't have to constantly remember of think about the fact that an ebook is actually comprised of dozens, or hundreds, of fedora objects.  It is sufficient to refer to refer to it as a single "object" or "item" when indexing, migrating, etc.  On the back-end, dozens or hundreds of objects are being updated, with 5-10 datastreams each, but the ebook *Sketches and Scraps*, is for all intents and purposes, "an object in the repository".

## The Models

Each WSUDOR Content Model has it's own readme file in this directory with information specific to it.  A good starting place is [`WSUDOR_Object`](content_models/WSUDOR_Object.md), the WSUDOR Content Model from which all others derive from and extend.

