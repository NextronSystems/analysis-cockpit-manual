.. Index:: Multi Factor Authentication reset

Multi Factor Authentication reset
---------------------------------

**Q: How do I reset Multi Factor Authentication for a specific user**

If you or another user lost their second factor (MFA) to log into the
ASGARD Web UI, you can reset the users MFA Settings with the following
command (in this example we assume that the user is called ``john``):

.. code-block:: console

   nextron@cockpit:~$ sudo mysql analysiscockpit3 --execute "UPDATE users SET tfa_valid = 0 WHERE name = 'john';"
