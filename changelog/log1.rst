.. Index:: 4.1 Changes

Analysis Cockpit v4.1
---------------------

Analysis Cockpit 4.1.9
######################

Release Date: Thu,  4 Jul 2024 15:17:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Breaking Changes
      - If you are upgrading from a version older than 4.1.5, please read the release notes of 4.1.5 carefully.
    * - Bugfixes
      - Fixed grouping criteria issues when applying suggested cases

Analysis Cockpit 4.1.8
######################

Release Date: Tue,  2 Jul 2024 11:02:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Security
      - OS Security Fix
    * - Bugfix
      - Fixed missing grouping criteria when applying suggested cases
    * - Bugfix
      - Fixed too many events in LogWatcher's 'All Events' section
    * - Bugfix
      - Fixed an escape issue in conditions with double backslashes
    * - Bugfix
      - Fixed inaccurate estimated remaining time for reindexing
    * - Bugfix
      - Fixed an off-by-one date error in the incoming events graph
    * - Bugfix
      - Fixed non-working table search for some columns in the 'Manage Dashboards' section
    * - Bugfix
      - Fixed 'csrf error' popup when using the 'Session expired' login dialog
    * - Bugfix
      - Fixed an startup error when using 'Matched Signatures' with wide date range

Analysis Cockpit 4.1.5
######################

Release Date: Wed, 19 Jun 2024 09:41:00 +0200

----

* **Breaking Changes**
  
  - Changed the way events are indexed in Elasticsearch. The new index structure significantly improves performance but increases disk space usage by 30%-40%. After the upgrade, all events will be reindexed, which can take several hours depending on the number of events in your system. The system remains usable during this process, but we recommend performing the upgrade during off-peak hours. If the Analysis Cockpit reaches its disk space limit during reindexing, the process will pause until more disk space is available. The Analysis Cockpit will guide you on how to free up or increase disk space, and the reindexing process will automatically resume once enough disk space is available. Contact our support for assistance.
  - Conditions in cases are now case-insensitive. Existing conditions will be converted automatically. We believe this change will not affect case quality.

----

* **Highlights**

  - Added the ability to create custom Event Dashboards in the Baselining and All Events sections.
  - Added event insights by ChatGPT, enabling automatic analysis of THOR events with assessments and recommendations. Also, added the ability to ask ChatGPT to explain THOR events or terms within an event.
  - Introduced a new 'Matched Signatures' section showing all matched signatures chronologically.
  - Added the ability to collect files from an asset via the Management Center.
  - Implemented a Data Retention Policy for retaining events for a specified period and automatically deleting them afterwards.
  - Added graphs and statistics to the Overview Dashboard.

----

* **Features**

  - Added the ability to assign priorities to cases.
  - Introduced a new field 'compromised' to track compromised assets.
  - Added a detailed diagnostics status page showing system health and connectivity.
  - Added a Diagnostics Pack that can be downloaded and sent to Nextron Systems for support.
  - Included a base64 and hex decoder in the context menu of THOR events.
  - Added a new field 'under investigation' to track ongoing investigations in cases.
  - Added the ability to schedule reports, including the option to send them via email.
  - Added the ability to enforce 2FA or password resets for users.

----

* **Improvements**

  - New index structure for events in Elasticsearch, significantly improving performance.
  - Re-added the 'Incoming events' graph in Baselining and All Events sections.
  - Improved the query for compromise assessment mode.
  - Added the ability to edit case details and conditions in the 'Add to Case' dialog.
  - Added the ability to bulk merge cases, including merging cases with different assignment types.
  - Forwarded OS information to the Security Center now uses data from the Management Center.
  - Display which users have set up 2FA in the user management section.
  - Added a stop button for 'Auto Baselining'.
  - Enhanced bulk actions in the case table, allowing editing of tags, priorities, and more.
  - Automatically adjust heap size for Elasticsearch and MariaDB based on system memory.
  - Re-added the 'Last 30 days' filter in the event table of an asset or case.
  - Added a 'Delete' button in the table of connected Management Centers.
  - Enhanced security by preventing API endpoint leaks and using a more secure password hash algorithm.
  - Refactored the case comments section.
  - Display additional asset information like file systems and MAC addresses.
  - Improved support for THOR 10.7, especially for case assignments using Auto Case IDs.

----

* **UX**

  - Improved the error message when Elasticsearch aborts a query due to RAM issues.
  - Prevented 'raw contains' search with an empty value.
  - Enabled submitting a Lucene query with the 'Enter' key.
  - Moved submit buttons from left to right.
  - Enhanced the visibility of the right-click context menu for events.
  - Improved the 'Merge case' dialog and positioning of search bubbles in the event table.
  - Show 'group scan' in the scan table.
  - Reuse the last status and type of the previous guided baselining case as the default for the next one.
  - Added a description to unresolvable Auto Case IDs.
  - Improved the column preferences dialog for tables with many columns.
  - Removed links from breadcrumbs.
  - Added dark mode for API documentation.
  - Hide the Valhalla link for some YARA rules, e.g., external or custom rules.
  - Enabled dragging and dropping condition terms in the 'Create Case' dialog.
  - Moved example events in 'Create Case' from top to bottom and made them expandable.
  - Improved error messages for login failures due to incorrect credentials.
  - Enabled selecting asset labels and case tags from a dropdown when creating reports.
  - Enhanced cosmetics for tooltips in event charts.
  - Allowed searching for displayed text instead of numeric values in most tables.
  - Removed zero bytes ('\x00') from THOR events in the GUI.
  - Preserved conditions when switching from guided to custom mode in the condition builder.
  - Display version number and 'up-to-date' status on the overview page.
  - Hide deleted Management Centers in the connected Management Centers table.
  - Updated menu items for the sandbox.
  - Showed actual values instead of numeric values in event charts (e.g., for case type).
  - Improved change history for cases, showing the diff of conditions.
  - Added THOR key highlighting in Guided Baselining.
  - Rearranged menu items in the settings section.
  - Enhanced cosmetics for the 'similar cases' dropdown in the 'Create Case' dialog.
  - Optionally hide all non-favorite THOR keys.
  - Moved manuals and API documentation to the navbar.
  - Highlighted searched terms in the Event table.

----

* **Bugfixes**

  - Fixed an issue where bulk updating cases with many events would fail.
  - Fixed an error when creating a case without a name.
  - Corrected the event count in the detailed view of the most frequent event values.
  - Fixed sorting of the level by criticality instead of alphabetically.
  - Fixed issues with hiding columns in the column preferences.
  - Reduced occurrence of MariaDB deadlock errors.
  - Fixed 'could not create GUI notification file' error.
  - Resolved errors when downloading sandbox files.
  - Made the 'Re-link' button visible in the connected Management Centers table.
  - Corrected the event count in some Group Scans.
  - Fixed typos in success and error messages.
  - Improved report generation speed by eliminating unnecessary data.
  - Ensured the green loading indicator is always visible.
  - Fixed the backup script.
  - Resolved cut-off elements in the UI.
  - Corrected a typo in the version number in /etc/issue.
  - Fixed issues with the http proxy configuration on fresh installations.

----

* **Chore**

  - Reduced the time range of signature feedback collection from 90 days to 30 days.
