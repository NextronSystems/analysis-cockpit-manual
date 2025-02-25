.. Index:: 4.2 Changes

Analysis Cockpit v4.2
---------------------

Analysis Cockpit 4.2.2
######################

Release Date: Tue, 25 Feb 2025 09:59:00 +0100

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Bugfix
      - Fixed an issue in the sandbox retention settings where 'Keep everything' was interpreted as 'Delete everything'

Analysis Cockpit 4.2.1
######################

Release Date: Thu, 13 Feb 2025 10:56:00 +0100

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Bugfix
      - Removed 'Legitimate Anomaly' and 'False Positive' case types from Security Center synchronization configuration, as they are not supported by Security Center
    * - Bugfix
      - Fixed an issue where the Analysis Cockpit treated ElasticSearch responses as errors, even when the operation had actually succeeded, which, among other things, led to missing default cases in some freshly installed Analysis Cockpits
    * - Bugfix
      - Fixed an issue where event counts in the database were displayed as zero when at least one case contained more than 2 billion events
    * - Bugfix
      - Fixed an issue where case statuses were not sorted correctly on the overview page
    * - Bugfix
      - Fixed an issue where cases using both regex and condition would temporarily lose their conditions, and improved the condition tester in case details to match the behavior of the condition tester in the baselining section, resolving inconsistencies. Also added a regex tester in case details, similar to the one in the baselining section

Analysis Cockpit 4.2.0
######################

Release Date: Mon,  2 Dec 2024 11:49:00 +0100

----

* Features

  - Introduced a new notification type to alert users on events without case assignments
  - Added a new notification type that triggers when a new asset is affected by a case
  - Added an option to run event retention based on the ``time`` field instead of ``@timestamp``
  - Enhanced the Overview page with connectivity details for Management Center and Security Center
  - Enabled Management Center to connect with Security Center via a reverse proxy, eliminating the need for direct access
  - Cases can now be assigned directly to specific users, supporting user-specific workflows
  - Added LDAP users to the User Management table for improved user administration

----

* Improvements

  - Converted 'Started' and 'Duration' graphs in the scan table to more intuitive line charts
  - Established a real-time sync API between Management Center and Analysis Cockpit for Thunderstorm events
  - Added "Expunge Deleted Events" setting for complete event deletion in retention settings
  - Made the 'Assets' column in the Management Centers table sortable
  - Implemented a fallback in event table filters to truncate search terms over 1000 characters
  - Improved ``rsyslog`` configuration by switching to ``imptcp`` from ``imtcp``
  - Cases can now be sorted correctly by their status in the case table

----

* UX

  - Automatically clear empty condition fields in the 'Create Case' condition builder
  - Added a 'Back' button in the 'Create Scheduled Report' dialog for easier navigation
  - Added a loading indicator when testing proxy connections
  - Enabled ChatGPT prompt submission with the 'Enter' key
  - Expanded THOR event right-click context menu to additional views
  - Adjusted retention settings page to use full-width layout
  - Added THOR's 'Archive' field as an option for file collection from assets
  - Removed the option to delete oneself from the User table
  - Restricted creation of THOR dashboards for Aurora and vice versa
  - Enhanced handling of ElasticSearch error messages for better troubleshooting
  - Made the right sidebar resizable for flexible layout adjustment

----

* Bugfixes

  - Resolved an issue with event assignments to already merged cases; this update will automatically correct any prior mis-assignments
  - Restored missing example events for certain findings in the Security Center
  - Added missing API key in curl examples within API documentation
  - Addressed timezone issues in MariaDB by setting the timezone in configuration
  - Correctly display negation filters in the 'Save Dashboard' dialog
  - Validated 'Run at' field in retention settings before submission
  - Increased Elasticsearch's ``max_nested_depth`` to 100 to prevent query failures
  - Corrected a typo in API documentation for ``GET /events/search`` endpoint
  - Fixed processing of Bifrost file names
  - Ensured UUIDs are generated for new suggested cases
  - Added a ``.gitignore`` file to the config directory to avoid certain files from being backed up
  - Fixed updates in the 'Actual events' column
  - Addressed empty entries in case change logs when adding comments without other changes

----

* Chore

  - Corrected a typo in the licensing section