# `WSUDOR_########` - ######## objects

## Description

This content model describes the constituent page objects for `WSUDOR_WSUebook` "parent" or "primary" objects.

These are not meant to be rendered on their own, but must be preserved as they contain the original page images and other page representations like HTML, PDF, etc.

## Content Type Methods and Attributes

 * `order` - returns integer of page's determined order in book, likely originating from `objMeta.json`, but also encoded in RDF relationships
 * `processImage` - used primarily for ingest, creates derivative images from original
 * `processHTML` - creates `HTML` datastream
 * `processALTOXML` - creates `ALTOXML` datastream
 * `regenJP2` - inspired by `WSUDOR_Image` Content Model, recreates JP2 derivative from original image file


## Ingest

### Expected Files

This content model is a bit different from others, as it is usually instantiated and created by the `ingest` method in [`WSUDOR_WSUebook`](WSUDOR_WSUebook.md).

It expects it's designated page number, which indicates where in the `objMeta.json` and bagit archive to look for the appropriate page files (image, HTML, PDF, and ALTO XML).  

## Datastreams

### Preserved

For a [`WSUDOR_WSUebook`](WSUDOR_WSUebook.md) "book", the assets for each page are stored and preserved in this constituent, content model for each page.

For each page, four unique datastreams are created:

 * `HTML` - HTML for the page
 * `PDF` - PDF of page
 * `IMAGE` - original page image, usually TIFF
 * `ALTOXML` - ALTO XML

Why aren't there page numbers associated with these datastreams?  How can we differentiate `IMAGE` from page 1 and `IMAGE` from page 4?  Remember, these datastreams are contained in unique fedora objects for each page, so they may have the same datastream ID.  The original filenames, such as `004.tiff` are stored in the parent book object's `OBJMETA` datastream if needed later.

### Derivative

In addition to the original files from digitization and the Abbyy OCR process, the following derivatives are created as well (taking cues from `WSUDOR_Image`):

 * `JP2` - JPEG2000 derivative of `IMAGE` datastream
 * `IIIF_ANNOLIST` - laying ground work for IIIF annotations, this datastream is created, but not yet used
 * `THUMBNAIL` - 200x200 thumbnail of `IMAGE` datastream

### Other

Other than storing the original page assets, and creating derivatives for access, no other unique, preserved datastreams are created.

