.. Index:: Hardware Requirements

Hardware Requirements
---------------------

.. list-table::
   :header-rows: 1
   :widths: 30, 70

   * - Connected Endpoints
     - Minimum  Hardware Requirements
   * - up to 1,000
     - System memory: 16 GB, Hard disk: 200 GB (500 GB), CPU Cores: 4
   * - up to 10,000
     - System memory: 16 GB, Hard disk: 1TB, CPU Cores: 6
   * - up to 15,000
     - System memory: 32 GB, Hard disk: 2TB SSD (min 100 MB/s), CPU Cores: 8
   * - up to 20,000
     - System memory: 32 GB, Hard disk: 2TB SSD (min 100 MB/s), CPU Cores: 12

There are a few things to consider, before you start with the
installation.

The disk size of 200 GB is fine in scenarios where you import only
Alerts and Warnings into the Cockpit, scan less than 1.000 systems on a
weekly basis and want to keep the logs for less than one year. If you
also import Notices and Info messages for these 1.000 servers, we
recommend a disk size of at least 500 GB.
