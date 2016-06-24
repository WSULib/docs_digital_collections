# Helpful Console Commands

Below are a bunch of helpful command chunks for indexing, purging, interacting with Readux books.

#### Index Proxy Objects
Uses `eulindexer` as run through `Ouroboros`:
<pre><code>from console import *

sparql_response = fedora_handle.risearch.sparql_query('select $virtobj where  {{ $virtobj &lt;http://digital.library.wayne.edu/fedora/objects/wayne:WSUDOR-Fedora-Relations/datastreams/RELATIONS/content/isVirtualFor&gt; &lt;info:fedora/%s&gt; . }}' % (ENTER_PID_HERE))

for obj in sparql_response:
    print "Indexing object: %s" % obj['virtobj']
    print requests.get("http://localhost/ouroboros/solrReaduxDoc/%s/%s" % (obj['virtobj'].split("info:fedora/")[-1],action) ).content
</code></pre>

#### Generate virtual objects
```
from console import *
o = w('wayne:Almanackfo1887b4801574x')
o.regenReaduxVirtualObjects()
o = w('wayne:DSJv4i14DSJ19990221')
o.regenReaduxVirtualObjects()
```

#### Generate TEI
From command line:
```
python manage.py add_pagetei -u wayne:Almanackfo1887b4801574x_Readux_VirtualVolume
python manage.py add_pagetei -u wayne:DSJv4i14DSJ19990221_Readux_VirtualVolume
```

#### Operate on Volume or Page object in Readux Django shell
Open Django shell from `/opt/readux`
```
python manage.py shell
```
```
from readux.fedora import ManagementRepository
repo = ManagementRepository()
from readux.books.models import Volume, VolumeV1_0, VolumeV1_1, PageV1_0, PageV1_1
vol_o = repo.get_object('wayne:DSJv4i14DSJ19990221_Readux_VirtualVolume',type=Volume) #Volume object
page_o = repo.get_object('wayne:DSJv4i14DSJ19990221_Readux_VirtualPage_7',type=PageV1_1) #Page object
```