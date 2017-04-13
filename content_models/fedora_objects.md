# Fedora Objects

As we use Fedora Commons digital object repository software to store our digital objects, a reasonable granular unit to talk about preservation are **fedora objects**.

To think about what we are preserving, it can be helpful to differntiate between **intellectual** items and **fedora** digital objects.

## Intellectual Items

Intellectual items might include a single photograph, a book, an newspaper issue, an audio piece, a movie, or something more abstract like a "Learning Object".  In this context, an intellectual item is high above the bits and bytes of files.  It is probably what many of us would refer to in casual conversation, "We have an amazing item in our collection: a civil war letter between two brothers," or "Another item in our digital colllections is a 19th century children's book title, *Sketches and Scraps*".  Both that single letter or book we would consider an "intellectual item".

## Fedora Digital Objects

Fedora digital objects -- aka "fedora objects", "objects" -- are a bit more tightly defined.

Fedora 3.x -- the version we are using as of this writing -- is comprised of **objects** and **datastreams**.  Objects are containers for datastreams.  Datastreams are just single digital files, e.g. JPEG image, WAV audio, PDF, XML, etc..  

Often, there is a 1:1 relationship between an intellectual item and a fedora object.  In the case of the civil war letter, we might have one fedora digital object `wayne:MSS-001-001-005` that is a container for all the files that work in harmony to act as a digital representation of the physical letter.

### Why are there multiple files, and not just one digital TIFF image?

Fedora objects also must contain **metadata** about the item, sometimes in multiple forms.  For example we include metadata in `MODS` format, Dublin Core `DC`, and RDF, linked data relationships about the object `RELS-EXT`.  Each of these is a single **datastream**, and are all part of that single fedora **object**.

### What about a more complicated example like an ebook?

Where things get a bit more complicated is when a *single* intellectual item is preserved and made accessible by way of *multiple* fedora objects.  A book is a good example.  The single intellectual item, physical book *Sketches and Scraps*, when digitized and ingested into our digital collections, actually results in dozens of fedora objects!  The **primary** object oftens contains metadata information about the book, including datastreams like `MODS` and `DC`, but there can be lots of **linked** objects that contain the actual page images and text for each page in the book.  These are linked to the primary book object with RDF relationships.

## Why does this matter for Preservation?

This matters for preservation because we need to think carefully about what we are preserving.  When we say we are preserving the book *Sketches and Scraps*, we need to be clear we are managing dozens of unique fedora objects that all make up the intellectual item, *Sketches and Scraps*.  Most all of this is handled for us "under the hood" by Fedora and Ouroboros, but these distinctions are helpful when looking at datastreams we focus on for preservation.

## WSUDOR Content Models

This is all well and good, but how do you actually manage these things?

Because Fedora Commons will let you "model" objects -- what they are called, how many datastreams, what files go where, how many objects represent a single intellectual item -- any way you want, it requires some "opinionation" or modeling to make sure your digital objects are all preserved and accessed in the same way.  To that end, we have developed **WSUDOR Content Models**, which are basically blueprints for different kind of intellectual items, be them images, books, audio, video, documents, etc.  [Read more about WSUDOR Content Models here](wsudor_content_models.md).














