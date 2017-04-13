# Fedora Commons

[Fedora Commons](http://fedorarepository.org/), "Fedora" for short, and not to be confused with [Fedora the Linux distribution](https://getfedora.org/), is digital object open-source software.  We are currently using Fedora 3.x (specifically, 3.8 as of 07/2016).

Fedora Commons is where all of the repository digital objects are stored.  This includes metadata, large binary files, and more.  In Fedora 3.x, items in the repository are comprised of **objects** and **datastreams**.  These objects are related to one another via **RDF relationships** as encoded in the `RELS-EXT` datastream for an object.

Specifically what datastreams each object contains are covered in more detail in the Content Types section, but most object contain at least the following datastreams (think: files):

* `MODS`
 * descriptive metadata
* Dublin Core (`DC`)
 * descriptive metadata *derived* from the MODS datastream
* `POLICY`
 * an XACML XML document that enforces security policies for object access
* `RELS-EXT`
 * RDF file that contains relationships to other files and collections

Fedora runs under our instance of Tomcat at `:8080`, at `/fedora`.   

Fedora is installed at `/opt/fedora`.

### Configuring Fedora
Most of our Fedora-level configurations are done in the with the `fedora.fcfg` file at `/opt/fedora/server/config/fedora.fcfg`.

Our changes / modifications are minimal, but we have a couple.

#### XACML
One are we have changed the default settings are for XACML policies.  Fedora Commons installs without enforcing XACML policies with the value, `permit-all-requests` in the `fedora.fcfg` file.  We enforce XACML policies by setting that value to, `enforce-policies`.  You can find that here in the `fedora.fcfg` file:



### Starting / Restarting / Stopping
Starting, stopping and restarting Fedora is done through Tomcat, `sudo service tomcat7 start|restart|stop`.  You can also _reload_ Fedora from the Tomcat manager GUI.

## :tomato:ToDo
* Finish modifications / configurations
