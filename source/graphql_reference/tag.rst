.. _graphql_tag:

####
Tags
####

Tags are strings that can be applied to docSets, documents and sequences. They are intended to support application-defined workflows and categories, eg to denote draft or unchecked documents.

The regular expression that validates tag names is

.. code::

   ^[a-z][a-z0-9]*(:.+)?$

ie a lower-case letter, followed by optional lower-case letters and digits, optionally followed by a colon and an arbitrary string.

No-colon tag names are intended to be used for simple labels. Tag names with colons can be used to implement basic key-value logic (although the underlying implementation is not designed for scale.)

Tags are managed using set logic. This means that it is legal to attempt to add the same tag multiple times, or to attempt to remove a tag that does not exist. Tags are stored as an unordered collection, so applications should make no assumptions about the order in which tags will be returned.

In some cases, tags may be specified when documents are created. Tags may also be added or removed via GraphQL mutations.

Tags can be returned for the type to which they are attached, and may also be used to filter collections.
