.. Index:: Other Installer Steps

Choosing a password
-------------------

.. figure:: ../images/setup_password.png
   :alt: Choosing a password

   Choosing a password for the nextron user

Partitioning of the Hard Disk
-----------------------------

.. warning:: 
   The Analysis Cockpit is intended to be installed with
   only one disk. Do not configure your server with
   multiple disks. The system won't configure additional
   disks. Make sure that your disk has the recommended
   size. See :ref:`requirements/hardware:hardware requirements`
   for more information.

Finally, confirm the settings, select “Yes” and click “Continue”.

.. figure:: ../images/image20.png
   :alt: Partition Disks - Write changes to disks 

   Partition Disks – Write changes to disks

.. figure:: ../images/image21.png
   :alt: Partition disks - Select disk to partition

   Partition disks – Select disk to partition

Proxy Configuration
-------------------

If you are using a proxy to access the Internet, enter the proxy details
in the next step. Please note, Internet connectivity is required for the
next step – the installation of the ASGARD Analysis Cockpit service.

.. figure:: ../images/image22.png
   :alt: Proxy Configuration 

   Proxy Configuration

The proxy configuration supports unauthorized access and HTTP Auth, for
example :samp:`http://our-proxy.local:8080` and :samp:`http://username:password@our-proxy.local:8000`

.. hint:: 
    Your Installer will finish now the installation. After the
    installation is done, you will be prompted to log in to your
    server.