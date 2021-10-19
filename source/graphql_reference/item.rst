.. _graphql_items:

#####
Items
#####

Items are the basic unit of content in Proskomma. There are three types of items. All items have the same structure:

- a type ('token', 'scope' or 'graft').
- a subType (depending on the type).
- a payload (depending on the type).

------
Tokens
------

Tokens contain text:

- the type is 'token'.
- the subType describes the text ('wordlike', 'linespace' or 'punctuation').
- the payload contains the actual text.

------
Scopes
------

Scopes enclose other content, and are used to represent a wide range of markup:

- the type is 'scope'.
- the subType is 'start' or 'end'.
- the payload contains a string representation of the scope (strings separated by '/').

------
Grafts
------

Grafts connect sequences, and are used to add headings, footnotes and other content:

- the type is 'graft'.
- the subType is the type of graft.
- the payload contains the id of the grafted sequence.

See the `full schema for items <../_static/schema/item.doc.html>`_ for more details.
