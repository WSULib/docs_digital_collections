# Ouroboros

Ouroboros is python-based middlware, written in-house, that acts as a glue for our digital collections infrastructure.  It functions in a similar space to Hydra or Islandora, providing a middleground between low-level applications like Fedora Commons, Solr, SQL, Redis, etc. and the higher level front-end applications.  

Ouroboros is structured in three main areas, all of which run under a single [Twisted server](https://twistedmatrix.com/trac/) instance:

### API

The API is the primary link between the backend and the front-end.  The front-end queries Fedora Commons and Solr through this custom API via ajax calls.  The API is a flask app running under Twisted at `/WSUAPI`.

[More detailed API information](api/README.md)