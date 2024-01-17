.. Index:: Admin Password reset

Admin Password reset
--------------------

**Q: I forgot my admin password and lost access to the WebUI. How do I reset the admin user password?**

If you've lost the password of the local ``admin`` user (Web GUI) but still have access
the system via SSH, you can reset it via command line using the following command.

.. code-block:: console

   nextron@cockpit:~$ sudo mysql analysiscockpit -e "UPDATE users SET password = '7951GYqdAjLAoO1NaQu1ManJDIk' WHERE name = 'admin';"

This resets the password to ``admin``. You should then change that password immediately.
