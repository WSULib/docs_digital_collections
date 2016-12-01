# troubleshooting

First and foremost, check the logs!  They should be located at: `/var/log/readux/debug.l`.

## 404 for book that should be there

If you receieve a 404 error for a book that should be there, make sure it belongs to a collection object that also has virtual Readux objects created for it.  

For example, `wayne:Sketchesa1881b48389304_Readux_VirtualVolume` was returning the following error:

    RequestFailed: 404 Object not found in low-level storage: wayne:collectionRamsey_Readux_VirtualCollection
    
This confirms that a collection object is missing, as it cannot find `wayne:collectionRamsey_Readux_VirtualCollection` which is the associated collection object for this book.  Try creating virtual Readux objects for that collection object as well.
