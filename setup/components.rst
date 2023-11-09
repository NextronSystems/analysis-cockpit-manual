.. Index:: Install Service

Install the Analysis Cockpit Services
-------------------------------------

The base installation is now complete. In the next step we'll install
the Analysis Cockpit service.

.. important::
   - Internet connectivity is required for this step.
   - Use an upper case ``i`` in the word ``nextronInstaller``.

Use the VMWare console or SSH to the appliance using the user
``nextron``.

To start the Analysis Cockpit installation run the following command:

.. code:: console
   
   nextron@asgard-ac:~$ sudo nextronInstaller -cockpit

After the installer has completed its operations successfully, the
system is ready to be used.

.. figure:: ../images/image23.png
   :alt: Message upon successful completion

   Message upon successful completion

Note that the FQDN shown after ``https://`` has to be resolvable by the
connected ASGARD Management Centers and users that try to access the
Analysis Cockpit.

