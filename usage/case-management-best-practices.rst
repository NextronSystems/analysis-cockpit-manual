Case Management Best Practices
==============================

This section assumes, that a 2-Level model as described in :ref:`chapter
6.3. Understanding Users, Roles, Rights and Case Status <usage/basic-concepts:Understanding Users, Roles, Rights and Case Status>` is used.

The following actions will be explained:

-  Opening a case

-  Handing a case over to the next level

-  Closing a case

-  Reviewing the rules that add future logs to this case (Grouping
   Criteria)

Open a Case for Editing
-----------------------

The picture below shows the Case Management view with cases that have
been created with the ``Auto Case`` feature.

.. figure:: ../images/image84.png
   :target: ../_images/image84.png
   :alt: Opening a Case for editing

   Opening a Case for editing

In our example a Level 1 Analyst would now pick one of these open cases
and set the Status to "Level 1 Working" by opening the case (clicking on
the magnifier button), modifying the status and then clicking ``Update``.

.. figure:: ../images/image85.png
   :target: ../_images/image85.png
   :alt: Change Status

   Change Status

Now the logs within the case can be analyzed and results can be
documented in the assessment field. Recommendations can be set from the
canned recommendations list. Columns can be faded in and out and
comments can be added.

Case Dispatching
----------------

Let’s assume, our Level 1 Analyst concludes, that this is a "Legitmate Anomaly". 
He will now set the status to "Level 1 Finished" and update
the case. After setting the case to "Level 1 Finished" the case becomes
visible to the Level 2 Analyst.

Closing a Case
--------------

Let’s assume, that a Level 2 Analyst now picks one of the cases in
status "Level 1 Finished" and starts working on this case.

In this respect we assume, that something suspicious has been found,
that needs further analysis by the system administration team. In most
organizations this will be controlled through the organization’s action
request or ticketing system. So, we assume, that we will close the case
in the Analysis Cockpit as it is progressed in another system. Thus, the
status is changed to closed and the case gets updated.

.. figure:: ../images/image86.png
   :target: ../_images/image86.png
   :alt: Closing a Case

   Closing a Case

.. note::
  The Analysis Cockpit provides interfacing to action-request and
  external ticketing systems using the API.

Generate and Review auto\_case\_ids
-----------------------------------

These auto\_case\_ids can be reviewed in the ``Grouping Criteria`` section
of the case.

.. figure:: ../images/image87.png
   :target: ../_images/image87.png
   :alt: Reviewing Grouping Criteria

   Reviewing Grouping Criteria

In our example, three auto\_case\_ids were added that match all 1,000
loglines. In the future all incoming logs, that match one of the three
“Detailed Reasons” will be added to this case directly and will not show
up in the Log Management section.

Limitations
^^^^^^^^^^^

There are limitations to the visibility of grouping criteria. Grouping
Criteria are only calculated for Alerts and Warnings. For all other
types of logs (Notices, Info, Error) auto\_case\_ids are not calculated,
so every logline gets its own highly specific filter that matches future
occurrences of exactly the same logline but will not do any kind of
generic matching. These highly specific filters are not displayed in the
case for simplicities sake.

In rare cases the Analysis Cockpit will find it difficult to calculate
auto\_case\_ids even for Alerts and Warnings. These logs will get tagged
with ``optimized\_template=false``. In this case, the behavior is like for
Notices, Info and Error messages. Grouping Criteria will not show up as
it will be one highly specific filter per logline.

More Information about Cases
----------------------------

The ``Assets`` tab of a case shows assets that have contributes at least
one log line to this case. In this example 1.169 assets are affected.
All of them have the same operating system “Debian GNU/Linux 9
(stretch)”.

.. figure:: ../images/image88.png
   :target: ../_images/image88.png
   :alt: Case - Assets Tab

   Case – Assets Tab

The ``Scans`` tab shows information about the scans (scan ID, group scan
ID) the events have been found in.

.. figure:: ../images/image89.png
   :target: ../_images/image89.png
   :alt: Case - Scans tab

   Case – Scans tab

In the ``Comments / Attachments`` tab you can add comments and attachments
to this case. Attachments can be used to pass additional information to
members of the analysis team (e.g. memory dump for further analysis).

.. figure:: ../images/image90.png
   :target: ../_images/image90.png
   :alt: Case - Comments / Attachments tab

   Case – Comments / Attachments tab

The ``Changes`` tab shows information about changes to this case.

In other words: This your case audit log.

.. figure:: ../images/image91.png
   :target: ../_images/image91.png
   :alt: Case - Changes tab

   Case – Changes tab

Bulk Edit / Bulk Delete
-----------------------

The Analysis Cockpit features a convenient way to make certain changes
to groups of cases. Just select the case in the left column and click
the ``Bulk Edit / Bulk Delete`` button. Now you can select what you want
to change and click the ``Edit Selected Cases`` button to edit. If you
want to delete all of those selected cases, just click the 
``Delete Selected Cases`` button.

.. figure:: ../images/image92.png
   :target: ../_images/image92.png
   :alt: Bulk Edit / Bulk Delete

   Bulk Edit / Bulk Delete

In this example clicking the ``Edit Selected Cases`` Button would set the
type to "Noteworthy" and the status to 
"Level 1 Finished" for cases with
ID 392 and 393. No comments would have been added. Clicking the ``Delete Selected Cases``
button would delete those cases. As a consequence of
deleting the cases all logs within the deleted cases would show up in
the baselining section.

