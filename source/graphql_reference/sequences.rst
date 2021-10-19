.. _graphql_sequences:

#########
Sequences
#########

Each document contains one or more sequences. A sequence is a contiguous flow of content. Each document has exactly one main
text sequence, to which other sequences may be grafted. For example, titles and footnotes are stored as separate sequences that
are grafted to another sequence.

By default, all sequences are treated as text sequences. (This always 'works' although the results may not be very useful in some cases.)

.. toctree::
   :maxdepth: 5

   text_sequence
   table_sequence
   tree_sequence
   kv_sequence
