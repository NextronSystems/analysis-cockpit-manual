.. Index:: AC4 Changes

Analysis Cockpit v4
-------------------

Analysis Cockpit 4.0.12
#######################

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Tue, 20 Feb 2024 16:20:00 +0200

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Bugfix
      - Fixed import of THOR logfiles with very long lines
    * - Bugfix
      - Fixed error on creating new cases based on condition and time range
    * - Bugfix
      - Fixed non-working ntp service restart after ntp configuration changes

This chapter contains all the changes of the ASGARD
Analysis Cockpit.

Analysis Cockpit 4.0.10
#######################

.. list-table:: 
    :header-rows: 1

    * - Release Date
    * - Tue, 16 Jan 2024 10:26:00 +0100

.. list-table::
    :header-rows: 1
    :widths: 15, 85

    * - Type
      - Description
    * - Feature
      - Automatic index rollover
    * - Feature
      - Cluster configuration
    * - Change
      - Using timesyncd instead of ntpd. We recommend to check your NTP settings in the UI after upgrade
    * - Change
      - Improved sync performance between Management Center and Analysis Cockpit