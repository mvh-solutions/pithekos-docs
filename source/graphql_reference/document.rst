.. _graphql_document:

#########
Documents
#########

A document typically represents the content relating to a single Bible book.

Identification
--------------

Each document has a generated id that it unique to the Proskomma instance. The headers of USFM documents (or their equivalents) can be accessed, as key-value tuples or by key. Additional fields exist to parse the \id header which typically contains several types of information.

Tags
----

Tags may be applied to a docSet. It is possible to filter docSets by the presence or absence of tags, and to request that tag information
in various ways.

Sequences
---------

Each document contains a main sequence and, optionally, other sequences which are grafted recursively to the main sequence to produce a tree structure. Fields exist to return the main sequence, to return an array of sequences, and to return the number of sequences cheaply.

Fields also exist to return text, table, tree or key-value sequences. (All sequences can be queried as vanilla sequences, but the results may not always be very useful). These fields essentially cast a sequence to a more specific GraphQL type. This casting will fail if, eg, a table is treated as a tree.

Chapter/Verse Lookup
--------------------

Fields exist to return the content for a chapter, a verse, a range of verses within a chapter and a range that spans chapters, specified in various ways. If a versification file has been added to the docSet, it may be used to query chapter/verse via verse mapping.

Content by chapter/verse
------------------------

It is also possible to query for all the chapters in the document, or for a single chapter, optionally chunked by verse.

Convenience Fields
------------------

Various fields exist to provide easy access to the text of the document, without explicitly destructuring sequences and blocks.

See the `full schema for documents <../_static/schema/document.doc.html>`_ for more details.
