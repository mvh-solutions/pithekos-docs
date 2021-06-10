.. _interacting_javascript:

##########################################
Interacting with Proskomma from Javascript
##########################################

The typical, basis workflow is

- import Proskomma
- instantiate Proskomma
- import some data
- query Proskomma (async)

.. code:: javascript

   const fse = require('fs-extra');
   const { Proskomma } = require('proskomma'); // Import Proskomma

   const pk = new Proskomma(); // Instantiate Proskomma

   const content = fse.readFileSync('my_usfm_file.usfm');
   pk.importDocument( // Import Data
      {
         lang: 'en',
         abbr: 'kjv',
      },
      'usfm',
      content,
   );

   const query = '{id}';
   pk.gqlQuery(query) // Query Proskomma
     .then(output => console.log(JSON.stringify(output, null, 2)))
     .catch(err => console.log(`ERROR: Could not run query: '${err}'`));
