.. Index:: Initial Configuration

Initial Tasks
=============

License Installation
--------------------

Before you can use the cockpit, you must install a license. Navigate to
``Licensing`` section in the ``Settings`` menu, click the ``Upload License``
button, select your license file and click ``Upload``. After verifying
if your license is valid, you will be able to use your Analysis Cockpit.

.. figure:: ../images/cockpit_license.png
   :alt: Licensing 

   Licensing

System Update
-------------

All updates are applied from the Web GUI. Simply navigate to the ``Updates``
section in the ``Settings`` menu, review the release notes and click the update
button. You can also check for new updates by clicking the ``Check for Updates``.

.. figure:: ../images/cockpit_update.png
   :alt: Updating the System

   Updating the System

Elasticsearch Cluster Update
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

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

Set Users and User Rights
-------------------------

The chapter :ref:`basic-concepts/permissions:understanding users, roles, rights and case status`
already describes how to set up a 2-level analyst model for working with cases.
The roles defined in that section are non-administrative roles, meaning
they are only allowed to access cases based on the respective status of
a ticket. The following permissions are related to the Analysis Cockpit as a whole.

Additionally, roles can have the following rights:

* Administrator
* Universal
* View Notifications
* Acknowledge Notifications
* Upload Events
* Delete Events
* Upload File(s) for Sandbox Analysis
* Download File(s) for Sandbox Analysis

Roles can be granted these privileges by choosing them in the ``New Role``
dialogue.

.. figure:: ../images/cockpit_new_role.png
   :alt: New Role

   New Role
