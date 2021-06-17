
Typical Pitfalls
================

Certificate Validation Failed
-----------------------------

If you receive the following error, SSL/TLS interception interrupted the
installation process.

.. code:: bash
   
   nextron@analysis3:~$ sudo nextronInstaller -cockpit 
   [sudo] Passwort für nextron:
   Ign:1 https://update3.nextron-systems.com analysis InRelease
   Err:2 https://update3.nextron-systems.com analysis Release
   Certificate verification failed: The certificate is NOT trusted. The certificate issuer is unknown. Could not handshake: Error in the certificate verification. [IP: 192.168.3.21 8080]

Since we do not support setups in which the connections to our update
servers are intercepted (see chapter :doc:`Requirements <./requirements>`), the
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

ElasticSearch Index Locked Due to Low Free Disk Space
-----------------------------------------------------

.. code:: bash
   
   Mar 26 09:48:09 analysis-cockpit[22732]: [ERROR] could not update log: could not update logs: could not update documents: http status 403 ({"took":48,"timed\_out":false,"total":136,"updated":0,"deleted":0,"batches":1,"version\_conflicts":0,"noops":0,"retries":{"bulk":0,"search":0},"throttled\_millis":0,"requests\_per\_second":-1.0,"throttled\_until\_millis":0,"failures":[{"index":"logs-2019-03-21","type":"doc","id":"L11527716281914854515","cause":{"type":"cluster\_block\_exception","reason":"blocked by: [FORBIDDEN/12/index read-only / allow delete (api)];"},"status":403},{"index":"logs-2019-03-21","type":"doc","id":"L12526619521231613944","cause":{"type":"cluster\_block\_exception","reason":"blocked by: [FORBIDDEN/12/index read-only / allow delete (api)];"},"status":403},{"index":"logs-2019-03-21","type":"doc","id":"L10726191995274581682","cause":{"type":"cluster\_block\_exception","reason":"blocked by: [FORBIDDEN/12/index read-only / allow delete (api)];"},"status":403},{"index":"logs-2019-03-21","type":"doc","id":"L17340155165061572392","cause":{"type":"cluster\_block\_exception","reason":"blocked by: [FORBIDDEN/12/index read-only / allow delete (api)];"},"status":403},{"index":"logs-2019-03-21","type":"doc","id":"L10064611600393832220","cause":{"type":"cluster\_block\_exception","reason":"blocked by: [FORBIDDEN/12/index read-only / allow delete (api)];"},"status":403}   

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

.. code:: bash
   
   curl -XPUT -H "Content-Type: application/json" http://localhost:9200/_all/_settings -d '{"index.blocks.read_only_allow_delete": null}'


Debug Failed File Imports
-------------------------

Check for reported problems using this command:

.. code:: bash
   
   find /var/lib/nextron/analysiscockpit3/events -name "\*.problem"

Make sure that you’re able to see the imported log data and review the
selected time range in the time range picker in whatever view you’re
reviewing the data. Be aware that the log data gets indexed with the
creation timestamp of the log lines not the time of their import.

This means that if you’re importing log data that is old, the default
date range set in the date range picker may be too narrowly defined so
that you’re just unable to see the imported data.

Fixing a Broken Proxy Configuration
-----------------------------------

Sometimes during installation, proxy settings get mixed up or a typo in
the proxy URL leads to a broken Internet connection.

It is not trivial to fix this situation, since the proxy settings
collected during installation are changed in so many different locations
on a Linux system for all the different services and command line tools.

Broken before Analysis Cockpit Installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you’ve set a wrong proxy before the package installation using the
**sudo nextronInstaller -cockpit** command and the installer failed to
fetch the required packages from our update servers, perform the
following steps.

Fix the proxy string in the file **/etc/apt/apt.conf.d/00proxy**

E.g.

.. code:: bash
   
   sudo edit /etc/apt/apt.conf.d/00proxy


Then rerun the installer.

Broken after the Analysis Cockpit Installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If your infrastructure has changed and you have to change the proxy
server somewhen later edit the proxy settings in the Web GUI.

``Settings`` > ``System`` > ``Proxy``
