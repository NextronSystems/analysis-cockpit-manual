Changelog
=========

This chapter contains all new changes to the ASGARD
Analysis Cockpit.

Analysis Cockpit 3.7
####################

Analysis Cockpit 3.7.8
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Fri, 14 Apr 2023 10:42:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Bugfix
      - Fixed non-working "add role case status"
    * - Bugfix
      - Fixed issues with LogWatcher cases

Analysis Cockpit 3.7.7
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Wed, 29 Mar 2023 10:18:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Change
      - Decreased file size and rotation config of assignment log
    * - Change
      - Improved ip ban config
    * - Bugfix
      - Fixed missing LogWatcher section
    * - Bugfix
      - Fixed missing upgrade available indicator

Analysis Cockpit 3.7.4
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Fri, 17 Mar 2023 16:18:00 +0100

.. list-table::
    :header-rows: 1

    * - IMPORTANT
    * - This release completely refactored the UI. The old API endpoints will still be supported.

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Feature
      - Suggested Cases
    * - Feature
      - Guided Baselining
    * - Feature
      - Added more aggressive Auto Case IDs that can be used to detect bigger groups of similar events
    * - Feature
      - Configure number of graphs and number of entries per graph
    * - Feature
      - Resolve Auto Case IDs in graphs
    * - Feature
      - Switch between light and dark mode
    * - Feature
      - Added 'ASGARD Search Query' to most tables
    * - Feature
      - Select an assessment based on your previous assessments
    * - Feature
      - Highlight favorite fields in event table
    * - Feature
      - Added new context menu when right-clicking on events, can be used to create fast filters, cases and more.
    * - Feature
      - Added baselining count per asset
    * - Feature
      - Added detailed event field view containing the top 1000 and rarest 1000 values of the selected field
    * - Feature
      - Send automated YARA rule feedback to Nextron Systems (disabled per default, can be enabled in UI)
    * - Feature
      - Automatically run an Baselining Optimize in background once per day (disabled per default, can be enabled in UI)
    * - Feature
      - Delete users
    * - Feature
      - Added Cape v2 sandbox connector
    * - Feature
      - Automatically block ip for a few minutes on many bad requests / login requests
    * - Change
      - Improved our engine for generating Auto Case IDs
    * - Change
      - Completely refactored UI
    * - Bugfix
      - Fixed non-working asset label filter in timeframe-based reports
    * - Bugfix
      - Reduced occurrence of "trying to create too many scroll contexts" error
    * - Bugfix
      - Fixed corrupt 'To:' mail header in some notification mails
    * - Bugfix
      - Fixed missing ntp restrictions in ntp config

Analysis Cockpit 3.5
####################

Analysis Cockpit 3.5.6
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Tue, 23 Aug 2022 14:28:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Feature
      - Baselining Modes 'Compromise Assessment' and 'Deep Inspection'
    * - Feature
      - UUID for assets that are synchronized from ASGARD Management Center
    * - Feature
      - Label events with the asset's labels
    * - Change
      - Hide static search bubbles
    * - Change
      - Load total count of baselining events in background to improve ui performance
    * - Bugfix
      - Fixed non-working counter links in additional key value information
    * - Bugfix
      - Fixed non-working sync between Management Center and Analysis Cockpit due to very large Bifrost quarantine files
    * - Bugfix
      - Fixed non-working last seen filter in asset table

Analysis Cockpit 3.4
####################

Analysis Cockpit 3.4.7
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Mon, 30 May 2022 11:30:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Security
      - OS Security Fix

Analysis Cockpit 3.4.6
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Thu, 17 May 2022 10:09:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Feature (Beta)
      - use Elasticsearch clusters instead of single-node setup
    * -
      - script to add Elasticsearch cluster nodes
    * -
      - script to configure number of replicas for each index
    * -
      - check Elasticsearch status before API calls
    * -
      - improved Elasticsearch error detection (disallow searches when shards are down)
    * -
      - automatic update while installing cluster nodes
    * - Fix
      - improved Active Directory support in ldap configuration
    * - Fix
      - collect individual bulk indexer errors and report on close
    * - Fix
      - remove unused kernel versions from boot partition
    * - Change
      - use file timestamp when loading events from events directory

Analysis Cockpit 3.3
####################

Analysis Cockpit 3.3.7
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Thu, 17 Feb 2022 12:09:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Bugfix
      - Fixed a bug in 'add to case' by similar case name

Analysis Cockpit 3.3.6
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Fri, 11 Feb 2022 09:30:00 +0200

.. list-table::
    :header-rows: 1

    * - IMPORTANT
    * - The previous update routine interrupted some case assignments. Use of Optimize function after the update is recommended.

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Bugfix
      - Fixed a bug in the update routine

Analysis Cockpit 3.3.5
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Tue,  8 Feb 2022 09:01:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Feature
      - Aurora Support
    * - Feature
      - Add comment to assets
    * - Feature
      - Custom labels for assets
    * - Feature
      - Download reports as yaml
    * - Change
      - Assigned each case to a scanner / agent, e.g. THOR, Aurora, LogWatcher
    * - Bugfix
      - Fixed a bug in the condition engine in combination with merged cases
    * - Bugfix
      - Fixed a bug that caused some cases to break case priority
    * - Bugfix
      - Fixed escaping of ldap usernames with special characters
    * - Bugfix
      - Fixed 'too many scroll contexts' error, when creating large regex cases
    * - Bugfix
      - Fixed non-working 'add filter' button in group scans section
    * - Bugfix
      - Fixed ntp configuration

Analysis Cockpit 3.2
####################

Analysis Cockpit 3.2.2
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Thu, 28 Oct 2021 14:23:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Feature
      - Merge Cases
    * - Feature
      - Import statistics on overview page
    * - Change
      - Separate events in baselining and event view between THOR- and Log Watcher events
    * - Bugfix
      - Fixed recommendations and custom recommendations in csv export
    * - Bugfix
      - Fixed a bug in the condition engine that caused some events to not match the specific condition in rare cases

Analysis Cockpit 3.1
####################

Analysis Cockpit 3.1.5
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Thu, 16 Sep 2021 11:49:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Bugfix
      - Fixed a bug in the new condition engine that caused some events to not match the specified condition in rare cases.

Analysis Cockpit 3.1.4
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Wed, 21 Jul 2021 11:13:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Security
      - OS Security Fix

Analysis Cockpit 3.1.3
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Fri,  2 Jul 2021 14:29:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Feature
      - Added support for new ASGARD Security Center
    * - Change
      - Regenerated TLS certificate with SAN extension for ASGARD Management Center synchronization
    * - Change
      - Toggle between "show" and "hide" additional asset information in asset table to improve performance
    * - Change
      - Cosmetics and wordings
    * - Change
      - Highly reduced length of server-side table urls due to issues with older browsers and reverse proxies
    * - Bugfix
      - Fixed non-working text highlighting in some table cells (also text highlighting will not trigger a click event anymore)
    * - Bugfix
      - Allow import of .log files in scan section

Analysis Cockpit 3.0
####################

Analysis Cockpit 3.0.4
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Mon,  7 Jun 2021 09:09:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Bugfix
      - Fixed an issue that caused synchronization of Log Watcher events to not work anymore in specific cases
    * - Bugfix
      - Fixed "trying to create too many scroll contexts" error that sporadically occured during case creation or regex testing

Analysis Cockpit 3.0.2
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Thu,  6 May 2021 09:14:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Feature
      - Added new "similar cases" feature in Add Case form
    * - Feature
      - Added pagination to additional asset information
    * - Change
      - Improved API documentation
    * - Change
      - Refactored condition engine to be more performant in some cases
    * - Change
      - Cosmetics
    * - Bugfix
      - Fixed missing events of some scans that were collected by an additional "log collection" job
    * - Bugfix
      - Fixed default values in cuckoo config
    * - Bugfix
      - Fixed missing MATCH_STRINGS field in the search bar
    * - Bugfix
      - Removing events from a case caused the scan- and asset table of this case to be inconsistent for a few hours

Analysis Cockpit 3.0.0
~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Fri, 19 Mar 2021 09:52:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Major Release
      - Initial release

Analysis Cockpit 3.0 unstable
#############################

Analysis Cockpit 3.0.0~pre+20210319.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Fri, 19 Mar 2021 09:36:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Change
      - Renamed ASGARD's new Log Scanner to Log Watcher

Analysis Cockpit 3.0.0~pre+20210315.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Mon, 15 Mar 2021 10:22:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Bugfix
      - Fixed corrupt case-insensitive search for 'contains' search
    * - Bugfix
      - Increased ~tls certificate validity (between ASGARD and Analysis Cockpit)

Analysis Cockpit 3.0.0~pre+20210309.1
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Tue,  9 Mar 2021 11:28:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Feature
      - Support Eventlog Scanner

Analysis Cockpit 3.0.0~pre+20210308.1
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Fri,  5 Mar 2021 08:42:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Feature
      - New column 'last scan completed' per asset
    * - Security
      - Fixed smaller security issues (Added more CSP headers, added logout headers, improved yaml decoder, jquery upgrade, ..)

Analysis Cockpit 3.0.0~pre+20210305.1
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Fri,  5 Mar 2021 08:42:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Feature
      - Receive additional asset information from ASGARD, e.g. installed software, local users, ...
    * - Feature
      - Request THOR logs of group scan from ASGARD
    * - Feature
      - Create empty case (in Case Management)
    * - Change
      - Added THOR key whitelisting - Only known THOR keys will be parsed from THOR events and added to ElasticSearch
    * - Change
      - The collapse button in the Baselining / All Events section will only collapse the timeline and keep all bar charts expanded
    * - Change
      - Cosmetics
    * - Change
      - Updated templates in filter engine
    * - Bugfix
      - Added timeout for LDAP requests
    * - Bugfix
      - Fixed noteworthy cases of group scans in suspicious cases column
    * - Bugfix
      - Fixed missing grouping criteria for initial cases

Analysis Cockpit 3.0.0~pre+20210222.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Mon, 22 Feb 2021 08:55:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Change
      - Updated min. TLS version and TLS cipher suites
    * - Bugfix
      - Automatically reconnect to LDAP server on broken pipe
    * - Bugfix
      - Fixed CSRF protection
    * - Bugfix
      - Do not show 'undefined' in some cells in Baselining- and All Events Section
    * - Bugfix
      - Fixed corrupt 'continue' button in 'Your session will expire soon' popup

Analysis Cockpit 3.0.0~pre+20210218.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Thu, 18 Feb 2021 10:13:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Change
      - Improved performance
    * - Bugfix
      - Fixed corrupt GUI notification table

Analysis Cockpit 3.0.0~pre+20210212.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Fri, 12 Feb 2021 11:35:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Bugfix
      - Some newly created cases had corrupt grouping criteria. This release will remove all automatically assigned
        events from the affected cases and reassign them with an automatically started Optimize. There might be more
        events in the Baselining section after this upgrade due to events that were accidentally assigned to a case before.

Analysis Cockpit 3.0.0~pre+20210205.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Fri,  5 Feb 2021 09:12:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Bugfix
      - Increased limit of total fields in ElasticSearch from 1000 to 8000

Analysis Cockpit 3.0.0~pre+20210204.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Thu,  4 Feb 2021 10:29:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Feature
      - Auto-Resize for some textareas, e.g. Summary, Assessment, Comment
    * - Feature
      - Bulk Delete Cases
    * - Feature
      - Added hide button to additionally loaded event information
    * - Feature
      - Made 'Events Assigned' clickable in 'Optimize' section to show all events that were assigend in the current optimize run
    * - Change
      - Automatically focus inputs in some popups
    * - Change
      - Allow 'Shift + Click' for negated search, too (instead of 'Alt + Click')
    * - Change
      - Improved performance of 'Remove Events from Case'
    * - Change
      - Added VirusTotal URL to MD5 and SHA1, too
    * - Change
      - Improved MOTD config
    * - Change
      - Increased time-based default filters from 'Last 7 Days' to 'Last 30 Days'
    * - Change
      - Truncated summary in case table
    * - Change
      - Sort users by user name instead of creation date
    * - Bugfix
      - Fixed corrupt generation of conditions based on current query
    * - Bugfix
      - Fixed reduction of multiple whitespaces to one whitespace of THOR events in GUI (caused some filters to not work)

Analysis Cockpit 3.0.0~pre+20210203.1
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Wed,  3 Feb 2021 08:11:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Bugfix
      - Removing events from condition cases caused them to be corrupt until reboot
    * - Bugfix
      - Fixed typo in filter engine
    * - Bugfix
      - Fixed security issues with LDAP

Analysis Cockpit 3.0.0~pre+20210201.1
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Mon,  1 Feb 2021 08:59:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Feature
      - Persistent page length per section per user
    * - Feature
      - Completely refactored the 'Create Case' dialog
    * - Feature
      - Remove events from case
    * - Feature
      - Added Log Analysis Guide and THOR Manual to downloads section
    * - Feature
      - Favorite Fields per user in event section
    * - Feature
      - Persistent time range filter in event-, asset- and scan section
    * - Feature
      - Resolve asset- and case ids in event details to hostname and case name
    * - Feature
      - New button 'Valhalla' in event detail fields that contain a YARA rule name that will lookup the rule in Valhalla
    * - Feature
      - Backup configuration (cases, grouping criteria, users, ...) and Restore on a fresh Analysis Cockpit
    * - Feature
      - Replaced all graphs in several sections with horizontal bar charts
    * - Feature
      - Added 'Download Sandbox Sample' button in sandbox samples table
    * - Feature
      - Added 'Origin' column in sandbox samples table
    * - Change
      - Removed 'Close' button from all dialogs
    * - Change
      - Cosmetics
    * - Change
      - Wordings
    * - Change
      - Added more tooltips
    * - Change
      - Sort by score in baselining section and by timestamp in event section
    * - Change
      - Added refresh button in report section
    * - Change
      - Prevent users from creating duplicate bubble filters
    * - Change
      - Files that could not be imported will now be rotated to .problem
    * - Change
      - Highly improved performance of case creation and condition tests based on condition
    * - Change
      - Added more configurable LDAP settings
    * - Bugfix
      - Fixed corrupt search for integers in ElasticSearch
    * - Bugfix
      - Redirect to case table if case detail page was opened without case id in URL
    * - Bugfix
      - Fixed corrupt mysql config that occurs on >30 GB systems due to a wrong installation script
    * - Bugfix
      - Fixed wrong scan duration in scan table
    * - Bugfix
      - Removed revise of THOR events in import procedure that added fields that do not exist in original event, e.g. BASENAME

Analysis Cockpit 3.0.0~pre+20210121.2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Thu, 21 Jan 2021 15:45:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Feature
      - Two Factor Authentication
    * - Feature
      - New filter bar in baselining and event section
    * - Feature
      - New icon in aggregation graphs that counts unique values
    * - Feature
      - Added progress bar for optimizer
    * - Feature
      - Add comments to cases in 'Create Case', 'Add to Case', 'Update Case' and 'Bulk Update Case' dialogs
    * - Feature
      - Auto-Summary in 'Create Case' dialog
    * - Change
      - Improved column visibility selection
    * - Change
      - Added 'Notification Name' to notifications table
    * - Change
      - Cosmetics
    * - Change
      - Wordings
    * - Bugfix
      - Restrict users to create or change 'Open' or 'Closed' case status in settings section
    * - Bugfix
      - Fixed ntp configuration issues
    * - Bugfix
      - 'equals' and 'not equals' searches in baselining and event section are now case insensitive
    * - Bugfix
      - Added 'Disabled' column in user table
    * - Bugfix
      - Added 'Unknown' to scan status selection

Analysis Cockpit 3.0.0~pre+20210118.2
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Mon, 18 Jan 2021 15:28:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Change
      - Improved performance of THOR events import
    * - Bugfix
      - Add group ids of manually added events to case engine
    * - Bugfix
      - Fixed assignment of events to already deleted cases
    * - Bugfix
      - Fixed wrong suspicious cases count of scans in scan table
    * - Bugfix
      - Fixed wrong include path in rsyslog config for port 514 listener
    * - Bugfix
      - Fixed upgrade via GUI

Analysis Cockpit 3.0.0~pre+20210114.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Thu, 14 Jan 2021 06:40:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Bugfix
      - Fixed wrong API base path for Update section
    * - Bugfix
      - LDAP Fixes
    * - Bugfix
      - Fixed typo in case assignment engine for THOR's "ProcessCheck" module
    * - Bugfix
      - Added missing dependency

Analysis Cockpit 3.0.0~pre+20201207.1
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Mon,  7 Dec 2020 13:13:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Beta release
      -
