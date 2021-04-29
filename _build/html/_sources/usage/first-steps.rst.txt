First Steps
===========

Change User Password for the Console Logon
------------------------------------------

The User password can be changed by opening a command line on the
Analysis Cockpit.

The default user is **nextron**, the default password is **nextron**.

Simply type the following command to set a new password for the nextron
user.

.. code:: bash
   
   passwd

Make sure to write that new password down or better save it into a
password safe.

Change User Password for the Web Frontend
-----------------------------------------

Log into the web-based frontend with user **admin** and password
**admin** and change the initial password.

The Analysis Cockpit Web interface password can be changed by opening
the Analysis Cockpit frontend with your browser and clicking on ``User Settings``.

``User Settings`` > ``Password``

.. figure:: ../images/image24.png
   :target: ../_images/image24.png
   :alt: User Settings 

   User Settings

Migrate from Cockpit v2.8.x to Cockpit v3.x
-------------------------------------------

In order to migrate an old Cockpit Version 2.x to a newly installed
Cockpit 3.x proceed as follows:

On Analysis Cockpit Version 2.x
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Make sure you have installed the latest updates.

On the command line type:

.. code:: bash
   
   sudo ac2toac3 export -o export.ac2

This will create the output file export.ac2 that will contain the entire
Cockpit V2.x configuration including, users, rights, cases and case
content but it WILL NOT contain any logs.

Copy the file export.ac2 to your newly installed Cockpit V3.x.

On the command line type:

.. code:: bash
   
   sudo ac2toac3 import -f export.ac2

This will import the entire Cockpit 2.x configuration into your Cockpit
V3.x.

Caution: This will overwrite your existing configuration.

Now your cockpit v3.x contains all v2.x configuration including all
users, roles and cases.

As the cases also contain all grouping criteria, group IDs and rules,
incoming logs will from now on be moved to the respective cases – just
like your cockpit V2.x would have done.

If you also require logs to be migrated from Cockpit v2.x to your new
Cockpit v3.x proceed as follows:

In ASGARD Management Center Version 2:

* Link your new Cockpit v3 to your ASGARD Management Center(s)

In Cockpit v3 navigate to ``Scans``.

* Select the Scans you want to import into Cockpit
* Click ``Request Events``

.. figure:: ../images/image25.png
   :target: ../_images/image25.png
   :alt: Request Events from ASGARD Management Center 2.x

   Request Events from ASGARD Management Center 2.x

Events will show up in Analysis Cockpit shortly. Of course, this also
works for “Group Scans”.

ASGARD Management Center Version 1:

* On ASGARD navigate to /var/lib/bsk/asgard/log
* Copy and upload scan.log into Analysis Cockpit via web-based GUI (see
   below)

.. note::
   Scan.log rotates every month. Be sure to import older logs as needed.

To import old log data, see chapter 7.9 “Log File Import”.
