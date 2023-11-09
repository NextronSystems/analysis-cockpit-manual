.. Index:: System Settings

TLS Certificate Installation
----------------------------

Instead of using the pre-installed self-signed TLS Certificate,
users can upload their own TLS Certificate for ASGARD. 

In order to achieve the best possible compatibility with the
most common browsers, we recommend using the system's FQDN
in both fields ``Common Name`` AND ``Hostnames``.

.. figure:: ../images/cockpit_new_csr.png
   :alt: Generate a Certificate Signing Request (CSR)

   Generate a Certificate Signing Request (CSR)

.. hint::
   Please note that generating a CSR on the command line is not supported.   

The generated CSR can be used to generate a TLS Certificate.
Subsequently, this TLS Certificate can be uploaded in the ``Settings`` > ``TLS`` section.

.. figure:: ../images/cockpit_upload_certificate.png
   :alt: Upload a TLS Certificate

   Upload a TLS Certificate

Configure LDAP
--------------

The LDAP tab in the ``Users and Roles`` section lets you configure an LDAP server
and define mappings for LDAP groups to roles within the Analysis
Cockpit.

The figures below illustrate options of a possible LDAP configuration.

.. figure:: ../images/cockpit_ldap.png
   :alt: Configure LDAP 

   Configure LDAP

Configure Notifications
-----------------------

As described in :ref:`basic-concepts/cases:cases and log processing`, the
Analysis Cockpit is able to forward logs to a SIEM system in case
this particular log line was added automatically to a case with the type "Incident".

The ``Notifications`` tab allows you to define custom notifications for
event assignments (Event Assignment Notifications). It is recommended to
at least configure an Event Assignment Notification for events that get
added to existing Incident cases.

Additionally, notifications can be defined for changes to cases (Case
Change Notifications), so Level 2 analysts can get notified if a case
gets added to their in-queue (e.g., Finished Level 1).

The notification itself can be a syslog message or an email. In order to
use email for notifications you have to setup an email account in the
``Mail Account`` Tab. Additionally webhook support has been added to
facilitate interfacing to services like Slack.

.. figure:: ../images/cockpit_notifications.png
   :alt: Case Management- Notifications

   Case Management- Notifications

.. note::
   The Analysis Cockpit will collect all triggering events and send only
   one email every 15 minutes. Syslog and Webhooks are triggered in real
   time for every single event.

Additionally, you can see the notifications in the top right corner (bell
icon) and inspect them. You will see all ``Unread`` notifications, which can
be ``Acknowledged`` by selecting one or more notification and clicking
``Acknowledge``. Only ``Unread`` notifications will show up in the top right
status bar of the Cockpit.

.. figure:: ../images/cockpit_notifications2.png
   :alt: UI Notifications

   UI Notifications

Configure Event Assignment Notifications
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To configure log notifications, click the 
``Add Event Assignment Notification`` button in the Notifications Tab of the 
``Settings`` section.
This leads you to a form that allows you to set a name for your
notification, the notification type (syslog, email, webhook or
notification within the Analysis Cockpit) and the condition that will
trigger your notification.

.. figure:: ../images/cockpit_event_assignment_notification.png
   :alt: Event Assignment Notification

   Event Assignment Notification

Configure Case Change Notifications
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To configure Case Change Notifications, click the 
``Add Case Change Notification`` button in the Notifications Tab of the 
``Settings`` section.
This leads you to a form that allows setting a name for your
notification, the notification type (syslog, email, webhook or
notification within the Analysis Cockpit) and the condition that will
trigger your notification.

.. figure:: ../images/cockpit_case_assignment_notification.png
   :alt: Case Change Notification 

   Case Change Notification
