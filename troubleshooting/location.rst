.. Index:: Location of Scan Logs

Location of Scan Logs
---------------------

**Q: Where are Scan Logs on the system located?**

You can find the Scan Logs  in ``/var/lib/asgard-analysis-cockpit/events``.
In this folder you will find three different naming schemes:

* **.txt.gz** - Logs which are not imported yet

* **.txt.gz.ok** - Logs which were imported successfully

* **.txt.gz.problem** - Logs which could not be imported correctly due to an error

If you need to manually investigate logs which failed during the import (.gz.problem),
you can do so by copying the files to a different location (``/tmp`` for example)
and remove the suffix .problem. After that you can use ``gunzip`` to extract the log
and inspect it. Most likely you will find that the file did not transfer correctly
over to the Analysis Cockpit. This can be seen if you open the file and scroll to the
very end. In this case the file will just end in the middle of a log line.

The Logs can be imported into the Cockpit via the ``Scans`` menu. Select the Asset which
had a problem with the log transfer and click ``Request Events``. This will transfer
the Events from the corresponding ASGARD. You can also use the Fields **Log Requested**,
**Log Received** and **Log Received Error** to filter and look for other failed log transmissions.
