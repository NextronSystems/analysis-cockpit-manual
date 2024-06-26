.. Index:: Hardware Requirements

Hardware Requirements
---------------------

There are a few things to consider, before you start with the
installation.

If you install on VMWare, the minimum requirements for the virtual
machine are as follows:

* System memory: 16 GB
* Hard disk: 200 GB
* CPU cores: 4

The disk size of 200 GB is fine in scenarios where you import only
Alerts and Warnings into the Cockpit, scan less than 1.000 systems on a
weekly basis and want to keep the logs for less than one year. If you
also import Notices and Info messages for these 1.000 servers, we
recommend a disk size of at least 500 GB.

The Analysis Cockpit does not have any filters on which type of events
will be imported into the database. This has to be controlled by chaning
your scan parameters in your ASGARD Management Center. To change the log
level, you can use the ``--reduced`` parameter for all of your scans.

.. hint::
    ``--reduced`` - Reduced output mode - only warnings, alerts and errors will
    be printed.

For an Installation of up to 20.000 endpoints the following
specifications are recommended:

* System memory: 32 GB
* Hard disk: 2 TB SSD
* CPU cores: 8
