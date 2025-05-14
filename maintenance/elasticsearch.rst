.. Index:: ElasticSearch Heap Space

Increasing ElasticSearch's Heap Space
-------------------------------------

This chapter is related to ElasticSearch, which stores
your Analysis Cockpit's events. Elasticsearch calculates
the required RAM for operations before executing them.
This information is important to understand why changing
the below value can be helpful in rare cases.

When installing your Analysis Cockpit, your Elasticsearch
instance - which is running on the same server - will be
initialized with a heap space of 50% of the available physical
RAM of the system.

If you recently increased the RAM of your server, you need
to reconfigure the heap used by Elasticsearch. To do this,
you can run the following command:

.. code-block:: console

    nextron@cockpit:~$ sudo dpkg-reconfigure asgard-analysis-cockpit
    Upgrading from ASGARD Analysis Cockpit '4.2.4'
    The server currently has 7940 MB of total RAM.
    Successfully configured heap size of 3970 MB in /etc/elasticsearch/jvm.options.d/10-cockpit.options

You can run the above command whenever you made changes on
your system in regards to the physical RAM.

.. warning::
    The above command will restart the Elasticsearch service if changes
    have been made.
    The above command is also adjusting the MariaDB Buffer Pool Size
    and will also restart the service if changes were detected.

You can also change the heap space manually, though this should only be
done if you urgently need more RAM allocated for Elasticsearch. Edit the
following configuration file on your Analysis Cockpit:

.. code-block:: console

    nextron@cockpit:~$ sudoedit /etc/elasticsearch/jvm.options.d/10-cockpit.options

You should see the values similar to the ones below:

.. code-block:: none

    -Xms3970m
    -Xmx3970m

- Xms represents the initial size of total heap space
- Xmx represents the maximum size of total heap space

The ``3970m`` part of the values indicates the heap space in megabytes (you
can also use gigabyte values, like ``Xms4g``). We advise you to not use more than
75% of your system's memory for ElasticSearch. Using more RAM for Elasticsearch
could lead to an unstable system. Please always use the same values for
both entries.

After you saved your changes, restart the elasticsearch service (this
could take a few seconds!):

.. code-block:: console

    nextron@cockpit:~$ sudo systemctl restart elasticsearch.service

Make sure the service is in ``active (running)`` state after you
restarted it:

.. code-block:: console

    nextron@cockpit:~$ sudo systemctl status elasticsearch.service
