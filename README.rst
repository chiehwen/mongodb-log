
MongoLog: Centralized logging made simple using MongoDB
=======================================================

:Info: MongoDB python logging handler. Python centralized logging made easy.
:Author: `Andrei Savu`_
:Maintainer: `Jorge Puente Sarrín`_

Setup
-----

Before using this handler for logging you will need to create a capped
collection on the MongoDB server.

You can do this using the following commands in the MongoDB shell::

   > use mongolog
   > db.createCollection('log', {capped:true, size:100000})

... and you are ready. Running ``stats()`` function on ``log`` collection
should show something like this::

   > db.log.stats()
   {
           "ns" : "mongolog.log",
           "count" : 0,
           "size" : 0,
           "storageSize" : 102400,
           "numExtents" : 1,
           "nindexes" : 1,
           "lastExtentSize" : 102400,
           "paddingFactor" : 1,
           "systemFlags" : 1,
           "userFlags" : 0,
           "totalIndexSize" : 8176,
           "indexSizes" : {
                   "_id_" : 8176
           },
           "capped" : true,
           "max" : 2147483647,
           "ok" : 1
   }


Usage
-----

>>> import logging
>>> from mongolog.handlers import MongoHandler
>>>
>>> log = logging.getLogger('demo')
>>> log.setLevel(logging.DEBUG)
>>> log.addHandler(MongoHandler.to(db='mongolog', collection='log'))
>>>
>>> log.debug('Some message')


Check the samples folder for more details.


Why centralized logging?
------------------------

* Easy troubleshouting:
    * Having the answers to why? quickly and accurately.
    * For troubleshouting while the system is down.
    * Removed risk of loss of log information.
* Resource tracking.
* Security.


What is MongoDB?
----------------

"MongoDB is a high-performance, open source, schema-free document-oriented
database."

It can eficiently store arbitrary JSON objects. You can read more at
`MongoDB website`_.


Why MongoDB is great for logging?
---------------------------------

* MongoDB inserts can be done asynchronously.
* Old log data automatically LRU's out thanks to capped collections.
* It's fast enough for the problem.
* Document-oriented / JSON is a great format for log information.

Read more about this subject on the `MongoDB blog`_.


Have fun!


.. _Andrei Savu: https://github.com/andreisavu
.. _Jorge Puente Sarrín: https://github.com/puentesarrin
.. _MongoDB website: http://www.mongodb.org
.. _MongoDB blog: http://blog.mongodb.org
