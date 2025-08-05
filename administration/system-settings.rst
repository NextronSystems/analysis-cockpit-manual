.. Index:: System Settings

TLS Certificate Installation
----------------------------

``>Settings\System\TLS``

Instead of using the pre-installed self-signed TLS Certificate,
users should upload their own TLS Certificate for ASGARD. This
will avoid browser warnings when navigating to your Analysis
Cockpit's web interface.

In order to achieve the best possible compatibility with the
most common browsers, we recommend using the system's FQDN
in both fields ``Common Name`` AND ``Hostnames``.

You can click ``Generate CSR`` to open the following modal which
lets you specify the information needed for the CSR.

.. figure:: ../images/cockpit_new_csr.png
   :alt: Generate a Certificate Signing Request (CSR)

   Generate a Certificate Signing Request (CSR)

.. hint::
   Please note that generating a CSR on the command line is not supported.   

The generated CSR can be used to generate a TLS Certificate.
Subsequently, this TLS Certificate can be uploaded in the in
the same section of your Analysis Cockpit.

.. figure:: ../images/cockpit_upload_certificate.png
   :alt: Upload a TLS Certificate

   Upload a TLS Certificate

Configure LDAP
--------------

``>Settings\Users and Roles\LDAP``

This section lets you configure an LDAP server and define mappings between
LDAP groups and roles within the Analysis Cockpit.

.. figure:: ../images/cockpit_ldap1.png
   :alt: Configure LDAP 

   Configure LDAP

.. figure:: ../images/cockpit_ldap2.png
   :alt: Configure LDAP 

   Configure LDAP

Cockpit Notifications
---------------------

``>Settings\Case Management\Notifications``

You can define custom notifications for the following types:

- **Case Intelligence Match**
  
  * Case Intelligence Notifications are triggered when incoming events
    match a template for the first time. You can configure what kind
    of suggested cases trigger a notification, based on the case's type.

- **Case Change**

  * Case Change Notifications are triggered when a new case is created
    or an existing case is updated. You can configure what kind of cases
    trigger a notification, based on the case's status or type.

- **Unassigned Event**

  * Unassigned Event Notifications are triggered when newly incoming events
    are not automatically assigned to existing cases. You can configure what
    kind of events trigger a notification, based on the event's level or score.

- **Event Assignment**

  * Event Assignment Notifications are triggered when newly incoming events are
    automatically assigned to existing cases. You can configure what kind of
    cases trigger a notification, based on the case's status or type.

- **New Asset Affected**

  * Asset Affected Notifications are triggered when an asset is affected by a
    case for the first time. You can configure what kind of cases trigger a
    notification, based on the case's status or type.

The notification targets can be the following:

- Application (This shows a notification in the Analysis Cockpit)
- Syslog
- Email (SMTP has to be configured to use this)
- Webhook

.. figure:: ../images/cockpit_notifications.png
   :alt: Case Management - Notifications

   Case Management - Notifications

.. note::
   The Analysis Cockpit will collect all triggering events and send only
   one email every 15 minutes. Syslog and Webhooks are triggered in real
   time for every single event.

Below you can see how **Application Notifications** look like. You can see
the bell icon in the top right corner and view all ``unread`` notifications
by clicking the icon. ``Unread`` notifications can be ``Acknowledged`` by
selecting one or more notification and clicking ``Acknowledge``. The
notification bell in the status bar will only show an indicator if you
have unread notifications.

.. figure:: ../images/cockpit_notifications_indicator.png
   :alt: UI Notification Bell

   UI Notification Bell

.. figure:: ../images/cockpit_notifications_details.png
   :alt: UI Notifications

   UI Notifications

It is recommended to configure an *Event Assignment Notification* for events
that get added to existing **Incident** cases.

Configure Notifications
^^^^^^^^^^^^^^^^^^^^^^^

``>Settings\Case Management\Notifications``

To configure notifications, click the ``Create Notification`` button.
This leads you to a form that allows you to set a name for your
notification, the notification type (syslog, email, webhook or notification
within the Analysis Cockpit) and the condition that will trigger your notification.

.. figure:: ../images/cockpit_create_notification.png
   :alt: Example Notification Creation

   Example Notification Creation

You can have multiple **Notifications**, also of the same type.