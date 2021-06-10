.. _interacting_command_line:

##############################################
Interacting with Proskomma using a Node script
##############################################

There are simple scripts for using Proskomma from the command line `in the Proskomma repo <https://github.com/mvahowe/proskomma-js/tree/master/scripts>`_. eg

.. code:: bash

   cd scripts
   node ./do_graph.js ../test/test_data/usfm/hello.usfm example_query.txt

The script imports a USFM or USX file into Proskomma and then runs the query contained in a text file
against it, outputting the result to `stdout`. on un*x systems you can redirect that result to a file:

.. code:: bash

   node ./do_graph.js ../test/test_data/usfm/hello.usfm example_query.txt > ~/my_result.json

If you want to write your own script to do something different, the code for `do_graph.js` would be
a good starting point.