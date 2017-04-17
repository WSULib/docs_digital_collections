# Solr

Solr is a fast, full-text search database from Apache.  We use Solr to search metadata, full-text, and other information from our digital objects.  Solr is the primary search database for the front-end (and library QuickSearch).

### Deployment
Solr runs at `:8080` under Tomcat, at `/solr4`.  

We have a single instance of Solr, running multiple cores.  These cores include:

* **fedobjs**
 * This core is an index of MODS, Dublin Core (DC), RDF relationships from digital objects, and more.  This core is queried for every search in digital collections, and is critical for overall functionality.
* **bookreader**
 * Used for indexing full-text from WSUebooks at the page level.

### Solr & Ouroboros
Ouroboros communicates with Solr via the [`mysolr`](http://mysolr.readthedocs.io/en/latest/) python package.  This package is used to index and search documents.

Indexing is performed via an action in Ouroboros called [`solrIndexer`](https://github.com/WSULib/ouroboros/tree/master/WSUDOR_Manager/actions/solrIndexer).  This module was written before Ouroboros was fully formed and will likely get rewritten at some point, to better align with Ouroboros job workflows.


## :tomato:ToDo
* outline and explain other cores (wait until moved?)
