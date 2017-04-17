# `WSUDOR_Image` - Image objects

## Description

This Content Model (CM) handles "simple" image items with a single primary image, and "complex" image items with multiple images for a single intellectual item.  This Content Model creates JPEG2000 derivatives for zooming and IIIF capabilities.

## Content Type Methods and Attributes

 * `genIIIFManifest` - An important method for this model, this creates a IIIF manifest for the the object.  Iterating through `JP2` datastreams in returned by the `self.imageParts` method, it creates a manifest for all JP2's.
 * `imageParts` - returns dictionary with all image components, including pointer to "main" or representative image
 * `previewImage` - generates `PREVIEW` datastream based on `isRepresentedBy` relationship
  * `regenJP2` - re-derives JP2s for every `foo_JP2` datastream, anticipating an original file datastream at `foo`

## Ingest

### Expected Files

Expects `datastreams` component in `objMeta.json` file with image files.  TIFF is preferred, but other formats such as JPEG, PNG, GIF are accepted.

## Datastreams

### Preserved

Each original image is saved as a datastream based on the identifier in `OBJMETA`.  e.g. a TIFF file, `foobar.tiff` with the identifier `foobar`:

 * `foobar` - original image file

### Derivative

For each image in `OBJMETA`, e.g. `foobar`, the following derivatives are created:

 * `foober_ACCESS` - full-sized, JPEG derivative of original
 * `foobar_THUMBNAIL` - 200 pixel, JPEG derivative of original
 * `foober_PREVIEW` - 1280x960 max, JPEG derivative of original
 * `foobar_JP2` - full-sized, JPEG2000 derivative

Finally, the following are created based on the `isRepresentedBy` relationship:

 * `THUMBNAIL`
 * `PREVIEW`

### Other

Other than image derivatives, no new datastreams are created by this content model.

### Examples Datastream List

    {'BAGIT_META': <eulfedora.xml.ObjectDatastream at 0x7f48e867fe50>,
     'DC': <eulfedora.xml.ObjectDatastream at 0x7f48e8691090>,     
     'IIIF_MANIFEST': <eulfedora.xml.ObjectDatastream at 0x7f48e867fe90>,
     'MODS': <eulfedora.xml.ObjectDatastream at 0x7f48e867ffd0>,
     'OBJMETA': <eulfedora.xml.ObjectDatastream at 0x7f48e867fb90>,
     'POLICY': <eulfedora.xml.ObjectDatastream at 0x7f48e867fc90>,
     'PREMIS': <eulfedora.xml.ObjectDatastream at 0x7f48e867ff50>,
     'PREVIEW': <eulfedora.xml.ObjectDatastream at 0x7f48e867fe10>,
     'RELS-EXT': <eulfedora.xml.ObjectDatastream at 0x7f48e867ff10>,
     'RELS-INT': <eulfedora.xml.ObjectDatastream at 0x7f48e867fed0>,
     'THUMBNAIL': <eulfedora.xml.ObjectDatastream at 0x7f48e867fdd0>,     
     'vmc14515': <eulfedora.xml.ObjectDatastream at 0x7f48e867fcd0>,
     'vmc14515_ACCESS': <eulfedora.xml.ObjectDatastream at 0x7f48e867fd10>,
     'vmc14515_JP2': <eulfedora.xml.ObjectDatastream at 0x7f48e867fd90>,
     'vmc14515_PREVIEW': <eulfedora.xml.ObjectDatastream at 0x7f48e867fd50>,
     'vmc14515_THUMBNAIL': <eulfedora.xml.ObjectDatastream at 0x7f48e867f510>}