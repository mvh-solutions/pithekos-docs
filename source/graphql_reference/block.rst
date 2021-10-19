.. _graphql_block:

######
Blocks
######

In a text sequence, a block corresponds to a paragraph. In other sequences, the same underlying structure is
used to represent other structures. In all cases, each block contains several typed arrays that are used to store
document data in a succinct format:

- **c**: block **c**\ontent (an array of items).
- **bs**: **b**\lock **s**\cope (one start scope). In text sequences this denotes the type of paragraph.
- **bg**: **b**\lock **g**\rafts (zero or more grafts). In text sequences this denotes sequences that are attached to the top of the block, such as headings.
- **is**: **i**\ncluded **s**\copes (zero or more grafts). In text sequences this provides fast lookup of scopes in the paragraph.
- **os**: **o**\pen **s**\copes (zero or more grafts). In text sequences this caches scopes that have been opened but not closed above, such as the current chapter or verse.
- **nt**: **n**\ext **t**\oken (an integer). This caches the token count within the sequence.

---------------------
Low-Level Information
---------------------

Two fields describe each of the above arrays:

- a field ending in `BL` returns the length in bytes of the array. (This is mainly intended for debugging purposes.)
- a field ending in `L` returns the length in items of the array.

There is also a `dump` field that returns the block content in an arcane but compact string format. (This is mainly intended for debugging purposes.)

-----------------
Scope Information
-----------------

The raw scopes in `bs`, `bg`, `is` and `os` may be accessed via a field of that name. The `scopeLabels` field combines
these various sources of information to provide an array that is often easier to work with.

----------------
Document Content
----------------

Content may be accessed as items (ie tokens, scopes and grafts), as tokens (with or without denormalized scope information) and as a single text string.
Item and token output may be filtered in many different ways.

See the `full schema for blocks <../_static/schema/block.doc.html>`_ for more details.
