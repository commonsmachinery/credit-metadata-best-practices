Finding metadata
================

For objects published on webpages
---------------------------------

Objects published on a webpage (e.g. a Flickr image) may have RDFa
metadata embedded into the webpage.  The subject URI can be
determined by trying these in order and using the first one that has
RDFa metadata:

1. If the element representing the object (e.g. an `<img>` or a
   `<div>`) has an `id="objectId"` attribute, look for metadata for the relative
   subject `#objectId`, i.e. the absolute subject
   `http://pageURL#objectId`.

2. If the element has a `src="objectURL"` attribute, look for metadata
   with that URL as the subject URI.


Embedded metadata
-----------------

Follow the guidelines in Part 3 of the XMP specification to merge EXIF
and other native metadata into any XMP metadata, then process the
resulting XMP.


