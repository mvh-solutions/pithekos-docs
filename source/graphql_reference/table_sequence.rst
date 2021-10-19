.. _graphql_table_sequence:

###############
Table Sequences
###############

Table sequences are intended for handling tabular data. They repurpose various sequence features originally
designed for text sequences to offer reasonable performance via a convenient interface.

------------------
Descriptive Fields
------------------

Table sequences, like all sequences, have a unique id. It is also possible to query the number of columns, rows
and cells. Tags work as for text sequences.

---------------
Column Headings
---------------

Column headings are stored as tags. A convenience field returns all the column headings in order.

-----
Cells
-----

A cell is a Proskomma block by another name. It contains an array of content items, as well as arrays of rows and columns occupied by the cell. (The storage format supports multiple row and/or column spans although, at present,
the input filters do not support spans.) The cells endpoint provides cells as a flat array, as if reading the table from left to right and from top to bottom.

----
Rows
----

The rows field chunks up the table cells by rows, and allows filtering by rows, by columns and by content.

See the `full schema for table sequences <../_static/schema/tablesequence.doc.html>`_ for more details.
