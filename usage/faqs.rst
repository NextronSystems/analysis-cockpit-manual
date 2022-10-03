FAQs
====

It seems that events are not visible or have been lost. What can I do to verify that they’re still in the database?
-------------------------------------------------------------------------------------------------------------------

First, check your date range picker.

Very often, analysts forget to set it to the right time frame and old
events accidentally disappear from the view.

Secondly, make sure you’re using the search in the ``Events`` section and
not the ``Baselining`` section.

I have created a case but it seems that no new incoming events are assigned to that existing case. How can I check what’s wrong?
--------------------------------------------------------------------------------------------------------------------------------

The first thing that you should check are the **auto\_case\_ids** of the
events in that case (``Cases`` > ``Open Case`` > ``Events`` > ``auto_case_id`` Panel).

If they are distributed as in the following screenshot, it seems that
auto-casing doesn’t work on this case.

.. figure:: ../images/image95.png
   :target: ../_images/image95.png
   :alt: Auto Case ID

This case doesn’t have groupable contents and uses only so-called
"Dynamic Auto Case IDs", which are used whenever the Analysis cockpit
was unable to find a suitable filter template to create usable filters
for this type of events.

Also check the grouping criteria of that case:

``Cases`` > ``Open Case`` > Tab ``Grouping Criteria``

What are the conditions defined to assign new events to that case?

Where are Scan Logs on the system located?
----------------------------------------------------

You can find the Scan Logs  in ``/var/lib/nextron/analysiscockpit3/events``. In this folder you will find three different naming schemes:

* **.txt.gz** - Logs which are not imported yet

* **.txt.gz.ok** - Logs which were imported successfully

* **.txt.gz.problem** - Logs which could not be imported correctly due to an error

If you need to manually investigate logs which failed during the import (.gz.problem), you can do so by copying the files to a different location (*/tmp* for example) and remov the suffix .problem. After that you can use ``gunzip`` to extract the log and inspect it. Most likely you will find that the file did not transfer correctly over to the Analysis Cockpit. This can be seen if you open the file and scroll to the very end. In this case the file will just end in the middle of a log line.

To import the problematic scan result, you can copy the original file from the scanned system and upload it directly to the Analysis Cockpit (Scans -> Upload Scan(s)). You should find the timestamp and the hostname of the scanned system in the very top of the problematic log file.

After you are done with the manual upload, make sure to delete the .gz.problem file to free some space.

What is the password used to protect file downloads?
-----------------------------------------------------------------------------------------
Artefacts uploaded to a case might be malware. To ensure the file is not automatically deleted
by antivirus or executed by an unknowing user, we zip all files in the attachments and
encrypt the ZIP file with a default password. The default password ``infected`` can be 
used to extract the file.

My disk is getting full soon. What options do I have?
------------------------------------------------------

If your disk is already at or close to 100% and AC no longer works properly, see section
:ref:`Recover from a Full Disk<usage/typical-pitfalls:Recover from a Full Disk>`.

In other cases check section :ref:`Regain Disk Space<usage/maintenance:Regain Disk Space>`.


I am using a Reverse Proxy to access the Analysis Cockpit. What do I have to take care of?
------------------------------------------------------------------------------------------

The Analysis Cockpit partially uses large URLs to communicate with its backend.
Proxy server usually do not allow arbitrary large URLs.

In case of nginx the default header size is 8k (see http://nginx.org/en/docs/http/ngx_http_core_module.html#large_client_header_buffers).
If you want to use the Analyst Cockpit behind a nginx reverse proxy, you need to increase the *large_client_header_buffer*.
A size of 100k should be sufficient. Also the HTTP2 protocol has to be disabled.

A minimal example configuration for nginx looks as follows:

.. code::

    server {
       listen 443 ssl; # !! no http2 !!
       ssl_certificate /path/to/your/certificate.crt;
       ssl_certificate_key /path/to/your/private.key;
       location / {
          proxy_pass https://analysis-cockpit.your.org;
          proxy_set_header Host $http_host;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
       }
       large_client_header_buffers 4 100k; # increase maximal allowed URL length
    }


I am using Internet Explorer and the Analyst Cockpit seems to run into a timeout. What can I do?
------------------------------------------------------------------------------------------------

Modern browsers (e.g. Firefox, Chrome, Edge, Safari) support large URLs. Internet Explorer does not. If you want to access the Analyst Cockpit and all its features, you need to switch your browser.

