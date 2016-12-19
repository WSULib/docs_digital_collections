# Deploy

Though our instance of Readux will likely be installed with the vagrant build, here are instructions to inform that process and/or fixes to install.


## PreReqs
Hopefully these are covered with vagrant build, but worth noting here as well.

Requires Ruby and Ruby-Dev 2.x:

```
sudo apt-get -y install python-software-properties
sudo apt-add-repository -y ppa:brightbox/ruby-ng
sudo apt-get -y update
sudo apt-get -y install ruby2.2 ruby-switch
sudo ruby-switch --set ruby2.2
sudo apt-get -y install ruby2.2-dev
```

And the `teifacsimile_to_jekyll` gem from Emory:

```
sudo gem install /vagrant/downloads/teifacsimile_to_jekyll-0.6.0.gem
```


## Instructions


#### 1) Clone WSUDOR fork of Readux and use `wsu` branch:
```
git clone https://github.com/WSULib/readux.git
cd readux
git checkout wsu_deploy
```


#### 2) Prepare Solr
* create `readux` core using [INSERT LINK HERE]


#### 3) Install Readux
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
# install WSUDOR fork / copy of Emory's eultheme for local editing
cd /opt
git clone https://github.com/WSULib/wsudor_django_theme
cd wsudor_django_theme
# install from github
pip install -e git://github.com/WSUlib/wsudor_django_theme.git#egg=eultheme
```

#### 4) Configure
* create superuser
```
python manage.py createsuperuser
```

* Setup site domain:
"Use Django admin interface to configure the site domain name (used to generate absolute urls to full-text content for use with Voyant, and IIIF
server URL patterns)""
    * navigate to admin @ `/admin`
    * select "Sites" and add host information here


* Collect static files
```
python manage.py collectstatic
```


#### Create proxy Readux objects from WSUDOR objects
Creating proxy Readux proxy objects relies on methods built-in to WSUDOR objects.

* `.createReaduxVirtualObjects()` - creates proxy objects
* `.regenReaduxVirtualObjects()` - purges and recreates proxy objects

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
