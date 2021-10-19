.. _graphql_kv_sequence:

###################
Key-Value Sequences
###################

Key-value sequences are intended for handling data that is accessed by one or more key, like a card index. They repurpose various sequence features originally
designed for text sequences to offer reasonable performance via a convenient interface.

------------------
Descriptive Fields
------------------

Key-value sequences, like all sequences, have a unique id. It is also possible to query the number of entries. Tags work as for text sequences.

-------
Entries
-------

An entry is a block by another name. Entries can be filtered by primary and secondary keys and by content. The fields of each entry are exposed as item groups.

See the `full schema for key-value sequences <../_static/schema/kvsequence.doc.html>`_ for more details.
