.. index:: Resetting TLS/SSL Certificates

Resetting TLS/SSL Certificates
------------------------------

**Q: How can I reset TLS/SSL Certificates?**

The Analysis Cockpit ships with a self-signed certificate for its web interface
that expires after 182 days. If you do not use your own CA
infrastructure and want to renew the certificate or want to revert
from a broken state, you can recreate a self-signed certificate.
To do so log in using SSH and execute:

.. code-block:: console

   nextron@asgard:~$ sudo openssl req -new -newkey rsa:4096 -days 182 -nodes -x509 -subj "/O=Nextron Systems GmbH/CN=$(hostname --fqdn)" -keyout /etc/asgard-analysis-cockpit/http.key -out /etc/asgard-analysis-cockpit/http.pem

You need to restart the Analysis Cockpit in order for the changes to take effect.

.. code-block:: console

   nextron@asgard:~$ sudo systemctl restart asgard-analysis-cockpit.service
