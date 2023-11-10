.. Index:: Initial Configuration

Administration
==============

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
