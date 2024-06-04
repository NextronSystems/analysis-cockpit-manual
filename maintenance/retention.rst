.. Index:: Data Retention
   
Data Retention
--------------

You can configure a Data Retention Policy for your Analysis Cockpit.
This will delete old events from the database, based on the retention
policy you have configured. This is useful to keep the database size
manageable and to keep the performance of the Analysis Cockpit at a
reasonable level.

The Data Retention Policy is configured in ``Settings`` > ``Advanced`` >
``Data Retention``.

.. figure:: ../images/cockpit_data-retention.png
   :alt: Data Retention

   Data Retention

.. hint::
   The default setting is to keep all events indefinitely. If you want to
   delete old events, you need to configure a Data Retention Policy.