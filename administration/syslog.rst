Syslog Forwarding
-----------------

``>Settings\System\Rsyslog``

The Analysis Cockpit allows forwarding of all incoming THOR events,
along with all audit logs and all other Cockpit related logs.

Please note, that forwarding THOR Logs through syslog might lead to a
loss of information as THOR events might exceed syslog length restrictions.

.. figure:: ../images/cockpit_rsyslog_forwarding.png
   :alt: Add Rsyslog Forwarding

   Add Rsyslog Forwarding
