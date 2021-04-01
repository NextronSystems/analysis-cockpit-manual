.. role:: raw-html-m2r(raw)
   :format: html

FAQs
====

It seems that events are not visible or have been lost. What can I do to verify that they’re still in the database?
-------------------------------------------------------------------------------------------------------------------

First, check your date range picker.

Very often, analysts forget to set it to the right time frame and old
events accidentally disappear from the view.

Secondly, make sure you’re using the search in the ``Events`` section and
not the ``Baselining`` section.

I have created a case but it seems that no new incoming events are assigned to that existing case. How can I check what’s wrong?
--------------------------------------------------------------------------------------------------------------------------------

The first thing that you should check are the **auto\_case\_ids** of the
events in that case (``Cases`` > ``Open Case`` > ``Events`` > ``auto\_case\_id`` Panel).

If they are distributed as in the following screenshot, it seems that
auto-casing doesn’t work on this case.

.. figure:: ../images/image95.png
   :target: ../_images/image95.png
   :alt: Auto Case ID

This case doesn’t have groupable contents and uses only so-called
"Dynamic Auto Case IDs", which are used whenever the Analysis cockpit
was unable to find a suitable filter template to create usable filters
for this type of events.

Also check the grouping criteria of that case:

``Cases`` > ``Open Case`` > Tab ``Grouping Criteria``

What are the conditions defined to assign new events to that case?

