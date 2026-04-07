.. Index:: 4.4 Changes

Analysis Cockpit v4.4
---------------------

Analysis Cockpit 4.4.6
######################

Release Date: Tue, 07 Apr 2026 13:15:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Security
      - Fixed MFA bypass where TFARequired was true even when TFAValid was not set
    * - Bugfix
      - Fixed condition builder import silently dropping certain conditions
    * - Bugfix
      - Fixed scrolling to top when opening bubbles menu
    * - Bugfix
      - Fixed retention running constantly when no policies are configured
    * - Bugfix
      - Added maxsize for logrotate in asgard-analysis-cockpit
    * - Bugfix
      - Fixed race condition in fixed bubbles updater
    * - Bugfix
      - Fixed filter forwarding and case statistics sync while editing
    * - Bugfix
      - Fixed missing THOR and signatures version in scan table
    * - Bugfix
      - Fixed 24-hour time format and datetime precision in incoming events
    * - Bugfix
      - Fixed scan parameter display for resource control badges
    * - Bugfix
      - Fixed double escaping in search/filter context menu actions
    * - Bugfix
      - Fixed backslash and quote escaping in AQL reason query for baselining
    * - Bugfix
      - Fixed forwarding from matching events
    * - Bugfix
      - Fixed duplicate filter bubbles via addEntryToBubbles
    * - Bugfix
      - Fixed aggregation chart filter returning no results for long strings by truncating to ES keyword limit
    * - Bugfix
      - Fixed aggregation detail sidebar filter always using equals operator for long strings

Analysis Cockpit 4.4.5
######################

Release Date: Mon, 02 Mar 2026 13:15:00 +0100

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Feature
      - Added case import from suggested cases
    * - Security
      - Encrypted LDAP password in configuration
    * - Security
      - Hardened backup validation against zip slip and rsyslog injection
    * - Bugfix
      - Fixed wrong operator used in AQL filter
    * - Bugfix
      - Fixed AQL parser silently dropping unparseable parts and mixed OR/NOT handling
    * - Bugfix
      - Fixed filtering multiple values in raw field with contains operator
    * - Bugfix
      - Fixed unsupported operators shown for raw fields
    * - Bugfix
      - Fixed page scrolling to top when adding filter for THOR events
    * - Bugfix
      - Fixed depth guard issue in AQL parser
    * - Bugfix
      - Fixed escape handling for backslashes and quotes in context menu search bubbles
    * - Bugfix
      - Fixed backslash handling in case conditions
    * - Bugfix
      - Fixed case import (update case) and case export (use selection)
    * - Bugfix
      - Fixed Case Intelligence Feed last check timestamp showing false warning
    * - Bugfix
      - Fixed AQL parser rejecting invalid IN/NOT IN syntax and improved type safety in condition builder

Analysis Cockpit 4.4.3
######################

Release Date: Wed, 28 Jan 2026 16:18:00 +0100

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Bugfix
      - Fixed autocompletion error in event-anonymization-table
    * - Bugfix
      - Fixed flickering tooltip on aggregation chart (events-table)
    * - Bugfix
      - Fixed render error when showing more information in event-details-row
    * - UI
      - Updated icons to be consistent for searching and filtering in the events-table

Analysis Cockpit 4.4.2
######################

Release Date: Fri, 23 Jan 2026 13:11:00 +0100

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Bugfix
      - Fixed missing filter in affected assets
    * - Bugfix
      - Fixed validation bug when uploading a scan

Analysis Cockpit 4.4.1
######################

Release Date: Tue, 20 Jan 2026 16:02:00 +0100

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Bugfix
      - Fixed bug for imported condition when creating a new case

Analysis Cockpit 4.4.0
######################

Release Date: Thu, 15 Jan 2026 16:16:00 +0100

----

* Highlights

  - Improved FilterBar and overall UI consistency across DataTables
  - Added Management Center 4 integration for improved compatibility
  - Enhanced performance and reliability of Baselining and Case Intelligence modules

----

* Improvements

  - Support email and GUI notifications for unassigned events
  - THOR time fields can now be searched like other time fields
  - Added confirmation before activating new retention policies
  - Enabled export of search results and case templates
  - Introduced score slider for better case prioritization and visualization
  - Case comments and attachments can now be modified and deleted
  - Implemented automatic deactivation of inactive user accounts
  - Added configurable session timeout value
  - Allowed case notifications to rsyslog targets via TLS
  - Supported LDAP login with different role assignments
  - Included rotated log files in diagnostics pack
  - Added validation for uploaded scan result files before saving
  - Improved error messages for filter queries
  - Increased maximum upload size for scan files
  - Adjusted color codes and UI elements for cleaner visual consistency
  - Implemented disk usage monitoring for ES cluster nodes with write lock on low memory
  - Reworked CSR generator in Web GUI

----

* Bugfixes

  - Fixed CSV export of events causing internal server errors
  - Fixed Case Intelligence Feed indicator not disabling when no cases found
  - Fixed condition handling in Suggested-Case-Events
  - Removed trailing linebreaks in case intelligence fields
  - Fixed data loss in case fields when switching to details view
  - Fixed input fields resetting after clearing during case creation
  - Fixed Baselining event search field clearing itself without reason
  - Fixed progress bar display and sidebar navigation issues
  - Non-admin users can no longer download diagnostics or log files
