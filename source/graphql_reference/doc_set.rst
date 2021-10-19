.. _graphql_doc_set:

#######
DocSets
#######

A docSet is a collection of documents. DocSets may be used to represent something similar to a Digital Bible Library bundle, a Paratext
project or a Scripture Burrito. The boundaries of collections are defined globally, at processor instantiation, using selectors.

Selectors
---------

Selectors, together, form a composite, primary key for a collection. A new document that has the same set of selectors as an existing
docSet will be added to that docSet. A new document that has a set of selectors that matches no existing docSet will be added to a
newly-created docSet. Each selector may be a string or a number, and the range of values may be constrained in various ways:

- for numbers, minimum and/or maximum value
- for strings, regex match
- for numbers and strings, enum membership

The default selectors are

- lang (a string representing the language code of the docSet)
- abbr (a string abbreviation for the docSet)

The id field of a docSet is composed of its selectors. By default the selectors are are separated by underscores, eg `en_ust`.

Subclasses of Proskomma may specify different selectors, and may concatenate those selectors in a different way.

It is also possible to request all the selectors, or one specific selector.

Tags
----

Tags may be applied to a docSet. It is possible to filter docSets by the presence or absence of tags, and to request that tag information
in various ways.

Documents
---------

A docSet always contains at least one document. Fields exist to return a single document, by bookCode, and to return an array of documents,
filtered by many criteria.

The DocSet Token Enums
----------------------

The DocSet stores enums for all the tokens in all the documents in the docSet. Various fields allow introspection of that information.

See the `full schema for docSets <../_static/schema/docset.doc.html>`_ for more details.
