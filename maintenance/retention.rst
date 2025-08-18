.. Index:: Data Retention
   
Data Retention
--------------

``>Settings\Advanced\Data Retention``

You can configure the Data Retention Policy for your Analysis Cockpit.
This will delete old events from the database, based on the retention
policy rules you have defined. This is useful to keep the database size
manageable and to keep the performance of the Analysis Cockpit at a
reasonable level. Additionally, raw data on disk and sandbox files can
also be deleted with the Data Retention Policy, which can help you to
manage your disk space usage.


.. hint::
   Data Retention takes the import timestamp ``@timestamp`` into account
   to decide whether an event should be deleted or not.

.. figure:: ../images/cockpit_data_retention.png
   :alt: Data Retention

   Data Retention

.. hint::
   The default setting is to keep all events indefinitely. If you want to
   delete old events automatically, you need to configure a Data Retention
   Policy.

There are multiple options within the Data Retention Policy:


- **Event Retention per Case Type / Status** - this setting will allow you to
  set a different retention period rule for each case type and status. This is
  useful if you have different retention requirements for different case types
  and statuses. You can create multiple rules for different case types and case
  statuses. This policy will only apply to cases which have the "default" retention
  period set (see next option).

  .. figure:: ../images/cockpit_data_retention_per_case_type_status.png
      :alt: Data Retention - Case Type / Status

      Data Retention - Case Type / Status
- **Event Retention per Case** - this setting will allow you to set a
  different retention period rule for each case. This is useful if you have
  different retention requirements for different cases. This value takes
  precedence over the **Event Retention per Case Type / Status**. You can
  choose from the following options:

  - **Default** - uses retention period from the General Event Retention setting.
  - **Indefinite** - keeps all events indefinitely.
  - **Custom** - allows you to specify a custom retention period in days.

   .. figure:: ../images/cockpit_data_retention_per_case.png
         :alt: Data Retention - Case
   
         Data Retention - Case

- **General Event Retention** - this setting will delete events older than the
  specified number of days. For example, if you set this to 30 days, all
  events older than 30 days will be deleted from your Analysis Cockpit.
  Raw data on disk will not be deleted. The default setting is to keep all
  events indefinitely. We recommend to only use this setting if necessary,
  as it will delete all events older than the specified number of days.
  The reason for this is that this setting is taking precedence over the
  other settings. Please use this option with caution.

  .. figure:: ../images/cockpit_data_retention_general.png
      :alt: Data Retention - General

      Data Retention - General

- **Others** - this deletes raw data on disk and sandbox files older than
  the specified number of days. Default value: 0 for both.

  .. figure:: ../images/cockpit_data_retention_other.png
      :alt: Data Retention - Others

      Data Retention - Others

- **Settings** – These settings specify when events should be deleted.
  Change the ``Daily Schedule`` to avoid slowing down your system during
  working hours of your analysts.
  The ``Expunge Deleted Events`` value is used for the above **Data
  Retention Policies**, as the actions taken here only soft-delete events,
  meaning the affected events are not deleted immediately, but rather
  marked for deletion. All your events are stored inside specific indices,
  and rewriting those takes (CPU) time. This is why we reindex indices
  only when an index contains a specific percentage of deleted events
  (by default, 20%). If you need more free disk space, lower this threshold.
  If you're experiencing high CPU load, you can raise it.

  .. figure:: ../images/cockpit_data_retention_settings.png
      :alt: Data Retention - Settings

      Data Retention - Settings