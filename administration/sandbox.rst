.. Index:: Sandbox Integration

Sandbox Integration
-------------------

You can configure your Analysis Cockpit to upload files to a local sandbox.
Currently you can use `CAPEv2 <https://github.com/kevoreilly/CAPEv2>`_
(recommended) or `Cuckoo <https://cuckoosandbox.org/>`_.

Additionally, you can look at the following ``python`` file and write
your own connector, for a different sandbox, if you need to:
``/etc/nextron/analysiscockpit3/sandbox/connector/capev2.py``

.. note:: 
   This section only focuses on the integration of your Analysis Cockpit
   with an existing sandbox. We will not cover how to set up the sandbox.

Analysis Cockpit Sandbox Configuration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the web view of your Analysis Cockpit, navigate to ``Sandbox`` > ``Sandboxes``.
Click ``Add Sandbox`` in the top right corner. Keep the ``Name`` short and add a
proper ``Description``.

.. figure:: ../images/cockpit_add_sandbox.png
   :alt: Adding a new Sandbox

   Adding a new Sandbox

Once you click ``Add`` the page will display an API token. Copy this token, we will need it later.

.. figure:: ../images/cockpit_sandbox_token.png
   :alt: Sandbox API Token

   Sandbox API Token

Connect to your Analysis Cockpit via SSH and follow the steps below.

Change the user to the root user:

.. code:: console

   nextron@cockpit:~$ sudo su -
   [sudo] password for nextron:
   root@cockpit:~# 

We change into the configuration directory of the sandbox:

.. code:: console
   
   root@cockpit:~# cd /etc/nextron/analysiscockpit3/sandbox/connector
   root@cockpit:/etc/nextron/analysiscockpit3/sandbox/connector#

Here you can find multiple files and folders. The ``.py`` and ``.ini``
files represent each the type of sandbox you want to integrate. In
this example, we will configure the CAPv2 sandbox with our Analysis Cockpit.

.. code:: console
   
   root@cockpit:/etc/nextron/analysiscockpit3/sandbox/connector# ls -lA
   total 36
   drwxr-xr-x 2 analysiscockpit3 analysiscockpit3 4096 Apr 21 15:27 analysiscockpit
   -rw-r--r-- 1 analysiscockpit3 analysiscockpit3  253 Mär  3 11:20 capev2.ini
   -rw-r--r-- 1 analysiscockpit3 analysiscockpit3 4934 Mär  3 11:20 capev2.py
   -rw-r--r-- 1 analysiscockpit3 analysiscockpit3  278 Mär 28  2021 cuckoo.ini
   -rw-r--r-- 1 analysiscockpit3 analysiscockpit3 9867 Nov 17  2020 cuckoo.py
   drwxr-xr-x 2 analysiscockpit3 analysiscockpit3 4096 Apr 14 15:29 sandboxapi

Here we have two files which are of relevance for us:

- capev2.ini

  - This holds the configuration for both the sandbox and your Analysis Cockpit

- capev2.py
      
  - This has the systemd configuration to create the actual service on the system (we don't change anything in here)

Change the ``capev2.ini`` with a text editor. The important lines, which need to
be changed accordingly to your environment, are marked:

.. code-block:: console
   
   root@cockpit:/etc/nextron/analysiscockpit3/sandbox/connector# nano capev2.ini

.. code-block:: ini
   :linenos:
   :emphasize-lines: 6-10, 16-17

   [DEFAULT]
   debug = yes
   tmp_directory = /var/lib/nextron/analysiscockpit3/sandbox/capev2

   [capev2]
   protocol = http
   host = 192.168.0.50
   port = 8000
   token = <your CAPEv2 API token here>
   verify = no
   all = yes
   html = yes

   [analysis-cockpit]
   host = localhost:443
   apikey = <your API Key here>
   verify = no

For lines 6-10, please fill the information accordingly. ``host`` is the IP/FQDN
of your sandbox. ``port`` is the listening port of the web interface of your sandbox.
``token`` is the API token generated in the user management of your sandbox.
``verify`` is for verification of the TLS certificate (if you don't use TLS or don't
want to verify the certificate, set this option to ``no``).

For lines 16-17 you have to set the ``apikey`` of your Analysis Cockpit (see "Add
Sandbox" step in the beginning of this section) and ``verify``, which can be set to
``no``; this will verify the TLS certificate.

Save your files after you made your changes.

Now you have to create a new directory and give the ``analysiscockpit3`` user permission:

.. code:: console
   
   root@cockpit:/etc/nextron/analysiscockpit3/sandbox/connector# mkdir -p /var/lib/nextron/analysiscockpit3/sandbox/capev2
   root@cockpit:/etc/nextron/analysiscockpit3/sandbox/connector# chown -R analysiscockpit3: /var/lib/nextron/analysiscockpit3

We need to create a systemd service file in order to run the CAPEv2 connector on your
Analysis Cockpit. Below you can find a predefined service file which we will use: 

.. code-block:: ini
   :linenos:

   [Unit]
   Description=CAPEv2 Sandbox Connector
   After=network.target
   
   [Service]
   ExecStart=/usr/bin/python3 /etc/nextron/analysiscockpit3/sandbox/connector/capev2.py
   Restart=on-failure
   User=analysiscockpit3
   Group=analysiscockpit3
   SyslogIdentifier=capev2_connector
   
   [Install]
   WantedBy=multi-user.target

Now we run the following command and paste the content from the output earlier into it:

.. code-block:: console

   root@cockpit:/etc/nextron/analysiscockpit3/sandbox/connector# nano /lib/systemd/system/capev2-connector.service

The file should now look like this:

.. code-block:: console

   root@cockpit:/etc/nextron/analysiscockpit3/sandbox/connector# cat /lib/systemd/system/capev2-connector.service
   [Unit]
   Description=CAPEv2 Sandbox Connector
   After=network.target

   [Service]
   ExecStart=/usr/bin/python3 /etc/nextron/analysiscockpit3/sandbox/connector/capev2.py
   Restart=on-failure
   User=analysiscockpit3
   Group=analysiscockpit3
   SyslogIdentifier=capev2_connector

   [Install]
   WantedBy=multi-user.target

   root@cockpit:/etc/nextron/analysiscockpit3/sandbox/connector#

Now that the systemd service file is created, we need to activate it. Run the following command:

.. code-block:: console

   root@cockpit:/etc/nextron/analysiscockpit3/sandbox/connector# systemctl daemon-reload && systemctl enable capev2-connector && systemctl start capev2-connector
   Created symlink /etc/systemd/system/multi-user.target.wants/capev2-connector.service → /lib/systemd/system/capev2-connector.service.
   root@cockpit:/etc/nextron/analysiscockpit3/sandbox/connector# 

The connection to your sandbox should work now. You can see the ``capev2.log`` for debug output and troubleshooting:

.. code-block:: console

   root@cockpit:~# tail /var/lib/nextron/analysiscockpit3/sandbox/capev2/capev2.log
   22-11-15 12:07:46 DEBUG: Starting new HTTPS connection (1): localhost:443
   22-11-15 12:07:46 DEBUG: https://localhost:443 "GET /api/sandboxes/a/reports/pending?limit=10&offset=0 HTTP/1.1" 200 13
   22-11-15 12:07:46 DEBUG: no pending references found
   22-11-15 12:08:46 DEBUG: Starting new HTTP connection (1): 192.168.0.50:8000
   22-11-15 12:08:46 DEBUG: http://192.168.0.50:8000 "GET /apiv2/cuckoo/status/ HTTP/1.1" 200 289
   22-11-15 12:08:46 DEBUG: Starting new HTTPS connection (1): localhost:443
   22-11-15 12:08:46 DEBUG: https://localhost:443 "GET /api/sandboxes/a/get-sha256s-without-report?limit=10 HTTP/1.1" 200 13
   22-11-15 12:08:46 DEBUG: Starting new HTTPS connection (1): localhost:443
   22-11-15 12:08:46 DEBUG: https://localhost:443 "GET /api/sandboxes/a/reports/pending?limit=10&offset=0 HTTP/1.1" 200 13
   22-11-15 12:08:46 DEBUG: no pending references found
   root@cockpit:~# 


Analysis Cockpit Sandbox Usage
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Once your sandbox is set up and running, you can see the status of it in the sandbox view (Last Seen):

.. figure:: ../images/cockpit_sandbox_view.png
   :alt: Sandbox View in the Analysis Cockpit

If you wish to enable automatic scanning for uploaded files
(`Bifrost <https://asgard-manual.nextron-systems.com/en/latest/usage/administration.html#bifrost-quarantine>`_),
you can do so by pressing the play button to the right hand side.

In the ``Files`` view you can see previously analyzed files or upload files for analysis by yourself:

.. figure:: ../images/cockpit_sandbox_file_upload.png
   :alt: File View in the Analysis Cockpit

.. note:: 
   If you did not enable ``auto mode`` of your configured sandbox, you have
   to manually add the file for scanning in here. You can do this by pressing
   the ``Scan file with sandbox`` button to the right of your file.

After your file has been uploaded, you have to wait until your sandbox
is finished with analyzing the file. Change to the ``Reports`` view
to see the status of the files.

.. figure:: ../images/cockpit_sandbox_reports_view1.png
   :alt: Reports View in the Analysis Cockpit

Once the file was analyzed and the reports are ready, you will see that
the status of the file changed to ``SUCCESS`` and the buttons ``REPORT``,
``JSON`` and ``HTML`` can be clicked.

.. figure:: ../images/cockpit_sandbox_reports_view2.png
   :alt: Reports View in the Analysis Cockpit

You can now download the report.