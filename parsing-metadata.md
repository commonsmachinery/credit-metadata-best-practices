Parsing credit metadata
=======================

The discussion is split into a section on each of the parts of a
credit, preceded by a section on common rules.

Within each section there are subsections for different data sources:

* RDF, which include RDFa, XMP, Open Graph and similar
  subject-predicate-object-based formats
* Native tags, e.g. EXIF or ID3 (to be added)


Common rules
============

RDF
---

### Alternative text values

If there are more than one property when a single text value is
expected, or a single property whose value is an ```rdf:Alt```
container, a single value should be chosen:

1. Use the property or item that has an ```xml:lang``` property
   matching the preferred language of the user.
2. If the preferred language is not known or found, use a property in
   English: ```en```, ```en_US``` or another ```en_XX```.
3. If an English value is not found, use whichever is the first
   property.  This is not possible to determine with some RDF
   libraries, in which case just use the first one returned from the
   graph. 

   
### Promote literal values to URLs

If a literal value looks like a URL, use it as if it was specified as
a ```rdf:resource``` URI rather than as a text value.


### Clickable URLs

Only usefully clickable URLs should be used as links, i.e. a
well-formed URL with the protocol ```http``` or ```https```.

Non-clickable URIs specified with ```rdf:resource``` should not be
used as links, but should be kept as subject URIs when embedding RDFa
in the credit.


### Use URLs for missing text values

If there is no text but only a link for one part of the credit, the
link should be used for the text as well.  This ensures that there is
always text if there is a link too, simplifying rendering the credit.


Work information
================

RDF
---

### Title text

Use the title from the first of these properties that are available:

1. ```dc:title```
2. ```dcterms:title```
3. ```og:title```


### Title link

The title should link to the original work, if possible:

1. Use ```og:url``` if available, since that is defined to be a
   canonical and persistent work URL
2. If the subject URI is a clickable URL, use that.   


Creator attribution
===================

### Attribution text

Use an explicit attribution if possible, falling back on creator
properties:

1. ```cc:attributionName``` (even if the license is not Creative
   Commons, since ccREL could be used for non-CC licenses)
2. ```dc:creator```, joining multiple properties or the items of an
   ```rdf:Seq``` or ```rdf:Bag``` container
3. ```dcterms:creator```, joining as above
4. ```twitter:creator``` (which should be a Twitter ```@handle```)


### Attribution link

1. Use ```cc:attributionURL``` (even if the license is not Creative
   Commons)
2. Use ```twitter:creator``` to create a URL to the profile page at
   ```http://twitter.com/handle```.

#### Flickr specific

On ```www.flickr.com```, use ```flickr_photos:by``` if no other URL is
provided (it usually isn't).


License information
===================

### License link

Use the first URI specified with one of these properties:

1. ```xhv:license```
2. ```dcterms:license```
3. ```cc:license``` (low precedence since ccREL recommends the other two)


### License text

Use a known license short name if possible, otherwise whatever license
or rights information there might be:

1. If the license URI is a known license, translate it into a short
   name.
2. Use a literal value from ```xhv:license```
3. Use a literal value from ```dc:rights```
4. Use the license URI

Some short names are defined here:
http://wiki.creativecommons.org/Property:License_short_name


#### Regexps for parsing license URIs

Creative Common licenses, match groups are: type, version, optional jurisdiction.

    ^https?://creativecommons.org/licenses/([-a-z]+)/([0-9.]+)/(?:([a-z]+)/)?(?:deed\..*)?$

The short name is ```CC type version (jurisdiction)/Unported```,
e.g. ```CC BY 3.0 Unported``` or ```CC BY-NC 3.0 (AU)```.

Public domain marks from Creative Commons, match groups are: type,
version.

    ^https?://creativecommons.org/publicdomain/([a-z]+)/([0-9.]+)/(?:deed\..*)$?

The short name for type ```zero``` is ```CC0 version```.  For type
```mark``` it is "public domain".
(Creative Commons recommend PD, but that is too non-descript to be
understood as a rights term.)

Free Art License, match group is: language or version.

    ^https?://artlibre.org/licence/lal(?:/([-a-z0-9]+))?$



Source works
============

The source works consist of the union of:

* ```dc:source``` with either an ```rdf:resource``` URI or a
  literal value containing a URL
* ```dcterms:source``` with an ```rdf:resource``` URI

The credits for the source works are parsed recursively.  Take care to
handle source loops.
