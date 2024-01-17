.. Index:: Disabling Assignment Logs

Disabling Assignment Logs
-------------------------

**Q: My assignment Logs on the server are growing quickly, how can
I turn them off**

The assignment logs located at ``/var/lib/nextron/analysiscockpit3/log/assignment.log``
write warnings and errors for the ``Optimize`` function of the Cockpit.

If you have the feeling that the log is filling up too quickly, you can
turn off those logs completely. It is advised to try and see what the problem
is before turning off the log completely, as this might indicate an underlying
issue.

Run the following command on your Analysis
Cockpit (warning: this will restart your Analysis Cockpit. If you do not
want to restart the Analysis Cockpit, you can run the second command at a
later time):

.. code-block:: console

   nextron@cockpit:~$ echo "REPLACE INTO config VALUES ('write-assignment-log','false')" | sudo mysql analysiscockpit3
   nextron@cockpit:~$ sudo systemctl restart analysiscockpit3.service

To turn back on the ``assignment.log``, run the following command:

.. code-block:: console

   nextron@cockpit:~$ echo "REPLACE INTO config VALUES ('write-assignment-log','true')" | sudo mysql analysiscockpit3
   nextron@cockpit:~$ sudo systemctl restart analysiscockpit3.service
