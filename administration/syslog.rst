Syslog Forwarding
-----------------

``>Settings\System\Rsyslog``

The Analysis Cockpit allows forwarding of all incoming THOR events,
along with all audit logs and all other Cockpit related logs.

.. figure:: ../images/cockpit_rsyslog_forwarding.png
   :alt: Add Rsyslog Forwarding

   Add Rsyslog Forwarding

.. note::
   Forwarding THOR logs via syslog might lead to a loss of information,
   since THOR events could exceed syslog length restrictions.