.. Index:: 4.4 Changes

Analysis Cockpit v4.4
---------------------

Analysis Cockpit 4.4.0
######################

Release Date: Thu, 15 Jan 2025 16:16:00 +0100

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
