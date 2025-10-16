Syslog Forwarding
-----------------

``>Settings\System\Rsyslog``

The Analysis Cockpit allows forwarding of all incoming THOR events,
along with all audit logs and all other Cockpit related logs.

.. figure:: ../images/cockpit_rsyslog_forwarding.png
   :alt: Add Rsyslog Forwarding

   Add Rsyslog Forwarding

The following log sources are available for forwarding:

.. list-table::
   :header-rows: 1

   * - Log
     - Origin
     - Content
     - Purpose
   * - Analysis Cockpit Log
     - Analysis Cockpit Backend
     - System and operating events
     - Error diagnosis, system operation
   * - Analysis Cockpit Audit Log 
     - Analysis Cockpit (user interactions)
     - User actions, changes
     - Compliance, traceability
   * - THOR Log
     - THOR scanner on endpoint
     - Scan results, findings
     - Forensic analysis, indicator evaluation

.. note::
   Forwarding THOR logs via syslog might lead to a loss of information,
   since THOR events could exceed syslog length restrictions.

