# Ouroboros Deploy

Though Ouroboros will likely be installed with the vagrant build, here are instructions to inform that process and/or fixes to install.

## Configuration

### Remote Repositories
One capability of Ouroboros is the ability to move objects from one repository to another.  Most often, in the name of moving objects from a `workdev` server to the `production` machine.  Or, `production` to `storage`, `archivematica` to `storage`, etc.

The `local` and remote repositories are configured in the `localConfig.py` file.  The default vagrant build comes with a local repository at `192.168.42.5`, obviously this needs to be updated for production!  And for dev work, as it's handy to "point" to the production box to grab and send objects.

Default in `localConfig.py`:
```
REMOTE_REPOSITORIES = {
    'local' : {
        'OUROBOROS_BASE_URL':'http://localhost/ouroboros',
        'FEDORA_ROOT':'http://localhost/fedora',
        'FEDORA_USERNAME':'fedoraAdmin',
        'FEDORA_PASSWORD':'fedorapassword',
        'SOLR_ROOT':'http://localhost/solr4',
        'IIIF_MANIFEST_TARGET_HOST':'192.168.42.5'
    }
}
```

Example of a dev configuration, pointing to production:
```
REMOTE_REPOSITORIES = {
    'local' : {
        'OUROBOROS_BASE_URL':'http://localhost/ouroboros',
        'FEDORA_ROOT':'http://localhost/fedora',
        'FEDORA_USERNAME':'fedoraAdmin',
        'FEDORA_PASSWORD':'fedorapassword',
        'SOLR_ROOT':'http://localhost/solr4',
        'IIIF_MANIFEST_TARGET_HOST':'192.168.42.5'
    },
    'production' : {
        'OUROBOROS_BASE_URL':'http://production.foo.bar/ouroboros',
        'FEDORA_ROOT':'http://production.foo.bar/fedora',
        'FEDORA_USERNAME':'SECRET_PASSWORD',
        'FEDORA_PASSWORD':'SECRET_PASSWORD',
        'SOLR_ROOT':'http://production.foo.bar/solr4',
        'IIIF_MANIFEST_TARGET_HOST':'production.foo.bar'
    }
}
```

The dictionary key `production` is then used throughout Ouroboros to send and recieve objects.