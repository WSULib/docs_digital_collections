# Deploy

Though our instance of Readux will likely be installed with the vagrant build, here are instructions to inform that process and/or fixes to install.


## Instructions


#### Clone WSUDOR fork of Readux:
```
git clone https://github.com/WSULib/readux.git
```


#### Prepare Solr
* create `readux` core using [INSERT LINK HERE]


#### Ingest supporting fedora objects
* ingest Emory control objects from [INSERT LINK HERE]



#### Install Readux
(also see [Emory's deploy notes](http://readux.readthedocs.io/en/develop/deploynotes.html))
* Use pre-configured `localsettings.py`, or update `localsettings.py.dist` in `/opt/readux/readux`

* navigate to repo

* use ouroboros virtual environment (**important!**)
```
workon ouroboros
```

* Requires some prerequisites.
```
pip install fabric
fab build
```

* Database prep
```
python manage.py syncdb
python manage.py migrate
```

* clone and install WSUDOR fork / copy of Emory 'eultheme' for theming
```
git clone https://github.com/WSULib/wsudor_django_theme
cd wsudor_django_theme
python setup.py install
```

#### Configure
* create superuser
```
python manage.py createsuperuser
```

* Setup site domain:
"Use Django admin interface to configure the site domain name (used to generate absolute urls to full-text content for use with Voyant)""
    * under "Sites" in the admin


#### Create proxy Readux objects from WSUDOR objects
Creating proxy Readux proxy objects relies on methods built-in to WSUDOR objects.

* `createReaduxVirtualObjects` - creates proxy objects
* `regenReaduxVirtualObjects` - purges and recreates proxy objects

It is worth noting that all proxy objects contain `_Readux_Virtual` as part of the PID, and will ultimately terminate with something like `Volume`, `Book`, or `Page`.

e.g.
```
wayne:campbellamericansalvageb44603320 --> wayne:campbellamericansalvageb44603320_Readux_VirtualVolume
```

In addition to creating the proxy objects, these WSUDOR methods also generate Solr-ready metadata using Readux views, and index in Solr with Ouroboros.

Remember to create proxy objects for associated collection objects as well!


#### Create TEI
Readux includes python scripts (well, commands that Django can run from command line) to create TEI datastreams.  This should fire with the creation of proxy objects (or ingest), but here's how to run manually:

```
python manage.py add_pagetei -u wayne:bookpid_Readux_VirtualVolume
```

where `-u` forces update.


#### Start Server
```
python manage.py runserver HOST:PORT
```






