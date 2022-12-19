Setup Guide
===========

Create a New ESX VM and Mount the ISO
-------------------------------------

Create a new VM with your virtualization software. In this case, we will
use VMWare ESX managed through a VMWare VCenter.

The new VM must be configured with a Linux base system and Debian
GNU/Linux 10 (64 bits) as target version. It is recommended to upload
the Nextron Universal Installer ISO to an accessible datastore and mount
the same to your newly created VM.

.. figure:: ../images/image4.png
   :target: ../_images/image4.png
   :alt: Create a new virtual Machine I

.. figure:: ../images/image5.png
   :target: ../_images/image5.png
   :alt: Create a new virtual Machine II

.. figure:: ../images/image6.png
   :target: ../_images/image6.png
   :alt: Create a new virtual Machine III

.. figure:: ../images/image7.png
   :target: ../_images/image7.png
   :alt: Create a new virtual Machine IV 

   Create a new virtual Machine

Please make sure to select a suitable v-switch or physical interface
that reflects the IP address scheme you are planning to use for the new
ASGARD.

Analysis Cockpit Installation
-----------------------------

Start the installation confirming the only available option in the boot
loader screen.

The installer then loads the additional components from the ISO image
and lets you select a location and language.

.. figure:: ../images/image8.png
   :target: ../_images/image8.png
   :alt: Starting the installation

   Starting the installation

.. figure:: ../images/image9.png
   :target: ../_images/image9.png
   :alt: Choosing language, location and locales I

.. figure:: ../images/image10.png
   :target: ../_images/image10.png
   :alt: Choosing language, location and locales II

.. figure:: ../images/image11.png
   :target: ../_images/image11.png
   :alt: Choosing language, location and locales III

.. figure:: ../images/image12.png
   :target: ../_images/image12.png
   :alt: Choosing language, location and locales IV

   Choosing language, location and locales

If DHCP is available, network parameters will be configured
automatically.

Without DHCP, ASGARD proceeds with the manual network configuration
dialogue.

Network Configuration
---------------------

The next step prompts for a hostname for the device. After entering a
hostname and clicking ``Continue``, it also prompts for the Domain Name.
After this Information is submitted, the Installer tries to get network
configurations from a DHCP-Server. If there is none to be found, it will
prompt for a static IP-Configuration.

.. figure:: ../images/image13.png
   :target: ../_images/image13.png
   :alt: Network Configuration I

.. figure:: ../images/image14.png
   :target: ../_images/image14.png
   :alt: Network Configuration II

Enter the IP address that Analysis Cockpit should use and optimally
directly add a netmask in CIDR notation. (see below) If you don’t append
the netmask, you’ll be asked for a network mask in the following
dialogue.

.. figure:: ../images/image15.png
   :target: ../_images/image15.png
   :alt: Network Configuration - IP addresses

   Network Configuration - IP addresses

.. figure:: ../images/image16.png
   :target: ../_images/image16.png
   :alt: Network Configuration - Enter the DNS server addresses 

   Network Configuration – Enter the DNS server addresses

.. figure:: ../images/image17.png
   :target: ../_images/image17.png
   :alt: Network Configuration - Enter the Gateway

   Network Configuration - Enter the Gateway

.. figure:: ../images/image18.png
   :target: ../_images/image18.png
   :alt: Network Configuration - Enter the Hostname 

   Network Configuration - Enter the Hostname

.. figure:: ../images/image19.png
   :target: ../_images/image19.png
   :alt: Network Configuration - Enter the Domain name

   Network Configuration - Enter the Domain name

.. important::
   Make sure that the combination of hostname and domain creates an FQDN 
   that can be resolved from the endsystems on which you intend to
   install the ASGARD agents. If you’ve configured a FQDN (hostname +
   domain) that cannot be resolved on the clients, no agent will be able
   to find and reconnect to the ASGARD server.

Choosing a password
-------------------

.. figure:: ../images/setup_password.png
   :target: ../_images/setup_password.png
   :alt: Choosing a password

   Choosing a password for the nextron user

Partitioning of the Hard Disk
-----------------------------

Finally, confirm the settings, select “Yes” and click “Continue”.

.. figure:: ../images/image20.png
   :target: ../_images/image20.png
   :alt: Partition Disks - Write changes to disks 

   Partition Disks – Write changes to disks

.. figure:: ../images/image21.png
   :target: ../_images/image21.png
   :alt: Partition disks - Select disk to partition

   Partition disks – Select disk to partition

Proxy Configuration
-------------------

If you are using a proxy to access the Internet, enter the proxy details
in the next step. Please note, Internet connectivity is required for the
next step – the installation of the ASGARD Analysis Cockpit service.

.. figure:: ../images/image22.png
   :target: ../_images/image22.png
   :alt: Proxy Configuration 

   Proxy Configuration

The proxy configuration supports unauthorized access and HTTP Auth.

e.g.

http://our-proxy.local:8080

http://username:password@our-proxy.local:8000

Install the Analysis Cockpit Services
-------------------------------------

The base installation is now complete. In the next step we’ll install
the Analysis Cockpit service.

Important: Internet connectivity is required for this step.

Use the VMWare console or SSH to the appliance using the user
**nextron** and default password **nextron**.

To start the Analysis Cockpit installation run the following command:

.. code:: bash
   
   sudo nextronInstaller -cockpit

Important: use an upper case “i” in the word installer

After the installer has completed its operations successfully, the
system is ready to be used.

.. figure:: ../images/image23.png
   :target: ../_images/image23.png
   :alt: Message upon successful completion

   Message upon successful completion

Note that the FQDN shown after “https://” has to be resolvable by the
connected ASGARD Management Centers and users that try to access the
Analysis Cockpit.

Changing the IP-Address
-----------------------

The Analysis Cockpit's IP-Address can be changed in **/etc/network/interfaces**. The IP is configured with the ``address`` variable.

.. code-block:: console

   nextron@asgard-ac:~$ sudo vi /etc/network/interfaces

.. code-block::

   auto ens32
   iface ens32 inet static
   address 192.0.2.7
   netmask 255.255.255.0
   gateway 192.0.2.254

Important: There might be a case where the name of the network adaptor (in this example: ``ens32``) can vary.

The new IP can be applied with the command **sudo systemctl restart networking**

Verifying DNS Settings
^^^^^^^^^^^^^^^^^^^^^^

To verify if ASGARD is using the correct DNS Server, you can inspect the file ``/etc/resolv.conf``:

.. code-block:: console

   nextron@asgard-ac:~$ cat /etc/resolv.conf 
   search example.org
   nameserver 172.16.200.2

If you see errors in this configuration, you can change it with the following command:

.. code-block:: console

   nextron@asgard-ac:~$ sudoedit /etc/resolv.conf
