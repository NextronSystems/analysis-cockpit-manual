.. Index:: Migration

Migrate from Cockpit v3.8.10 to Cockpit v4.x
============================================

This Chapter contains instructions on how to migrate
your running Analysis Cockpit version 3.8.10 to the
newest version 4.x

We have two chapters, one for a standalone installation
and one for an installation with a Elasticsearch Cluster.
If you are running a standalone installation, you can
skip the Cluster chapter and jump straight ahead to
:ref:`migrate/standalone:standalone migration`.

We developed an update program which helps you through
the upgrade by automating as much as possible. Unfortunately,
you still have to upgrade your Elasticsearch cluster manually.

.. toctree::
    :caption: Contents

    cluster
    standalone