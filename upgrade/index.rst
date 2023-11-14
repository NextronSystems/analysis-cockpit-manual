.. Index:: Upgrade

Upgrade from Cockpit v3.8.10 to Cockpit v4.x
============================================

This Chapter contains instructions on how to upgrade
your running Analysis Cockpit version 3.8.10 to the
newest version 4.

There are two chapters, one for a **standalone installation**
and one for an installation with an **Elasticsearch Cluster**.
Depending on your environment, please follow **only one** section:

- Standalone Installation - :ref:`upgrade/standalone:standalone upgrade`
- Cluster Installation  - :ref:`upgrade/cluster:cluster upgrade`

We developed an update program which helps you through
the upgrade by automating as much as possible. You still
have to upgrade your Elasticsearch cluster manually, due
to version limitations with your master node.

.. important:: 
    Your cockpit will be unavailable for an extended period of time
    during the upgrade proccess, usually between 30 and 60 minutes.
    Please make sure that no user is working with the Analysis Cockpit
    during the upgrade process.

.. toctree::
    :caption: Contents

    cluster
    standalone