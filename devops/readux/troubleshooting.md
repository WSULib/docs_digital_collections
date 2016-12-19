# troubleshooting

First and foremost, check the logs!  They should be located at: `/var/log/readux/debug.l`.

## 404 for book that should be there

If you receieve a 404 error for a book that should be there, make sure it belongs to a collection object that also has virtual Readux objects created for it.  

For example, `wayne:Sketchesa1881b48389304_Readux_VirtualVolume` was returning the following error:

    RequestFailed: 404 Object not found in low-level storage: wayne:collectionRamsey_Readux_VirtualCollection
    
This confirms that a collection object is missing, as it cannot find `wayne:collectionRamsey_Readux_VirtualCollection` which is the associated collection object for this book.  Try creating virtual Readux objects for that collection object as well.

## OperationalError: no such table: downtime_period

If you receive a 500 error when accessing Readux front-end, and you see the following in the logs, `OperationalError: no such table: downtime_period`, it is possible the databases were not setup properly on build. 

Try running the following commands:
```
cd /opt/readux
workon ouroboros
python manage.py syncdb
python manage.py migrate
```
