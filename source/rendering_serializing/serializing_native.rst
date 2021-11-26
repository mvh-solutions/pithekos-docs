.. _rendering_native:

######################################
Serializing to Proskomma Native Format
######################################

Proskomma docSets may be serialised as follows:

.. code::

      const serialized = pk.serializeSuccinct('eng_kjv');

All loaded docSets may be serialized using the `proskomma-freeze` module:

.. code::

   const { freeze, thaw } = require('proskomma-freeze');
   const frozen = await freeze(pk);

   // some time later...

   await thaw(pk2, frozen);

There are currently no serialization options below the docSet level because, internally, Proskomma generates content enums for each docSet. This means that two serialized documents cannot be merged into one docSet, because the same content in the two documents is likely to be encoded using different enums.
