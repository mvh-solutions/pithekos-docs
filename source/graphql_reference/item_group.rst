.. _graphql_item_group:

###########
Item Groups
###########

Internally, sequence content is represented as an array of blocks. This is sometimes a convenient way to access the data,
eg when rendering documents by paragraph. For other use cases it may be easier to work with data that has been chunked by some other
criterion. Item groups provide a generic type to represent this.

-----------------
Scope Information
-----------------

The `scopeLabels` field returns the scopes that are active within each item group (both the scopes used to delimit the item groups and other
scopes.)

----------------
Document Content
----------------

Content may be accessed as items (ie tokens, scopes and grafts), as tokens, and as a single text string.

See the `full schema for itemGroups <../_static/schema/itemgroup.doc.html>`_ for more details.
