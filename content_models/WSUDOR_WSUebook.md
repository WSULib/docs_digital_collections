# `WSUDOR_WSUebook` - eBook objects

## Description

This content model describes digitized versions of physical books.  The overall structure is a "primary" object containing metadata, thumbnails and previews, and some other representations of the full-book such as PDF, plain text, HTML, etc, and "constituent" objects that are instances of `WSUDOR_WSUebook_Page` for each page.

At this time, this is one of the more complex content model types.  

## Content Type Methods and Attributes

 * `pages_from_objMeta` - gets anticipated pages from `objMeta.json` file, used primarily for ingest
 * `pages_from_rels` - pages from RDF relationships, preferred to `pages_from_objMeta`
 * `representative_page` - returns eulfedora object for representative page object for the book
 * `genMissingPages` - method to generate blank pages, with message, for missing pages in sorted pages
 * `purgeConstituents` - purges all constituent objects (pages)
 * `processPDF` - creates and returns location of tempfile PDF that concatenates PDFs from each page into a single whole
 * `genIIIFManifest` - generates IIIF manifest by iterating through constituent pages objects
 * `indexPageText` - indexes full text from constituent page objects in `bookreader` core in Solr
 * Methods related to [Readux virtual objects](WSUDOR_Readux.md):
   * `createReaduxVirtualObjects` - creates and indexes Readux virtual objects
   * `regenReaduxVirtualObjects` - purges, recreates, and reindexes Readux

## Ingest

### Expected Files

WSUDOR eBooks expect a bag of files, with multiple file formats for each page:

 * image of page - usually TIFF
 * HTML of page text, with some formatting - created by Abbyy during OCR process
 * PDF of page, with image and overlayed text - created by Abbyy during OCR process
 * [ALTO XML](https://www.loc.gov/standards/alto/), geometric coordinates of each word on page - created by Abbyy during OCR Process

## Datastreams

### Preserved

Because eBook objects have constituent [`WSUDOR_WSUebook_Page`](WSUDOR_WSUebook_Page.md) objects for each page, the original files for each page -- image, HTML, PDF, ALTO XML -- are not preserved in this "parent" book object.

### Derivative

Similarily, derivatives are also created at the [`WSUDOR_WSUebook_Page`](WSUDOR_WSUebook_Page.md) level.

### Other

However, while original files are not preserved here, or 1:1 derivatives, there are some unique and important datastreams created, that are versioned and preserved.  These include:

 * `HTML_FULL` - fullbook, concatenated HTML from each page
 * `PDF_FULL` - fullbook_ concatenated PDF from each page

