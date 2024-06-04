.. Index:: Network Requirements

Network Requirements
--------------------

The Analysis Cockpit and other systems which will have to communicate
with each other, need the following ports opened within the network.
For a detailed and up to date list of our update and licensing
servers, please visit https://www.nextron-systems.com/resources/hosts/.

The Analysis Cockpit requires the following open ports (incoming).

From Management Workstation to Analysis Cockpit
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
   :header-rows: 1
   :widths: 50, 50

   * - Description
     - Ports
   * - Administrative Web Interface
     - 443/tcp
   * - Command Line Access
     - 22/tcp

From Analyst Workstation to Analysis Cockpit
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
   :header-rows: 1
   :widths: 50, 50

   * - Description
     - Ports
   * - Administrative Web Interface
     - 443/tcp

From ASGARD Management Center to Analysis Cockpit
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
   :header-rows: 1
   :widths: 50, 50

   * - Description
     - Ports
   * - Syslog Forwarding
     - 514/tcp, 514/udp
   * - Asset Synchronization
     - 7443/tcp

From Analysis Cockpit to SIEM (optional)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
   :header-rows: 1
   :widths: 50, 50

   * - Description
     - Ports
   * - Syslog Forwarding
     - 514/tcp, 514/udp

From Analysis Cockpit to the Internet
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Analysis Cockpit is configured to retrieve updates from the
following URLs:

* :samp:`https://update-301.nextron-systems.com`

A proxy system should be configured to allow access to these URLs
without TLS/SSL interception (Analysis Cockpit uses client-side SSL
certificates for authentication). It is possible to configure a proxy
server, username and password during the setup process of the Analysis
Cockpit platform. It only supports BASIC authentication, not NTLM
Authentication.

If you are planning to use the **ChatGPT** integration, make sure that the
Analysis Cockpit can reach the following URL:

* :samp:`https://api.openai.com`

From Analysis Cockpit to Sandbox Systems (optional)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Depending on the Sandbox system and your individual configuration.

.. list-table::
   :header-rows: 1
   :widths: 50, 50

   * - Description
     - Ports
   * - Sandbox (typically)
     - 443/tcp, 8080/tcp

Time Synchronization
^^^^^^^^^^^^^^^^^^^^

Analysis Cockpit tries to reach the public Debian time servers by
default.

.. list-table::
   :header-rows: 1
   :widths: 50, 50

   * - Server
     - Port
   * - 0.debian.pool.ntp.org
     - 123/udp
   * - 1.debian.pool.ntp.org
     - 123/udp
   * - 2.debian.pool.ntp.org
     - 123/udp

The NTP server configuration can be changed in the settings.

DNS
^^^

Analysis Cockpit needs to be able to resolve internal and external IP addresses.

.. warning:: 
  Please make sure that you install your Analysis Cockpit with a
  ``domain name`` (see :ref:`setup/network:network configuration`).
  If you do not set the domain name and install the ASGARD package,
  you will have problems connecting your ASGARD(s) to the Analysis Cockpit.

  All components you install should have a proper domain name configured to avoid issues further during the configuration.

Internet Access during Installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Analysis Cockpit installer requires Internet access during the
setup. The installation process will fail if required packages cannot be
loaded from https://update3.nextron-systems.com

SSL/TLS Interception
~~~~~~~~~~~~~~~~~~~~

The installation and update processes do not accept an unknown but valid
SSL/TLS certificate presented by an intercepting entity and therefore
don't support SSL/TLS interception.

Since our products are usually used in possibly compromised
environments, the integrity of our software and update packages has
highest priority.

Architecture Overview
^^^^^^^^^^^^^^^^^^^^^

The following image shows an architecture overview with all products and
their communication relationships.

.. figure:: ../images/asgard_architecture.png
   :alt: Full Architecture
	
   Full Architecture