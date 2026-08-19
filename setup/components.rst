.. Index:: Install Service

Install the Analysis Cockpit
----------------------------

The Nextron Universal Installer is a web based installer
which will guide you through the installation of our
products. The Nextron Universal Installer will install
**one** of the following products on your server (this manual
focuses on the ``Analysis Cockpit``):

- Management Center; alternatively if your license permits:
  
  * Broker
  * Gatekeeper
  * Lobby

- Master Management Center

- Analysis Cockpit; alternatively:
  
  * Elasticsearch Cluster Node for Analysis Cockpit

- Security Center, in the following variants:

  * Security Center (Backend Only)
  * Security Center (Frontend Only)
  * Security Center (All-in-one, unrecommended)

.. note::
   You can only install one product on one server, since the
   products are not designed to coexist on the same server.
   The exception being the Security Center (All-in-one).

The installation takes roughly between 5-15 minutes, depending
on your internet connection and the server you are installing
the product on.

If you encounter problems during your installation, please see
:ref:`setup/components:diagnostic pack` for further instructions.

Requirements
~~~~~~~~~~~~

The installation of the Analysis Cockpit requires
the following:

- A valid license file for the Analysis Cockpit
- A configured FQDN (with some exceptions, see :ref:`setup/components:valid fqdn`)
- Internet access during installation (see :ref:`setup/components:connectivity check`)

Installation
~~~~~~~~~~~~

After the ISO installer is finished with the setup,
you will be greeted at the console login prompt with
the following message:

.. figure:: ../images/setup_nextronInstaller.png
   :alt: Login prompt server

Follow the instructions and navigate to the webpage
displayed on your console. You will most likely get
a browser warning when you connect the first time to
the page. This is due to the page using a self signed
certificate, since it will only be used to install the
Analysis Cockpit. You can safely ignore this
warning and proceed to the page. Once the installation
is complete, the certificate can be replaced by a signed
certificate (see :ref:`administration/system-settings:tls certificate installation`)

You will be greeted with a small introduction as to what
the Nextron Universal Installer is and what it does. After
you click ``Next``, you will be presented with the landing
page of the Nextron Universal Installer.

.. figure:: ../images/setup_nextronInstaller-landing.png
   :alt: landing page of the Universal Installer

Enter the Installation Code from the terminal and click
``Next``. The Installer will now guide you through the
installation.

Connectivity Check
~~~~~~~~~~~~~~~~~~

The Nextron Universal Installer will try to connect to our
update server in order to download all the necessary packages
once the installation starts. Make sure you can reach the
update server (see :ref:`requirements/network:internet`).

Please configure your proxy settings if you are behind a
proxy (see :ref:`setup/components:proxy and ntp settings`).

Valid FQDN
~~~~~~~~~~

The Nextron Universal Installer will prompt you to verify the
FQDN which you configured during the installation of the base
system (see :ref:`setup/network:network configuration`). This
is needed in order for your Management Center to communicate
via a HTTPs connection with the Analysis Cockpit. The Management
Center will use the FQDN of your Analysis Cockpit to connect to
it and also verify the Common Name of the certificate to verify its
authenticity. If there is a mismatch the Management Center will
not be able to sync events with the Analysis Cockpit.

If the displayed FQDN is not correct, you can change it by
clicking on the ``View FQDN Change Instructions`` button.
This will open a dialog with instructions on how to change
the FQDN of your server. Once you have changed the FQDN,
you can continue with the installation.

.. figure:: ../images/setup_nextronInstaller-fqdn.png
   :alt: FQDN Verification of the Universal Installer

Proxy and NTP Settings
~~~~~~~~~~~~~~~~~~~~~~

If you need to configure a proxy or change the NTP settings
of your system, you can do so by clicking on the ``Settings``
button in the left menu of the Nextron Universal Installer.

.. figure:: ../images/setup_nextronInstaller-settings.png
   :alt: Settings of the Universal Installer

If you configured a proxy during the ISO installation, those
settings will be carried over into the Universal Installer.
The settings will also be carried over into your Analysis Cockpit.
The same goes for NTP.

Diagnostic Pack
~~~~~~~~~~~~~~~

In case of errors or problems during the installation, you can
download a diagnostic pack by navigating to the ``Diagnostics``
tab in the left menu of the Nextron Universal Installer. Click
on the ``Download Diagnostic Pack`` button to download the
diagnostic pack. You can then send the diagnostic pack to our
support team for further analysis.

.. figure:: ../images/setup_nextronInstaller-diagnostics.png
   :alt: Diagnostics of the Universal Installer