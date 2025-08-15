.. Index:: 4.3 Changes

Analysis Cockpit v4.3
---------------------

Analysis Cockpit 4.3.0
######################

Release Date: Fri, 01 Aug 2025 17:08:00 +0200

----

* Highlights

  - Completely redesigned the user interface for a modern, consistent, and intuitive experience
  - Introduced the new **Case Intelligence** feature with automated case suggestions based on Nextron's Intelligence Feed
  - Added full integration with **THOR Cloud** for extended analysis and enrichment

----

* Features

  - **Case Intelligence**

    - Receive automated case suggestions from Nextron based on threat intel and event patterns
    - Configure fetching intervals and enable automatic case creation for high-confidence anomalies and false positives
    - Optionally alert users for new high-priority case suggestions

  - **THOR Cloud Integration**

    - Seamlessly connect and interact with THOR Cloud to fetch enriched context

  - **Global Alerts**

    - Display critical system-wide alerts and warnings prominently in the interface

----

* Improvements

  - **Webhook Notifications**: Added support for custom HTTP headers in webhook configurations
  - Enhanced condition layout in case details for better readability and editing
  - Cleaner, more consistent table layouts with clearly visible header action buttons when rows are selected
  - Added an indicator to case suggestions and notifications to clearly mark critical recommendations
  - Advanced table preferences: More options for persistent layout preferences
  - Columns are now resizable for more flexible table views
  - Warn users when their session is about to expire
  - Sidebar can be resized and minimized for layout customization
  - Improved accessibility and responsiveness of all primary views

----

* Security

  - Disabled API access when a user is required to change their password or set up two-factor authentication (2FA), preventing unauthorized automated access under non-compliant security states

----

* Bugfixes

  - Fixed various layout and rendering issues introduced during the Mantine migration
  - Corrected table selection behavior in multiple views
  - Restored missing filter and sort functionality in dashboard management
  - Resolved tooltip glitches and layout cutoffs in edge cases
  - Fixed incorrect rendering of condition fields under certain complex regex configurations
  - Fixed sporadic error messages during login token refresh