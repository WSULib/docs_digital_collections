# WSUDOR Content Models

*Note: WSUDOR Content Models are also referred to as "Content Types" in code and documentation; both refer to the same thing described below.*

WSUDOR Content Models (CMs) are a bit of a hybrid between **intellectual items** and **fedora objects** ([read more about that distinction here](fedora_objects.md)).  WSUDOR Content Models are python files, python classes specifically, that Ouroboroes leverages to create objects, edit and manage them, and provide access through the API and front-end.

Similar to [Islandora's Solution Packs](https://wiki.duraspace.org/display/ISLANDORA711/Solution+Packs), [Hydra Content Models](https://wiki.duraspace.org/display/hydra/Hydra+objects%2C+content+models+(cModels)+and+disseminators), and the inspiration behind the [Portland Common Data Model (PCDM)](https://github.com/duraspace/pcdm/wiki), WSUDOR Content Models are "opinionated" models, imposed at the level of code to faciliate the programmatic creation, preservation, managment, and access of things in our repository.  They are critically important as they codify our preservation and access approaches and philosophies in human and machine readable formats.

WSUDOR Content Models are models, but we often refer to the actual instantiation of of a content model -- technically one or many fedora objects -- as a **WSUDOR Object** because they do drive the creation of actual fedora objectcs.  Object-Oriented Programming (OOP) is a very nice metaphor for the whole thing, and in fact, has many direct parallels.  

For example, the WSUDOR Content Model `WSUDOR_Image` -- a python class -- has the method `regenJP2`.  This method creates a new JPEG2000 datastream based on the original TIFF image file.  When we open up a single Fedora object that is of the type `WSUDOR_Image` -- let's say a civil war item -- it will have that `regenJP2` as a method to regenerate its own JPEG200 datastream.

Or, there is an even more general WSUDOR Content Model, `WSUDOR_Object`, that all objects in our repository share as a parent content model.  `WSUDOR_Object` has a `index` method which indexes the object in Solr.  Whether its a simple image object like the civil war letter, or a complex object like the book *Sketches and Scraps*, the primary object for an item will have the method `index` to index itself.  

## Disclaimer

It's very easy to use the words "fedora object", "object", "item", "WSUDOR object", etc., interchangeably.  They do have specific meanings in the context of this repository, but it's common to use them somewhat interchangeably.  

One goal of the WSUDOR Content Models is that you don't have to constantly remember to be cognizant that an ebook is actually comprised of dozens, or hundreds, of discrete fedora objects.  It is sufficient to refer to it as a single "object" or "item" when indexing, migrating, etc.  On the back-end, dozens or hundreds of objects are being updated, with 5-10 datastreams each, but the ebook *Sketches and Scraps* is, for all intents and purposes, "an object in the repository," and we refer to it as such.

## Instantiating a Content Model

An object is opened or created as a WSUDOR Content Model by using the base class, `WSUDOR_Object`.  For example, from the command line, any pre-existing object in Fedora can be opened as a WSUDOR Object like this:

    obj = WSUDOR_ContentTypes.WSUDOR_Object('wayne:vmc14515')

Running a `dir` of that python object reveals the WSUDOR methods available:

    In [99]: dir(obj)
    Out[99]: 
    ['DC_Solr_flat',
     'DC_XML',
     'DC_dict',
     'DCfromMODS',
     'Fedora_ContentType',
     'MODS_Solr_flat',
     'MODS_XML',
     'MODS_dict',
     'RELS_EXT_Solr_flat',
     'RELS_INT_Solr_flat',
     'SolrDoc',
     'SolrSearchDoc',     
     '_checkJP2Codestream',
     '_checkJP2Orientation',
     '_checkJP2OrientationAndSize',
     '_extract_with_pillow',
     '_from_jp2',
     '_imageOrientation',
     '_removeDatastreamFromLorisCache',
     '_removeObjFromLorisCache',
     '_removeObjFromVarnishCache',
     'add_to_indexer_queue',
     'cacheInVarnish',
     'calc_object_size',
     'checkJP2',
     'collectionMembers',
     'constituents',
     'content_type',
     'description',
     'enrichMODSFromMETS',
     'finishIngest',
     'fixJP2',
     'genIIIFManifest',
     'hasInternalParts',
     'hasLearningObjects',
     'hasMemberOf',
     'iiif_factory',
     'iiif_manifest',
     'imageParts',
     'index',
     'indexToSolr',
     'index_on_ingest',
     'ingestBag',
     'isMemberOfCollections',
     'isSensitive',
     'label',
     'objMeta',
     'object_hierarchy',
     'object_size',
     'object_type',
     'ohandle',
     'orig_payload',
     'pid',
     'pid_suffix',
     'premis',
     'previewImage',
     'previewSolrDict',
     'prune',
     'public_api_additions',
     'purge',
     'rdf_triples',
     'refresh',
     'refresh_content_type',
     'regenJP2',
     'regenRDF',
     'registerOAI',
     'removeObjFromCache',
     'reportProb',
     'sendObject',
     'struct_requirements',
     'timeline',
     'update_object_size',
     'validIngestBag',
     'version']

When the object is instantiated, it's specific Content Model type is automatically determined, and the base `WSUDOR_Object` is extended with that class.  In the case of above, it was an image object and so extended with `WSUDOR_Image`.  You can check this:

    In [112]: obj.content_type
    Out[112]: 'WSUDOR_Image'

To see the whole hierarchy of classes extended:

    In [113]: print obj
    <WSUDOR_ContentTypes.WSUDOR_Image.WSUDOR_Image object at 0x7f48e8770690>

WSUDOR Content Models are *also* used for creating brand new WSUDOR Objects for ingest by pointing to a bagit file on disk and including the argument `object_type='bag'` when instantiating:

    In [101]: obj = WSUDOR_ContentTypes.WSUDOR_Object('/home/ouroboros/ingest_jobs/ingest_job_1/ea9dcf9a-d8a9-42bc-84b7-8d4d31d064ae', object_type='bag')
    object_type is bag, creating working dir at /tmp/Ouroboros/06c18cc0-9e7d-4c1c-aa0c-a5b1245e984f
    directory detected, symlinking
    payload is: /tmp/Ouroboros/06c18cc0-9e7d-4c1c-aa0c-a5b1245e984f
    objMeta.json loaded for: wayne:fourthfolio / Tragedy of King Lear

As this is a somewhat generic "bag" type object at this point, one of the few things you could do would be to ingest that object or "bag" with the following method:

    obj.ingest()

All of these methods are availalbe on the command line, or more commonly, are fired by actions and tasks in Ouroboros.

## objMeta

Another important thing to note is the `objMeta.json` referenced above when instantiating a WSUDOR Object from a bagit file.  All bags destined for ingest must contain an `objMeta.json` file that contains information about how the bag is structured.  This includes what file should be used as the thumbnail (`isRepresentedBy`), what datastreams are included, and extremely important, what WSUDOR Content Model to use!  

For example, after loading the bagit file above, and similar to what we did with a pre-existing object we opened, you can check what kind of WSUDOR Content Model the `objMeta.json` stated the object was:

    In [110]: obj.content_type
    Out[110]: u'WSUDOR_WSUebook'

With that information, the base object type `WSUDOR_Object` knows to extend itself with the content model, `WSUDOR_WSUebook`.  

Creating this `objMeta.json` is one of the trickier parts of preparing an intellectual item for ingest, and one of the most important.  Each WSUDOR Content Model requres an `objMeta.json` file included in the bagit file.  The `objMeta.json` file is usually prepared automatically in the bag creation step of the Ingest Workflow, but that is a bit out of scope here.  [You can read more about that process here](#).

## Content Type Specific Models

Each Content Type -- e.g. Image, Audio, Document, etc. -- has its own WSUDOR Content Model.  These Content Type specific Models have their own markdown file in this directory with information specific to it.

The basic documentation structure for each is as follows:

 * **Description** - short description of the content model
 * **Content Type Methods and Attributes** - methods and attributes *unique* to that content model, building on the base methods and attributes in `WSUDOR_Object`
 * **Ingest** - notes about ingest and object structure
   * **Expected Files** - files and structure expected for ingest, including 
 * **Datastreams** - notes about datastreams created and managed
   * **Preserved** - describes original, archival files, versioned in Fedora
   * **Derivative** - outlines derivative files created from originals, these are *not* versioned in Fedora and considered expendable
   * **Other** - other datastreams created, default to versioned in Fedora unless otherwise stated

A good starting place might be the base object type, [`WSUDOR_Object`](WSUDOR_Object.md), the WSUDOR Content Model from which all others are derived from and extend.

### WSUDOR Content Models:

 * [WSUDOR_Object - Generic, base object](WSUDOR_Object.md)
 * [WSUDOR_Image - Audio objects](WSUDOR_Audio.md)
 * [WSUDOR_Image - Collection objects](WSUDOR_Collection.md)
 * [WSUDOR_Image - Container objects](WSUDOR_Container.md)
 * [WSUDOR_Image - Document objects](WSUDOR_Document.md)
 * [WSUDOR_Image - Hierarchical Files objects](WSUDOR_HierarchicalFiles.md)
 * [WSUDOR_Image - Image objects](WSUDOR_Image.md)
 * [WSUDOR_Image - Learning objects](WSUDOR_LearningObject.md)
 * [WSUDOR_Image - Readux objects](WSUDOR_Readux.md)
 * [WSUDOR_Image - Video objects](WSUDOR_Video.md)
 * [WSUDOR_Image - Volume objects](WSUDOR_Volume.md)
 * [WSUDOR_Image - eBook objects](WSUDOR_WSUebook.md)
 * [WSUDOR_Image - eBook Page objects](WSUDOR_WSUebook_Page.md)



