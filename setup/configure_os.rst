.. Index:: Configure the OS

Changing the IP-Address
-----------------------

The Analysis Cockpit's IP-Address can be changed in **/etc/network/interfaces**.
The IP is configured with the ``address`` variable.

.. code-block:: console

   nextron@asgard-ac:~$ sudo vi /etc/network/interfaces

.. code-block::

   auto ens32
   iface ens32 inet static
      address 172.16.2.7/24
      gateway 172.16.2.254
      dns-nameservers 172.16.20.20

You can now restart ``networking.service`` to apply the changes.

.. code-block:: console

   nextron@asgard-ac:~$ sudo systemctl restart networking.service

.. important::
   - The network interface might have a different name, so pay attention
     to the name (in this example ``ens32``).

   - If restarting the ``networking.service`` is throwing an error, you
     you can restart the server

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
