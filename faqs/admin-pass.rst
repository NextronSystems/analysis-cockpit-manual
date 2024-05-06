.. Index:: Admin Password reset

Admin Password reset
--------------------

**Q: I forgot my admin password and lost access to the WebUI. How do I reset the admin user password?**

If you've lost the password of the local ``admin`` user (Web GUI) but still have access
the system via SSH, you can reset it via command line using the following command.

.. code-block:: console

   nextron@cockpit:~$ sudo asgard-analysis-cockpit set-password
   Please enter password for user `admin`: 
   Please re-enter password for user `admin`: 
   2024-04-10T08:26:29Z [INF] SET_PASSWORD: Database initialized..
   2024-04-10T08:26:29Z [INF] SET_PASSWORD: password successfully updated
