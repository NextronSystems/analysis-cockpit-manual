.. Index:: Backend

Invisible (Backend)
-------------------

Filter Templates
^^^^^^^^^^^^^^^^

The Analysis Cockpit uses so-called filter templates that describe which
fields in which event types are specific enough to be used in a filter
that can be used to automatically group events.

These groups can be identified by a common so-called "Auto Case ID"
(formerly Group ID). See the respective entry in this Glossary.

The filter templates are static and predefined.

E.g., a typical filter template states that for events in the Module
``Filescan``, the fields **FILE** and **SHA1** are sufficiently specific to group
events based on equal values in these two fields.
