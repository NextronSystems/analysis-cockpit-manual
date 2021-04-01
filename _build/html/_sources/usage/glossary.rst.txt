.. role:: raw-html-m2r(raw)
   :format: html

Glossary
========

Baselining
----------

The ``Baselining`` section is meant to assign all unassigned events to
cases, so that newly incoming events are immediately assigns to existing
cases and only differences to the last scan have to be reviewed. (new
malware, new signatures)

Auto Baselining
^^^^^^^^^^^^^^^

The Auto Baselining feature can be used to assign events to new and
automatically generated cases. Auto Casing makes use of the so-called
Auto Case ID, which is the same for all events of a certain type (see
Glossary > Cases > Auto Case ID for details).

Auto Baselining is typically used to quickly reduce the remaining events
in the Baselining section. It reduced the burden to manually group
together events of a similar type.

Automatically cased events can then be reviewed in the ``Cases`` section.

Auto Baselining uses a threshold that defines the minimum number of
events required in each of these automatically generated cases. A
threshold of 10 instructs the process to create only cases for groups of
at least 10 similar events. Obviously, we do not recommend using
threshold of 1, but everything higher than 1 can be reasonable.

The best practice is to start the Auto Baselining process with a
relatively high threshold (e.g., 10) and then subsequently perform
iterations with lower thresholds.

Optimization
^^^^^^^^^^^^

The Optimization is used to assign unassigned events to cases based on
their filters.

Usually, an analyst selects events and creates a case with these events.
During the case creation a set of filters gets generated to
automatically assign newly incoming events to this case.

Often, characteristics of existing older events also align with the
criteria described in the filters of the new case. However, they do not
get assigned to that case, because they’re already in the database and
the case assignment only happens when new events arrive.

Optimization is used to assign unassigned events to existing cases.

Cases
-----

Auto Case ID (formerly Group ID)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Auto Case ID is an automatically generated ID for a group of events.

This group has been formed automatically by the use filters generated
from predefined filter templates (see Glossary > Invisible > Filter
Templates).

Auto Case IDs identify a groupable set of events.

The Auto Case IDs are used in case creation as the default method to
assign new events to a case. You can review the Auto Case IDs used to
assign new events to a case in the Tab ``Grouping Criteria`` of each case.

.. figure:: ../images/image96.png
   :target: ../_images/image96.png
   :alt: Create Case

They are also used in “Auto Casing” and “Optimization”. (see Glossary >
Baselining)

Dynamic Auto Case ID
^^^^^^^^^^^^^^^^^^^^

The Dynamic Auto Case IDs are generated for events that don’t have a
corresponding filter template defined. This is often the case for very
rare event types or events of a low level (Info, Notice).

You can think of them as a fallback in form of a less efficient grouping
method.

They are usually created of all fields of an event except the ones that
are highly specific, like the HOSTNAME field.

If your case uses many Dynamic Auto Case IDs, distinguishable by the
leading uppercase “D”, then automatic event assignment is nearly
impossible. In these cases, you should rather use a string conditions to
group events into that case and assign new incoming events
automatically.

Filter Priority
^^^^^^^^^^^^^^^

It is possible that two or more cases include filters that would assign
a new incoming event to them. This often happens when one case uses Auto
Case ID (see Glossary section) and another case uses a string selection
(String Condition).

The filter priority can be used to prioritize the filters of a case so
that newly incoming events go to that prioritized case and not the one
with the default priority.

You could also create fallback cases, e.g., for all events of the level
“Notice” and intentionally reduce the priority of this case so that
other cases that select events of that level always come first.

The full prioritization process looks like:

-  Case with higher priority takes the event

-  If both cases have the same priority, the case with the higher “Type”
   takes the event (Incident > Noteworthy)

-  If both cases have the same priority and the same type, the case with
   the smaller case ID (older case) takes the events

External ID
^^^^^^^^^^^

This field is optional and can be used to refer to an ID that you use in
a different system, like a ticket management system or an incident
response platform.

Difference between Summary and Assessment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The field ``Summary`` is meant to include the elements (fields) of events
that are used as characteristics to perform an assessment. You can think
of it as the values that you as an analyst want to highlight for other
analysts that review that specific case. It’s often a special file name
and location or a process name and YARA rule match on that process.

You can use the “Auto Summary” feature to get an auto-recommended
content for this field.

The field ``Assessment`` is the one that requires the most effort. It
contains the findings of the analyst’s review.

Difference between False Positive and Legitimate Anomaly
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

We use "False Positive" and "Legitmate Anomaly" to distinguish between
situations in which the scanner (THOR) made an error and situations in
which a customer environment contains suspicious or malicious elements
that are known.

E.g., a Winrar used by admins as “r.exe” in “C:\\users\\public” for
software rollout purposes is not considered a “False Positive” but a
"Legitmate Anomaly". It is a finding which doesn’t have to be fixed in
THOR’s signature set but is simply a specific situation in the analyzed
environment.

Matches that are clearly an error in THOR signatures should be
classified as "False Positive".

Examples for Legitimate Anomalies”:

* Word documents with Macros that write to the filesystem and include a
   “AutoOpen” event trigger
* Procdump.exe findings
* Suspicious RUN Key entries that use customer software
* Custom software that uses suspicious folders, e.g. C:\\Users\\Public,
   %AppData%
* Process memory match with a “ReflectiveLoader” YARA rule on a third
   party EDR agent process

Examples for “False Positives”:

* YARA rule match on Bloomberg or SAP software
* Filename IOC match “w64.exe” on a Perl for Windows build tool
* YARA rule match with “Putty\_Anomaly” on a legitimate and signed
   putty.exe

Another good example is one of the many anomaly signatures that triggers
on an XORed MS-DOS Stub. A match with such a signature only qualifies as
false positives when there is no XORed MS-DOS stub in that file and not
when it turns out to be a legitimate file. The signature detects what it
is designed to detect.

A signature with a rule named MAL\_Xrat\_Mar21\_1 that triggers on a
legitimate and signed executable, however, is a false positive.

Case Types
^^^^^^^^^^

The following table describes the cases types taxonomy used in Analysis
Cockpit.

.. list-table:: 
   :header-rows: 0
   
   * - Incident
     - | Incident cases report a clear threat, indicated by a hard match and verified by 
       | research. Analysts create incident cases to indicate the highest possible 
       | certainty and risk. Incident cases are also characterized by the fact that they 
       | do not need to be verified by someone else. The either indicate malware, threat 
       | group or penetration testing activity and should trigger immediate response.
   * - Suspicious
     - | Suspicious cases are based on significant indicators that require a review by 
       | someone within the organization or more evidence to come to a final conclusion. 
       | Often, file samples or process memory dumps are required to verify/falsify a 
       | verdict. Cases of this type usually trigger evidence collection or review actions.
   * - Noteworthy
     - | Noteworthy cases are based on soft indicators or elements that should be 
       | reviewed whenever there is time to do that. They include all kinds of events that 
       | cannot be dismissed as false positives or anomalies but are likely uncritical. 
       | Noteworthy cases don’t trigger an immediate response but should be reviewed 
       | whenever there is time to do that.
   * - Vulnerability
     - | Vulnerability cases contain detected software or configuration weaknesses that 
       | system integrity. The reported vulnerabilities often include easy to exploit 
       | weaknesses that are frequently used by threat groups to executed code remotely, 
       | gain access or escalate privileges on affected systems. Cases classified as 
       | Vulnerability are typically integrated into a vulnerability management process 
       | as additional input channel.   
   * - | Legitimate 
       | Anomaly
     - | Legitimate Anomaly cases contain events that related to legitimate elements 
       | that are suspicious but in the context of the analyzed organization an ordinary 
       | finding. The reason for an anomaly is not a malfunction of the scanner but a 
       | peculiarity within the analyzed environment. Legitimate Anomalies don’t trigger 
       | any further activity.
   * - False Positive
     - | False Positive cases contain events that indicate suspicious or malicious activity, 
       | but the review revealed that is actually legitimate software or other elements. 
       | The only reason for a false positive is a scanner malfunction or signatures that 
       | falsely report a threat (see the section 13.2.6 “Difference between False Positive 
       | and Legitimate Anomaly” for more details). A false positive usually triggers a 
       | review by Nextron Systems and a signature adjustment.
   * - Unknown
     - The default state of newly created cases.



Invisible (Backend)
-------------------

Filter Templates
^^^^^^^^^^^^^^^^

The Analysis Cockpit uses so-called filter templates that describe which
fields in which event types are specific enough to be used in a filter
that can be used to automatically group events.

These groups can be identified by a common so-called “Auto Case ID”
(formerly Group ID). See the respective entry in this Glossary.

The filter templates are static and predefined.

E.g., a typical filter template states that for events in the Module
“Filescan”, the fields FILE and SHA1 are sufficiently specific to group
events based on equal values in these two fields.
