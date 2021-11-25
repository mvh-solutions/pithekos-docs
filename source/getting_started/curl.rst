.. _interacting_curl:

#####################################
Interacting with Proskomma using Curl
#####################################

To use an HTTP client with Proskomma, you first need an HTTP server. (Unlike most systems offering
a GraphQL interface, Proskomma does not itself wait on a socket.) So the first step is to install
and fire up proskomma-node-express:

.. code:: bash

   git clone git@github.com:mvahowe/proskomma-node-express.git
   cd proskomma-node-express
   npm install
   npm run dev

Node Express should now be listening on port 2468 of localhost. You can test this by pointing your
web browser at

.. code:: bash

  http://localhost:2468

Now open a second terminal window (since the server needs to continue running) and type

.. code:: bash

   curl -X POST http://localhost:2468/gql -d 'query={ id }'
