Metadata on the clipboard
=========================

The clipboard is used to copy and paste between applications (although
it is called Pasteboard on Mac).  Windows, MacOSX and X Windows (used
by e.g. GNOME on Linux) all share the common feature that multiple
representations of an object can be put on the clipboard when an
object is copied.  This is intended to allow the destination
application to select the richest format it understands, while still
allowing wide compatibility with e.g. common image or plain text types.

This can be used to copy metadata together with an object, even when
any embedded metadata is stripped when copied.  (The Windows clipboard
only supports bitmap images with no embedded metadata, and the common
X framework GTK just copies the pixels even though full PNGs with
metadat could be copied.)

Format
------

Put metadata on the clipboard as RDF/XML.  
  
## Windows and X Windows

Use the MIME type `application/rdf+xml`.

## MacOSX

__TODO__: There is no Uniform Type Identifier defined for RDF/XML yet. A type
something like `public.rdf.xml` should be registered by W3C.


Copying metadata
----------------

The RDF/XML can come from two sources:

* Embedded metadata in the object.  Follow the guidelines in Part 3 of
  the XMP standard to merge EXIF etc into XMP metadata.
  
* RDFa metadata embedded in the webpage containing the object.  Use an
  RDFa parser to extract all triples about the object, as well as
  triples for source works and other references that are also present.

## Subject URI

The subject URI should be retained for the copied object.  Lacking one
(as XMP does), use the URL of the copied object as subject URI.

To discover the URI, add a triple to the RDF that identifies the
object as a source (which it logically becomes when copied) for the
empty URI.  In RDF/XML notation:

    <rdf:Description about="">
       <dc:source rdf:resource="copied-subject-URI">
	</rdf:Description>

And in Turtle notation:

    <> dc:source <copied-subject-URI> .


__TODO__: some RDF libraries seem to have a trouble with the empty URI
`<>`.  This recommendation also means that an XMP packet can't be put
on the clipboard as-is as a sidecar, but first has to be modified.
Because of these problems, it may be a better approach to put the
subject URI as a separate representation on the clipboard with an
appropriate type.


Pasting metadat
---------------

When pasting an object, the destination application should see if it
can get RDF/XML from the clipboard in addition to the object itself.

If it can, the metadata of the object can be found by querying the RDF
graph for

    <> dc:source ?copiedSubjectURI


__TODO__: As noted above, it might be better to get the subject URI
from the clipboard instead.
