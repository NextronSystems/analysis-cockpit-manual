Known Issues
============

AAC#001: Nested LDAP Groups not working
---------------------------------------

Using nested groups in your LDAP/AD will result in no users because the query will fail.

AAC#001: Workaround
~~~~~~~~~~~~~~~~~~~

Change your LDAP GroupFilter to the following:

.. code-block:: none
    
    (&(objectCategory=group)(objectClass=group)(member:1.2.840.113556.1.4.1941:=%s))

AAC#001: Status
~~~~~~~~~~~~~~~

Fixed in next ASGARD version.