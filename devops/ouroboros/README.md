# Ouroboros

Ouroboros is python-based middlware, written in-house, that acts as a glue for our digital collections infrastructure.  It functions in a similar space to Hydra or Islandora, providing a middleground between low-level applications like Fedora Commons, Solr, SQL, Redis, etc. and the higher level front-end applications.

The name "Ouroboros" comes from an ancient symbol of a snake eating its own tail.  This symbol has many meanings, but one interesting one is the idea creating something from nothing, edges to primordial chaos.  Ouroboros provides a similar function in our digital collection infrastructure, actualizing abstract ideas about content types, ingest, metadata, and more in actionable code.  It's also fun to type.

[Ouroboros in GitHub](https://github.com/WSULib/ouroboros).

Ouroboros is structured in three main areas, all of which run under a single [Twisted server](https://twistedmatrix.com/trac/) instance:

### API (`WSUDOR_API`)

The API is the primary link between the backend and the front-end.  The front-end queries Fedora Commons and Solr through this custom API via ajax calls.  The API is a flask app running under Twisted at `/WSUAPI`.

[More information about the API](api/README.md)

### Manager (`WSUDOR_Manager`)

Referred to as "WSUDOR Manager", or often just "Ouroboros" for short, the Manager component of Ouroboros is where things are "done" in a practical sense.  WSUDOR Manager is a flask app that provides a GUI for performing just about any repository work that is not performed on the command line.  WSUDOR Manager has user login, is availble to multiple people (usually limited by IP), performs long, complex background jobs, and much more.  

[More information about WSUDOR Manager](manager/README.md)

### Content Types (`WSUDOR_ContentTypes`)

Content types in Ouroboros can be thought of as a combination of abstract digital object types found in the repository, and actual code / object methods that are used in the Ouroboros ecosystem to assert those abstract characteristics.  All Ouroboros content types extend the most general `WSUDOR_Object` type.

Examples include:
* `Image`
* `Collections`
* `Audio / Video`
* `WSUebooks`
* etc.

Ouroboros content types are central to WSUDOR.  The provide details for ingest for different types of materials, specifics on how metadata should be returned, and much more.

[More information about Ouroboros Content Types](content_types/README.md)

## :pizza: ToDo
* discuss Eulfedora