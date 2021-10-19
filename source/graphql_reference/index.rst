.. _graphql_reference:

#################
GraphQL Reference
#################

This section introduces and links to various parts of the `schema documentation <../_static/schema/index.html>`_ that has been auto-generated
using `graphdoc <https://www.npmjs.com/package/@2fd/graphdoc>`_.

++++++++++++++
Overall Design
++++++++++++++

Proskomma's GraphQL schema is quite deeply nested. Where many schema provide a set of top-level accessors that take a large number of arguments,
and which return quasi-tabular results, Proskomma exposes a tree view, with filtering at each level. Convenience fields have been added to
make the simple things simpler, but the full tree representation makes the hard things possible. Conceptually, Proskomma proceeds as if it was
cascading Javascript map and filter operations to destructure a complex object. (In some cases this is exactly what happens under the hood, although,
in many cases, the actual mechanism involves operations on byte arrays.)

In many places, fields are provided to return counts, eg `nDocSets`, `nDocuments`. These are often much cheaper than constructing a nested array just
to count the number of elements.

Several types include :ref:`tags<graphql_tag>`. These can be used to support business logic such as workflow and translation status.

Some types such as :ref:`DocSet<graphql_doc_set>` and :ref:`Document<graphql_document>` appear at a specific level in the GraphQL schema.
Others, such as :ref:`ItemGroup<graphql_item_group>` are used as semi-generic containers in multiple contexts. This makes some results a little
messier, but also reduces the number of types that need to be understood in order to use Proskomma.

By the same logic, the :ref:`item<graphql_items>` type is used for tokens, scopes and grafts, with three fields of the same name in all cases. Initially,
Proskomma used 3 different GraphQL types, which allowed more descriptive field names. However, it was also necessary to cast items whenever they were used,
which resulted in a lot of repetitive boilerplate in queries. The current approach trades a little self-documentation for considerably shorter queries.

++++++++++++++++++
Major Schema Types
++++++++++++++++++

.. toctree::
   :maxdepth: 2

   top_level_fields
   doc_set
   tag
   document
   sequences
   block
   item_group
   indexes
   item
   mutations
