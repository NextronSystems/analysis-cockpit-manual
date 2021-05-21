Requirements
============

Hardware Requirement
--------------------

There are a few things to consider, before you start with the
installation.

If you install on VMWare, the minimum requirements for the virtual
machine are as follows:

* System memory: 16 GB
* Hard disk: 200 GB
* CPU cores: 2

The disk size of 200 GB is fine in scenarios where you import only
Alerts and Warnings into the Cockpit, scan less than 1.000 systems on a
weekly basis and want to keep the logs for less than one year. If you
also import Notices and Info messages for these 1.000 servers, we
recommend a disk size of at least 500 GB.

For an Installation of up to 20.000 endpoints the following
specifications are recommended:

* System memory: 32 GB
* Hard disk: 2 TB SSD
* CPU cores: 4

Network Requirements
--------------------

The Analysis Cockpit requires the following open ports (incoming).

From Management Workstation to Analysis Cockpit
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Administrative web interface: 443/tcp
* Command line administration: 22/tcp

From Analyst Workstation to Analysis Cockpit
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Administrative web interface: 443/tcp

From ASGARD Management Center to Analysis Cockpit
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Syslog forwarder: 514/tcp, 514/udp
* Asset synchronization: 7443/tcp

From Analysis Cockpit to SIEM (if needed)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  Syslog forwarder: 514/tcp, 514/udp

From Analysis Cockpit to the Internet
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Analysis Cockpit is configured to retrieve updates from the
following URLs:

* Analysis Cockpit packages: https://update3.nextron-systems.com

A proxy system should be configured to allow access to these URLs
without TLS/SSL interception (Analysis Cockpit uses client-side SSL
certificates for authentication). It is possible to configure a proxy
server, username and password during the setup process of the Analysis
Cockpit platform. It only supports BASIC authentication, not NTLM
Authentication.

From Analysis Cockpit to Sandbox Systems (optional)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Depending on the Sandbox system and your individual configuration.

Typically, 8080/tcp and 443/tcp are used.

Time Synchronization
^^^^^^^^^^^^^^^^^^^^

Analysis Cockpit tries to reach the public Debian time servers by
default.

* 123/udp to 0.debian.pool.ntp.org
* 123/udp to 1.debian.pool.ntp.org
* 123/udp to 2.debian.pool.ntp.org

The NTP server configuration can be changed after logging in to the Web
guide.

DNS
^^^

Analysis Cockpit needs to be able to resolve internal and external IP
addresses.

Internet Access during Installation
-----------------------------------

The Analysis Cockpit installer requires Internet access during the
setup. The installation process will fail if required packages cannot be
loaded from https://update3.nextron-systems.com

SSL/TLS Interception
^^^^^^^^^^^^^^^^^^^^

The installation and update processes do not accept an unknown but valid
SSL/TLS certificate presented by an intercepting entity and therefore
don’t support SSL/TLS interception.

Since our products are usually used in possibly compromised
environments, the integrity of our software and update packages has
highest priority.
