.. Index:: ElasticSearch Heap Space

Increasing ElasticSearch's Heap Space
-------------------------------------

When installing your Analysis Cockpit, your Elasticsearch
instance running on the same server will be initialized with
a heap space of 2GB. This means, it will only use up to
2GB RAM to perform search queries. This might also cause
unused RAM and could lead to issues in rare cases.

This issue is related to ElasticSearch, which stores
your Analysis Cockpit's events. Elasticsearch calculates
the required RAM for operations before executing them.

If you recently increased the RAM of your server, you need
to change the below configuration to make use of it. If you
did not increase your RAM, but initially set up your server
with more RAM, you can also go ahead and change this.

To increase heap space for ElasticSearch, edit the following
configuration file on your Analysis Cockpit:

.. code-block:: console

    nextron@cockpit:~$ sudoedit /etc/elasticsearch/jvm.options.d/10-cockpit.options

You should see the following default values:

.. code-block:: none

    -Xms2g
    -Xmx2g

- Xms represents the initial size of total heap space
- Xmx represents the maximum size of total heap space

The ``2g`` part of the values indicates the heap space in gigabytes.
We advise to use 50% of your system's memory for ElasticSearch. On a
system with a maximum of 8 GB of RAM, this would be ``4g``:

.. code-block:: console

    -Xms4g
    -Xmx4g

After you saved your changes, restart the elasticsearch service (this
could take a few seconds!):

.. code-block:: console

    nextron@cockpit:~$ sudo systemctl restart elasticsearch.service

Make sure the service is in ``active (running)`` state after you
restarted it:

.. code-block:: console

    nextron@cockpit:~$ sudo systemctl status elasticsearch.service
