.. _graphql_text_sequence:

##############
Text Sequences
##############

Text sequences are intended for handling documents containing paragraphs of text. All sequences can be treated
as text sequences.

--------------
Identification
--------------

Each sequence has a generated id that it unique to the Proskomma instance. It also has a type. For the main sequence,
which is always a text sequence, that type is 'main'. For non-text sequences the type is 'table', 'tree' or 'kv'. Other types are used for parts of the decomposed text document, such as headings, footnotes and sidebars.

Tags
----

Tags may be applied to a docSet. It is possible to filter docSets by the presence or absence of tags, and to request that tag information
in various ways.

------
Blocks
------

In a text sequence, a block corresponds to a paragraph. They are stored in an array, and may be filtered by a large number of criteria.

-----------
Item Groups
-----------

Sequence content may also be chunked up according to some combination of scopes. This was initially used to split
up sequences by chapter and verse, but can be used to destructure any semantic, scope-based markup. This is a relatively expensive operation since the whole sequence is traversed, and because the block-oriented indexes are not optimised for this.

-----------------
Token Information
-----------------

Fields exist to return all the unique tokens used in a sequence, and to test whether specific tokens are used.

Convenience Fields
------------------

Various fields exist to provide easy access to the text, tokens or items of the sequence, without explicitly destructuring blocks.

See the `full schema for text sequences <../_static/schema/sequence.doc.html>`_ for more details.
