.. Index:: AC4 Changes

Analysis Cockpit v4.1
---------------------

Analysis Cockpit 4.1.6
######################

Release Date: Fri, 28 Jun 2024 15:46:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Bugfix
      - Fixed missing grouping criteria when applying suggested cases (AC-556)
    * - Bugfix
      - Fixed too many events in LogWatcher's 'All Events' section (AC-561)
    * - Bugfix
      - Fixed an escape issue in conditions with double backslashes (AC-564)
    * - Bugfix
      - Fixed inaccurate estimated remaining time for reindexing (AC-566)
    * - Bugfix
      - Fixed an off-by-one date error in the incoming events graph (AC-567)
    * - Bugfix
      - Fixed non-working table search for some columns in the 'Manage Dashboards' section (AC-570)
    * - Bugfix
      - Fixed 'csrf error' popup when using the 'Session expired' login dialog (AC-571)

Analysis Cockpit 4.1.5
######################

Release Date: Wed, 19 Jun 2024 09:41:00 +0200

----

* **Breaking Changes**
  
  - Changed the way events are indexed in Elasticsearch. The new index structure significantly improves performance but increases disk space usage by 30%-40%. After the upgrade, all events will be reindexed, which can take several hours depending on the number of events in your system. The system remains usable during this process, but we recommend performing the upgrade during off-peak hours. If the Analysis Cockpit reaches its disk space limit during reindexing, the process will pause until more disk space is available. The Analysis Cockpit will guide you on how to free up or increase disk space, and the reindexing process will automatically resume once enough disk space is available. Contact our support for assistance.
  - Conditions in cases are now case-insensitive. Existing conditions will be converted automatically. We believe this change will not affect case quality.

----

* **Highlights**

  - Added the ability to create custom Event Dashboards in the Baselining and All Events sections. (AC-6)
  - Added event insights by ChatGPT, enabling automatic analysis of THOR events with assessments and recommendations. Also, added the ability to ask ChatGPT to explain THOR events or terms within an event. (AC-89)
  - Introduced a new 'Matched Signatures' section showing all matched signatures chronologically. (AC-83)
  - Added the ability to collect files from an asset via the Management Center. (AC-10)
  - Implemented a Data Retention Policy for retaining events for a specified period and automatically deleting them afterwards. (AC-12, AC-175)
  - Added graphs and statistics to the Overview Dashboard. (AC-235, AC-299, AC-300, AC-301, AC-303, AC-309, AC-310, AC-316, AC-317)

----

* **Features**

  - Added the ability to assign priorities to cases. (AC-84)
  - Introduced a new field 'compromised' to track compromised assets. (AC-69)
  - Added a detailed diagnostics status page showing system health and connectivity. (AC-182)
  - Added a Diagnostics Pack that can be downloaded and sent to Nextron Systems for support. (AC-298)
  - Included a base64 and hex decoder in the context menu of THOR events. (AC-18)
  - Added a new field 'under investigation' to track ongoing investigations in cases. (AC-79)
  - Added the ability to schedule reports, including the option to send them via email. (AC-229)
  - Added the ability to enforce 2FA or password resets for users. (AC-231)

----

* **Improvements**

  - New index structure for events in Elasticsearch, significantly improving performance. (AC-313)
  - Re-added the 'Incoming events' graph in Baselining and All Events sections. (AC-2, AC-289, AC-341)
  - Improved the query for compromise assessment mode. (AC-348)
  - Added the ability to edit case details and conditions in the 'Add to Case' dialog. (AC-28, AC-172)
  - Added the ability to bulk merge cases, including merging cases with different assignment types. (AC-238, AC-167)
  - Forwarded OS information to the Security Center now uses data from the Management Center. (AC-85)
  - Display which users have set up 2FA in the user management section. (AC-13)
  - Added a stop button for 'Auto Baselining'. (AC-14)
  - Enhanced bulk actions in the case table, allowing editing of tags, priorities, and more. (AC-23)
  - Automatically adjust heap size for Elasticsearch and MariaDB based on system memory. (AC-160)
  - Re-added the 'Last 30 days' filter in the event table of an asset or case. (AC-196)
  - Added a 'Delete' button in the table of connected Management Centers. (AC-197)
  - Enhanced security by preventing API endpoint leaks and using a more secure password hash algorithm. (AC-215, AC-370)
  - Refactored the case comments section. (AC-266)
  - Display additional asset information like file systems and MAC addresses. (AC-286)
  - Improved support for THOR 10.7, especially for case assignments using Auto Case IDs. (AC-287)

----

* **UX**

  - Improved the error message when Elasticsearch aborts a query due to RAM issues. (AC-86)
  - Prevented 'raw contains' search with an empty value. (AC-1)
  - Enabled submitting a Lucene query with the 'Enter' key. (AC-39)
  - Moved submit buttons from left to right. (AC-21)
  - Enhanced the visibility of the right-click context menu for events. (AC-16)
  - Improved the 'Merge case' dialog and positioning of search bubbles in the event table. (AC-34, AC-42)
  - Show 'group scan' in the scan table. (AC-46, AC-47)
  - Reuse the last status and type of the previous guided baselining case as the default for the next one. (AC-49)
  - Added a description to unresolvable Auto Case IDs. (AC-51)
  - Improved the column preferences dialog for tables with many columns. (AC-59)
  - Removed links from breadcrumbs. (AC-62)
  - Added dark mode for API documentation. (AC-71)
  - Hide the Valhalla link for some YARA rules, e.g., external or custom rules. (AC-74, AC-27)
  - Enabled dragging and dropping condition terms in the 'Create Case' dialog. (AC-102)
  - Moved example events in 'Create Case' from top to bottom and made them expandable. (AC-103, AC-104)
  - Improved error messages for login failures due to incorrect credentials. (AC-151)
  - Enabled selecting asset labels and case tags from a dropdown when creating reports. (AC-228)
  - Enhanced cosmetics for tooltips in event charts. (AC-177)
  - Allowed searching for displayed text instead of numeric values in most tables. (AC-204, AC-282)
  - Removed zero bytes ('\x00') from THOR events in the GUI. (AC-19)
  - Preserved conditions when switching from guided to custom mode in the condition builder. (AC-36)
  - Display version number and 'up-to-date' status on the overview page. (AC-223)
  - Hide deleted Management Centers in the connected Management Centers table. (AC-251)
  - Updated menu items for the sandbox. (AC-253)
  - Showed actual values instead of numeric values in event charts (e.g., for case type). (AC-256)
  - Improved change history for cases, showing the diff of conditions. (AC-259)
  - Added THOR key highlighting in Guided Baselining. (AC-284)
  - Rearranged menu items in the settings section. (AC-307)
  - Enhanced cosmetics for the 'similar cases' dropdown in the 'Create Case' dialog. (AC-264)
  - Optionally hide all non-favorite THOR keys. (AC-319)
  - Moved manuals and API documentation to the navbar. (AC-339)
  - Highlighted searched terms in the Event table. (AC-355)

----

* **Bugfixes**

  - Fixed an issue where bulk updating cases with many events would fail. (AC-87)
  - Fixed an error when creating a case without a name. (AC-95)
  - Corrected the event count in the detailed view of the most frequent event values. (AC-35)
  - Fixed sorting of the level by criticality instead of alphabetically. (AC-70)
  - Fixed issues with hiding columns in the column preferences. (AC-157)
  - Reduced occurrence of MariaDB deadlock errors. (AC-161)
  - Fixed 'could not create GUI notification file' error. (AC-163)
  - Resolved errors when downloading sandbox files. (AC-173)
  - Made the 'Re-link' button visible in the connected Management Centers table. (AC-198)
  - Corrected the event count in some Group Scans. (AC-203)
  - Fixed typos in success and error messages. (AC-207, AC-208)
  - Improved report generation speed by eliminating unnecessary data. (AC-25)
  - Ensured the green loading indicator is always visible. (AC-220)
  - Fixed the backup script. (AC-315)
  - Resolved cut-off elements in the UI. (AC-326, AC-327)
  - Corrected a typo in the version number in /etc/issue. (AC-217)
  - Fixed issues with the http proxy configuration on fresh installations. (AC-545)

----

* **Chore**

  - Reduced the time range of signature feedback collection from 90 days to 30 days. (AC-131)