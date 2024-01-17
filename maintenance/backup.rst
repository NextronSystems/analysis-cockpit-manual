.. Index:: Backup & Restore

Configuration Backup & Restore
------------------------------

The Analysis Cockpit comes with a backup and restore function
for its configuration. The Configuration Backup contains the
following data:

- Cases, Grouping Criteria, Recommendations, Case Changes, Case Comments
- Users, Roles, LDAP Roles, Role Rights
- User Configurations

To perform a backup, you can simply go to ``Settings`` > ``Backup``
and click ``Create Configuration Backup``. To restore from an old backup,
it is important to understand the implications of the restore. From the
Backup page of the Analysis Cockpit:

    The restore procedure will install a previously generated configuration
    backup on this Analysis Cockpit. All data on this Analysis Cockpit will
    be deleted before. This can only be done on newly installed Analysis Cockpits
    and not on an Analysis Cockpit that is already in use. Do not use the restore
    to rollback to an earlier point in time, this will cause inconsistent data.

    .. warning::
        Installing a configuration backup of an earlier Analysis Cockpit Release
        Version is not supported and may fail. The currently installed version is
        3.5.6. The version of the configuration backup can be found in the file name.
        The backup's file name has the following pattern: ``analysis_cockpit_%VERSION%_backup_%DATE%.sql.gz``

.. figure:: ../images/cockpit_backup-and-restore.png
   :alt: Configuration Backup & Restore

   Configuration Backup & Restore
