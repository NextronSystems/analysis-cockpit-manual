.. Index:: Log File Import

Log File Import
---------------

Basic Concepts
^^^^^^^^^^^^^^

All imported THOR logs can be found in the ``Events`` section. All
Alerts and Warnings that are not matching a particular case will be visible
in the ``Baselining`` section. Notices and informational events will NOT
show up in the Baselining Section as they match the predefined default
cases for these events. We strongly advise to **not** delete those
cases, as those event levels contribute to the majority of THOR events.

All logs are tagged with a specific scan id – regardless of how the log
was integrated. This enables filtering down to all logs contained in a
specific scan.

If an ASGARD Management Center is connected and the events were generated as
part of a group scan, those events are also tagged with this particular group
scan id. This allows for filtering down to all logs of particular group
scan.

Assets are identified through the asset ID that was issued by the ASGARD
Management Center during the setup of the ASGARD Agent. If this ID is
not available to the Analysis Cockpit (e.g. log has been uploaded
manually or sent through syslog) the hostname (NOT the FQDN) will be
used instead.

Direct Integration with ASGARD Management Center
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``>Scans\Scans``

If the Analysis Cockpit is linked to one or more ASGARD Management
Center, all THOR logs get integrated automatically and can be found
in your Baselining and Events section. The same is true for Aurora
events.

To see how to connect an ASGARD Management Center with your Analysis
Cockpit, follow the instructions in the chapter
:ref:`administration/amc:link asgard management center`.

Syslog Input
^^^^^^^^^^^^

Another way to import log data is by using SYSLOG.

The Analysis Cockpit listens on port 514/udp and 514/tcp for incoming
log data. Incoming syslog messages get assigned to a single scan using
the "ScanID" value, which is unique per default.

File Import Through Web-Based GUI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``>Scans\Scans``

THOR logs can be uploaded through the web-based interface. You can upload
a particular log file (**.txt**) or multiple log files compressed into
a gzip archive (**.gz**). Clicking the ``Upload Scans`` button will open
the upload dialog and show you the available file formats.

.. note::
   You can upload one or more THOR scans in one or more text files.
   The Analysis Cockpit will automatically generate scans in the database,
   based on the scanned assets and the SCAN_IDs in the events.

.. figure:: ../images/cockpit_upload_scan_logs.png
   :alt: Upload logs using the web-based interface 

   Upload logs using the web-based interface

After a successful upload, the scans should appear in **Scans** table.

.. important::
   If you can not see events in the ``Events`` or ``Baselining`` view,
   please make sure that you've selected the correct time frame as filter.
   Often times manually uploaded scans happened days or weeks before the
   upload. The log data gets indexed with the timestamp of their creation
   and not the import time, and can therefore be outside of your defined
   time range of your table.

After the upload, you're able to link the recently uploaded scans with
an existing or new group scan. You can also unlink scans from a group scan.

.. figure:: ../images/cockpit_link_unlink_scans.png
   :alt: Link/Unlink scans with an existing or new group scan

   Link/Unlink scans with an existing or new group scan
