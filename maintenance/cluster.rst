.. index:: Cluster Update

Elasticsearch Cluster Update
============================

If you are running an Elasticsearch Cluster with your Analysis Cockpit,
we recommend to update the cluster members anytime you are installing an
update on your Analysis Cockpit. Not only might an update for the Analysis
Cockpit contain an update for Elasticsearch, but more importantly, system
and security updates for the underlying debian system are also included.

To update your cluster members, run the following commands on each of them:

.. code-block:: console

   nextron@node-1:~$ sudo apt update
   nextron@node-1:~$ sudo apt upgrade

.. note::
   Performing system updates is usually risk free. However, we still recommend that you
   create a backup/snapshot before updating your cluster nodes.