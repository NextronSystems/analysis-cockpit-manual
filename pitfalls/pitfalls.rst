.. Index:: Pitfalls

Certificate Validation Failed
-----------------------------

If you receive the following error, SSL/TLS interception interrupted the
installation process.

.. code-block:: console
   
   nextron@cockpit:~$ sudo nextronInstaller -cockpit 
   [sudo] password for nextron:
   Ign:1 https://update3.nextron-systems.com analysis InRelease
   Err:2 https://update3.nextron-systems.com analysis Release
   Certificate verification failed: The certificate is NOT trusted. The certificate issuer is unknown. Could not handshake: Error in the certificate verification. [IP: 192.168.3.21 8080]

Since we do not support setups in which the connections to our update
servers are intercepted (see chapter :ref:`requirements/network:ssl/tls interception`), the
only way to resolve this problem is to deactivate SSL/TLS interception
for our update servers.

Log File Import of Previous Years
---------------------------------

The log file format of (old) THOR scan logs is the original SYSLOG
format, which contains no year value in the timestamp of the message
header.

You can modify the timestamp of old THOR logs by using the following
script:

https://github.com/NextronSystems/nextron-helper-scripts/blob/master/asgard-analysis-cockpit/thor-timestamp-coverter.py

Recover from a Full Disk
------------------------

If your disk is full or near full, ASGARD Analysis Cockpit will
not work properly. In order to resume its operation you need to
make free space on the disk.

We suggest to save the files to another system beforehand, if you
want to keep the information for future usage. ASGARD will not need
the following files to function and they can be removed safely:
    
- ``/var/lib/nextron/analysiscockpit3/log/*.gz``
- ``/var/lib/nextron/analysiscockpit3/events/*.ok``

Especially the assignment log can grow big in production environments.
If deleting the logs is not enough, deleting the already read-in events (ending on ``.ok``)
is the next best location to regain disk space. If there are too many files for a 
simple ``rm *.ok``, you can use find to delete them:

.. code-block:: console

   nextron@cockpit:~$ sudo su -
   [sudo] password for nextron:
   root@cockpit:~# find /var/lib/nextron/analysiscockpit3/events -name "*.ok" -print0 | xargs -0 -I'{}' rm '{}'

If Elasticsearch does not automatically work again after cleaning up some disk space, restart
it under ``Settings`` > ``System`` > ``Services`` or with ``sudo systemctl restart elasticsearch.service``.
If this is not working either, you may need to disable Elasticsearch's read-only mode. See 
:ref:`pitfalls/pitfalls:elasticsearch index locked due to low free disk space` for a how-to.

Deleting the files given above should be enough to resume operation. If the disk on your
ASGARD Analysis Cockpit is full because of growing data over time, the disk space should be
increased. If that is not an option you can delete old scans as described in section
:ref:`maintenance/disk-space:regain disk space`.

ElasticSearch Index Locked Due to Low Free Disk Space
-----------------------------------------------------

.. code-block:: none
   
   Mar 26 09:48:09 analysis-cockpit[22732]: [ERROR] could not update log:
      could not update logs: could not update documents: http status 403

.. literalinclude:: ../examples/elastic_error.json
   :language: json

This happens when Elasticsearch thinks the disk is running low on space
so it puts itself into read-only mode.

By default, Elasticsearch's decision is based on the percentage of disk
space that's free, so on big disks this can happen even if you have many
gigabytes of free space.

The flood stage watermark is 95% by default, so on a 1TB drive you need
at least 50GB of free space or Elasticsearch will put itself into
read-only mode.

You can fix that issue with the following command using the command line
on ASGARD:

.. code-block:: console
   
   nextron@asgard:~$ curl -X PUT -H "Content-Type: application/json" http://localhost:9200/_all/_settings -d '{"index.blocks.read_only_allow_delete": null}'


Debug Failed File Imports
-------------------------

Check for reported problems using this command:

.. code-block:: console
   
   nextron@cockpit:~$ sudo su -
   [sudo] password for root:
   nextron@cockpit:~$ find /var/lib/nextron/analysiscockpit3/events -name "\*.problem"

Make sure that you're able to see the imported log data and review the
selected time range in the time range picker in whatever view you're
reviewing the data. Be aware that the log data gets indexed with the
creation timestamp of the log lines not the time of their import.

This means that if you're importing log data that is old, the default
date range set in the date range picker may be too narrowly defined so
that you're just unable to see the imported data.

Fixing a Broken Proxy Configuration
-----------------------------------

Sometimes during installation, proxy settings get mixed up or a typo in
the proxy URL leads to a broken Internet connection.

It is not trivial to fix this situation, since the proxy settings
collected during installation are changed in so many different locations
on a Linux system for all the different services and command line tools.

Broken before Analysis Cockpit Installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you have set a wrong proxy before the package installation using the
**sudo nextronInstaller -cockpit** command and the installer failed to
fetch the required packages from our update servers, perform the
following steps.

Fix the proxy string in the file ``/etc/apt/apt.conf.d/00proxy``

.. code:: console
   
   nextron@cockpit:~$ sudoedit /etc/apt/apt.conf.d/00proxy


Then rerun the installer.

Broken after the Analysis Cockpit Installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If your infrastructure has changed and you have to change the proxy
server sometime later, edit the proxy settings in the Web GUI.

``Settings`` > ``System`` > ``Proxy``
