Known Issues
============

AAC#005: Could not get table data: Data too large
-------------------------------------------------

This issue is related to ElasticSearch, which stores
your Analysis Cockpit's events. Elasticsearch calculates
the required RAM for operations before executing them.

The below error might occur on complex searches or aggregations
(e.g. for the graphs in the baselining view). To fix this issue,
you have to increase the RAM of your Analysis Cockpit and reconfigure
ElasticSearch to actually use more RAM.



AAC#005: Fix
~~~~~~~~~~~~

To actually fix the problem, you have to allocate more RAM
to your Analysis Cockpit. You should be able to do this
via your hypervisor.

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
