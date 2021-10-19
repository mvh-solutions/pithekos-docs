.. _graphql_tree_sequence:

##############
Tree Sequences
##############

Tree sequences are intended for handling tree data. (They were initially implemented to handle syntax trees.) They repurpose various sequence features originally
designed for text sequences to offer reasonable performance via a convenient interface.

------------------
Descriptive Fields
------------------

Tree sequences, like all sequences, have a unique id. It is also possible to query the number of nodes. Tags work as for text sequences.

-----
Nodes
-----

A node is a block by another name. Node fields provide easy access to the node id, its parent and children ids,
its keys and the items it contains.

---------------------
Tribos Query Language
---------------------

Tribos is a DSL for querying tree sequences. Tribos queries look a bit like XPath, and are submitted as a single string. The result is also a string containing serialized JSON. Tribos is in active development, and the most
current - if terse - documentation is available via a GraphQL field.

See the `full schema for tree sequences <../_static/schema/treesequence.doc.html>`_ for more details.
