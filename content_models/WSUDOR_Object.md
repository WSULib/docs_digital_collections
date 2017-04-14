# `WSUDOR_Object` - Generic, base object

## Description

This is the most basic Contnt Model.  It provides methods and attributes that all WSUDOR Objects share, such as indexing, calculating object size, returning IIIF manifest (if it has one), etc.

**All** objects are instantiated as a `WSUDOR_Object`, and then extend the appropriate the appropriate Content Model type.

### Pre-existing objects

If objects already exist in Fedora, the appropriate Content Model type is deteremined by pinging the RDF relationship, `hasContentModel`.  It is worth noting that WSUDOR Objects are allowed to claim multiple Content Model types, in those cases, it falls back on the WSUDOR RDF relationship, `http://digital.library.wayne.edu/fedora/objects/wayne:WSUDOR-Fedora-Relations/datastreams/RELATIONS/content/preferredContentModel`.  

### New objects

If the object does not yet exist, it is assumed it is being instantiated from a bagit file.  In that case, the appropriate Content Model type is determined from the `content_type` attribute in the `objMeta.json` file that is part of the bag.

## Content Type Methods and Attributes

As mentioned, `WSUDOR_Object` contains methods shared by all objects in the repository.  Examples include:

 * `index` - used for indexing objects in Solr
 * `ingestBag` - used for ingesting a bag, fires associated Content Model type `ingest` method
 * `finishIngest` - runs *after* Conent Model specific ingest for all object types
 * `MODS_dict` - returns MODS datastream as python dictionary
 * `SolrDoc` - instance of `models.SolrDoc` used for accessing metadata after transform for Solr, and actually indexing in Solr
 * `iiif_manifest` - returns IIIF manifest (if available)
 * `object_size` - returns total object size, including constituent objects (if complex object), also calculates if not yet determined
 * `constituents` - returns list of constituent objects
 * `add_to_indexer_queue` - queues for index
 * `removeObjFromCache` - very important one, removes object from Loris and Varnish cache
 * `refresh` - index, regens some derivatives, and removes from cache
 * `sendObject` - send object to remote repository
 * `registerOAI` - created OAI-PMH identifier and addsd to OAI-PMH feed
 * `purge` - removes object from Fedora
 * `object_hierarchy` - for objects with hierarchical relationships, returns hierarchy as python dictionary
 * `regenRDF` - regenerates `RELS-EXT` datastream based on RDF relationships in triplestore
 
## Ingest

### Expected Files

As the base class, expectations for ingest are minimal but critical:

 * `objMeta.json` - JSON file that states Content Model type, object structure, XACML policy, and other pertinent information
 * `MODS.xml` - MODS descriptive metadata

## Datastreams

### Preserved

As the base class, this content model does not have any original files to preserve.

### Derivative

As this class is meant to be extended for more specific Content Model types, it does not create derivatives.

### Other

However, as the base Content Model type, it does create some essential datastreams on ingest for every object:

 * `POLICY` - XACML Fedora policy, pulling from `objMeta.json` file and pre-existing Fedora policy objects
 * `OBJMETA` - saves `objMeta.json` file as JSON datastream
 * `RELS-EXT` - while all objects have `RELS-EXT` by default, `WSUDOR_Object` writes some of the first relationships before the Content Model type steps in
 * `MODS` - creates datastream from `MODS.xml` file from bag
 * `BAGIT_META` - saves bagit file metadata as a tarball in datastream
 * `IIIF_MANIFEST` - if applicable, fires during `finishIngest` method
 * `PREMIS` - begins PREMIS log for this object

These datastreams become central for preservation, management, and access for the object.





