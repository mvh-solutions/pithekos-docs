.. _interacting_chaliki:

#########################################################
Interacting with Proskomma using the Chaliki Electron App
#########################################################

Chaliki is an electron app built around Proskomma. It comes preloaded with
several complete translations and provides a desktop UI.

.. code:: bash

   git clone git@github.com:Proskomma/chaliki.git
   cd chaliki/data
   # unzip translations.zip into the data/ directory (ie 10 files directly under data/)
   yarn install
   yarn start

The menu, top left, should be fairly self-explanatory. Each page demonstrates the use of
a different query to meet a different use case. You can see the query, and then modify it
yourself, by clicking the `Inspect Query` button at the top of each page.
