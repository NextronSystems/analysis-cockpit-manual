.. Index:: Upgrade

Upgrade from Cockpit v3.8.10 to Cockpit v4.x
============================================

This Chapter contains instructions on how to upgrade
your running Analysis Cockpit version 3.8.10 to the
newest version 4.x

We have two chapters, one for a standalone installation
and one for an installation with an Elasticsearch Cluster.
If you are running a standalone installation, you can
ignore the Cluster chapter and jump straight ahead to
:ref:`upgrade/standalone:standalone upgrade`.

We developed an update program which helps you through
the upgrade by automating as much as possible. You still
have to upgrade your Elasticsearch cluster manually, due
to version limitations with your master node.

.. important:: 
    Your cockpit will be unavailable for an extended period of time
    during the upgrade proccess, usually between 15 and 30 minutes.

.. toctree::
    :caption: Contents

    standalone
    cluster