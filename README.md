Credit metadata best practices
==============================

This is a set of best practices for writing and parsing metadata to
handle attribution and license information.

The purpose is to provide an area for discussion and
consensus-building about how to best manage metadata that describe how
to credit the creators of digital works.

The technologies and standards available today provide many different
mechanisms for doing this.  There are both formal and ad hoc schemas
for recording the metadata, and many different ways to make the
information available as embedded or linked metadata.  Tool support
for this metadata varies a lot.

There are two general sets of practices here:

* How to write metadata that is robust and can be understood by many
  applications and services.

* How to parse existing metadata to extract as much information as
  possible, even when it is ad-hoc or patchy


Contribute
----------

All thoughts are welcome!  You can contribute in several ways:

* Comment on the pages for the documents in the repository.  It is
  also possible to comment on individual lines in the documents.
* Write an issue to suggest changes
* Fork this repository and change the documents yourself.  Then submit
  a pull request to get it merged into the master.


Discuss
-------

A mailing list is planned to provide a forum for discussions about
metadata best practices.  This section will be updated when it is
available.


Scope of credit metadata
------------------------

For the purpose of these practices, credit metadata consists of any
combination of this set of four parts:

* Work information
* Creator attribution
* License information
* Source works

The three first parts can have both a textual representation and a URL
that links to more information.

The list of source works is ideally the credit metadata for the source
work, and can thus have source works of its own.  How many ancestor
works to include in different scenarios is a topic of these best
practices.

These best practices does not discuss how to encode license
information itself, beyond a set of standard URIs (e.g. the Creative
Commons license deeds).  How to guide or even force users to comply
with the license of the work when redistributing or remixing works is
not covered here either.


Document structure
------------------

There's one file per main topic, all written with [Github Markdown
syntax](https://help.github.com/articles/github-flavored-markdown).

Example files may later be added in a subdirectory.


Notation
--------

Properties are written with the common namespace prefix,
e.g. ```dc:title```.

Namespace definitions are generally excluded from inline examples (but
not from standalone example files).  The following set of namespaces
are used, including some de facto namespaces that is only identified
by their prefixes:

<table>
 <tr>
  <td>dc:</td>
  <td>Dublin Core elements</td>
  <td>http://purl.org/dc/elements/1.1/</td>
 </tr>
 <tr>
  <td>dcterms:</td>
  <td>Dublin Core terms</td>
  <td>http://purl.org/dc/terms/</td>
 </tr>
 <tr>
  <td>cc:</td>
  <td>ccRel</td>
  <td>http://creativecommons.org/ns#</td>
 </tr>
 <tr>
  <td>og:</td>
  <td>Open Graph</td>
  <td>http://ogp.me/ns#</td>
 </tr>
 <tr>
  <td>twitter:</td>
  <td>Twitter cards</td>
  <td>N/A</td>
 </tr>
 <tr>
  <td>flickr_photos:</td>
  <td>Flickr metadata</td>
  <td>N/A</td>
 </tr>
</table>


Authors
-------

The repository was initiated by Commons Machinery:
http://commonsmachinery.se/


See also
--------

libcredit: A multi-language implementation of these best practices.
https://github.com/commonsmachinery/libcredit
