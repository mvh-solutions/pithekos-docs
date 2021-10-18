.. _interacting:

##########################
Interacting with Proskomma
##########################

The officially-supported interface for almost all Proskomma operations is GraphQL. There are
multiple ways to interact with the GraphQl interface, all of which should produce the same
results.

In several of the following examples, the query is

.. code:: bash

   { id }

This is the shortest possible Proskomma query, and returns the unique id of the Proskomma instance.
(While short, this query is not that useful, except for 'hello world' testing, and for checking that
the Proskomma instance has not been overwritten unintentionally.)

.. toctree::
   :maxdepth: 5

   command_line
   javascript
   curl
   graphql_client
   chaliki
