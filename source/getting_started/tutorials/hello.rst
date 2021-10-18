.. _tutorials_hello:

########################
Hello Proskomma Tutorial
########################

This tutorial shows how to get up and running with Proskomma, in node. We will import and query a short sample document. All the code and data for the tutorial is presented inline. You will need to copy and paste the code into a file called
:code:`tutorial.js`, and the USFM into a file called :code:`psa.usfm`. You will also need to be able to type commands via
a terminal emulator such as Bash.

++++++++++++++++++++++++++++++++++
Installing and Importing Proskomma
++++++++++++++++++++++++++++++++++

Create a directory for this project and move into it:

.. code:: bash

   mkdir my_proskomma_tutorial
   cd my_proskomma_tutorial

Install proskomma:

.. code:: bash

   npm install proskomma

(If this command throws an error, check that you have already installed node and npm on your system, and
that you have access to the Internet.)

Create a file called :code:`tutorial.js` in your project directory, open it with the text editor of your choice
(which is probably Emacs) and enter the following code:

.. code:: javascript

    const { Proskomma } = require('proskomma');

Save that file and, from your terminal emulator, type

.. code:: javascript

   node tutorial.js

This command should run without throwing an error and without producing any output. You could add

.. code:: javascript

    console.log(Proskomma);

to convince yourself that the module has been loaded.

++++++++++++++++++++++++++
Interacting with Proskomma
++++++++++++++++++++++++++

The next step is to make an instance of Proskomma:

.. code:: javascript

    const pk = new Proskomma();

Add this line to your code file, so that the whole file looks like this:

.. code:: javascript

    const { Proskomma } = require('proskomma');
    const pk = new Proskomma();

You could peek at Proskomma internals by adding

.. code:: javascript

    console.log(pk);

You could get, say, the unique id of this Proskomma instance:

.. code:: javascript

    console.log(pk.processorId);

However, most Proskomma internals are hard to access in this way, because they are stored in a succinct,
binary format. In almost all cases it is better to interact with Proskomma via GraphQL. The GraphQL equivalent
to the previous example is

.. code::

   { id }

This looks a lot like a javascript destructuring assignment, such as the first line of our code file. It can be read as
`return the field called 'id' at the top level of the GraphQL structure`. Most GraphQL queries are longer (and more useful)
than this.

GraphQL queries are asynchronous, which means that they return a promise. You can see this by changing your script to

.. code:: javascript

    const { Proskomma } = require('proskomma');
    const pk = new Proskomma();
    console.log(pk.gqlQuery('{ id }'));

For the sake of this tutorial, we'll create a simple, asynchronous helper function that waits for the promise to be resolved
and then prints the result:

.. code:: javascript

    const { Proskomma } = require('proskomma');
    const pk = new Proskomma();

    const queryPk = async function (pk, query) {
        const result = await pk.gqlQuery(query);
        console.log(JSON.stringify(result, null, 2));
    }

    queryPk(pk, '{ id }');

You should see the following output:

.. code::

   {
     "data": {
       "id": "NGIxMTM0N2It"
     }
   }

The GraphQL result is an object that contains at least one of

- `data`: the requested information, as nested objects and arrays
- `errors`: any issues with the query as a whole, or with specific fields within the query

The nested structure of `data` corresponds to the structure of the query. If we were to change
the query to

.. code:: javascript

    queryPk(pk, '{ idx }'); // No such field!

we would see the following output:

.. code::

   {
     "errors": [
       {
         "message": "Cannot query field \"idx\" on type \"Query\". Did you mean \"id\"?",
         "locations": [
           {
             "line": 1,
             "column": 3
           }
         ]
       }
     ]
   }

Our Proskomma instance does not yet contain any data. If we ask for an array of documents

.. code:: javascript

    queryPk(pk, '{ documents { id } }');

the array will be empty:

.. code::

   {
     "data": {
       "documents": []
     }
   }

+++++++++++++++++++
Importing Scripture
+++++++++++++++++++

Proskomma imports content from Javascript strings. In this case we will read that string from a file,
but we could also download content from an API, or read it from a Javascript module, or even include
the content inline in the script. Create a file called :code:`psa.usfm`, using your text editor, paste
the following text into it, and save it.

.. code::

   \id PSA unfoldingWord® Simplified Text (truncated)
   \ide UTF-8
   \toc1 The Book of Psalms
   \mt1 Psalms
   \c 150
   \q1
   \v 1 Praise Yahweh!
   \q1 Praise God in his temple!
   \q2 Praise him who is in his fortress in heaven!
   \q1
   \v 2 Praise him for the mighty deeds that he has performed;
   \q2 praise him because he is very great!

   \q1
   \v 3 Praise him by blowing trumpets loudly;
   \q2 praise him by playing harps and small stringed instruments!
   \q1
   \v 4 Praise him by beating drums and by dancing.
   \q2 Praise him by playing stringed instruments and by playing flutes!
   \q1
   \v 5 Praise him by clashing cymbals;
   \q2 praise him by clashing very loud cymbals!

   \q1
   \v 6 I want all living creatures to praise Yahweh!
   \q1 Praise Yahweh!

This text represents part of the Psalms, from a translation by Unfolding Word, in a format called
USFM. USFM is widely used by Bible translators, and is one of the formats that Proskomma can import.

To read this text file, we will use `fs-extra` and `path`, the popular Node modules for interacting with filesystems:

.. code:: bash

   npm install path
   npm install fs-extra

Content may be imported via methods, or via GraphQL mutations. We're going to take the GraphQL mutation route.
Modify your script as follows:

.. code:: javascript

   const path = require('path');
   const fse = require('fs-extra');
   const { Proskomma } = require('proskomma');
   const pk = new Proskomma();
   let content = fse.readFileSync(path.resolve(__dirname, './psa.usfm').toString();

   const queryPk = async function (pk, query) {
       const result = await pk.gqlQuery(query);
       console.log(JSON.stringify(result, null, 2));
    }

    const mutation = `mutation { addDocument(` +
        `selectors: [{key: "lang", value: "eng"}, {key: "abbr", value: "ust"}], ` +
        `contentType: "usfm", ` +
        `content: """${content}""") }`;

    queryPk(pk, mutation);

A mutation is a GraphQL operation that modifies the internal state of the model behind the graph (ie Proskomma in this case). The mutation type is called `addDocument`. It takes three arguments:

- `selectors`: an array of key-value pairs that, together, describe the collection (docSet) to which the document will be added
- `contentType`: the format of the input - USFM in this case
- `content`: the string containing the content, which is triple-quoted so that quotes within the USFM do not mess up the GraphQL.

The output is:

.. code::

   {
     "data": {
       "addDocument": true
     }
   }

which tells us that the `addDocument` mutation succeeded. Now let's add a query to explore the document we just imported:

.. code:: javascript

   const path = require('path');
   const fse = require('fs-extra');
   const { Proskomma } = require('proskomma');
   const pk = new Proskomma();
   let content = fse.readFileSync(path.resolve(__dirname, './psa.usfm').toString();

   const queryPk = async function (pk, query) {
       const result = await pk.gqlQuery(query);
       console.log(JSON.stringify(result, null, 2));
    }

    const mutation = `mutation { addDocument(` +
        `selectors: [{key: "lang", value: "eng"}, {key: "abbr", value: "ust"}], ` +
        `contentType: "usfm", ` +
        `content: """${content}""") }`;

    queryPk(pk, mutation);

    const dataQuery = `{ documents { id } }`;
    queryPk(pk, dataQuery);

This is the query we tried above when Proskomma was empty. (For the rest of the tutorial we will change the value of `dataQuery` to try different queries.) The output is now

.. code::

   {
     "data": {
       "addDocument": true
     }
   }
   {
     "data": {
       "documents": [
         {
           "id": "ODA4ZDdhNjgt"
         }
       ]
     }
   }

(From now on we will not show the result of the mutation.) The `documents` array now contains one object
which in turn contains the requested id.

+++++++++++++++
Querying Basics
+++++++++++++++

Proskomma has many, many fields, and - thanks to the power of GraphQL - those fields may be combined in many, many ways. However, all GraphQL queries are structured in a similar way. (This consistency, which GraphQL imposes, is one of the advantages of a GraphQL interface.)

We have already seen that the result is a nested object corresponding to the query. To request additional fields, you simply list them at the appropriate level in the query. So

.. code::

   {
      id
      packageVersion
      documents {
         id
         headers {
            key
            value
         }
      }
   }

   ==>

   {
      "id": "ZDAzZGQyZGYt",
      "packageVersion": "0.4.78",
      "documents": [
           {
              "id": "M2NlYmJjNDAt",
              "headers": [
                 {
                    "key": "id",
                    "value": "PSA unfoldingWord® Simplified Text (truncated)"
                 },
                 {
                    "key": "bookCode",
                    "value": "PSA"
                 },
                 {
                    "key": "ide",
                    "value": "UTF-8"
                 },
                 {
                    "key": "toc",
                    "value": "The Book of Psalms"
                 }
              ]
           }
      ]
  }

`id` and `packageVersion` are at the top level of the query and thus refer to the Proskomma processor itself. `id` within `documents`
refers to each document in the processor. `headers` describes metadata for each document, and each element of that array describes `key` and `value` for one header.

GraphQL queries tend to become quite deeply nested. This has the advantage of making the structure very clear. However, it often makes sense
to post-process the raw result to make the data easier to use from Javascript. For example, the `headers` object could be represented as a simple object.

Fields may take arguments, typically to filter the results. For example, rather than returning all the headers as an array, we could ask
for one specific header:

.. code::

   {
      documents {
         header(id:"toc")
      }
   }

   ==>

   {
      "documents": [
         {
           "header": "The Book of Psalms"
         }
      ]
   }

The `header` field requires one argument, `id`. It returns a single string, which means that, unlike `headers`, there is no need to destructure its value. This is quite convenient... until you want multiple values from the same field:

.. code::

   {
      documents {
         header(id:"toc")
         header(id:"ide")
      }
   }

   ==>

   {
     "errors": [
       {
         "message": "Fields \"header\" conflict because they have differing arguments. Use different aliases on the fields to fetch both if this was intentional.",
         "locations": [
           {
             "line": 1,
             "column": 15
           },
           {
             "line": 1,
             "column": 32
           }
         ]
       }
     ]
   }

The error message in this case is quite informative. The solution is to explicitly assign labels (aliases) to the value of each use of the field:

.. code:

.. code::

   {
      documents {
         title: header(id:"toc")
         encoding: header(id:"ide")
      }
   }

   ==>

   {
      "documents": [
         {
            "title": "The Book of Psalms",
            "encoding": "UTF-8"
         }
      ]
   }

In addition to solving the name conflict, the use of aliases here makes the result more self-documenting.

++++++++++++++++++
Querying Scripture
++++++++++++++++++

Proskomma stores Scripture as a deep hierarchy, which allows for quite sophisticated queries. There are also convenience
fields to get basic information easily.

To get all the text for a document:

.. code::

   {
      documents {
         mainText
      }
   }

To get all the text as an array of strings (one per paragraph):

.. code::

   {
      documents {
         mainBlocksText
      }
   }

To get the book code of the document and the type of each paragraph too:

.. code::

   {
      documents {
        bookCode: header(id:"bookCode")
         mainBlocks {
            bs { payload } text
         }
      }
   }

To get one verse:

.. code::

   {
      documents {
         cv(chapterVerses:"150:3") {
            text
         }
      }
   }

To get several verses:

.. code::

   {
      documents {
         cv(chapterVerses:"150:3-4") {
            text
         }
      }
   }

To get a chapter, split by verse, with the verseRange for each verse:

.. code::

   {
      documents {
         cvIndex(chapter:150) {
            verses {
               verse {
                  verseRange
                  text
               }
            }
         }
      }
   }

See elsewhere in the documentation for more possibilities.
