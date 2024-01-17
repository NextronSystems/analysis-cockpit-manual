.. Index:: Baselining Glossary

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
get assigned to that case, because they're already in the database and
the case assignment only happens when new events arrive.

Optimization is used to assign unassigned events to existing cases.
