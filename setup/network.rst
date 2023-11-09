.. Index:: Network

Network Configuration
=====================

The next step prompts for a hostname for the device. After entering a
hostname and clicking ``Continue``, it also prompts for the Domain Name.
After this Information is submitted, the Installer tries to get network
configurations from a DHCP-Server. If there is none to be found, it will
prompt for a static IP-Configuration.

.. figure:: ../images/image13.png
   :alt: Network Configuration I

.. figure:: ../images/image14.png
   :alt: Network Configuration II

Enter the IP address that Analysis Cockpit should use and optimally
directly add a netmask in CIDR notation. (see below) If you don't append
the netmask, you'll be asked for a network mask in the following
dialogue.

.. figure:: ../images/image15.png
   :alt: Network Configuration - IP addresses

   Network Configuration - IP addresses

.. figure:: ../images/image16.png
   :alt: Network Configuration - Enter the DNS server addresses 

   Network Configuration – Enter the DNS server addresses

.. figure:: ../images/image17.png
   :alt: Network Configuration - Enter the Gateway

   Network Configuration - Enter the Gateway

.. figure:: ../images/image18.png
   :alt: Network Configuration - Enter the Hostname 

   Network Configuration - Enter the Hostname

.. figure:: ../images/image19.png
   :alt: Network Configuration - Enter the Domain name

   Network Configuration - Enter the Domain name

.. danger::
   **Important:** Make sure that the combination of hostname and domain
   creates an FQDN that can be resolved from the ASGARD Management Center(s)
   you want to connect with your Analysis Cockpit. If you've configured a
   FQDN (hostname + domain) that cannot be resolved, your ASGARDs will
   encounter an error during connection.

   This is especially important since your Analysis Cockpit will create
   some certificates during the installation, which will not contain an
   IP Address as its Subject Alternative Name (SAN), but only the FQDN!
   You will not be able to connect your ASGARD Management Center with
   your Analysis Cockpit via IP Address.
