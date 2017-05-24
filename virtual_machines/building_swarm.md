# Building VM swarm

The Digital Collections ecosystem is comprised of a handful of cooperating, complimentary Virtual Machines (VMs).  Each VM serves a different role in the ecosystem:

  * `dataslice`: primary Fedora Commons repository instance, other VMs connect to this
  * `public`: front-facing, public interface
  * `workdev`: stable management server, that consumes messages from `dataslice` VM
  * local VMs: these are small VMs built on local machines for ingest and development
  
Each VM follows essentiall the same vagrant / provisioning, but requires a bit of configuration to satisfy its unique role.

## dataslice

The `dataslice` is primarily just a spinning instance of Fedora for other VMs to utilize, the following can be flipped off or removed:

  * Solr
  * Ouroboros

`dataslice` must also accept connections at `/fedora` for a handful of expectant servers, which is configured in Apache by adding those IP addresses to the `ADMIN_IP_ADDRESSES` variable.

## public

The `public` VM is designed to be a **read-only** connection to `dataslice`.  The following components can be flipped off:

  * Fedora
  
Additionally, you'll want to setup the `REMOTE_REPOSITORIES` dictionary in `localConfig.py` to point at `dataslice` as the user `fedoraView`.  This grants only `API-A` access to `public`'s Ouroboros instance, ensuring it cannot write to `dataslice`.

You will also need to point `public`'s instance of Loris at Fedora on `dataslice`.  This can be done in `/etc/loris2/loris2.conf` by changing the following:

    [[fedora]]
        url = 'http://localhost/fedora/objects/%s/datastreams/%s/content'
        
Finally, it is important to turn **off** consuming of messages from Fedora on `dataslice` (as this is the job of `workdev`).  This can be done in `/opt/ouroboros/localConfig.py` under the `FEDCONSUMER_FIRE` variable.

## workdev

The `workdev` VM is designed to be a stable instance of Ouroboros that can be used for management of WSUDOR objects.  As such, it requires as read/write connection to `dataslice` and should use the user `fedoraAdmin` when connecting.  

Like `public`, the following components can be turned off:

  * Fedora
  
One particularly special and important configuration for `workdev` is configuring it to consume messages from the Fedora instance on `dataslice`.   

## local VMs

Build away!  These are unique builds, designed to have 100% functionality, with optional tethers to `dataslice` for sending objects to.  This VM can be configured to have read/write access as well to `dataslice`, making development of the front-end possible with live objects from Fedora.

# Troubleshooting / Notes

  * Remember: each VM may be connected to Fedora on `dataslice`, but it will need to index the objects locally.  This can be performed in Ouroboros (and may take some time).  

# Removing Services

## Fedora
First stop the tomcat service `service tomcat7 stop` and then remove the fedora war file from `/var/lib/tomcat7/webapps`. Also delete the `fedora` directory inside webapps. Start tomcat back up with `service tomcat7 start`.


## Ouroboros
Remove `ouroboros.conf` from /etc/supervisor/conf.d. This is the configuration file that Supervisor uses to automatically start Ouroboros on boot. Next remove the folder `/opt/ouroboros` using a command such as `rm -r /opt/ouroboros`.


## Solr
First stop the tomcat service `service tomcat7 stop` and then remove the solr4 war file from `/var/lib/tomcat7/webapps`. Also delete the `solr4` directory inside webapps. Start tomcat back up with `service tomcat7 start`.
