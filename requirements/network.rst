.. Index:: Network Requirements

Network Requirements
--------------------

The Analysis Cockpit and other systems which will have to communicate
with each other, need the following ports opened within the network.
For a detailed and up to date list of our update and licensing
servers, please visit https://www.nextron-systems.com/resources/hosts/.

The Analysis Cockpit requires the following open ports (incoming).

Workstation
^^^^^^^^^^^

.. list-table::
   :header-rows: 1

   * - Description
     - Port
     - Source
     - Destination
   * - Web Interface
     - 443/tcp
     - Workstation
     - Analysis Cockpit
   * - Command Line Access
     - 22/tcp
     - Workstation
     - Analysis Cockpit

ASGARD Management Center
^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
   :header-rows: 1

   * - Description
     - Port
     - Source
     - Destination
   * - Asset Synchronization
     - 7443/tcp
     - Management Center
     - Analysis Cockpit

Internet
^^^^^^^^

The Analysis Cockpit is configured to retrieve updates, THOR events, or
Case Intelligence Feeds from the following URLs:

.. list-table:: Mandatory Services
   :header-rows: 1

   * - Description
     - Port
     - Source
     - Destination
   * - Product Updates
     - 443/tcp
     - Analysis Cockpit
     - update-301.nextron-systems.com [1]_

.. list-table:: Optional Services
   :header-rows: 1

   * - Description
     - Port
     - Source
     - Destination
   * - Case Intelligence Feed
     - 443/tcp
     - Analysis Cockpit
     - update1.nextron-systems.com [1]_
   * - Case Intelligence Feed
     - 443/tcp
     - Analysis Cockpit
     - update2.nextron-systems.com [1]_
   * - THOR Cloud Integration
     - 443/tcp
     - Analysis Cockpit
     - thor-cloud.nextron-services.com
   * - THOR Cloud Lite Integration
     - 443/tcp
     - Analysis Cockpit
     - thorcloud-lite.nextron-systems.com
   * - ChatGPt Integration
     - 443/tcp
     - Analysis Cockpit
     - api.openai.com

.. [1]
  If a proxy is needed to allow access to those URLs, configure them without TLS/SSL
  interception. See :ref:`requirements/network:ssl/tls interception`

NTP
^^^

The below NTP servers are the default servers used during installation.
Those servers can be changed manually during or after the installation.

.. list-table::
   :header-rows: 1

   * - Description
     - Port
     - Source
     - Destination
   * - NTP
     - 123/udp
     - Analysis Cockpit
     - 0.debian.pool.ntp.org
   * - NTP
     - 123/udp
     - Analysis Cockpit
     - 1.debian.pool.ntp.org
   * - NTP
     - 123/udp
     - Analysis Cockpit
     - 2.debian.pool.ntp.org

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